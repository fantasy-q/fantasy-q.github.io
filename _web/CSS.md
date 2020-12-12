---
layout: post
title:  CSS
summary: 关于 CSS 中字体的一些相关内容
categories: note
published: false
---

### 优先级

1. 选择器 Selector	
2. 继承 Inheritance
3. 默认值 Default

### 选择器

- [优先级](#优先级)
- [选择器](#选择器)
  - [标签选择器](#标签选择器)
  - [类选择器](#类选择器)
- [继承](#继承)


#### 标签选择器
```css
h1, h2 {
  font-family: sans-serif;
  color: gray;
}
h1 {
  border-bottom: 1px solid black;
}
p {
  color: maroon;
}
```
#### 类选择器
```css
p.greentea {
  color: green;
}
blockquote.greentea, p.greentea {
  color: green;
}
.greentea {
  color: green;
}

```

### 继承

- 覆盖继承(Overriding)