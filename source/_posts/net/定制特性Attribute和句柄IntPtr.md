---
title: 定制特性Attribute和句柄IntPtr
date: "2018-11-24"
---

## 定制特性Attribute
##### 1、Attribute与Property
Attribute的翻译是特性,要与c#中类的属性Property区分
##### 2、Attribute与注释
- 注释：是给程序员看的，编译的时候会去掉这些信息，也就是说，程序集中没有注释的内容。
- Attribute：会被编译到程序集中，在程序集的元数据中，在加载程序集的时候，可以从它的元数据中提取出这些信息。
==也就是说绑定特性后能在编程时使用==

==MSDN中对Attribute的定义是：Attribute 类将预定义的系统信息或用户定义的自定义信息与目标元素相关联。目标元素可以是程序集、类、构造函数、委托、枚举、事件、字段、接口、方法、可移植可执行文件模块、参数、属性 (Property)、返回值、结构或其他属性 (Attribute)。==

#### 接下来分3步讲解特性
##### 1. 自定义特性

```
 [AttributeUsage(AttributeTargets.Property| AttributeTargets.Class, AllowMultiple = true)]
public class ColumnAttribute : Attribute
{
    public string ColumnName { get; set; }
    public string ColumnAlias { get; set; }
    public ColumnAttribute(string columnName)
    {
        this.ColumnName = columnName;
    }
}
```
==所有自定的Attribute的必须继承自抽象类Attribute==
######  AttributeUsageAttribute特性
```
    //
    // 摘要:
    // 指定一个类使用
    [AttributeUsage(AttributeTargets.Class, Inherited = true)]
    public sealed class AttributeUsageAttribute : Attribute
    {
        //构造函数指定可以使用目标元素
        public AttributeUsageAttribute(AttributeTargets validOn);
        
        //这个属性标记了我们的定制特性能否被重复放置在同一个程序实体前多次。
        public bool AllowMultiple { get; set; }

        //用于确定指定的属性是否由派生类和重写成员继承。
        public bool Inherited { get; set; }
        
        //指定可以使用目标元素
        public AttributeTargets ValidOn { get; }
    }
```


```
    //使用对象
    // 摘要:
    //     Specifies the application elements on which it is valid to apply an attribute.
    [Flags]
    public enum AttributeTargets
    {
        Assembly = 1,
        Module = 2,
        Class = 4,
        Struct = 8,
        Enum = 16,
        Constructor = 32,
        Method = 64,
        Property = 128,
        Field = 256,
        Event = 512,
        Interface = 1024,
        Parameter = 2048,
        Delegate = 4096,
        ReturnValue = 8192,
        GenericParameter = 16384,
        All = 32767
    }
```
##### 2. 绑定特性
```
public class SysUserInfo
    { 
        [Column("UserID", ColumnAlias = "用户账号")]
        public string UserID
        {
            get;
            set;
        }

        [ColumnAttribute("UserID")]
        [ColumnAttribute("UserID", ColumnAlias = "用户账号")]
        public string UserID
        {
            get;
            set;
        }

        [ColumnAttribute("UserID"), ColumnAttribute("UserID", ColumnAlias = "用户账号")]
        public string UserID
        {
            get;
            set;
        }

        [ColumnAttribute("UserID", ColumnAlias = "用户账号"), ColumnAttribute("UserID")]
        public string UserID
        {
            get;
            set;
        }
    }
```
以上4中都是一样的,在定义特性类时，我们约定在其类名后添加“Attribute”，当然你也可以不加，程序也一样正常运行，但建议加上，原因一：这是一个约定；原因二：当你的Attribute施加到一个程序的元素上的时候，编译器先查找你的Attribute的定义，如果没有找到，那么它就会查找“Attribute名称"+Attribute的定义

##### 3. 获取使用特性

```
static void Main(string[] args)
        { 
            foreach (var pi in typeof(SysUserInfo).GetProperties())
            {
               // ColumnAttribute columnAttr = pi.GetCustomAttributes(false)[0] as ColumnAttribute;    //等价于下面的语句
                ColumnAttribute columnAttr = Attribute.GetCustomAttribute(pi, typeof(ColumnAttribute)) as ColumnAttribute;
                if (columnAttr != null)
                {
                    Console.WriteLine(columnAttr.ColumnName);
                }
            }
        }
```


## C# 关键字 IntPtr
#### extern
修饰符用于声明在外部实现的方法。extern 修饰符的常见用法是在使用 Interop 服务调入非
托管代码时与 DllImport 属性一起使用；在这种情况下，该方法还必须声明为 static，如下面的示例所示：

