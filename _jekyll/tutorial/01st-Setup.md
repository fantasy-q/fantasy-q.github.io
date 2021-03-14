---
layout: note
title: Jekyll — Ⅰ.前期准备
summary: Step by Step Tutorial - Ⅰ. SETUP（部分翻译，自用帮助了解）
categories: jekyll
published: true
---

## 目录

- [一、前期准备 ](./01st-setup.html)
	- [安装 ](#installation)
	- [创建站点](#create-a-site)
	- [构建](#build)
- [二、模板语言 ](./02nd-Liquid.html)
- [三、头部信息 ](./03rd-Front-Matter.html)
- [四、布局文件 ](./04th-Layouts.html)
- [五、包含文件 ](./05th-Includes.html)
- [六、数据文件 ](./06th-Data-Files.html)
- [七、网站素材 ](./07th-Assets.html)
- [八、博客写作 ](./08th-Blogging.html)
- [九、集合内容 ](./09th-Collections.html)
- [十、部署网站 ](./10th-Deployment.html)

这个教程的目的是在有一定前端 Web 开发经验的基础上，手把手教你从头开始搭建第一个 Jekyll 站点 — 即不依赖默认的主题。

## Installation
Jekyll 是一个 Ruby 程序，所以开始前要线安装 Ruby。详情查看 [install guide](https://jekyllrb.com/docs/installation/)。

1. 安装 Jekyll。
```
gem install jekyll bundler
```
2. 创建 `Gemfile` 记录网站所需的**依赖**（Dependency）。
```
bundle init
```
3. 编辑 `Gemfile` 把 Jekyll 添加作为依赖。
```
gem "jekyll"
```
4. 运行 `bundle` 命令。
```
bundle install 
bundle exec jekyll COMMANDS
```

## Create a site
现在可以真正开始了！随便新建一个文件夹，在后文把这个文件夹叫做**根目录**（Root）。如果比较喜欢鼓捣，可以直接在这创建 Git 仓库。Jekyll 没有数据库，所有网站结构和内容都是文件，可利用 Git 进行**版本控制**（Version）。这一步虽是可选的，为了养成好习惯还是比较推荐试一试的。详情请看 [Git Handbook](https://guides.github.com/introduction/git-handbook/)。

在根目录下创建第一个文件 `index.html`，并添加如下内容：
```html
<!doctype html>
<html>
  <head>
    <meta charset="utf-8">
    <title>Home</title>
  </head>
  <body>
    <h1>Hello World!</h1>
  </body>
</html>
```

## Build
Jekyll 是一个静态网站生成器，在能看到网站之前，要先用 Jekyll 构建网站。在根目录下有两条命令可以用来构建网站：
- `jekyll build` - 构建并输出静态网站到一个叫 `_site` 的目录。
- `jekyll serve` - 和上面差不多，不过执行这条命令后，你进行任何修改，都会实时重构建，并且它还运行在本地服务器 `http://localhost:4000` 上。

在上面的例子，用浏览器访问 [http://localhost:4000](http://localhost:4000/) 应该能看到“Hello World!”。

可能你会想问《意义》何在？把 HTML 文件从复制到另一个地方？这 Jekyll 就是个复读机？Patience, young grasshopper[^1], 还有得学呢！

---
###### Links
[[Ⅰ]](https://jekyllrb.com/docs/step-by-step/01-setup/) Setup - Jekyll Docs Step by Step Tutorial 

---
###### Notes

[^1]: "**Patience, young grasshopper**" comes from a 1970s TV show called *Kung Fu*. [【Quora】](https://www.quora.com/Where-does-that-phrase-patience-young-grasshopper-originate)

