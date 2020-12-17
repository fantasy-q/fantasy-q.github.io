---
layout: note
title:  JEKYLL DOCUMENTS
date:   2019-12-04 00:43:00 +0800
summary: 摘抄 Jekyll 官方文档，帮助自己理解
categories: note
published: true
---

- [GETTING STARTED](#getting-started)
- [QuickStart](#quickstart)
	- [Installation](#installation)
- [Ruby 101](#ruby-101)
	- [Gems](#gems)
	- [Gemfile](#gemfile)
	- [Bundler](#bundler)
- [CONTENT](#content)
- [Front Matter](#front-matter)
	- [Predefined Global Variables](#predefined-global-variables)
	- [Custom Variables](#custom-variables)
	- [Predefined Variables for Posts](#predefined-variables-for-posts)
- [Collections](#collections)
	- [Setup](#setup)
	- [Add content](#add-content)
- [SITE STRUCTURE](#site-structure)
- [Directory Structure](#directory-structure)
- [Liquid](#liquid)
	- [Filters](#filters)
	- [Tags](#tags)
		- [Includes](#includes)
		- [Code snippet highlighting](#code-snippet-highlighting)
			- [Line numbers](#line-numbers)
			- [Stylesheets for syntax highlighting](#stylesheets-for-syntax-highlighting)
	- [Links](#links)
		- [Linking to pages](#linking-to-pages)
- [Variables](#variables)
	- [Global Variables](#global-variables)
				- [References](#references)

## GETTING STARTED
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
5. 搭建网站并让它运行在本地服务器。
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

## CONTENT
## Front Matter

*Any file that contains a [YAML](https://yaml.org/) front matter block will be processed by Jekyll as a special file.*
简单说下 [Front Matter](https://jekyllrb.com/docs/front-matter/)。

```yaml
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

```html
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

## Collections
*Collections are a great way to group related content like members of a team or talks at a conference.*

### Setup
先在 `_config.yml` 定义集合，如：
```yaml
collections:
  - staff_members
```

在这个例子 `collections` 被定义为一个没有额外元数据的序列 (i.e array)，并定义给每一个集合。可以将 `collections` 定义为映射 (i.e hashmap) 而非序列，来给集合指定元数据，然后反映出额外的字段 (filed)：
```yaml
collections:
  staff_members:
    people: true
```

### Add content
创建对应文件夹 (e.g.`<source>/_staff_members`) ,添加文档。如果头部信息存在则处理，所有后面的内容都属于文档的 `content` 属性。如果没有头部信息，Jekyll 会认为这是一个 [static file](https://jekyllrb.com/docs/static-files/) 并且内容不会经过进一步的处理。如果有头部信息，Jekyll 则将文件内容处理成期望的输出。

不管有没有头部信息，Jekyll 都会写进宿 (destination directory) 目录 (e.g. `_site`) 仅当 `output: true` 被设置进集合的元数据。

举个例子，这是如何添加一份 Staff 名单到上面设置的集合，文件名为 `./_staff_members/jane.md` 有如下内容:
```yaml
---
name: Jane Doe
position: Developer
---
Jane has worked on Jekyll for the past *five years*.
```

注意不管被当作
合法文件名格式的 Posts 会被标记处理，即使它们不包括头部信息

## SITE STRUCTURE
## Directory Structure

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

## Liquid

*Jekyll uses the [Liquid](https://shopify.github.io/liquid/) templating language to process templates.*

简而言之，输出内容： {% raw %}`{{ variable }}`{% endraw %}；执行逻辑：{% raw %}`{% if statement %}`{% endraw %}。（[注](https://segmentfault.com/q/1010000004530151/a-1020000004530401)）

想了解更多关于 Liquid 的信息，请查看 [Liquid 官方文档](https://shopify.github.io/liquid/)。

除了 Liquid 官方文档中的，Jekyll 还额外添加了一些 [Filters](https://jekyllrb.com/docs/liquid/filters/) 和 [Tags](https://jekyllrb.com/docs/liquid/tags/) 帮助你搭建网站。

### Filters

所有滤器（Filter）都能[在这](https://jekyllrb.com/docs/liquid/filters/#standard-liquid-filters)查看。[标准 Liquid 滤器](https://shopify.github.io/liquid/filters/)。

为了让一些常见的需求更简单，Jekyll 本身也添加了一些方便的滤器，你也可以通过[插件](https://jekyllrb.com/docs/plugins/)来创建自己的滤器。

| FILTERS AND USAGE | DESCRIPTION |
| ---- | ---- |
| **Relative URL**<br>relative_url | 预置 baseurl 到输入。如果网站域名装载以 subpath 而非 root 形式时很有用。 |
| **Absolute URL**<br>absolute_url | 预置 url 和 baseurl 到输入。 |
| **Date to FORMAT**<br>date_to_FORMAT |  FORMAT: <br>・XML Schema<br>・RFC-822 Format<br>・Date to String<br>・Date to Long String<br>STYLE: <br>・ordinal, US, UK |
| **Where**<br>where:"key1", "key2" | 选择一个数组中所有键与给定值相符的对象 |
| **Where Expression**<br>where_exp: "exp" | 选择一个数组中所有使表达式为真的对象|
| **Find**<br>find:"key1", "key2" | 返回数组中所查询的属性与给定值相符的**第一个对象**，不存在则返回 `nil` |
| **Find Expression**<br>find_exp | 返回数组中使表达式为真的**第一个对象**，不存在则返回 `nil` |
| **Group By**<br>group_by:"" | 给定属性将数组各项分组 |
| **XML Escape**<br>xml_escape | Escape some text for use in XML<br>`{% raw %}{{ page.content \| xml_escape }}{% endraw %}` |
| **CGI Escape**<br>相对 URL | CGI escape 一个字符串用在 URL<br>用适当的 `%XX` 替换任意特殊字符，CGI escape 通常用加号 `+` 来替换空格<br>`{% raw %}{{ "foo, bar; baz?" \| cgi_escape }}{% endraw %}`<br>`foo%2C+bar%3B+baz%3F` |
| **URI Escape**<br>相对 URL | URI 用百分符编码任意特殊字符<br>URI escape 通常用加号 `%20` 来替换空格，保留字符不会逃逸(escaped)<br>`{% raw %}{{ "http://foo.com/?q=foo, \bar?" \| uri_escape }}{% endraw %}`<br>`http://foo.com/?q=foo,%20%5Cbar?` |

### Tags

所有标签 (Tags) 都能[在这](https://shopify.github.io/liquid/tags/control-flow/)查看。Jekyll 内置了一些标签帮助你搭建网站，你也可以通过[插件](https://jekyllrb.com/docs/plugins/)来创建自己的滤器。

#### Includes

如果你有会重复利用的页面代码片段，[include](https://jekyllrb.com/docs/includes/) 可以完美地提高站点地可维护性.

#### Code snippet highlighting
感谢 [Rouge](http://rouge.jneen.net/)提供给 Jekyll 超过 100 种语言的语句高亮，Rouge 是 Jekyll 3 和以上版本默认使用的语句高亮。

用语句高亮渲染代码块，如下所示：
```
{% raw %}{% highlight ruby %}
def foo
  puts 'foo'
end
{% endhighlight %}{% endraw %}
```
{% highlight ruby %}
def foo
  puts 'foo'
end
{% endhighlight %}

`highlight` 的参数 (在上例中为 `ruby`) 是语言标识符，查看 [Rouge wiki](https://github.com/jayferd/rouge/wiki/List-of-supported-languages-and-lexers) 的"short name"，寻找合适的标识符。

##### Line numbers

`highlight` 的第二个参数是可选的，叫作 `linenos`，作用是强制高亮代码并包含行号，如下所示：
```
{% raw %}{% highlight ruby linenos %}
def foo
  puts 'foo'
end
{% endhighlight %}{% endraw %}
```
{% highlight ruby linenos %}
def foo
  puts 'foo'
end
{% endhighlight %}

##### Stylesheets for syntax highlighting
为了让高亮能显示，你还要包含一个高亮样式表，对于 Pygments 或 Rouge 你可以使用 Pygments 的样式表，you can find an example gallery [here](https://jwarby.github.io/jekyll-pygments-themes/languages/ruby.html) or from [its repository](https://github.com/jwarby/jekyll-pygments-themes).

复制 CSS 文件 (如 native.css) 到你的 CSS 目录并导入这些语句样式到你的 `main.css` 中：
```css
@import "native.css";
```

### Links

Since Jekyll `4.0` , you don’t need to prepend `link` and `post_url` tags with `site.baseurl`.

#### Linking to pages

链接到文章


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