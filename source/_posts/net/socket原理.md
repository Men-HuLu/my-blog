---
title: socket原理
date: "2018-11-27"
---

## 同步
```
//1.建立socket对象(用于监听)
//1.网络地址。2.数据传输格式，3通信协议
Socket serverSocket = new Socket(AddressFamily.InterNetwork, SocketType.Stream, ProtocolType.Tcp);
//2.绑定ip和端口
IPAddress ip = IPAddress.Parse('192.168.168.108);
IPEndPoint iPEndPoint = new IPEndPoint(ip, 50505);
serverSocket.Bind(iPEndPoint);
//3.开始侦听
serverSocket.Listen(10);
//4.开始接受客户端链接（用于传输）
//Accept执行 ，阻塞当前主线程，一直到客户端链接上
Socket proxSocket = serverSocket.Accept();
string str = DateTime.Now.ToString();
byte[] data = Encoding.Default.GetBytes(str);
proxSocket.Send(data,0,data.Length,SocketFlags.None);
//5.关闭
proxSocket.Shutdown(SocketShutdown.Both);
proxSocket.Close();
//6.监听的关闭
serverSocket .Close();
```
## 异步改进

```
List<Socket> Clientsockets = new List<Socket>();
private void button1_Click(object sender, EventArgs e)
{
    //1.建立socket对象
    //1.网络地址。2.数据传输格式，3通信协议
    Socket serverSocket = new Socket(AddressFamily.InterNetwork, SocketType.Stream, ProtocolType.Tcp);
    //2.绑定ip和端口
    IPAddress ip = IPAddress.Parse("192.168.168.108");
    IPEndPoint iPEndPoint = new IPEndPoint(ip,int.Parse("5050"));
    serverSocket.Bind(iPEndPoint);
    //3.开始侦听
    serverSocket.Listen(10);
    ThreadPool.QueueUserWorkItem(new WaitCallback(this.StaetAcceptClient),serverSocket);
}

public void StaetAcceptClient(object state)
{
    //4.开始接受客户端链接
    //Accept执行 ，阻塞当前主线程，一直到客户端链接上
    var serverSocket = (Socket)state;
    while (true)
    {
        Socket proxSocket = serverSocket.Accept();
        Clientsockets.Add(proxSocket);             
        ThreadPool.QueueUserWorkItem(new WaitCallback(this.ReciveData), proxSocket);
    }
}

public void ReciveData(object obj)
{
    var proxSocket = (Socket)obj;
    byte[] data = new byte[1024 * 1024];
    while (true)
    {
        //代表实际上接收的返回数
        int reallen = proxSocket.Receive(data, 0, data.Length, SocketFlags.None);
        if (reallen==0)
        {
            //退出了
            proxSocket.Shutdown(SocketShutdown.Both);
            proxSocket.Close();
            Clientsockets.Remove(proxSocket);
            return;
        }
        string fromClientMsg = Encoding.Default.GetString(data,0,reallen);
        proxSocket.RemoteEndPoint.ToString();
    }
}

private void button2_Click(object sender, EventArgs e)
{
    foreach (var socket in Clientsockets)
    {
        if (socket.Connected)
        {
            string str = "发送的消息";
            byte[] data = Encoding.Default.GetBytes(str);
            socket.Send(data,0,data.Length,SocketFlags.None);
        }
    }
}
```
