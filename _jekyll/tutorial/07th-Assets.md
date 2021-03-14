---
layout: note
title:  Jekyll — Ⅶ. 资源素材
summary:  Step by Step Tutorial - Ⅶ. Assets（部分翻译，自用帮助了解）
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
	- [Syntactically Awesome Style Sheets](#sass)
- [八、博客写作 ](./08th-Blogging.html)
- [九、集合内容 ](./09th-Collections.html)
- [十、部署网站 ](./10th-Deployment.html)

Jekyll 里资源文件的使用都是很直接的，放到相应文件夹就行了。

Jekyll 里资源素材文件结构通常如下所示：
```
.
├── assets
│   ├── css
│   ├── images
│   └── js
...
```

## Sass
在 `_includes/navigation.html` 里内联（Inlining）样式不是最好的方法，一般会通过类来控制样式：
```html
{% raw %}<nav>
  {% for item in site.data.navigation %}
    <a href="{{ item.link }}" {% if page.url == item.link %}class="current"{% endif %}>{{ item.name }}</a>
  {% endfor %}
</nav>{% endraw %}
```

可以使用标准 CSS 文件控制样式，我们有更进一步的追求所以用  [Sass](https://sass-lang.com/)，这是一种非常好的 CSS 扩展。

首先在 `assets/css/styles.scss` 创建 Sass 文件并添加如下内容：
```sass
---
---
@import "main";
```

空着的头部信息告诉 Jekyll 这个文件需要处理。`@import "main"` 告诉 Sass 去查找 `main.scss` 文件（默认 `_sass/` 文件夹是放在根目录的）。

到这一步你有了主 CSS 文件。对于大型项目，这样组织 CSS 是非常好的方式。

在 `_sass/main.scss` 创建 Sass 文件并添加如下内容：
```sass
.current {
  color: green;
}
```

你要在布局中引用这个样式表。

打开 `_layouts/default.html` 并添加样式表到 `<head>`：
```html
{% raw %}<!doctype html>
<html>
  <head>
    <meta charset="utf-8">
    <title>{{ page.title }}</title>
    <link rel="stylesheet" href="/assets/css/styles.css">
  </head>
  <body>
    {% include navigation.html %}
    {{ content }}
  </body>
</html>{% endraw %}
```

在这里被引用的 `styles.css` 由 Jekyll 从之前在 `assets/css/` 创建的 `styles.scss`生成。

加载 [http://localhost:4000](http://localhost:4000/) 并检查导航中的有效链接为绿。

接下来看看 Jekyll 最受欢迎的特性，博客写作（Blogging）。

---
###### Links
[[Ⅶ]](https://jekyllrb.com/docs/step-by-step/07-assets/) Assets - Jekyll Docs Step by Step Tutorial

