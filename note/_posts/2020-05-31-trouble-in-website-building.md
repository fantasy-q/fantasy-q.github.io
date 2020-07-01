---
layout: note
title:  Jekyll 学习总结
date:   2020-05-31 11:52:32 +0800
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