---
layout: post
title:  Jekyll 手把手教学 - 集合内容
summary:  Step by Step Tutorial - Ⅸ. Collections（部分翻译，自用帮助了解。）
categories: jekyll
published: true
---

## 目录

- [一 、前期准备 ](../jekyll/01st-setup.html)
- [二、模板语言 ](../jekyll/02nd-Liquid.html)
- [三、头部信息  ](../jekyll/03th-Front-Matter.html)
- [四、布局文件 ](../jekyll/04th-Layouts.html)
- [五、包含文件 ](../jekyll/05th-Includes.html)
- [六、数据文件 ](../jekyll/06th-Data-Files.html)
- [七、资源素材 ](../jekyll/07th-Assets.html)
- [八、博客写作 ](../jekyll/08th-Blogging.html)
- [九、集合内容 ](../jekyll/09th-Collections.html)
	- [配置](#configuration) 
	- [添加作者](#add-authors)
	- [职员页面](#staff-page)
	- [输出页面](#output-a-page)
	- [头部信息缺省](#front-matter-defaults)
	- [链接到文章](#list-authors-posts)
	- [链接到作者页面](#link-to-authors-page)
- [十、部署网站 ](../jekyll/10th-Deployment.html)

下面看一看如何让每一个作者都能有自己的简介页面并且出版文章。

为了做到这些事情，需要用到**集合**（Collections），类似于文章但是内容没有被按日期分组。

## Configuration
想设置一个集合，你先要告诉 Jekyll，在叫作 `_config.yml` 的文件下配置（缺省）。

在根目录下创建 `_config.yml` 带如下内容：
```yaml
collections:
  authors:
```

重启 Jekyll 服务器重载配置，在终端按 `Ctrl` + `C` 停止服务器，然后 `jekyll serve` 重启。

## Add authors
文档（集合的一项）放在根目录的一个叫 `_*collection_name*` 的文件夹中。这里就是 `_authors`。

为每一个作者创建一个文档：

`_authors/jill.md`：

```markdonw
---
short_name: jill
name: Jill Smith
position: Chief Editor
---
Jill is an avid fruit grower based in the south of France.
```

`_authors/ted.md`：

```markdown
---
short_name: ted
name: Ted Doe
position: Writer
---
Ted has been eating fruit since he was baby.
```

## Staff page
让我们添加一个页面列出所有作者，Jekyll 通过 `site.authors` 使用集合。

创建 `staff.html` 并遍历 `site.authors` 输出所有职员：
```html
---
layout: default
title: Staff
---
{% raw %}<h1>Staff</h1>

<ul>
  {% for author in site.authors %}
    <li>
      <h2>{{ author.name }}</h2>
      <h3>{{ author.position }}</h3>
      <p>{{ author.content | markdownify }}</p>
    </li>
  {% endfor %}
</ul>{% endraw %}
```

因为是 markdown，所以要运行在 `markdowninfy` 滤器下，而使用 `{% raw %}{{ content }}{% endraw %}` 时会自动执行。

还要添加导航，打开 `_data/navigation.yml` 给职员页面添加条目：
```yaml
- name: Home
  link: /
- name: About
  link: /about.html
- name: Blog
  link: /blog.html
- name: Staff
  link: /staff.html
```

## Output a page
缺省状态下集合不会给文文档输出，这个例子中要想每个作者都有自己的页面，要给集合配置做点小小的修改：
```yaml
collections:
  authors:
    output: true
```

重启 Jekyll 服务器看看效果。

你可以用 `author.url` 链接输出页面。

给 `staff.html` 页面添加链接：
```html
---
layout: default
title: Staff
---
{% raw %}<h1>Staff</h1>

<ul>
  {% for author in site.authors %}
    <li>
      <h2><a href="{{ author.url }}">{{ author.name }}</a></h2>
      <h3>{{ author.position }}</h3>
      <p>{{ author.content | markdownify }}</p>
    </li>
  {% endfor %}
</ul>{% endraw %}
```

就像文章页面，同样要给作者页面创建布局。

创建 `_layouts/author.html` 带上如下内容：
```html
---
layout: default
---
{% raw %}<h1>{{ page.name }}</h1>
<h2>{{ page.position }}</h2>

{{ content }}{% endraw %}
```

## Front matter defaults
现在你要用 `author` 布局来配置作者文档，像前面一样在头部信息中使用，但这种重复动作很麻烦。

你想要的是让所有文章自动设置，一切都用缺省值。

这个可以通过 [front matter defaults](https://jekyllrb.com/docs/configuration/front-matter-defaults/) 实现，设置一个缺省值的作用域，然后你就能按你的想法来设置缺省值了。

在 `_config.yml` 里添加缺省值：
```yaml
collections:
  authors:
    output: true

defaults:
  - scope:
      path: ""
      type: "authors"
    values:
      layout: "author"
  - scope:
      path: ""
      type: "posts"
    values:
      layout: "post"
  - scope:
      path: ""
    values:
      layout: "default"
```

现在你能从所有页面和文章的头部信息种移除布局了，注意每次更新 `_config.yml` 都要重启 Jekyll 使其生效。

## List author’s posts
让我们在作者页面列出一个他发表的所有文章，首先将作者 `short_name` 匹配到 `author`，通过这样按作者来过滤文章。

在 `_layouts/author.html` 遍历这个筛选后的列表输出作者的文章：
```html
---
layout: default
---
{% raw %}<h1>{{ page.name }}</h1>
<h2>{{ page.position }}</h2>

{{ content }}

<h2>Posts</h2>
<ul>
  {% assign filtered_posts = site.posts | where: 'author', page.short_name %}
  {% for post in filtered_posts %}
    <li><a href="{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>{% endraw %}
```

## Link to authors page
文章有一个作者的引用，所以让我们把他链接到作者页面，在 `_layouts/post.html` 用相同的筛选方法：
```html
---
layout: default
---
{% raw %}<h1>{{ page.title }}</h1>

<p>
  {{ page.date | date_to_string }}
  {% assign author = site.authors | where: 'short_name', page.author | first %}
  {% if author %}
    - <a href="{{ author.url }}">{{ author.name }}</a>
  {% endif %}
</p>

{{ content }}{% endraw %}
```

打开  [http://localhost:4000](http://localhost:4000/) 看一看职员页面，确保所有链接都正确。

在下一节，也是教程的最后一节，我们再润色一下并为生产环境部署做准备。

---
###### Links
[[Ⅸ]](https://jekyllrb.com/docs/step-by-step/09-collections/) Collections - Jekyll Docs Step by Step Tutorial

