---
title: hexo-blog-build
date: 2018-05-18 16:00:14
categories: 技术
tags: [hexo, github-pages, blog, yilia]
---
## 用Hexo搭建自己的博客记录
> 1. 本机安装node, git, 生成公钥。[供参考](https://blog.csdn.net/chwshuang/article/details/52350377)
2. 全局安装 `npm install hexo-cli -g`
3. 选择一个目录新建blog文件夹并创建站点：先命令1：`mkdir blog`,  后命令2： `hexo init blog`
4. 安装依赖包 `npm install`
5. 启动站点 `hexo server`

但是服务器启动不起来，经过搜索引擎得知，是端口号被福昕阅读器的一个服务占用。  
> 1. 命令行输入`netstat -ano` 查看4000端口号，找到对应PID
2. 打开windows任务管理器->服务->对应PID服务是否存在  

<!-- more   -->
Solutions:  
> 1. 一次性的：`$ hexo s -p 5000`
2. 一次性的：杀掉4000进程  
3. 在站点配置文件_config.yml加入 
``` yml
# Server Port
server:
    port: 4001
    log: false
    ip: 0.0.0.0
    compress: false
    header: true
    serveStatic:
    extensions:
    - html
```
执行`hexo server`
顺利开启！     
Keep going~     
打开根目录下_config.yml文件，继续修改配置  
```yml
deploy:
type: git
repo: <repository url>
branch: [branch]
message: [message]
```
#### more info
Quick Start
Create a new post
``` bash
$ hexo new "My New Post"
```
Run server
``` bash
$ hexo server
```
Generate static files
``` bash
$ hexo generate
```
Deploy to remote sites
``` bash
$ hexo deploy
```

- 安装部署插件
```npm
$ npm install hexo-deployer-git --save
```

- hexo clean -> hexo generate
- deploy部署的时候repo的git仓库地址是https形式的会报错，换成了ssh方式就可以。[供参考](https://segmentfault.com/q/1010000003734223)
- 部署到github page上（有点久）：hexo deploy
- 在https://hexo.io/themes/ 找一个自己喜欢的主题并安装起来~
  1.  查看主题github页面，复制下载地址          
  2.  克隆主题到本地blog目录
  主题：
  https://github.com/Haojen/hexo-theme-Anisina 
   https://github.com/ahonn/hexo-theme-even  
   https://github.com/litten/hexo-theme-yilia<- finally choice
- 修改blog根目录的_config.yml,将theme修改为yilia
ps: 
1. 以防以后有用 e.g. 更换电脑 https://www.jianshu.com/p/ca5f3fc708c7
2. hexo文件夹目录说明 https://xuanwo.org/2015/03/26/hexo-intor/
3. yilia主题需要在blog根目录下安装 `npm i hexo-generator-json-content --save`
4. 添加新文章打开Hexo目录下的source文件夹，所有的文章都会以md形式保存在_post文件夹中，只要在_post文件夹中新建md类型的文档，就能在执行1hexo g1的时候被渲染。 新建的文章头需要添加一些yml信息，如下所示：  

``` yml
---title: hello-world   //在此处添加你的标题。
date: 2014-11-7 08:55:29   //在此处输入你编辑这篇文章的时间。
categories: Exercise   //在此处输入这篇文章的分类。
toc: true  //在此处设定是否开启目录，需要主题支持。
---
```
- 添加标签
``` markdown
---
title: Hello World
tag: [Hexo, Github pages]
---
```
- 截断文字
在需要截断的位置插入`<!-- more -->` 即可。  
- [yilia主题文章导航教程](http://www.54tianzhisheng.cn/2017/06/13/Hexo-yilia-toc/#%E6%B7%BB%E5%8A%A0-CSS-%E6%A0%B7%E5%BC%8F) 【未实践】
- 归档，分类（categories），标签
归档： `hexo n page 'archives'`     
默认hexo n "test" 生成的md文件
``` markdown
---title: test
date: 2018-05-18 16:19:18
tags:categories:
---
```
可以编辑标题、日期、标签和内容，但是没有分类的选项。我们可以手动加入`categories:`项，或者打开`scaffolds/post.md`文件，在`tages:`上面加入`categories:`,保存后，重新执行`hexo n 'name'`命令，会发现新建的页面里有`categories:`项了
- 维护博客内容 [参考](https://crazymilk.github.io/2015/12/28/GitHub-Pages-Hexo%E6%90%AD%E5%BB%BA%E5%8D%9A%E5%AE%A2/#more)
1. 创建两个分支：master(放生成的静态网页) 与 hexo(存放网站的原始文件)；
2. 设置hexo为默认分支（git bash更新）, master通过`hexo d`更新；
3. 使用`git clone`拷贝hexo仓库；
4. 在本地xx.github.io文件夹下通过git bash依次执行`npm install hexo`, `hexo init`, `npm install` 和 `npm install hexo-deployer-git`（此时当前分支应显示为hexo），安装hexo基本环境;
5. 修改_config.yml中的deploy参数，分支应为master；
6. 依次执行`git add .`, `git commit -m '…'`, `git push origin hexo`提交网站相关的文件；
7. 执行`hexo generate -d`生成网站并部署到GitHub master主分支上。
8. 更换电脑，重新安装的话，执行步骤3， 4，注意：4**不需要**`hexo init`命令。

- Git出现**fatal: Pathspec is in submodule**解决方案 [参考](http://cloudbps.com/2017/06/22/git-fatal/)
``` bash
git rm -rf --cached themes/yilia
git add themes/yilia/*
git commit
git push
```
*Reference:
[git在线文档](https://git-scm.com/book/zh/v2)
[创建github pages项目](https://pages.github.com/)
[Hexo搭建教程](https://blog.csdn.net/column/details/12738.html)
[Hexo官方文档](https://hexo.io/docs/server.html)*