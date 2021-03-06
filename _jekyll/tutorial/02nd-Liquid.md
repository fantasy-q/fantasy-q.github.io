---
layout: note
title:  Jekyll — Ⅱ. 模板语言
summary:  Step by Step Tutorial - Ⅱ. LIQUID（部分翻译，自用帮助了解）
categories: jekyll
published: true
---

## 目录

- [一、前期准备 ](./01st-Setup.html)
- [二、模板语言 ](./02nd-Liquid.html)
	- [对象](#objects) 
	- [标签](#tags)
	- [滤器](#filters)
	- [使用 Liquid](#use-liquid)
- [三、头部信息 ](./03rd-Front-Matter.html)
- [四、布局文件 ](./04th-Layouts.html)
- [五、包含文件 ](./05th-Includes.html)
- [六、数据文件 ](./06th-Data-Files.html)
- [七、网站素材 ](./07th-Assets.html)
- [八、博客写作 ](./08th-Blogging.html)
- [九、集合内容 ](./09th-Collections.html)
- [十、部署网站 ](./10th-Deployment.html)

从 Liquid 开始 Jekyll 就变得稍微有趣起来了。Liquid 是一种**模板语言**，主要分为三部：**对象**，**标签**和**滤器**（*objects*, *tags* and *filters*）。

## Objects
对象指明需要输出的内容在哪。它们被一对双花括号 `{% raw %}{{{% endraw %}` 和 `{% raw %}}}{% endraw %}` 所标志。像这样：
```html
{% raw %}{{ page.title }}{% endraw %}
```

输出那个叫 `page.title` 的变量到这个页面。

## Tags
标签给模板创造逻辑和控制流。它们被一对花括百分号 `{% raw %}{%{% endraw %}` 和 `{% raw %}%}{% endraw %}` 所标志。像这样：
```html
{% raw %}{% if page.show_sidebar %}
  <div class="sidebar">
    sidebar content
  </div>
{% endif %}{% endraw %}
```

输出**侧栏**（Sidebar），如果 `page.show_sidebar` 为真。更多关于标签的说明可看[这儿](https://jekyllrb.com/docs/liquid/tags/)。

## Filters
滤器改变对象的输出。它们和输出一起使用，并用 `|` 分隔。像这样：
```html
{% raw %}{{ "hi" | capitalize }}{% endraw %}
```

输出 `Hi`。更多关于滤器的说明看[这儿](https://jekyllrb.com/docs/liquid/filters/).。

## Use Liquid
你的回合，把那个 Hello World! 改成小写输出：
```html
...
<h1>{% raw %}{{ "Hello World!" | downcase }}{% endraw %}</h1>
...
```

为了让这个修改被 Jekyll 处理，去页面顶部添加一下**头部信息**（Front Matter）：
```yaml
---
# front matter tells Jekyll to process Liquid
---
```

现在这个  “Hello World!” 会渲染成小写。

可能现在体会不到，但 Jekyll 的大多数能力都是来自于 Liquid 与其他特性的绑定。

为了观察滤器 `downcase` 带来的改变，需要添加头部信息。

这就是下一节的内容，让我们继续吧。

---
###### Links
[[Ⅱ]](https://jekyllrb.com/docs/step-by-step/02-liquid/) Liquid - Jekyll Docs Step by Step Tutorial

