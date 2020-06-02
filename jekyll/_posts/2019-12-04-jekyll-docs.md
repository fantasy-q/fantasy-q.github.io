---
layout: post
title:  JEKYLL DOCUMENTS
date:   2019-12-04 00:43:00 +0800
summary: 摘抄 Jekyll 官方文档，帮助自己理解
categories: note
published: true
---

- [Jekyll 简介](#quickstart)
	- [安装](安装)
- [Ruby 基础](#ruby-101)
	- [Gem 包](#gems) 
	- [Gemfile 文件](#gemfile)
	- [Bundler 包管理工具](#bundler)
- [YAML 头信息](#front-matter)
	- [预定义全局变量](#predefined-global-variables) 
	- [自定义变量](#custom-variables)
	- [post 的预定义变量](#predefined-variables-for-posts)
- [目录结构](#directory-structure)
- [模板语言 Liquid](#liquid)
- [网站变量](#variable)
	- [全局变量](#global-variables)

## QuickStart
*Jekyll is a static site generator.*

使用标记语言键入文本，用**布局**创建静态网站，然后可以决定如何显示内容，调整网站 URL等。

### Installation

*Jekyll is a Ruby Gem that can be installed on most systems.*

安装前的准备 [(Requirements)](https://jekyllrb.com/docs/installation/#requirements)。

1. 安装 Ruby 开发环境。
2. 安装 Jekyll 和 bundler gem。
```
gem install jekyll bundler
# 之前安装过：gem update jekyll
```
3. 创建网站在 `./myblog`。
```
jekyll new myblog
# 强制执行：--force
```
4. 切换目录。 
```
cd myblog
```
5. 搭建网站并让它哟行在本地服务器。
```
bundle exec jekyll serve
# 自定义HOST：--host=HOST
# 自定义PORT：--port=PORT
```
6. 浏览 `http://localhost:4000`。

## Ruby 101

*Jekyll is written in Ruby.*

简单了解下 [Ruby](https://jekyllrb.com/docs/ruby-101/) 的相关技术。

### Gems
*A gem is code you can include in Ruby projects.*
Gems 有这些功能：

- 将 Ruby object 转换成 JSON
- 分页 （Pagination）
- 与 APIs 交互，比如 GitHub
- Jekyll 本身就是 gem，包括很多 Jekyll plugins 如 [jekyll-feed](https://github.com/jekyll/jekyll-feed), [jekyll-seo-tag](https://github.com/jekyll/jekyll-seo-tag) 和 [jekyll-archives](https://github.com/jekyll/jekyll-archives) 也是

### Gemfile
`Gemfile` 是记录着网站必需的 gem 的一个列表。对于一个比较简单的网站它可能长这样：

```
source "https://rubygems.org"

gem "jekyll"

group :jekyll_plugins do
  gem "jekyll-feed"
  gem "jekyll-seo-tag"
end
```

### Bundler
*Bundler installs the gems in your `Gemfile`.*

虽然不是必需的，但它可以确保你在不同的环境中，运行着相同版本的 Jekyll 和 plugins，所以还是安装比较好。

关于如何使用 Bundler 戳[这里](https://jekyllrb.com/tutorials/using-jekyll-with-bundler/)。

## Front Matter

*Any file that contains a [YAML](https://yaml.org/) front matter block will be processed by Jekyll as a special file.*
简单说下 [Front Matter](https://jekyllrb.com/docs/front-matter/)。

```
---
layout: post
title: Blogging Like a Hacker
---
```

在 `---` 之间，你可以预定义变量，甚至创造自定义变量。

These variables will then be available to you to access using Liquid tags both further down in the file and also in any layouts or includes that the page or post in question relies on.

### Predefined Global Variables

*There are a number of predefined global variables that you can set in the front matter of a page or post.*

| 变量 | 描述 |
| ---- | ---- |
| `layout` | 指定使用的 layout 文件。layout 文件必须放在 `_layouts` 目录中。<br>- `null` 表示不使用 layout 文件。对 post/document 无效。<br>- 从版本 3.5.0 之后，可以在 post/document 中用 `none` 。 |
| `permalink` | 用于生成 URLs。（缺省为 `/year/month/day/title.html`） |
| `published` | 设为 `false`，可以在生成网站时，不上传指定的 post。 |

### Custom Variables

*You can also set your own front matter variables you can access in Liquid. For instance, if you set a variable called `food`, you can use that in your page:*

```
---
food: Pizza
---

{% raw %}<h1>{{ page.food }}</h1>{% endraw %}
```

### Predefined Variables for Posts

*These are available out-of-the-box to be used in the front matter for a post.*

| 变量 | 描述 |
| ---- | ---- |
| `date` | 重写文件名的日期，确保 post 的排序。（格式：`YYYY-MM-DD HH:MM:SS +/-TTTT`） |
| `category`<br>`categories` | 可以指定多个类别，代替文件夹进行分类。指派多个类别时可以使用 [YAML list](https://en.wikipedia.org/wiki/YAML#Basic_components) 或空格分隔的字符串。 |
| `tags` | 类似 `categories`，可以添加多个 tag。 |

## [Directory Structure](https://jekyllrb.com/docs/structure/)

| 文件 / 目录 | 描述 |
| ---- | ---- |
| `_config.yml` | 配置数据。多数选项可以从命令行得到说明，不用特地去记。 |
| `_drafts` | 暂时用不上。Learn how to [work with drafts](https://jekyllrb.com/docs/posts/#drafts) |
| `_includes` | 可以重复利用的片段。匹配在 layouts 和 posts 中。 |
| `_layouts` | wrap posts 的模板。可以匹配在 layouts 和 posts 中。了解 [Liquid](https://jekyllrb.com/docs/step-by-step/02-liquid/)。 |
| `_posts` | 动态内容。注意文件格式：`YEAR-MONTH-DAY-title.MARKUP` |
| `_data` | 各种格式化好的数据。（支持 `.yml`, `.yaml`, `.json`, `.csv` 或 `.tsv`） |
| `_sass` | 可以导入到 `main.scss` 的片段。定义网站的样式。 |
| `_site` | Jekyll 生成的网站。建议加到 `gitignore` 文件中。 |
| `jekyll-metadata` | 暂时用不上，跳过 |
| `index.html` 或<br> `index.md` 和<br>其他的 HTML，<br>Markdown文件 | 主要就是 [Front Matter](https://jekyllrb.com/docs/front-matter/) 部分。 |
| Other Files/Folders | 可以自己创建目录。了解有哪些[使用 Jekyll 的网站](https://jekyllrb.com/showcase/)。 |

## [Liquid](https://jekyllrb.com/docs/liquid/)

*Jekyll uses the [Liquid](https://shopify.github.io/liquid/) templating language to process templates.*

简而言之，输出内容： {% raw %}`{{ variable }}`{% endraw %}；执行逻辑：{% raw %}`{% if statement %}`{% endraw %}。（[注](https://segmentfault.com/q/1010000004530151/a-1020000004530401)）

想了解更多关于 Liquid 的信息，请查看 [Liquid 官方文档](https://shopify.github.io/liquid/)。

除了 Liquid 官方文档中的，Jekyll 还额外添加了一些 [Filters](https://jekyllrb.com/docs/liquid/filters/) 和 [Tags](https://jekyllrb.com/docs/liquid/tags/) 帮助你搭建网站。

## [Variables](https://jekyllrb.com/docs/variables/)

*Jekyll makes a variety of data available via the [Liquid](https://jekyllrb.com/docs/liquid/).*

### Global Variables

| 变量 | 描述 |
| ---- | ---- |
| `site` | 全站信息 + `_config.yml` 里的配置设定。 |
| `page` | 页面信息 + [front matter](https://jekyllrb.com/docs/front-matter/)。可以通过 front matter 自定义变量。 |
| `layout` | Layout 信息 + [front matter](https://jekyllrb.com/docs/front-matter/). 可以通过 front matter 自定义变量。 |
| `content` | In layout files, the rendered content of the Post or Page being wrapped. Not defined in Post or Page files. |
| `paginator` | 配置了 `paginate` 后，就可以使用这个变量。See [Pagination](https://jekyllrb.com/docs/pagination/) for details. |

此外还有 [Site Variables](https://jekyllrb.com/docs/variables/#site-variables) 和 [Page Variables](https://jekyllrb.com/docs/variables/#page-variables)，以及 [Paginator](https://jekyllrb.com/docs/variables/#paginator) 的变量。太多了，不复制了。

---

###### References

[1](https://jekyllrb.com/docs/) JEKYLL 文档

[2](http://jekyllcn.com/docs/home/) JEKYLL 中文文档