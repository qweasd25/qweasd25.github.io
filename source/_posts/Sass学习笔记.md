---
title: Sass学习笔记
date: 2018-07-09 10:34:30
tags: sass
categories: 技术
copyright: true
---
## 前言

一直听说Sass入门很快，但是一直没有时间学习，今天就下定决心学一波，然后下一个项目开始使用这个sass。

> 优点：
> 1. 兼容css:Sass完全兼容所有版本的CSS。
> 2. 特性丰富:Sass拥有比其他任何CSS扩展语言更多的功能和特性。
> 3. 团队成熟:其核心团队超过8年的精心打造。
> 4. 行业认可:一次又一次地，行业把Sass作为首选CSS扩展语言。
> 5. 社区庞大:数家科技企业和成百上千名开发者为Sass提供支持。
> 6. 框架:有无数的框架使用Sass构建。比如Compass，Bourbon，和Susy。

## 入门

1. [Sass中文网](https://www.sass.hk/guide/)
2. [Sass用法指南](http://www.ruanyifeng.com/blog/2012/06/sass.html)
3. [前端构建工具gulpjs的使用介绍及技巧](https://www.cnblogs.com/2050/p/4198792.html)

- 保持sass条理性和可读性的最基本的三个方法：嵌套、导入和注释

## 安装

### 安装Sass和Compass

- `sass`基`于Ruby`语言开发而成，因此安装`sass`前需要安装`Ruby`。（注:mac下自带Ruby无需在安装Ruby!）
- 安装过程中请注意勾选`Add Ruby executables to your PATH`添加到系统环境变量。
- 测试是否安装成功

```
ruby -v
//如安装成功会打印
ruby 2.2.2p95 (2015-04-13 revision 50295) [i386-mingw32]
```

- 更换`gem`源:因为国内网络的问题导致`gem`源间歇性中断

```
//1.删除原gem源
gem sources --remove https://rubygems.org/

//2.添加国内淘宝源
gem sources -a https://ruby.taobao.org/

//3.打印是否替换成功
gem sources -l

//4.更换成功后打印如下
*** CURRENT SOURCES ***
https://ruby.taobao.org/
```

- `Ruby`自带一个叫做`RubyGems`的系统，用来安装基于`Ruby`的软件。我们可以使用这个系统来 轻松地安装`Sass`和`Compass`。

```
//安装如下(如mac安装遇到权限问题需加 sudo gem install sass)
gem install sass
gem install compass
```

- 安装完成检测

```
sass -v
Sass 3.x.x (Selective Steve)

compass -v
Compass 1.x.x (Polaris)
Copyright (c) 2008-2015 Chris Eppstein
Released under the MIT License.
Compass is charityware.
Please make a tax deductable donation for a worthy cause: http://umdf.org/compass
```
- `Sass`常用命令

```
//更新sass
gem update sass

//查看sass版本
sass -v

//查看sass帮助
sass -h
```

### sass在`vue`中的使用

上述全都是基础，重点还是想学`sass`在`vue`中的使用，详细深入学习`sass`，[请点击此处(sass中文文档)](hthttps://www.sass.hk/docs/)。

- 1、创建一个基于 webpack 模板的新项目

```
$ vue init webpack myvue
```

- 2、在当前目录下，安装依赖

```
$ cd myvue
$ npm install
```

- 3、安装sass的依赖包

```
npm install --save-dev sass-loader
//sass-loader依赖于node-sass
npm install --save-dev node-sass
```

- 4、在build文件夹下的webpack.base.conf.js的rules里面添加配置

```
{
  test: /\.scss$/,
  loaders: ['style', 'css', 'sass']
}
```

- 5、在APP.vue中修改style标签

```
<style lang="scss">
```

- 6、然后运行项目

```
$ npm run dev
```

- 7、可以修改相关配置，检测配置是否成功

## 编译`sass`

编译方式:
1. 命令行编译模式

```
//单文件转换命令
sass input.scss output.css

//单文件监听命令
sass --watch input.scss:output.css

//如果你有很多的sass文件的目录，你也可以告诉sass监听整个目录：
sass --watch app/sass:public/stylesheets
```

> 四种编译排版：

> 未编译：

```
//未编译样式
.box {
  width: 300px;
  height: 400px;
  &-title {
    height: 30px;
    line-height: 30px;
  }
}
```

> 1. nested 编译排版格式

```
/*命令行内容*/
sass style.scss:style.css --style nested

/*编译过后样式*/
.box {
  width: 300px;
  height: 400px; }
  .box-title {
    height: 30px;
    line-height: 30px; }
```

> 2. expanded 编译排版格式

```
/*命令行内容*/
sass style.scss:style.css --style expanded

/*编译过后样式*/
.box {
  width: 300px;
  height: 400px;
}
.box-title {
  height: 30px;
  line-height: 30px;
}
```

> 3. compact 编译排版格式

```
/*命令行内容*/
sass style.scss:style.css --style compact

/*编译过后样式*/
.box { width: 300px; height: 400px; }
.box-title { height: 30px; line-height: 30px; }
```

> 4. compressed 编译排版格式

```
/*命令行内容*/
sass style.scss:style.css --style compressed

/*编译过后样式*/
.box{width:300px;height:400px}.box-title{height:30px;line-height:30px}
```

2. `sublime`插件`SASS-Build`

3. 编译软件`koala`
- `koala`是一个国产免费前端预处理器语言图形编译工具，支持`Less`、`Sass`、`Compass`、`CoffeeScript`，帮助`web`开发者更高效地使用它们进行开发。跨平台运行，完美兼容windows、linux、mac。
- [下载地址](https://www.sass.hk/skill/koala-app.html)
4. 前端自动化软件`codekit`
5. `Grunt`打造前端自动化工作流`grunt-sass`
6. `Gulp`打造前端自动化工作流`gulp-ruby-sass`等

## 语法

### 1. 使用变量

- 用标识符$来标识变量
- 使用中划线的方式更为普遍，这也是compass和本文都用的方式。实际上，在sass的大 多数地方，中划线命名的内容和下划线命名的内容是互通的，除了变量，也包括对混合器和Sass函数的命名。

### 2. 嵌套css规则

```
#content article h1 { color: #333 }
#content article p { margin-bottom: 1.4em }
#content aside { background-color: #EEE }
```

可以写成

```
#content {
  article {
    h1 { color: #333 }
    p { margin-bottom: 1.4em }
  }
  aside { background-color: #EEE }
}
```

#### 2.1 父选择器的标识符`&`

不希望本属性被父选择器继承的话，在前面加上`&`。

```
article a {
  color: blue;
  &:hover { color: red }
}
```

#### 2.2 群组选择器的嵌套

第一种
```
.container {
  h1, h2, h3 {margin-bottom: .8em}
}
```

第二种
```
nav, aside {
  a {color: blue}
}
```

>注意:有利必有弊，你需要特别注意群组选择器的规则嵌套生成的css。虽然sass让你的样式表看上去很小，但实际生成的css却可能非常大，这会降低网站的速度。

#### 2.3 子组合选择器和同层组合选择器：>、+和~

```
article {
  ~ article { border-top: 1px dashed #ccc }
  > section { background: #eee }
  dl > {
    dt { color: #333 }
    dd { color: #555 }
  }
  nav + & { margin-top: 0 }
}
```

->

```
article ~ article { border-top: 1px dashed #ccc }
article > footer { background: #eee }
article dl > dt { color: #333 }
article dl > dd { color: #555 }
nav + article { margin-top: 0 }
```

#### 2.4 嵌套属性

```
nav {
  border: {
  style: solid;
  width: 1px;
  color: #ccc;
  }
}
```

> 属性和选择器嵌套是非常伟大的特性，因为它们不仅大大减少了你的编写量，而且通过视觉上的缩进使你编写的样式结构更加清晰，更易于阅读和开发。

> 即便如此，随着你的样式表变得越来越大，这种写法也很难保持结构清晰。有时，处理这种大量样式的唯一方法就是把它们分拆到多个文件中。sass通过对css原有`@import`规则的改进直接支持了这一特性。

### 3. 导入Sass文件

- `css`有一个特别不常用的特性，即`@import`规则，它允许在一个`css`文件中导入其他`css`文件。然而，后果是只有执行到`@import`时，浏览器才会去下载其他`css`文件，这导致页面加载起来特别慢。
- `sass`也有一个`@import`规则，但不同的是，`sass`的`@import`规则在生成css文件时就把相关文件导入进来。这意味着所有相关的样式被归纳到了同一个`css`文件中，而无需发起额外的下载请求。另外，所有在被导入文件中定义的变量和混合器（参见2.5节）均可在导入文件中使用。
- 使用`sass`的`@import`规则并不需要指明被导入文件的全名。你可以省略`.sass`或`.scss`文件后缀。在不修改样式表的前提下，你完全可以随意修改你或别人写的被导入的`sass`样式文件语法，在`sass`和`scss`语法之间随意切换。

#### 3.1 使用SASS部分文件

- `sass`局部文件的文件名以下划线开头。例如:`_night-sky.scss`
- 当你`@import`一个局部文件时，还可以不写文件的全名，即省略文件名开头的下划线。例如:`@import "themes/night-sky"`
- 局部文件可以被多个不同的文件引用

#### 3.2  默认变量值

```
$fancybox-width: 400px !default;
.fancybox {
width: $fancybox-width;
}
```

> 如果用户在导入你的sass局部文件之前声明了一个$fancybox-width变量，那么你的局部文件中对$fancybox-width赋值400px的操作就无效。

#### 3.3 嵌套导入

- 跟原生的`css`不同，`sass`允许`@import`命令写在`css`规则内
- 这种导入方式下，生成对应的`css`文件时，局部文件会被直接插入到`css`规则内导入它的地方

#### 3.4 原生的CSS导入

由于`sass`兼容原生的`css`，所以它也支持原生的CSS@import。尽管通常在`sass`中使用`@import`时，sass会尝试找到对应的`sass`文件并导入进来，但在下列三种情况下会生成原生的CSS@import，尽管这会造成浏览器解析`css`时的额外下载：
- 被导入文件的名字以`.css`结尾；
- 被导入文件的名字是一个`URL`地址（比如http://www.sass.hk/css/css.css），由此可用谷歌字体`API`提供的相应服务；
- 被导入文件的名字是CSS的url()值。

> 这就是说，你不能用`sass`的`@import`直接导入一个原始的`css`文件，因为`sass`会认为你想用`css`原生的`@import`。但是，因为`sass`的语法完全兼容`css`，所以你可以把原始的`css`文件改名为`.scss`后缀，即可直接导入了。

#### 3.5 占位符选择器

- 占位符选择器 (placeholder selector)
- 与常用的 `id` 与 `class` 选择器写法相似，只是 `#` 或 . 替换成了 `%`。必须通过 `@extend` 指令调用
- 它们单独使用时，不会被编译到 `CSS` 文件中
- 制作 `Sass` 样式库(希望 `Sass` 能够忽略用不到的样式)

### 4. 静默注释

- `sass`另外提供了一种不同于`css`标准注释格式/* ... */的注释语法，即静默注释，其内容不会出现在生成的`css`文件中

```
body {
  color: #333; // 这种注释内容不会出现在生成的css文件中
  padding: 0; /* 这种注释内容会出现在生成的css文件中 */
}
```

- 当注释出现在原生`css`不允许的地方，如在`css`属性或选择器中，也不会生成在对应`css`文件中

### 5. 混合器

- 混合器使用`@mixin`标识符定义

```
@mixin rounded-corners {
  -moz-border-radius: 5px;
  -webkit-border-radius: 5px;
  border-radius: 5px;
}
```

- 使用场景
    1. 发现自己在不停地重复一段样式
    2. 能找到一个很好的短名字来描述这些属性修饰的样式
    3. 用来描述`html`元素的含义而不是`html`元素的外观
    4. 用来描述一条`css`规则应用之后会产生怎样的效果
- 混合器中的`CSS`规则:混合器中不仅可以包含属性，也可以包含`css`规则,包含选择器和选择器中的属性
- `@include`指令引入混合器的那行代码替换成混合器里边的内容
- 可以使用`sass`的父选择器标识符`&`
- 给混合器传参

```
@mixin link-colors($normal, $hover, $visited) {
  color: $normal;
  &:hover { color: $hover; }
  &:visited { color: $visited; }
}
```

当混合器被`@include`时，你可以把它当作一个`css`函数来传参。如果你像下边这样写:

```
a {
  @include link-colors(blue, red, green);
}

//Sass最终生成的是：

a { color: blue; }
a:hover { color: red; }
a:visited { color: green; }
```
`sass`允许通过语法`$name`: `value`的形式指定每个参数的值。这种形式的传参，参数顺序就不必再在乎了，只需要保证没有漏掉参数即可：

```
a {
    @include link-colors(
      $normal: blue,
      $visited: green,
      $hover: red
  );
}
```

- 默认参数值

> 参数默认值使用`$name: default-value`的声明形式


```
@mixin link-colors(
    $normal,
    $hover: $normal,
    $visited: $normal
  )
{
  color: $normal;
  &:hover { color: $hover; }
  &:visited { color: $visited; }
}
```

如果像下边这样调用：`@include link-colors(red)` `$hover`和`$visited`也会被自动赋值为`red`。

### 6. 使用选择器继承来精简CSS

> 使用`sass`的时候，最后一个减少重复的主要特性就是选择器继承

- 通过`@extend`语法实现

```
//通过选择器继承 继承样式
.error {
  border: 1px solid red;
  background-color: #fdd;
}
.seriousError {
  @extend .error;
  border-width: 3px;
}
```

- `.seriousError`不仅会继承`.error`自身的所有样式，任何跟`.error`有关的组合选择器样式也会被`.seriousError`以组合选择器的形式继承

```
//.seriousError从.error继承样式
.error a{  //应用到.seriousError a
  color: red;
  font-weight: 100;
}
h1.error { //应用到hl.seriousError
  font-size: 1.2rem;
}
```

- 何时使用继承

> 5.1节介绍了混合器主要用于展示性样式的重用，而类名用于语义化样式的重用。

> 某个类（比如说.seriousError）另一个类（比如说.error）的细化

- 继承的高级用法
- 继承的工作细节

> 跟混合器相比，继承生成的css代码相对更少。因为继承仅仅是重复选择器，而不会重复属性，所以使用继承往往比混合器生成的css体积更小。如果你非常关心你站点的速度，请牢记这一点。

> 继承遵从css层叠的规则。当两个不同的css规则应用到同一个html元素上时，并且这两个不同的css规则对同一属性的修饰存在不同的值，css层叠规则会决定应用哪个样式。相当直观：通常权重更高的选择器胜出，如果权重相同，定义在后边的规则胜出。

- 不要在css规则中使用后代选择器
