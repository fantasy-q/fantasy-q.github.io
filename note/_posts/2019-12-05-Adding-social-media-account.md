---
layout: post
title:  "在页脚添加特定账号"
date:   2019-12-05 01:24:41 +0800
summary: 在 FOOTER 部分添加特定的社交媒体账号
categories: note
published: true
---

## 写在前面

想给网站改个样子，然而什么都不懂。看文档，大段大段的英文看得头疼，又不想简单粗暴地用别人的主题，还是先试着默认的主题上做修改吧。

看到网页底部可以显示 GitHub 和 Twitter，看了下它默认还可以显示 YouTube、Instagram 什么的。因为都已经设置好了，只需要在 `_config.yml` 中添加 `SOCIAL_username: USERNAME` 就可以显示了。

综上，先自己试着实现添加 bilibili 账号。

## 添加链接

先在页面上找线索，主页的源代码底部，有这样一段：

```html
<div class="footer-col footer-col-2">
    <ul class="social-media-list">
        <li><a href="https://github.com/fantasy-q">
                <svg class="svg-icon">
                    <use xlink:href="/assets/minima-social-icons.svg#github"></use>
                </svg>
                <span class="username">fantasy-q</span>
            </a>
        </li>
    </ul>
</div>
```

`footer-col-2`：footer 的第二列？

`social-media-list`：社交媒体列表？

`svg-icon`：svg？ Scalable Vector Graphics，可缩放矢量图形？

`/assets/minima-social-icons.svg#github`：应该是图标的数据。

好像都没什么用，于是翻了下 minima 的 gem，在 `_includes` 中找到了 `social.html`，其中一段：

```html
{% raw %}{%- if site.github_username -%}{% endraw %}
<li>
    <a href="https://github.com/{% raw %}{{ site.github_username| cgi_escape | escape }}{% endraw %}">
        <svg class="svg-icon">
            <use xlink:href="{% raw %}{{ '/assets/minima-social-icons.svg#github' | relative_url }}{% endraw %}"></use>
        </svg> 
        <span class="username">{% raw %}{{ site.github_username| escape }}{% endraw %}</span>
    </a>
</li>
{% raw %}{%- endif -%}{% endraw %}
```

这和主页底部的源码很相似嘛，依葫芦画瓢：

```html
{% raw %}{%- if site.bilibili_uid -%}{% endraw %}
<li>
    <a href="https://space.bilibili.com/{% raw %}{{ site.bilibili_uid| cgi_escape | escape }}{% endraw %}">
        <svg class="svg-icon">
            <use xlink:href="{% raw %}{{ '/assets/minima-social-icons.svg#bilibili' | relative_url }}{% endraw %}"></use>
        </svg> 
        <span class="username">{% raw %}{{ site.bilibili_uid| escape }}{% endraw %}</span>
    </a>
</li>
{% raw %}{%- endif -%}{% endraw %}
```

按照文档所说，我应该自己在目录中重新创建一个同名文件来**重写**它默认的文件。效果很好，立竿见影。但它还没有图标，而且显示的是 `uid`，由于 b 站使用昵称，可以随时更改，所以我希望它直接显示 `bilibili`，

## 关于图标

初步想法：

1. 通过 `https://www.bilibli.com/favicon.ico` 获取 `.ico`
2. 将 `.ico` 转换成 `.svg`
3. 放到 `/assets/minima-social-icons.svg#bilibili` 

试了下果然没那么简单，直接转换的 `.svg` 没有 `<path d="..."/>`，强行放进去结果就是图标尺寸不对，颜色不搭，还是先了解下 `.svg` 文件吧。

`bitmap` 转 ` vector` 好像不是一件简单的事，可能要自行绘制，看来是弄不好了。

发现 [nullice](https://github.com/nullice/NViconsLib_Silhouette) 绘制了一些矢量图标，其中包括b站的，在此表示感谢。

## 写在最后

姑且算弄好了，不知道绘制矢量图标难度如何，找个时间学习下。

还有不知道什么原因，我自己添加的账号和默认的没对齐，差了一个字符，像这样：

```
[图标] GitHub
[图标]bilibli
```

于是我在前面加了一个空格，但对我来说，人为对齐很不「自然」，心里不舒服，然而现在不想弄了，先不管了。

虽然变化不大，不过知道了矢量图这种东西，并稍微理解了 Liquid 和 variable 的关系，也挺好的。