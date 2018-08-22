---
title: 更新nodejs版本
date: 2018-08-22 15:29:08
tags: [node, nvm, npm]
categories: [技术, 问题]
---

### 安装NVM

在[nvm-windows](https://github.com/coreybutler/nvm-windows/releases) 下载nvm-set.zip文件，安装nodejs版本管理器nvm。`nvm list available`查看可下载版本，安装指定版本 `nvm install 8.11.4`, `nvm ls`查看当前已安装版本，一个是安装nvm之前的6.10.2，一个是8.11.4，使用`nvm use 8.11.4`显示正在使用，但是`nvm ls`打印出来的正在使用的版本前面没有`*`号，输入`node -v`提示node不是内部或外部命令，也不是可运行的程序。安装的目录没有空格，`nvm on`也没有用[(ref)](https://github.com/coreybutler/nvm-windows/issues/58#issuecomment-102892409)。
**解决方法**是将环境变量的用户和系统中的`NVM_SYMLINK`修改为安装nvm路径下的nodejs【e.g. %nvm安装路径%\nodejs】。
![最终效果](https://imgur.com/3bCI6Ht.png)
P.S. 在命令行输入`npm use 8.11.4`, nvm安装路径下生成nodejs快捷方式文件夹。切换不同的node版本时，快捷方式目标指向也随之改变。
<!-- more -->
![目录](https://i.imgur.com/jTLcUwA.png) 

### 安装全局NPM

1. `npm config set prefix "D:\Software\Coding\Nvm\nvm\npm"`
2. 编辑`C:\Users\%username%`目录下的`.npmrc`文件，添加全局npm缓存的配置路径
```
prefix=D:\Software\Coding\Nvm\nvm\npm  
cache=D:\Software\Coding\Nvm\nvm\npm-cache  
```
3. `npm install -g npm`下载全局npm包
4. 配置npm的环境变量，将之前配置的C:\Users\username\AppData\Roaming\npm删除掉
![示例](https://imgur.com/xt8iErS.png)  
![示例](https://imgur.com/7e2Iatg.png)
5. `npm install -g nrm`安装nrm
6. `nrm ls` -> `nrm use taobao`使用淘宝镜像
7. `npm install -g npm` 重新全局安装npm

现在npm都是一个版本的了！
![示例](https://imgur.com/XzyEvt6.png) 
 
*Reference:
[参考1](https://hk.saowen.com/a/89ab8f089d4d120f803a8f7d6180221d0695ad6a0200c731ff28e48c9959a75a)