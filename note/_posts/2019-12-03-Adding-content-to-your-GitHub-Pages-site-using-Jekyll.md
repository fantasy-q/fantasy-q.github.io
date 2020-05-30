---
layout: post
title:  给网站添加内容
date:   2019-12-03 20:00:07 +0800
summary: 用 Jekyll 添加 Content 到 GitHub Pages
categories: note
published: true
---

本文内容来源于[这里](https://help.github.com/en/github/working-with-github-pages/adding-content-to-your-github-pages-site-using-jekyll)。

## 关于 Jekyll 的 Content 
- Jekyll 的 Content 分为 2 种：[Page](https://jekyllrb.com/docs/pages/) 和 [Post](https://jekyllrb.com/docs/posts/)。
	- Page 是一种不与特定数据关联（就是一般不会变动）的独立内容，比如 `about.md`，可以把这个当作模板添加新的 Page。
	- Post 就是博客的一篇文章，在 `_posts` 中能找到创建新网站默认的生成的 post，当然也可以把这个当作模板添加新的 Post。
- 设置 variable 和 matedata 时，可以在 `.md` 或 `.html`  中添加 [YAML Front Matter]( https://jekyllrb.com/docs/front-matter/)。
- 完成后，可以先[在本地测试一下](https://help.github.com/en/github/working-with-github-pages/testing-your-github-pages-site-locally-with-jekyll)：`$ bundle exec jekyll serve`

## 添加新的 Post
1. 在 GitHub 中找到你网站的 [repository](https://github.com/fantasy-q/fantasy-q.github.io)。
2. 然后找到 publishing source。（还不是很懂这是啥）
3. 找到 `_post` 目录。
4. 创建一个新文件 `YYYY-MM-DD-NAME-OF-POST.md`。（就是日期和文章标题中间用 `-` 隔开）
5. 在文件开头写上:
```
---
layout: post
title: "POST TITLE"
date: YYYY-MM-DD hh:mm:ss -0000
categories: CATEGORY-1 CATEGORY-2
---
```
6. 然后就是文章内容了。
7. 就决定是你了，我的第一篇 Post！

## 添加新的 Page
1. 前面都一样，找对目录。
2. 创建文件 `PAGE-NAME.md`
```
---
layout: page
title: "PAGE TITLE"
permalink: /URL-PATH/
---
```
3. 然后在下面添加页面的内容
4. 暂时还不知道用来干嘛。