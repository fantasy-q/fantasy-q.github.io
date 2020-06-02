---
layout: post
title:  Jekyll 手把手教学 - 部署网站 
summary:  Step by Step Tutorial - Ⅹ. Deployment （部分翻译，自用帮助了解。）
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
- [十、部署网站 ](../jekyll/10th-Deployment.html)
	- [GEMFILE](#gemlfile)
	- [插件](#plugins)
	- [环境](#environments)
	- [部署](#deployment)
	- [圆满结束](#warp-up)

最后一节，我们要为网站的生产环境做准备。

## Gemlfile
网站里有 [Gemfile](https://jekyllrb.com/docs/ruby-101/#gemfile) 是比较好的习惯，这样能保证在不同的环境种 Jekyll 的版本的和其他 Gem 也能保持稳定不变。

在根目录下创建 `Gemfile` 带上如下内容：
```ruby
source 'https://rubygems.org'

gem 'jekyll'
```

然后在终端运行 `bundle install`，这会安装 Gem 并创建一个 `Gemfile.lock`，将 Gem 的版本锁定到下一次的 `bundle install`。也可以随时运行 `bundle update` 来更新版本。

使用 `Gemfile` 时，你要运行带有前缀 `bundle exec` 的 `jekyll serve` 命令，如下：
```
bundle exec jekyll serve
```

这能将你的 Ruby 环境限制在仅使用在 `Gemfile` 设置的 Gem。

## Plugins
Jekyll 插件可以让你创建特定的自定义生成内容，有许多现成的[插件](https://jekyllrb.com/docs/plugins/)，你也能自己编写。

有三个几乎对所有 Jekyll 网站都有用的官方插件：
- jekyll-sitemap -创建站点地图帮助搜索引擎索引内容
jekyll-feed - 给你的文章创建 RSS feed
jekyll-seo-tag - 添加元标签帮助搜索引擎优化（SEO）

为了使用这些，首先到 `Gemfile` 里添加，放在 `jekyll_plugins` 组下他们会自动被 Jekyll 需要：
```ruby
source 'https://rubygems.org'

gem 'jekyll'

group :jekyll_plugins do
  gem 'jekyll-sitemap'
  gem 'jekyll-feed'
  gem 'jekyll-seo-tag'
end
```

然后到 `_config.yml` 添加这几行：
```yaml
plugins:
  - jekyll-feed
  - jekyll-sitemap
  - jekyll-seo-tag
```

现在运行 `bundle update` 安装他们。

`jekyll-sitemap` 不需要任何设置，它会在构建的时候创建。

对于 `jekyll-feed` 和 `jekyll-seo-tag` 你要添加标签到 `_layouts/default.html`：
```html
<!doctype html>
{% raw %}<html>
  <head>
    <meta charset="utf-8">
    <title>{{ page.title }}</title>
    <link rel="stylesheet" href="/assets/css/styles.css">
    {% feed_meta %}
    {% seo %}
  </head>
  <body>
    {% include navigation.html %}
    {{ content }}
  </body>
</html>{% endraw %}
```

重启 Jekyll 服务器检查这些标签是否被添加到了 `<head>`。

## Environments
有时你可能想输出某些东西到生产环境（Production）但不在开发环境（Development）中，分析脚本就是一个常见的例子。

通过 [environments](https://jekyllrb.com/docs/configuration/environments/) ，在命令行下你能用 `JEKYLL_ENV` 环境变量设置，比如：
```
JEKYLL_ENV=production bundle exec jekyll build
```

缺省状态下 `JEKYLL_ENV` 是开发环境，Liquid 用 `jekyll.environment` 来提供 `JEKYLL_ENV`，所以为了仅在生产环境中输出分析脚本，要做下述动作：
```html
{% raw %}{% if jekyll.environment == "production" %}
  <script src="my-analytics-script.js"></script>
{% endif %}{% endraw %}
```

## Deployment
最后一步是把网站放到生产服务器上，最基本的方式是运行一次生产环境构建：
```
JEKYLL_ENV=production bundle exec jekyll build
```

并复制 `_site ` 的内容到服务器。

更好的方式是使用 [CI](https://jekyllrb.com/docs/deployment/automated/) 或 [3rd party](https://jekyllrb.com/docs/deployment/third-party/) 让这些过程自动化。

## Warp up
至此为止就是手把手教学的尾声了，同时也拉开你 Jekyll 旅程的序幕！

- Come say hi to the [community forums](https://talk.jekyllrb.com/)
- Help us make Jekyll better by [contributing](https://jekyllrb.com/docs/contributing/)
- Keep building Jekyll sites!

---
###### Links
[[Ⅹ]](https://jekyllrb.com/docs/step-by-step/10-deployment/)Deployment - Jekyll Docs Step by Step Tutorial
