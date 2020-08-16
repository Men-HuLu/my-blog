---
title: vscode使用教程
tags:
  - vscode
categories: 开发工具
description: vscode快捷键
abbrlink: 7ea82d0d
date: 2020-07-28
---
## 键盘快捷键

### 面板交互
```
Ctrl+Shift+P        //命令⾯板
Ctrl+o              //打开文件
Ctrl+R              //打开最近文件

Ctrl+Shift+E        //文件资源管理器
Ctrl+Shift+F        //文件搜索
Ctrl+Shift+G        //代码git管理
Ctrl+Shift+D        //启动和调试
Ctrl+Shift+X        //扩展
ctrl+shift+y        //控制台显示

Ctrl+K Ctrl+S       //自定义快捷键
```

### 2.代码键盘操作
#### 1.光标移动
```
Ctrl+左右方向       //单词句首句末
Home建              //句首
End 键              //句末
Ctrl+Shift+\        //代码方括号始末
Ctrl+Home/End       //是移动到⽂档的第⼀⾏或者最后⼀⾏
ctrl+U              //撤销光标移动

```
#### 文本选择
```
alt+上下方向            //选择代码（选择行上下移动）
ctrl+shift+左右方向键   //代码选择（光标在单词中间）
shift+上下方向键        //代码选择（跨行选择一行）
Shift+Home/end          //选择光标前一整行
```

#### 代码注释
```
ctrl+/          //代码注释
alt+shift+F     //代码格式化
Ctrl+F          //选中行代码格式化
ctrl+[          //缩进
ctrl+]          //拉开
```

#### 其他未绑定的一些
```
转置游标处的字符
转换为⼤写
转换为小写
合并⾏
⾏排序
```

#### 多个光标
```
alt+鼠标点击                //创建光标
shift+alt+上下⽅向键        //在代码上方复制相同代码
ctrl+alt+上下⽅向键     //在当前光标上下创建新光标（加上光标移动）

ctrl+D                  //先按选择一个,再按把附近的相同的选中,生成多光标
选择代码行+Alt+Shift+i      //行最后生成光标
```

#### 文件与符号之间的跳转
```
ctrl+tab 然后松掉tab        //切换当前打开文档
ctrl+P                      //打开文档(enter打开)
ctrl+enter                  //新窗口打开
ctrl+g                      //输入行号
Ctrl+Shift+O                //能够看到当前⽂件⾥的所有符号
Ctrl+Shift+O(再加上:)       //能够看到当前⽂件⾥的所有符号,并且分类
Cmd + T                     //多个文档,搜索这些⽂件⾥的符号

F12                         //跳转到函数的定义处(TypeScript,有函数的接⼝定义)
Cmd + F12                   //跳转到函数的实现的位置(TypeScript)

Shift + F12                 //查看引用(js也行)
```


#### 折叠代码
```
Ctrl+Shift+{        //折叠代码
Ctrl+Shift+}        //扩展代码
```

#### 单⽂件搜索
```
ctrl +F         //单文件搜索
ctrl+shift+f    //多文件搜索
f3/shift+f3     //ctrl +F搜索后快速跳转
alt+c           //是否启用⼤⼩写敏感
alt+w           //是否启用全单词匹配
alt+r           //是否启用正则表达式
```


```
1. >（⼤于号） ，⽤于显示所有的命令。
2. @ ，⽤于显示和跳转⽂件中的“符号”（Symbols），在@符号后添加冒号：则可以把符号们按类别归类。
3. #号，⽤于显示和跳转⼯作区中的“符号”（Symbols）。
4. ：（冒号）， ⽤于跳转到当前⽂件中的某⼀⾏。
```

## 鼠标快捷键

#### 文本选择
```
双击左键两次选单词
三次左键这⼀⾏代码
四次左键整个⽂档

单击行号,选一行
上下移动,就能选择多行
```

#### 2.⽂本编辑
```
点击选择块代码拖动
鼠标移到单词上,按ctrl，可以看到函数的实现
Ctrl + ⿏标左键(超链接)
```

#### 多光标
```
按鼠标中间
```

#### 快速预览 
```
Ctrl+空格键
```

#### 参数预览
```
Ctrl+Shift+Space        //参数预览
```

#### 快速修复
```
点击⻩⾊的灯泡图标
Ctrl + .
```

#### 重构
```
函数或变量上按F2,出现的地⽅就都会被修改.
```

## 代码片段

#### 配置用户代码片段"Configure User Snippets"

#### 选择一个语言JSON

JavaScript

{
    "Print to console": {
        "prefix": "log",
        "body": [
        "console.log('$1');",
        "$2" ],
        "description": "Log output to console" }
}
React示列

	"Print to console": {
		"prefix": "initreact",
		"body": [
			"import React, { Component, Fragment } from 'react';",
			"",
			"class $1 extends Component {",
			"  constructor(props) {",
			"    super(props);",
			"  }",
			"",
			"  render() {",
			"    return(",
			"      <Fragment>",
			"      </Fragment>",
			"    )",
			"  }",
			"}",
			"",
			"export default $2"
		],
		"description": "React initial Template"
	}
#### log输入完后，按tab切换$1位置

## code命令行使用

### 安装code
在 PATH 中安装 “Code” 命令 并执行，然后重启终 端模拟就可以了。

```
code --help     //获取帮助
code -r         //打开code
code .          //打开当前文件
code -r -g package.json:2   //打开当前文件，那个文件并且第几行
```

```
code -r -d a.txt b.txt      //文件对比
```

## 我的配置

### VS Code配置
```
{
  "files.exclude": {
    "node_modules/": false
  },
  "workbench.colorTheme": "Quiet Light",
  "editor.renderWhitespace": "all",
  "editor.renderIndentGuides": false,
  "editor.minimap.enabled": false,
  "editor.detectIndentation": false,
  "editor.tabSize": 2,
  "editor.formatOnSave": true,
  "editor.lineNumbers": "relative",
  "editor.rulers": [
    100
  ],
  "editor.renderLineHighlight": "all",
  "javascript.updateImportsOnFileMove.enabled": "always",
  "git.autofetch": true,
  "gitlens.advanced.messages": {
    "suppressSupportGitLensNotification": true
  },
  "files.associations": {
    "*.wpy": "vue",
    "*.vue": "vue",
    "*.wxss": "css",
    "*.wxs": "javascript",
    "*.tpl": "html"
  },
  "eslint.autoFixOnSave": true,
  "liveServer.settings.port": 8888,
  "liveServer.settings.donotShowInfoMsg": true,
  // // vetur 配置
  // "vetur.validation.template": false,
  // // 使用 VSCode 自带程序格式化 JS 文件
  // "vetur.format.defaultFormatter.js": "vscode-typescript",
  // // 使用 js-beautify-html 格式 HTML 模板
  // "vetur.format.defaultFormatter.html": "js-beautify-html",
  // "vetur.format.scriptInitialIndent": true,
  // "vetur.format.styleInitialIndent": true,
  // // 格式 HTML 模板
  // "vetur.format.defaultFormatterOptions": {
  //   "js-beautify-html": {
  //     // tag 属性对齐
  //     "wrap_attributes": "force-aligned"
  //   }
  // }
}
```