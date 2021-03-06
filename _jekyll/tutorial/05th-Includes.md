---
layout: note
title:  Jekyll — Ⅴ. 包含模板
summary:  Step by Step Tutorial - Ⅴ. Includes（部分翻译，自用帮助了解）
categories: jekyll
published: true
---

## 目录

- [一、前期准备 ](./01st-Setup.html)
- [二、模板语言 ](./02nd-Liquid.html)
- [三、头部信息 ](./03rd-Front-Matter.html)
- [四、布局模板 ](./04th-Layouts.html)
- [五、包含模板 ](./05th-Includes.html)
	- [包含标签](#include-tag)
	- [包含标签用法](#include-usage)
	- [高亮当前页面](#current-page-highlighting) 
- [六、数据文件 ](./06th-Data-Files.html)
- [七、网站素材 ](./07th-Assets.html)
- [八、博客写作 ](./08th-Blogging.html)
- [九、集合内容 ](./09th-Collections.html)
- [十、部署网站 ](./10th-Deployment.html)

网站快建好了，不过现在还不能在各个页面之间**导航**（Navigation ）。

导航应该显示在所有页面，因此布局文件就是一个添加导航的正道，不过不是直接添加到布局中。借此机会，了解下**包含模板**（Includes）。

## Include tag
标签 `include` 可以让你从 `_includes`文件夹中包含内容。对于那些来源单一、重复出现的源码或者为了提高可读性，都可以让包含模板帮你。

导航源码复杂的时候放在包含文件中就挺不错的。

## Include usage
给导航创建文件放在 `_includes/navigation.html`，添加如下内容：
```html
<nav>
  <a href="/">Home</a>
  <a href="/about.html">About</a>
</nav>
```

试着用包含标签把导航添加到 `_layouts/default.html`；
```html
{% raw %}<!doctype html>
<html>
  <head>
    <meta charset="utf-8">
    <title>{{ page.title }}</title>
  </head>
  <body>
    {% include navigation.html %}
    {{ content }}
  </body>
</html>{% endraw %}
```

打开 [http://localhost:4000](http://localhost:4000/) 看看能不能切换页面。

## Current page highlighting
继续深入顺便在导航中高亮下当前页面。

`_includes/navigation.html` 需要知道当前页面的 URL 方便添加样式，Jekyll 正好提供了一个[变量](https://jekyllrb.com/docs/variables/) `page.url`。

利用`page.url` 检查各个链接是否为当前页面，为真就把它设置为红：
```html
{% raw %}<nav>
  <a href="/" {% if page.url == "/" %}style="color: red;"{% endif %}>
    Home
  </a>
  <a href="/about.html" {% if page.url == "/about.html" %}style="color: red;"{% endif %}>
    About
  </a>
</nav>{% endraw %}
```

去 [http://localhost:4000](http://localhost:4000/) 看一看当前页面链接是否为红。

如果想添加新项到导航或者改变高亮颜色，就会产生许多重复工作。下一节讲讲这个问题。

---
###### Links
[[Ⅴ]](https://jekyllrb.com/docs/step-by-step/01-Setup/) Includes -  Jekyll Docs Step by Step Tutorial
