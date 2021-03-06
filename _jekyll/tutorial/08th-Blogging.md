---
layout: note
title:  Jekyll — Ⅷ. 博客写作
summary:  Step by Step Tutorial - Ⅷ. Blogging（部分翻译，自用帮助了解）
categories: jekyll
published: true
---

## 目录

- [一、前期准备 ](./01st-Setup.html)
- [二、模板语言 ](./02nd-Liquid.html)
- [三、头部信息 ](./03rd-Front-Matter.html)
- [四、布局模板 ](./04th-Layouts.html)
- [五、包含模板 ](./05th-Includes.html)
- [六、数据文件 ](./06th-Data-Files.html)
- [七、资源素材 ](./07th-Assets.html)
- [八、博客写作 ](./08th-Blogging.html)
  - [文章](#posts)
  - [布局](#layout)
  - [列出文章](#list-posts)
- [九、集合内容 ](./09th-Collections.html)
- [十、部署网站 ](./10th-Deployment.html)

可你你会疑惑没有数据库怎么写博客。在真正的 Jekyll 下，博客写作只由文本文件提供支持。

## Posts
博客文章放在文件夹 `_posts` 中。文件名要求特别的格式：出版日期，标题以及扩展名。

在 `_posts/2018-08-20-bananas.md` 创建第一个文章，添加如下内容：
```
---
layout: post
author: jill
---
A banana is an edible fruit – botanically a berry – produced by several kinds
of large herbaceous flowering plants in the genus Musa.

In some countries, bananas used for cooking may be called "plantains",
distinguishing them from dessert bananas. The fruit is variable in size, color,
and firmness, but is usually elongated and curved, with soft flesh rich in
starch covered with a rind, which may be green, yellow, red, purple, or brown
when ripe.
```

这有点像 `about.md`，不过这个有不同的布局和作者。`author` 是有个自定义变量，不是必要的而且可以命名为 `creator`之类的其他名字。

## Layout
现在还没有文章布局，所以赶紧在 `_layouts/post.html` 创建一个：
```hmtl
---
layout: default
---
{% raw %}<h1>{{ page.title }}</h1>
<p>{{ page.date | date_to_string }} - {{ page.author }}</p>

{{ content }}{% endraw %}
```

这是一个布局继承的例子。这个布局输出被缺省布局包裹的标题，数据，作者和内容主体。

还要注意 `date_to_string` 滤器，它能将格式化日期成一个更好的格式显示。

## List posts
当前还没有办法导航博客文章。通常博客会有一个页面列出所有文章，接下来就试试这个。

Jekyll 通过 `site.posts` 提供文章。

在根目录创建 `blog.html`(即 `/blog.html`)，添加如下内容：
```html
---
layout: default
title: Blog
---
{% raw %}<h1>Latest Posts</h1>

<ul>
  {% for post in site.posts %}
    <li>
      <h2><a href="{{ post.url }}">{{ post.title }}</a></h2>
      {{ post.excerpt }}
    </li>
  {% endfor %}
</ul>{% endraw %}
```

这段代码中有些许需注意之处：
- `post.url` 由 Jekyll 自动设置成文章的输出路径
- `post.title` 从文章文件名拉取，同时也能被头部信息的 `title` 重写。
- `post.excerpt` 缺省状态时是文章内容的第一段

你还要从主导航通过某种方式导航到这些页面，打开 `_data/navigation.yml` 给博客页面添加一个入口：
```yaml
- name: Home
  link: /
- name: About
  link: /about.html
- name: Blog
  link: /blog.html
```

## More posts
只有一篇文章没什么意思，再添加几篇吧：
`_posts/2018-08-21-apples.md`：
```markdown
---
layout: post
author: jill
---
An apple is a sweet, edible fruit produced by an apple tree.

Apple trees are cultivated worldwide, and are the most widely grown species in
the genus Malus. The tree originated in Central Asia, where its wild ancestor,
Malus sieversii, is still found today. Apples have been grown for thousands of
years in Asia and Europe, and were brought to North America by European
colonists.
```

`_posts/2018-08-22-kiwifruit.md`：
```markdown
---
layout: post
author: ted
---
Kiwifruit (often abbreviated as kiwi), or Chinese gooseberry is the edible
berry of several species of woody vines in the genus Actinidia.

The most common cultivar group of kiwifruit is oval, about the size of a large
hen's egg (5–8 cm (2.0–3.1 in) in length and 4.5–5.5 cm (1.8–2.2 in) in
diameter). It has a fibrous, dull greenish-brown skin and bright green or
golden flesh with rows of tiny, black, edible seeds. The fruit has a soft
texture, with a sweet and unique flavor.
```

打开  [http://localhost:4000](http://localhost:4000/) 看一看。

下一节我们重点讨论创建页面。

---
###### Links
[[Ⅷ]](https://jekyllrb.com/docs/step-by-step/08-blogging/) Blogging -  Jekyll Docs Step by Step Tutorial

