---
title: "使用hugo搭建博客"
date: 2020-01-31T13:29:23+08:00
draft: false
tags: ["hugo", "blog", "front end"]
---

Hugo 是 Go 语言实现的一个博客生成器，世界上最快的博客生成器，最受欢迎的开源靜态站点生成器之一。Hugo 和 Hexo 一样，是一种通用的网站框架。这类应用将 Markdown 文件和主题一起编译成由 HTML、CSS、JavaScript 组成的静态网页。
下面简单介绍一下如何使用 hugo 来搭建一个博客。

# Step 1:Install Hugo/安装 Hugo

## windows 安装方式：

1. 去 [Hugo Releases](https://github.com/gohugoio/hugo/releases)页面下载 hugo_xxx_Windows-64bit.zip，32 位就下载 32 位的。
2. 下载后解压，将 hugo.exe 放到 D:\Software\hugo
3. 将 D:\Software\hugo 加到 PATH
   > 如何设置环境变量 path？  
   > 打开文件夹-->右击此电脑-->选择属性-->高级系统设置-->环境变量-->双击 path-->新建-->将 hugo.exe 所在的路径复制粘贴-->确定
4. 重启终端，运行`hugo version`查看版本，若出现版本号表示成功安装，若不成功，查看加入 path 的路径是否填对。

```
λ hugo version
Hugo Static Site Generator v0.63.1-CE9ACEB7 windows/amd64 BuildDate: 2020-01-23T20:09:17Z
```

# Step 2:Create a New Site/创建一个新网站

`hugo new site 81kong.github.io-creator`
上面的代码将会在 81kong.github.io-creator 文件夹里创建一个新的网站

# Step 3: Add a Theme/添加主题

我使用默认的 ananke 主题
首先，我们先进入创建的文件夹 81kong.github.io-creator，并初始化。
然后，从 github 上下载主题 ananke，代码如下：

```
cd 81kong.github.io-creator
git init
git submodule add https://github.com/budparr/gohugo-theme-ananke.git themes/ananke
```

最后，将主题添加到网站配置中：
`echo 'theme = "ananke"' >> config.toml`

此时的目录结构应该是这样:

> .  
> ├── archetypes # 内容类型，在创建新内容时自动生成内容的配置  
> ├── content # 网站内容，Markdown 文件  
> ├── data  
> ├── layouts # 网站模版，选择主题后会将主题中的 layouts 文件夹中的内容复制到此文件夹中  
> ├── static # 包含 CSS、JavaScript、Fonts、media 等，决定网站的外观。选择主题后会将主题中的 ststic 文件夹中的内容复制到此文件夹中  
> ├── themes # 存放主题文件  
> └── config.toml # 网站的配置文件

# Step 4: Add Some Content/添加一些内容

写一篇新博客，名字叫《使用 hugo 搭建博客》
`hugo new posts/使用hugo搭建博客.md`  
此时 content 文件夹下就多了一个 使用 hugo 搭建博客.md 文件，打开文件就可以看到时间、文件名等信息已经自动生成了:

```
---
title: "使用hugo搭建博客"
date: 2020-01-31T13:29:23+08:00
draft: true
---
```

两条 --- 间的信息是文章的配置信息，有的信息是自动生成的 (如：title、date 等)，简单介绍以下各项配置:

- 以下项目是自动生成的:  
  title: # 文章标题  
  date: # 写作时间  
  draft: # 是否为草稿，如果为 true 需要在命令中加入 --buildDrafts 参数才会生成这个文档。或者写完后改为 false，则可以通过网址看到这篇博客。
- 以下项目需要自行添加:  
  description: # 描述  
  tags: # 标签，用于文章分类  
  自动生成 和 执行添加 的内容并不是绝对的，你可以根据自己的喜好配置模板文件 archetypes/default.md

## 配置 config.toml

config.toml 用于存放整个网站的配置信息。  
以下是我搜到的一个 config.toml 模板，按照需求更改：

1. baseURL = "https://81kong.github.io" # <head> 里面的 baseurl 信息，填你的博客地址
2. title = "Rona's Blog" # 浏览器的标题
3. languageCode = "zh-Hans" # 语言
4. hasCJKLanguage = true # 开启可以让「字数统计」统计汉字
5. theme = "ananke" # 主题 (需要自己下载)
6. paginate = 11 # 每页的文章数
7. enableEmoji = true # 支持 Emoji
8. enableRobotsTXT = true # 支持 robots.txt
9. googleAnalytics = "" # Google 统计 id

# Step 5: Start the Hugo server/启动 hugo 服务器

现在，可以启动服务器：  
`hugo server -D`  
界面如下：

```
λ hugo server -D
Building sites …
                   | EN
-------------------+-----
  Pages            | 11
  Paginator pages  |  0
  Non-page files   |  0
  Static files     |  3
  Processed images |  0
  Aliases          |  1
  Sitemaps         |  1
  Cleaned          |  0

Built in 51 ms
Watching for changes in D:\rona\81kong.github.io-creator\{archetypes,content,data,layouts,static,themes}
Watching for config changes in D:\rona\81kong.github.io-creator\config.toml
Environment: "development"
Serving pages from memory
Running in Fast Render Mode. For full rebuilds on change: hugo server --disableFastRender
Web Server is available at http://localhost:1313/ (bind address 127.0.0.1)
Press Ctrl+C to stop
```

现在，可以通过[http://localhost:1313/](http://localhost:1313/)来观看我的博客。  
可以随意编辑或者添加新内容，只需要在浏览器中刷新就可以快速查看更改。

# Step 6: Customize the Theme/自定义主题

## 站点配置

打开 config.toml，自行配置

```
baseURL = "http://81kong.github.io/"
languageCode = "zh-Hans"
title = "Rona's blog"
theme = "ananke"
hasCJKLanguage = true
enableEmoji = true
```

# Step 7: Build static pages/生成静态页

直接运行  
`hugo -D`  
此时你的博客目录下会多出一个 public 文件夹来。这便是 Hugo 生成的网站。

# step 8：发布

Hugo 并没有提供自动发布到 GitHub Pages 的功能。需要将 public 中的内容手动上传到 Github 上。  
上传步骤如下：

1. 在 81kong.github.io-creator 文件夹里新建.gitignore 文件，里面写上`/public/`
2. 在 github 中建新仓库 81kong.github.io
3. cd public，将仓库复制到本地，将 public 推送到仓库 81kong.github.io。
4. 通过 settings 即可找到预览网址。

# _知识链接_

如何在博客中添加字数统计：
先在自己主题的 single.html 的配置中搜索要放的位置,并在{{ end }}后面添加一下代码,比如我的主题对应的 single.html 路径为 themes\ananke\layouts_default\single.html，再添加如下代码：

```
<span class="post-word-count">, {{ .WordCount }} words</span>
```

·end·

本文参考了以下文章：

1. https://gohugo.io/getting-started/quick-start/
2. https://mogeko.me/2018/018/

声明：转载请注明出处，侵权必究。
