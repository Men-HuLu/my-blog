---
title: npm使用教程
tags:
  - npm
categories: 开发工具
description: npm入门基础知识及常用命令
abbrlink: d22ed76f
top_img: https://yuminjun.oss-cn-hangzhou.aliyuncs.com/wlop/2.jpg
cover: https://yuminjun.oss-cn-hangzhou.aliyuncs.com/zelda/8.jpg
date: 2020-07-28
---

## npm配置本地环境

### npm安装和版本更新
[node.js官网安装](https://nodejs.org/en/)
```
npm命令行界面（CLI）

//当前版本
npm -v
//更新最新版本
npm install npm@latest -g
//测试最新版本
npm install npm@next -g
```

### npm全局配置

node.js安装,npm默认路径为==C:/Users[用户]/administrator[你的计算机名字]/AppData/Roaming/npm==
```
//查看配置
C:\Users\Yuminjun>npm -g bin
C:\Users\Yuminjun\AppData\Roaming\npm
```

- npm实际去找全局命令的目录：==C:/Users/[username]/.npmrc== 文件内容的prefix值
- npm包全局cache目录：C:/Users/[username]/.npmrc 文件内容的cache值
```
npm config set prefix D:/node/nodejs/node_global/ //全局包目录，就在node安装目录新建了个nodejs文件夹存放
npm config set cache D:/node/nodejs/node_cache/  //全局包缓存目录，就在node安装目录新建了个nodejs文件夹存放
```

### npm初始化一个项目

```
npm init
npm init --yes
//默认初始化
```

配置:
```
name: the current directory name
version: always 1.0.0
description: info from the readme, or an empty string ""
main: always index.js
scripts: by default creates an empty test script
keywords: empty
author: empty
license: ISC
bugs: info from the current directory, if present
homepage: info from the current directory, if present
```

其他初始化
```
> npm set init.author.email "15705850186@163.com"
> npm set init.author.name "yuminjun"
> npm set init.license "MIT"

npm get init.license
npm delete init.license
```

依赖
```
"dependencies":您的应用程序在生产中需要这些包.
"devDependencies": 这些包只用于开发和测试.

添加到dependencies
//npm install <package_name> --save

添加到devDependencies
//npm install <package_name> --save-dev
```

### 配置查看命令

```
npm config ：管理配置文件
npm config set  <key>  <value>[-g|--global] 或 npm set  <key> <value>   [-g|--global] ：设置配置参数
npm config get  <key>或 npm get  <key> ：获取配置参数
npm config delete <key>：删除配置参数
npm config list ：列出配置参数
npm config edit ：直接编辑配置文件
npm config get prefix：获取全局安装包所在地址
```

## npm基础命令

### 安装包
```
npm install lodash
npm install lodash@版本号
```
### 更新包
```
npm update
```
### 卸载包
```
//
npm uninstall lodash
//从依赖包中删除
npm uninstall --save lodash
```
### 搜索包
```
npm search lodash
```
### 发布模块
```
npm publish lodash
```
### 撤销发布的代码
```
npm unpublish  <package>@<version>
```
### 清空本地缓存
```
npm cache clear： 清空npm本地缓存（相同版本号发布新版本时）
```

**安装全局包**
```
//将其作为一个命令行工具，那么你应该将其安装到全局

npm install -g jshint
npm update -g jshint
npm uninstall -g jshint
//-g    全局参数
```

**帮助命令**
```
npm [help | -h]：查看所有指令
npm [list | -l] ：查看所有指令使用方法
npm <指令> -h：查看具体某条命令的帮助信息
npm help <指令>：浏览器打开本地的命令帮助文档
```

**信息查看**

```
npm list -g 或 npm ls -g：获得全局安装的模块
npm list  <package>或 npm ls <package>  ：查看模块的版本号
npm info  <package>：显示包的信息
```

**参数**

```
-S 或 --save：包被写入到package.json的 dependencies。
-D 或 --save-dev：包被写入到package.json的 devDependencies。
-O 或 --save-optional：包被写入到package.json的optionalDependencies
-B 或 --save-bundle ： 包也将被添加到bundleDependencies。
-E 或 --save-exact ：会在 package.json 文件指定安装模块的确切版本。
```

**npm设置访问权限**
```
npm access public
npm access restricted
```
**npm浏览器打开github网站**
```
npm repo lodash
```


参考文档:
[CLI命令](https://docs.npmjs.com/cli-documentation/)

## npm源切换

### 安装nrm
```
npm i nrm -g
```

### 查看已有源
```
nrm ls //查看已有的源

* npm -------- https://registry.npmjs.org/
  yarn ------- https://registry.yarnpkg.com/
  cnpm ------- http://r.cnpmjs.org/
  taobao ----- https://registry.npm.taobao.org/
  nj --------- https://registry.nodejitsu.com/
  npmMirror -- https://skimdb.npmjs.com/registry/
  edunpm ----- http://registry.enpmjs.org/
```

### 切换已有源
```
nrm use <源名称> //切换到现有的源
```

### 新增已有源
```
nrm use <源名称> //新增现有的源
```

## npx命令

npx 在npm 5.2.0 是会引入
若无运行命令
```
npm install -g npx
```

### npx主要解决调用项目内部模块
```
npx eslint --init
```

```
node-modules/.bin/eslint --init
```

### 避免全局安装模块

```
npx create-react-app my-react-app
```
### 参数命令

--no-install
强制使用本地
```
$ npx --no-install http-server
```

--ignore-existing
强制使用网络
```
 npx --ignore-existing create-react-app my-react-app
```

-p
执行多条命令
```
npx -p lolcatjs -p cowsay [command]
```

-c
所有命令用npx解释
```
$ npx -p lolcatjs -p cowsay -c 'cowsay hello | lolcatjs'
```


### npx 还可以执行 GitHub 上面的模块源码。

#### 安装包
```
npm install lodash
npm install lodash@版本号
```

参考文档:

[npx](http://www.ruanyifeng.com/blog/2019/02/npx.html)

## 个人资料管理

### 登录

```
npm login
//登录

npm whoami
//检验登录
```


### 查看用户配置文件设置

```
npm profile get
```

| name            | yuminjun                 |
|-----------------|--------------------------|
| email           | 15705850186@163.com      |
| two-factor auth | disabled                 |
| fullname        | yuminjun                 |
| homepage        |                          |
| freenode        |                          |
| twitter         |                          |
| github          | Men-HuLu                 |
| created         | 2019-05-24T15:56:54.649Z |
| updated         | 2019-06-08T01:56:07.722Z |


### 修改用户配置文件设置

```
npm profile set <prop> <value>
npm profile set fullname ymj


npm profile set password
```

## 发布包


### 发布包
```
//发布前同样要登录
npm login
//登录
npm whoami
//检验登录

//发布
npm publish 
npm publish --access public
//Scoped包默认为受限制，但您可以将它们公开为使用
//公共发布权限 访问权限为公共
```

### 撤销包
//删除要用force强制删除。超过24小时就不能删除了。自己把握好时间。
```
npm --force unpublish [<@scope>/]<pkg>[@<version>]
```

### 初始化范围包
```
//初始化包
//对于组织范围的包 /my-org  组织名
npm init --scope=@my-org
//对于用户范围的包 /my-username 用户名
npm init --scope=@my-username
```

====PS==：npm包不支持es6 import关键字,采用commonjs规范,需要采用babel转义==

## 故障修复


### 生成日志文件

```
//npm install --timing
npm install --timing
//对于发布包
npm publish --timing

//npm-debug.log在.npm目录中找到该文件。
npm config get cache。
//要查找.npm目录，请使用
```

### 安全审查

```
npm audit [--json|--parseable]
npm audit fix [--force|--package-lock-only|--dry-run|--production|--only=dev]
```