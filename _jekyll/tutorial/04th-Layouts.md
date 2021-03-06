---
layout: note
title:  Jekyll — Ⅳ. 布局模板
summary:  Step by Step Tutorial - Ⅳ. Layouts（部分翻译，自用帮助了解）
categories: jekyll
published: true
---

## 目录

- [一、前期准备 ](./01st-Setup.html)
- [二、模板语言 ](./02nd-Liquid.html)
- [三、头部信息 ](./03rd-Front-Matter.html)
- [四、布局模板 ](./04th-Layouts.html)
	- [创建布局](#creating-a-layout)
	- [关于页面](#about-page) 
- [五、包含模板 ](./05th-Includes.html)
- [六、数据文件 ](./06th-Data-Files.html)
- [七、网站素材 ](./07th-Assets.html)
- [八、博客写作 ](./08th-Blogging.html)
- [九、集合内容 ](./09th-Collections.html)
- [十、部署网站 ](./10th-Deployment.html)

网站一般不止一个文件，这个也不例外。

Jekyll 支持 [Markdown](https://daringfireball.net/projects/markdown/syntax) 以及 HTML 页面。对于那些内容结构简单（只有段落，标题和图片）的页面，用 Markdown 准没错。比起 HTML 它简洁不少。下面就试一试。

在根目录创建 `about.md`。 

关于页面的结构可以复制 `index.html` 再做些许修改。问题就在这，比如说你想添加样式，可能要去改每个页面的 `<head>`。两个页面还好说，100 个呢？

## Creating a layout
使用布局模板是一个比较好的选择。**布局**是包裹（wrap）内容用的模板，它们位于 `_layouts` 目录。

在 `_layouts/default.html` 创建第一个布局文件，并添加如下内容：
```html
{% raw %}<!doctype html>
<html>
  <head>
    <meta charset="utf-8">
    <title>{{ page.title }}</title>
  </head>
  <body>
    {{ content }}
  </body>
</html>{% endraw %}
```

应该注意到了这和 `index.html` 基本相同。

在头部信息中添加 `layout` 变量，就能让 `index.html` 使用布局：
```html
{% raw %}---
layout: default
title: Home
---
<h1>{{ "Hello World!" | downcase }}</h1>{% endraw %}
```
做了这些微小工作后，输出应该和改之前完全一样。你也能中布局中访问 `page` 头部信息，这个例子中， `title` 在主页的头部信息中设置，在布局中输出。

## About page
回到关于页面，这次不复制 `index.html`，而是使用布局。

添加如下内容于 `about.md`：
```markdown
---
layout: default
title: About
---
# About page

This page tells you a little bit about me.
```

打开 [http://localhost:4000/about.html](http://localhost:4000/about.html)，看一看你的新页面。

Congratulations，你的网站现在有两个页面了！但要怎样才能实现页面到另一个页面的导航？继续。

---
###### Links
[[Ⅳ]](https://jekyllrb.com/docs/step-by-step/01-Setup/) Layouts - Jekyll Docs Step by Step Tutorial
