---
layout: note
title:  记录
date:   2020-07-18 02:51:07 +0800
categories: note
summary: 遇到的问题，自定义功能等。
published: true
---

- **2020-07-18** Markdown 不常用语法

  - blockquote **>**

    > Blockquote

  - Autolinks **< >**

    <https://fantasy-q.github.io/{{ page.url }}>

  - Strikethrough **\~\~ \~\~**

    ~~Strikethrough~~
    
    

- **2020-07-11** post 文件名不想使用日期 \|  [StackOverflow](https://stackoverflow.com/questions/27099427/jekyll-filename-without-date)
	
	- 顺便了解下集合
	
-  **2020-07-03** 在 markdown 中给 table 标签添加 class \| [GitHub](https://gist.github.com/tamouse/4204dddabb6b072b0242)

```markdown
# Let's try out a table with kramdown class tag

| A simple | table |
| with multiple | lines|
{: .my-class }
```

- **2020-04-17** 才知道 MarkDown 自带表格居中，但这样好像整体都会居中，不能单独让表头居中：

```markdown
|      |      |
| :--: | :--: |  <--- 像这样，两个冒号
```

- **2020-03-10** 用 MarkDown 添加目录，之前试了几次都没搞懂，原来不能有大写字母，空格要用`-`代替。
- 更换主题后的一些配置问题
###### 永久链接 **permalink**

| 永久链接类型 | URL 模板 |
| ---- | ---- |
| `date`       | `/:categories/:year/:month/:day/:title.html` |
| `pretty`     | `/:categories/:year/:month/:day/:title/`     |
| `ordinal`    | `/:categories/:year/:y_day/:title.html`      |
| `none`       | `/:categories/:title.html`                   |

- **2020-01-08** 表格头部文本居中
  得知 HTML5 废除了 `<center>` 标签，可用 CSS 代替，如下：、

  ```css
  th {
      text-align:center;
  }
  ```

- **2019-12-05** [网页底部添加了个人B站主页链接](/note/2019/12/05/Adding-social-media-account.html)