---
title: 个人博客的搭建和迁移
date: 2017-05-22 22:45:48
tags: hexo
categories: 技术
copyright: true
top: 400
---
## 最初的梦想
    从开始接触三剑客开始，就拥有一个梦想，想要一个自己的个人网站。但是对于服务器那块，我真的有点不来san！哎呀呀土话啦！！
在此之前，我有过很多次想要搭建个人博客的意向，看过很多篇文章，也问过远哥。噗，他的回答永远都感觉很容易。我这个人一听很容易，就不想弄了。好了废话说多了，下面进入正题。

本文主要分为三个大章节：

1. 方法一：采用github + hexo 搭建个人博客
2. 方法二：克隆心仪的博客
3. 关于博客迁移

好了，下面看文章吧~~
### 方法一：采用github + hexo 搭建个人博客
#### 1.github配置
##### 注册github账号
##### 配置SSH-Key（一般平时在github上放项目的，都是配置过的）

不会的可以参考 [github账号在本地配置SSH key](https://qweasd25.github.io/2017/07/22/github%E8%B4%A6%E5%8F%B7%E5%9C%A8%E6%9C%AC%E5%9C%B0%E9%85%8D%E7%BD%AESSH%20key/)

#### 2.安装[Hexo](https://hexo.io/zh-cn/docs/)（点击查看官网）

```
$ npm install -g hexo-cli
```
安装 Hexo 完成后，请执行下列命令，Hexo 将会在指定文件夹中新建所需要的文件。

```
$ hexo init <folder>  # 新建一个网站。如果没有设置 folder ，Hexo 默认在目前的文件夹建立网站。
$ cd <folder>
$ npm install
```

新建完成后，指定文件夹的目录如下：

``` plain
.
├── _config.yml  # 网站的 配置 信息，您可以在此配置大部分的参数。
├── package.json  # 应用程序的信息。EJS, Stylus 和 Markdown renderer 已默认安装，您可以自由移除。
├── scaffolds  # 模版 文件夹。当您新建文章时，Hexo 会根据 scaffold 来建立文件。
├── source  # 资源文件夹是存放用户资源的地方。
|   ├── _drafts
|   └── _posts  # md文件存放目录
└── themes  # 主题 文件夹。Hexo 会根据主题来生成静态页面。
```

#### 3.本地预览
运行以下命令将生成静态文件

```
$ hexo generate
$ hexo g  # 简写
```
启动服务器。默认情况下，访问网址为： http://localhost:4000/

```
$ hexo server
$ hexo s  # 简写
```
如果端口被占用运行以下命令给该端口再启动服务器。

```
$ hexo server -p 3000
```
在浏览器中输入 localhost:3000就可以看到博客。
#### 4.主题设置
这边采用[NexT主题](http://theme-next.iissnan.com/getting-started.html#top)（点击查看官网）
##### 1.下载主题
打开Git bash，在当前项目根目下使用git从github上checkout主题的代码，输入指令：

```
$ git clone https://github.com/iissnan/hexo-theme-next themes/next
```
下载完成后，在hexo\theme目录下回多出一个next文件夹，里面就是next主题所需的文件,当然我们也可以看到在theme文件目录还有一个landscape文件夹，这也就是hexo默认的主题。
##### 2.配置主题
之前我们配置hexo的时候，有用到`_config.yml`文件，称其为站点配置文件，而我们打开next主题文件夹，发现里面也有一个`_config.yml`文件，我们称这个为主题配置文件。在hexo中启用next主题的方式：就是打开站点配置文件，找到theme字段，将其值改为“next”，如下：

```
# Extensions
## Plugins: https://hexo.io/plugins/
## Themes: https://hexo.io/themes/
theme:  next
```

##### 3.next主题的样式选择
next的样式其实有三种：Muse、Mist和Pisces，步骤2中看到的其实是next默认的模式Muse，根据官方说明三个样式的特点如下：<br/>
Muse： 默认 Scheme，这是 NexT 最初的版本，黑白主调，大量留白<br/>
Mist： Muse 的紧凑版本，整洁有序的单栏外观<br/>
Pisces： 双栏 Scheme，小家碧玉似的清新<br/>
切换的控制其实很简单，使用next主题配置文件中的scheme字段来控制，假设我们选择Mist样式（个人认为最好看的样式），操作步骤是：打开next文件夹中的_config.yml文件，找到scheme字段，将其设置为“Mist”，如下所示：<br/>

```
# ---------------------------------------------------------------
# Scheme Settings
# ---------------------------------------------------------------

# Schemes
#scheme: Muse
scheme: Mist
#scheme: Pisces
#scheme: Gemini
```
##### 4.设置favicon
打开主题配置文件`_config.yml`可以看到favicon的配置信息：

```
favicon:
  small: /images/favicon-16x16-next.png
  medium: /images/favicon-32x32-next.png
  apple_touch_icon: /images/apple-touch-icon-next.png
  safari_pinned_tab: /images/logo.svg
  #android_manifest: /images/manifest.json
  #ms_browserconfig: /images/browserconfig.xml
```
##### 5.菜单栏控制
我们看到页面顶部的菜单栏，其实是由主题配置文件中的menu字段控制的

```
menu:
  home: / || home
  about: /about/ || user
  tags: /tags/ || tags
  categories: /categories/ || th
  archives: /archives/ || archive
  # schedule: /schedule/ || calendar
  # sitemap: /sitemap.xml || sitemap
  # commonweal: /404/ || heartbeat
```
然而，点击打开About却出现了“Cannot GET /about/”的页面错误，这是因为我们还没有about这个页面，需要使用`hexo new page "页面名称"`进行创建

```
$ hexo new page about
```
执行结果就是在hexo\source目录下面多出了一个about文件夹，里面有index.md，这就是点击About会展示的内容页面。同理，也可以创建tags页面
##### 6.侧栏设置
在主题配置文件的`sidebar`字段，此处我直接设置为侧栏一直显示，而且显示在右边

```
sidebar:
  # Sidebar Position, available value: left | right
  position: left
  #position: right

  # Sidebar Display, available value:
  #  - post    expand on posts automatically. Default.
  #  - always  expand for all pages automatically
  #  - hide    expand only when click on the sidebar toggle icon.
  #  - remove  Totally remove sidebar including sidebar toggler.
  #display: post
  display: always
  #display: hide
  #display: remove
```
##### 7.设置头像和作者名称
在站点配置文件中，新加一个字段`avatar`，值就是头像的连接地址，我没有设置，将avatar.png放到本地目录hexo\source\images中；作者名称直接设置站点配置文件中`author`字段的值：

```
# Site
title: 时光与你有染
subtitle:
description:
author: qweasd25
avatar: /images/avatar.png
language: zh-Hans
timezone:
```
##### 8.给文章设置阅读量，启用不蒜子统计，仅限于文章页面显示阅读书，在首页不显示。
在主题的配置文件找到`busuanzi_count`字段，把`enable`设置为`true`

```
# Show PV/UV of the website/page with busuanzi.
# Get more information on http://ibruce.info/2015/04/04/busuanzi/
busuanzi_count:
  # count values only if the other configs are false
  enable: true
  # custom uv span for the whole site
  site_uv: true
  site_uv_header: <i class="fa fa-user"></i>
  site_uv_footer:
  # custom pv span for the whole site
  site_pv: true
  site_pv_header: <i class="fa fa-eye"></i>
  site_pv_footer:
  # custom pv span for one page only
  page_pv: true
  page_pv_header: <i class="fa fa-file-o"></i>
  page_pv_footer:
```

##### 9.Hexo-Next底部logo栏更改
首先，找到 `\themes\next\layout\_partials\`下面的`footer.swig`文件，打开把这块语句删城跟我一样，别的不用删除，尤其要注意引号，否则会出错哦~~

```
{% if theme.footer.powered %}
  <div class="powered-by">{#
  #}{{ __('footer.powered', '') }}{#
#}</div>
{% endif %}

{% if theme.footer.powered and theme.footer.theme.enable %}
  <span class="post-meta-divider">|</span>
{% endif %}

{% if theme.footer.theme.enable %}
  <div class="theme-info">{#
  #}{{ __('footer.theme') }}{#
  #}{#
#}</div>
{% endif %}
```

然后，处理中文信息，打开`\themes\next\languages\`下面的文件`zh-Hans.yml`。找到对应位置，修改成跟我类似的喔，随意发展。

```
footer:
  powered: " %s 个人博客"
  theme: 前端/生活/心得
```

#### 上传到GitHub
在此部操作之前，建议已经把博客的配置全部设置好。

相关配置可以参考着一篇文章
[hexo的next主题个性化配置教程](http://shenzekun.cn/hexo%E7%9A%84next%E4%B8%BB%E9%A2%98%E4%B8%AA%E6%80%A7%E5%8C%96%E9%85%8D%E7%BD%AE%E6%95%99%E7%A8%8B.html)

打开站点`配置文件`(即更目录下的`_config.yml`)，在最后修改如下代码

```
# Deployment
## Docs: https://hexo.io/docs/deployment.html
deploy:
  type: git
  repository: https://github.com/dracoqiu/dracoqiu.github.io.git  # 库（Repository）地址
  branch: master  # 分支名称。如果您使用的是 GitHub 或 GitCafe 的话，程序会尝试自动检测。
  message: [message]  # 自定义提交信息 (默认为 Site updated: {{ now('YYYY-MM-DD HH:mm:ss') }})
```
每次修改本地文件都需执行以下命令

```
$ hexo generate
$ hexo deploy
# 以下为简写
$ hexo g
$ hexo d
```
如果执行`$ hexo deploy`提示`ERROR Deployer not found: git`，则执行以下命令，再执行`$ hexo deploy`上传到GitHub

```
$ npm install hexo-deployer-git --save
```
上传到github之后，以后想在服务器端修改直接输入命令`hexo d -g`。就可以在你的个人博客地址更新了。

### 方法二：克隆心仪的博客

本方法就相对简单一点，就是你把你心仪的个人博客github fork到你本地，然后安装之后，就可以修改一些基本配置。这样的话要改的也不多，所以更加容易点。
其实也是类似于下面的博客迁移啦。

### 关于博客迁移
此处是你已经根据上面的文章，已经成功利用hexo和github发布博客。
当我们更换电脑的时候，我们应该怎么办呢？

> 具体的思路是：在生成的已经推到github上的hexo静态代码出建立一个分支，利用这个分支来管理自己hexo的源文件。

如果能在刚刚配置hexo的时候就想好以后的迁移的问题就太好了，可以省掉很多麻烦，可实际使用中，刚刚配置hexo的时候，好多人都是初学，不会想到以后的问题，我就是这样的。

克隆gitHub上面生成的静态文件到本地

```
git clone https://github.com/yourname/xxx.github.io.git
```
把克隆到本地的文件除了git的文件都删掉，找不到git的文件的话就到删了吧。不要用`hexo init`初始化。将之前使用hexo写博客时候的整个目录（所有文件）搬过来。把该忽略的文件忽略了。

```
touch .gitignore
```
我自己忽略的是
```
.DS_Store
db.json
*.log
node_modules/
public/
.deploy*/
```

创建一个叫hexo的分支


```
git checkout -b hexo
```

提交复制过来的文件到暂存区


```
git add --all
```
如果这个时候你发现有提示

```
warning: adding embedded git repository: themes/next
hint: You've added another git repository inside your current repository.
hint: Clones of the outer repository will not contain the contents of
hint: the embedded repository and will not know how to obtain it.
hint: If you meant to add a submodule, use:
hint:
hint:   git submodule add <url> themes/next
hint:
hint: If you added this path by mistake, you can remove it from the
hint: index with:
hint:
hint:   git rm --cached themes/next
hint:
hint: See "git help submodule" for more information.
```

我采用了分次上传到github，记得清理下本地的git仓库缓存

提交

```
git commit -m "新建分支源文件"
```

推送分支到github

```
git push --set-upstream origin hexo
```
>注：使用－－ set-upstream 去跟踪远程分支。
