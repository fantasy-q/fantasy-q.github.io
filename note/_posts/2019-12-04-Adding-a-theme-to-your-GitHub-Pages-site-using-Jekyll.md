---
layout: post
title: "用 Jekyll 给网站添加主题"
date: 2019-12-04 20:24:00 +0800
categories: note
published: true
---

\[1] [Adding a theme to your GitHub Pages site using Jekyll - GitHub](https://help.github.com/en/github/working-with-github-pages/adding-a-theme-to-your-github-pages-site-using-jekyll)

\[2] [Themes - Jekyllrb](https://jekyllrb.com/docs/themes/)

## 主题 Themes

Jekyll 有海量的主题，能让你借助由社区维护 templates 和 style 来定制网站的表现方式。

Jekyll 主题指定的 plugins 以及打包好的 assets，layouts，includes 和 stylesheets 都能被你网站的 contents 重写。

## Understanding gem-based themes

创建新的 Jekyll site 时 (by running the `jekyll new ` command)，Jekyll 会使用一个叫作 [Minima](https://github.com/jekyll/minima) 的 gem-based theme。

若使用 gem-based themes，某些目录 (such as the `assets`, `_layouts`, `_includes`, and `_sass` directories) 会储存在  gem 中，不会被你直接看到。

In the case of Minima, you see only the following files in your Jekyll site directory:

```
├── Gemfile
├── Gemfile.lock
├── _config.yml
├── _posts
│   └── 2016-12-04-welcome-to-jekyll.markdown
├── about.markdown
└── index.markdown
```

The `Gemfile` and `Gemfile.lock` files are used by Bundler to keep track of the required gems and gem versions you need to build your Jekyll site.

这种 gem-based themes 由什么优点？

- 对主题开发者来说，只要推送更新到 RubyGems 就好了。

- 那么对使用者来说，就可以简单地通过 `bundle update <THEME>` 来更新，专注于内容创作。

## Overriding theme defaults

**Jekyll themes set default layouts, includes, and stylesheets.** 

你可以重写主题的缺省值。举个例子，如果所选主题有个 `page` layout，那么可以通过创建一个自己的 `page` 放到 `_layouts` 中来重写主题原来的 layout。(that is, `_layouts/page.html`)

如何在自己的计算机中找到主题的文件：运行 `bundle show` 并带上主题的名字。如 `bundle show minima`，Minima theme gem 包含这些文件：

```
 ├── LICENSE.txt
 ├── README.md
 ├── _includes
 │   ├── disqus_comments.html
 │   ├── footer.html
 │   ├── google-analytics.html
 │   ├── head.html
 │   ├── header.html
 │   ├── icon-github.html
 │   ├── icon-github.svg
 │   ├── icon-twitter.html
 │   └── icon-twitter.svg
 ├── _layouts
 │   ├── default.html
 │   ├── home.html
 │   ├── page.html
 │   └── post.html
 ├── _sass
 │   ├── minima
 │   │   ├── _base.scss
 │   │   ├── _layout.scss
 │   │   └── _syntax-highlighting.scss
 │   └── minima.scss
 └── assets
     └── main.scss
```

知道了主题的文件结构，就能通过创建同名文件，并放到网站目录中来重写主题。

修改 stylesheet 时必须先复制 main sass file (`_sass/minima.scss` in the Minima theme) 到 `_sass` 目录。

Note that making copies of theme files will prevent you from receiving any theme updates on those files. An alternative, to continue getting theme updates on all stylesheets, is to use higher specificity CSS selectors in your own additional, originally named CSS files.

参考你选择的主题文档和源码仓库，来具体了解你能重写哪些文件。

Refer to your selected theme’s documentation and source repository for more information on what files you can override.

## Converting gem-based themes to regular themes

如题，可以复制 theme gem 的目录到网站目录里，但要注意主题所需的插件。

If you were converting the Minima theme, for example, you might see:

```
spec.add_runtime_dependency "jekyll-feed", "~> 0.12"
spec.add_runtime_dependency "jekyll-seo-tag", "~> 2.6"
```

You should include these references in the `Gemfile` in one of two ways.

You can find these plugins in the theme’s gemspec file as runtime dependencies. You could list them individually in both `Gemfile` and `_config.yml`.

```
# ./Gemfile

gem "jekyll-feed", "~> 0.12"
gem "jekyll-seo-tag", "~> 2.6"
```

```
# ./_config.yml

plugins:
  - jekyll-feed
  - jekyll-seo-tag
```

Or you could list them explicitly as Jekyll plugins in your Gemfile, and not update `_config.yml`, like this:

```
# ./Gemfile

group :jekyll_plugins do
  gem "jekyll-feed", "~> 0.12"
  gem "jekyll-seo-tag", "~> 2.6"
end
```

Either way, don’t forget to `bundle update`.

**If you’re publishing on GitHub Pages you should update only your `_config.yml` as GitHub Pages doesn’t load plugins via Bundler.**

Finally, remove references to the theme gem in `Gemfile` and configuration. For example, to remove `minima`:

- Open `Gemfile` and remove `gem "minima", "~> 2.5"`.
- Open `_config.yml` and remove `theme: minima`.

Now `bundle update` will no longer get updates for the theme gem.