```
[DllImport("avifil32.dll")]
private static extern void AVIFileInit();
```
==注意==
- extern 关键字还可以定义外部程序集别名，使得可以从单个程序集中引用同一组件的不同版本。将 abstract（C# 参考）和 extern 修饰符一起使用来修改同一成员是错误的。使用 extern 修饰符意味着方法在 C# 代码的外部实现，而使用abstract修饰符意味着在类中未提供方法实现。注意 extern 关键字在使用上比在 C++ 中有更多的限制。若要与 C++ 关键字进行比较，请参见 C++ Language Reference 中的 Using extern to

```
[cpp] 
// cmdll.c   何问起
// compile with: /LD  
int __declspec(dllexport) SampleMethod(int i)  
{  
  return i*10;  
} 
 
该示例使用两个文件 CM.cs 和 Cmdll.c 来说明 extern。C 文件是示例 2 中创建的外部 DLL，它从 C# 程序内调用。
[c-sharp]  
 
// cm.cs  
using System;  
using System.Runtime.InteropServices;  
public class MainClass   
{  
  [DllImport("Cmdll.dll")]  
  public static extern int SampleMethod(int x);  
  //hovertree.com
  static void Main()   
  {  
      Console.WriteLine("SampleMethod() returns {0}.", SampleMethod(5));  
  }  
} 
```




#### IntPtr
C#中的IntPtr类型称为“平台特定的整数类型”，它们用于本机资源，如窗口句柄。
资源的大小取决于使用的硬件和操作系统，但其大小总是足以包含系统的指针（因此也可以包含资源的名称）。
```
[DllImport("winmm.dll")]
private static extern long MciSendString(string a, string b, uint c, IntPtr d);

MciSendString("set cdaudio door open", null, 0, this.Handle);
```
一是在C#中声明Win32API时，一定要按照WinAPI的原型来声明，不要改变它的数据类型； 
二是尽量不要过多使用类型强制转换或构造函数的方式初始化一个IntPtr类型的变量，这样会使程序变得难于理解并容易出错。

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Runtime.InteropServices;
using System.Diagnostics;
using System.Collections;
 
public class User32API
{
    private static Hashtable processWnd = null;
 
    public delegate bool WNDENUMPROC(IntPtr hwnd, uint lParam);
 
    static User32API()
    {
        if (processWnd == null)
        {
            processWnd = new Hashtable();
        }
    }
 
    [DllImport("user32.dll", EntryPoint = "EnumWindows", SetLastError = true)]
    public static extern bool EnumWindows(WNDENUMPROC lpEnumFunc, uint lParam);
 
    [DllImport("user32.dll", EntryPoint = "GetParent", SetLastError = true)]
    public static extern IntPtr GetParent(IntPtr hWnd);
 
    [DllImport("user32.dll", EntryPoint = "GetWindowThreadProcessId")]
    public static extern uint GetWindowThreadProcessId(IntPtr hWnd, ref uint lpdwProcessId);
 
    [DllImport("user32.dll", EntryPoint = "IsWindow")]
    public static extern bool IsWindow(IntPtr hWnd);
 
    [DllImport("kernel32.dll", EntryPoint = "SetLastError")]
    public static extern void SetLastError(uint dwErrCode);
 
    //找出当前进程的活跃窗口的句柄
    public static IntPtr GetCurrentWindowHandle()
    {
        IntPtr ptrWnd = IntPtr.Zero;
        uint uiPid = (uint)Process.GetCurrentProcess().Id;  // 当前进程 ID
        object objWnd = processWnd[uiPid];
 
        if (objWnd != null)
        {
            ptrWnd = (IntPtr)objWnd;
            if (ptrWnd != IntPtr.Zero && IsWindow(ptrWnd))  // 从缓存中获取句柄 IntPtr.Zero将句柄设置为0； 
            {
                return ptrWnd;
            }
            else
            {
                ptrWnd = IntPtr.Zero;
            }
        }
 
        bool bResult = EnumWindows(new WNDENUMPROC(pp), uiPid);
        // 枚举窗口返回 false 并且没有错误号时表明获取成功
        if (!bResult && Marshal.GetLastWin32Error() == 0)
        {
            objWnd = processWnd[uiPid];
            if (objWnd != null)
            {
                ptrWnd = (IntPtr)objWnd;
            }
        }
 
        return ptrWnd;
    }
 
    private static bool pp(IntPtr hwnd, uint lParam)
    {
        uint uiPid = 0;
 
        if (GetParent(hwnd) == IntPtr.Zero)
        {
            GetWindowThreadProcessId(hwnd, ref uiPid);
            if (uiPid == lParam)    // 找到进程对应的主窗口句柄
            {
                processWnd[uiPid] = hwnd;   // 把句柄缓存起来
                SetLastError(0);    // 设置无错误
                return false;   // 返回 false 以终止枚举窗口
            }
        }
 
        return true;
    }
```
