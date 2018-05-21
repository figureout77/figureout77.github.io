---
title: markdown-test
date: 2018-05-21 10:30:14
tags: markdown
categories:
---
## 标题
&#35; 二级标题
...
&#35;&#35;&#35;&#35;&#35;&#35; 六级标题
大标题
=
小标题
-
## 粗体斜体
*斜体文本* _斜体文本_
**粗体文本** __粗体文本__
***粗斜体文本*** ___粗斜体文本___

## 链接
文字链接 [github link](https://figureout77.github.io)
网址链接 <https://figureout77.github.io>
高级链接技巧
这个链接用1作为网址变量[Baidu][1].
这个链接用bing作为网址变量[Bing][bing].

[1]: http://www.baidu.com/
[bing]: http://www.bing.com.cn
<!-- more -->
## 列表
普通无序列表
- 列表文本前使用
+ 列表文本前使用
* 列表文本前使用

普通有序列表
1. 列表前使用
2. 我们会自动帮你添加数字
7. what's next? 

列表嵌套
1. 列出所有元素：
    - 无序列表元素 A
        1. 元素 A 的有序子列表
    - 前面加四个空格
2. 列表里的多段换行：
    前面必须加四个空格，
    这样换行，整体的格式不会乱
3. 列表里引用：

    > 前面空一行
    > 仍然需要在 >  前面加四个空格
## 引用
普通引用
> 引用文本前使用 [大于号+空格]
> 折行可以不加，新起一行都要加上哦

引用里嵌套引用
> 最外层引用
> > 多一个 > 嵌套一层引用
> > > 可以嵌套很多层

应用里嵌套列表
> - 这是引用里嵌套的一个列表
> - 还可以有子列表
>     * 子列表需要从 - 之后延后四个空格开始

## 换行
如果另起一行，只需在当前行结尾加2个空格
在当前行的结尾加2个空格  
这行就会新起一行

如果是要新起一个新段落，只需要空出一行即可。

## 分隔符
新起一行输入三个减号，当前后都有段落时，空出一行。
分隔符测试

---

分隔符测试

## 小型文本
normal text content  
<small>small text content</small>

## 注释
console.log('Hello world') <!-- 注释 --> 

## 表格
Markdown的扩展语法，hexo已经支持

| 参数           | 说明                 |   默认值            |
| ------------- |:-------------------:|:------------------:|
| host          | 远程主机的地址         |                    |
| user          | 使用者名称            |                    |
| root          |  远程主机的根目录      |                    |
| port          | 端口                 |       22           |
| delete        | 删除远程主机上的旧文件   |  true            |
| verbose       | 显示调试信息           |   true             |
| ignore_errors | 忽略错误              |     false          |

## 特殊字符
>! &#33; — 惊叹号Exclamation mark 
” &#34; &quot; 双引号Quotation mark 
\# &#35; — 数字标志Number sign 
$ &#36; — 美元标志Dollar sign 
% &#37; — 百分号Percent sign 
& &#38; &amp; Ampersand 
‘ &#39; — 单引号Apostrophe 
( &#40; — 小括号左边部分Left parenthesis 
) &#41; — 小括号右边部分Right parenthesis 
* &#42; — 星号Asterisk 
+ &#43; — 加号Plus sign 
< &#60; &lt; 小于号Less than 
= &#61; — 等于符号Equals sign 
> &#62; &gt; 大于号Greater than 
? &#63; — 问号Question mark 
@ &#64; — Commercial at 
[ &#91; --- 中括号左边部分Left square bracket 
\ &#92; --- 反斜杠Reverse solidus (backslash) 
] &#93; — 中括号右边部分Right square bracket 
{ &#123; — 大括号左边部分Left curly brace 
| &#124; — 竖线Vertical bar 
} &#125; — 大括号右边部分Right curly brace 

## 代码
使用\`\`\`包裹一段代码，并可以指定一种语言(\`\`\`javascript)
```javascript
console.log('hello world');
```
或者四个空格或一个制表符缩进【代码段】
    int i;
不需要代码高亮，使用\`\`\`nohighlight方法禁用
只想高亮语句中的某个函数名或关键字，可以使用\`keyname\`
e.g. 重点是`关键字`

## 图片
<!-- ![sherlock](./images/sh.jpg "sherlock") -->
引用自带图片  
根目录_config.yml开启(hexo 3.0及以上)
```
post_asset_folder: true
```
新建文章
hexo n testimg
引用图片时：  
{&#37; asset_img sh.jpg [Sherlock] &#37;}
{% asset_img sh.jpg [Sherlock] %}  
参考[文章资源文件夹](https://hexo.io/zh-cn/docs/asset-folders.html#%E6%96%87%E7%AB%A0%E8%B5%84%E6%BA%90%E6%96%87%E4%BB%B6%E5%A4%B9)



