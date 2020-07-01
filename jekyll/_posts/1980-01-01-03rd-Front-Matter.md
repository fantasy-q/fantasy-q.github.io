---
layout: note
title:  Jekyll 手把手教学 - 头部信息
summary:  Step by Step Tutorial - Ⅲ. Front Matter（部分翻译，自用帮助了解。）
categories: jekyll
tags: jekyll
published: true
---

## 目录

- [一 、前期准备 ](../jekyll/01st-setup.html)
- [二、模板语言 ](../jekyll/02nd-Liquid.html)
- [三、头部信息  ](../jekyll/03th-Front-Matter.html)
  - [使用头部信息](#use-front-matter)
- [四、布局文件 ](../jekyll/04th-Layouts.html)
- [五、包含文件 ](../jekyll/05th-Includes.html)
- [六、数据文件 ](../jekyll/06th-Data-Files.html)
- [七、网站素材 ](../jekyll/07th-Assets.html)
- [八、博客写作 ](../jekyll/08th-Blogging.html)
- [九、集合内容 ](../jekyll/09th-Collections.html)
- [十、部署网站 ](../jekyll/10th-Deployment.html)

头部信息是 [YAML](http://yaml.org/) 的一小部分，在文件顶部的两条三连划线之间。头部信息可以给页面设置变量，像这样：
```yaml
---
my_number: 5
---
```

Liquid 通过 `page` 可以使用头部信息变量。举个例子，输出上面的的变量：
```html
{% raw %}{{ page.my_number }}{% endraw %}
```

## Use front matter
添加头部信息来改变网站的 `title`：
```html
{% raw %}---
title: Home
---
<!doctype html>
<html>
  <head>
    <meta charset="utf-8">
    <title>{{ page.title }}</title>
  </head>
  <body>
    <h1>{{ "Hello World!" | downcase }}</h1>
  </body>
</html>{% endraw %}
```

注意为了让 Jekyll 处理页面的一切标签，必须包含头部信息。至少也要这样：
```
---
---
```

可能你不懂为什么要搞这么麻烦，源码写得都比 HTML 还要多了，下一节告诉你。

---
###### Links
[[Ⅲ]](https://jekyllrb.com/docs/step-by-step/03-front-matter/) Front Matter -  Jekyll Docs Step by Step Tutorial

