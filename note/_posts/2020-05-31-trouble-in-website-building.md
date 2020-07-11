---
layout: note
title:  Jekyll 学习总结
categories: note
published: false
---

更换主题后的一些配置问题

### 永久链接
**permalink**

| 永久链接类型 | URL 模板 |
| ---- | ---- |
| `date`       | `/:categories/:year/:month/:day/:title.html` |
| `pretty`     | `/:categories/:year/:month/:day/:title/`     |
| `ordinal`    | `/:categories/:year/:y_day/:title.html`      |
| `none`       | `/:categories/:title.html`                   |

### 2020-07-03 在 markdown 中给 table 标签添加 class
```markdown
# Let's try out a table with kramdown class tag

| A simple | table |
| with multiple | lines|
{: .my-class }
```
[GitHub](https://gist.github.com/tamouse/4204dddabb6b072b0242)

### 2020-07-11 post 文件名不用日期
[StackOverflow](https://stackoverflow.com/questions/27099427/jekyll-filename-without-date)

了解下集合
