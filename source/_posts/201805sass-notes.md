---
title: sass-notes
date: 2018-05-29 15:35:59
tags: [css, sass]
categories: 技术
---
- Sass, also known as the indented syntax
- SCSS, a CSS-like syntax  
[More differences between Sass and SCSS](https://www.sitepoint.com/whats-difference-sass-scss/) 
## sass guide
### Preprocessing 预处理
### Variables	变量
store information needed to reuse throughout the stylesheet. e.g. colors, font stacks （[字体库](http://book.51cto.com/art/201012/240026.htm)）.  
`$` symbol to make something a variable
```scss
	$font-stack:    Helvetica, sans-serif;
	$primary-color: #333;

	body {
        font: 100% $font-stack;
        color: $primary-color;
	}
```
<!-- more -->
### Nesting		嵌套
### Partials	片段
Modularize css files and keep things easier to maintain. A partial is simply a Sass file named with a leading underscore. e.g. `_partial.scss`. Sass partials are used with the `@import` directive.
Sass 有个特有的功能叫做「partial」，因为 Sass 默认的编译工具可以编译整个目录下的文件，所以当一些文件不需要编译时，可以在文件名前加上 _ 表明这是一个被别的模块引入本身不需要编译的代码片段。from [w3cplus](https://www.w3cplus.com/preprocessor/revisiting-css-preprocessors.html)
### Import	引入
CSS import option's drawback is that each time you use `@import` in CSS it creates another HTTP request. Sass will combine the import file into the file you're importing into so you can serve a single CSS file to the web browser.
### Mixins	复用
use `@minxin` directive to create a mixin.  
use `@include` directive to use a minxin.  
pass the variable by using `$variableName` inside the parentheses.
```scss
	@mixin border-radius($radius) {
	  -webkit-border-radius: $radius;
	     -moz-border-radius: $radius;
	      -ms-border-radius: $radius;
	          border-radius: $radius;
	}
	
	.box { @include border-radius(10px); }
```
### Extend/Inheritance 继承
Using `@extend` lets you share a set of CSS properties from one selector to another.  
```scss
	// This CSS will print because %message-shared is extended.
	%message-shared {
	  border: 1px solid #ccc;
	  padding: 10px;
	  color: #333;
	}
	
	.message {
	  @extend %message-shared;
	}
	
	.success {
	  @extend %message-shared;
	  border-color: green;
	}
```
### Operators 运算符
Sass provides a handful of standard math operator. e.g. `+`, `-`, `*`, `/` and `%`.

### Placeholder
Placeholder 是什么？简单来说就是一个声明块（预处理器 DSL 中的声明块，包含其下嵌套规则），但是不会在最终的 CSS 中输出。其实这是一组「抽象」样式，只存在于预处理器的编译过程中（类似 mixin），但不同之处是它可以被继承。这样我们就可以在纯样式层为声明块起与样式强耦合的名称而不怕它出现在 CSS 与 HTML 的「接口」——选择器之中了。
```scss
.success {
@extend %message-shared;
border-color: green;
```
## Sass doc
### Features
- Fully CSS-compatible
- Language extensions such as variables, nesting and mixins
- Many [useful functions](https://sass-lang.com/documentation/Sass/Script/Functions.html) for manipulating colors and other values
- Advanced features like [control directives](https://sass-lang.com/documentation/file.SASS_REFERENCE.html#control_directives__expressions) for libraries
- Well-formatted, customizable output
### Syntax
Two syntaxes available for Sass.
one is SCSS(Sassy CSS), an extension of the syntax of CSS. Every valid CSS stylesheet is a valid SCSS file with the same meaning. Files name ended with the .scss extension.
another older syntax, indented syntax(缩进格式）, known as Sass.
sass-convert command can convert these two syntaxes file.
```bash
# Convert Sass to SCSS
$ sass-convert style.sass style.scss

# Convert SCSS to Sass
$ sass-convert style.scss style.sass
```

### CSS Extensions
- Nested Rules
- Referencing Parent Selectors: &
- Nested properties
```scss
.funky {
  font: 20px/24px fantasy {
    weight: bold;
  }
}
```
is compiled to:
```scss
.funky {
  font: 20px/24px fantasy;
    font-weight: bold;
}
```
P.S.
With a font-family you set more than one font to the selected item that could be reverted to should the 1st font fail to load, the 2nd will take it's place and so on

while with the font-style you set only one font to selected item with no back up font to revert to. In this case the browser will set it's default font to the selected item should the font fail to load.
- Placeholder Selectors: %foo
### Comments: /\* \*/ and //
`/* */` multiline CSS comments will appear in the CSS output  
`//` single-line comment syntax won't appear in the CSS output
## @-Rules and Directives
### @import
Sass extends the CSS `@import` rule to allow it to import SCSS and Sass files. All imported SCSS and Sass files will be merged together into a single CSS output file. In addition, any variables or mixins defined in imported files can be used in the main file.
For example,
```scss
@import "foo.scss";
```
or
```scss
@import "foo";
```
would both import the file foo.scss, whereas
```scss
@import "foo.css";
@import "foo" screen;
@import "http://foo.com/bar";
@import url(foo);
would all compile to
```
```scss
@import "foo.css";
@import "foo" screen;
@import "http://foo.com/bar";
@import url(foo);
```
It's also possible to import multiple files in one @import. For example:
```scss
@import "rounded-corners", "text-shadow";
```
would import both the rounded-corners and the text-shadow files.
### @media
This directive can be nested in CSS rules.  
`@media` queries can contain SassScript expressions (including variables, functions, and operators) in place of the feature names and feature values.  
e.g.
```scss
$media: screen;
$feature: -webkit-min-device-pixel-ratio;
$value: 1.5;

@media #{$media} and ($feature: $value) {
  .sidebar {
    width: 500px;
  }
}
```
is compiled to:
```scss
@media screen and (-webkit-min-device-pixel-ratio: 1.5) {
  .sidebar {
    width: 500px; 
   } 
}
```
### @extend
### @each
`@each $var in <list or map>`. `$var` can be any variable name, like `$length` or `$name`, and `<list or map>` is a SassScript expression that returns a list or a map.
e.g.
```scss
@each $animal in puma, sea-slug, egret, salamander {
  .#{$animal}-icon {
    background-image: url('/images/#{$animal}.png');
  }
}
```
is compiled to:
```scss
.puma-icon {
  background-image: url('/images/puma.png'); }
.sea-slug-icon {
  background-image: url('/images/sea-slug.png'); }
.egret-icon {
  background-image: url('/images/egret.png'); }
.salamander-icon {
  background-image: url('/images/salamander.png'); }
```
### @debug
### @warn
### @error
## Control Directives & Expressions
### if()
### @if
---
## ps
对于属性的缩写形式，你甚至可以像下边这样来嵌套，指明例外规则：
```scss
nav {
	border: 1px solid #ccc {
		left: 0px;
		right: 0px;
	}
}
```
这比下边这种同等样式的写法要好：
```scss
nav {
  border: 1px solid #ccc;
  border-left: 0px;
  border-right: 0px;
}
```
expanded 编译排版格式
```bash
sass demo.scss ../css/output.css --style expanded

sass --watch demo.scss:../css/output.css --style expanded
```
命令行编译;
```bash
#单文件转换命令
sass input.scss output.css

#单文件监听命令
sass --watch input.scss:output.css

#如果你有很多的sass文件的目录，你也可以告诉sass监听整个目录：
sass --watch app/sass:public/stylesheets
```

*Reference: 
[解决sass编译中文出现错误](http://www.cnblogs.com/zhidong123/p/3902270.html) 
[Sass documentation](https://sass-lang.com/documentation/file.SASS_REFERENCE.html)
[中文文档](https://www.sass.hk/guide/)*