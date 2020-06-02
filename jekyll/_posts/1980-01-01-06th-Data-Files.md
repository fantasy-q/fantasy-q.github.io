---
layout: post
title:  Jekyll 手把手教学 - 数据文件
summary:  Step by Step Tutorial - Ⅵ. Data Files（部分翻译，自用帮助了解。）
categories: jekyll
published: true
---

## 目录

- [一 、前期准备 ](../jekyll/01st-setup.html)
- [二、模板语言 ](../jekyll/02nd-Liquid.html)
- [三、头部信息  ](../jekyll/03rd-Front-Matter.html)
- [四、布局模板 ](../jekyll/04th-Layouts.html)
- [五、包含模板 ](../jekyll/05th-Includes.html)
- [六、数据文件 ](../jekyll/06th-Data-Files.html)
	- [数据文件用法](#data-file-usage)
- [七、资源素材 ](../jekyll/07th-Assets.html)
- [八、博客写作 ](../jekyll/08th-Blogging.html)
- [九、集合内容 ](../jekyll/09th-Collections.html)
- [十、部署网站 ](../jekyll/10th-Deployment.html)

Jekyll 支持从位于 `_data` 目录的  YAML，JSON 和 CSV 文件中加载数据。数据文件将内容从源码分离，使得网站更容易维护。

这一节将会把导航的内容存储在数据文件中，然后在导航包含中遍历它。

## Data file usage

[YAML](http://yaml.org/) 是一个在 Ruby 生态圈常用的格式。

为导航在 `_data/navigation.yml` 处创建数据文件，并添加如下内容：
```yaml
- name: Home
  link: /
- name: About
  link: /about.html
```

Jekyll 让你通过 `site.data.navigation` 使用这个数据文件，现在可以遍历这个数据文件了：
```html
{% raw %}<nav>
  {% for item in site.data.navigation %}
    <a href="{{ item.link }}" {% if page.url == item.link %}style="color: red;"{% endif %}>
      {{ item.name }}
    </a>
  {% endfor %}
</nav>{% endraw %}
```

输出完全一样，区别在于添加新的导航项以及改变 HTML 结构都变得更简单了。

不过没有 CSS、JS 和图片的网站又有什么意思呢？让我们来看看在 Jekyll 里如何处理资源文件吧。

---
###### Links
[[Ⅵ]](https://jekyllrb.com/docs/step-by-step/06-data-files/) Data Files - Jekyll Docs Step by Step Tutorial
