---
layout: post
title:  "CSS 笔记（字体篇）"
date:   2020-03-10 18:00:00 +0800
categories: note
published: true
---
- [设置字体](#font-family-定制页面中的字体)
	- [常用字体格式](#常用字体格式)
- [字体大小](#font-size-控制字体大小)
- [字体颜色](#color-为文本添加颜色)
- [字体粗细](font-weight 影响字体粗细)
- [字体样式](font-decoration 为文本增加样式)

## font-family 定制页面中的字体
**Customize the fonts in your pages with the font-family property.**

```css
body {
    font-family: Verdana, Geneva, Arial, sans-serif
}
```
每个`font-family`包含一组相同特征的字体，共 5 类，每类都包含大量字体：

| FontFamily | Meaning | Font | Description |
| ---- | ----  | ---- | ---- |
| sans-serif | 无衬线 | Verdana, Arial Black, Trebuchet MS, Arial, Geneva | 常用于计算机显示 |
| serif | 有衬线 | Times, Times New Roman, Georgia | 常用于印刷 |
| monospace | 等宽度 | Courier, Courier New, Andale Mono | 适合用于写代码 |
| cursive | 手写体 | Comic Sans, Apple Chancery | 适用用于标题 |
| fantasy | ？？？ | LAST NINJA, IMPACT | 艺术设计？ |

- 字体名包含多个单词，使用时在两边加上引号
- font-family 实际上是一个字体优先级列表

### 常用字体格式

| Extension | Full Name | Description  |
| ---- | ---- | ---- |
| .ttf | True Type Font | ttf 与 otf 两者紧密相关 |
| .otf | Open Type Font | 建立在 ttf 的基础上，比 ttf 新 |
| .eot | Embedded Open Type | otf 的压缩格式，微软专用，仅 IE 提供支持 |
| .svg | Scalable Vector Graphics | 这种字体使用一种通用图像格式 svg 来表示字符 |
| .woff | Web Open Font Format | 基于 ttf 并发展成为 Web 字体的一个标准，大多数浏览器都提供支持 |

不能保证所有人都安装了指定的字体，为了避免显示出问题可使用 `@font-face`：
```css
@font-face {
    font-family: "Emblema One";
    src: url("http://wickedlysmart.com/hfhtmlcss/chapter8/journal/EmblemaOne-Regular.woff"),
         url("http://wickedlysmart.com/hfhtmlcss/chapter8/journal/EmblemaOne-Regular.ttf");
}
```
- `@font-face` 是一个内置的 CSS 规则，非选择器规则
- 使用 Web 字体时，第一次加载可能比较费时间
- Web 字体托管服务：[FontSquirrel](http:/www.fontsquirrel.com/)、[Google Fonts](https://fonts.google.com/)

## font-size 控制字体大小
**Control the size of your fonts with the font-size property.**
```css
body {
    font-size: 14px;
}
```

| CSS | Meaning | How to use | Description |
| ---- | ---- | ---- | ---- |
| px | pixel | font-size: 14px | 字母高度，单位像素 |
| % | percentage | font-size: 150% | 相对于父元素的百分数 |
| em | scaling factor | font-size: 1.2em | 相对于父元素的倍数 |
| keyword | keyword | font-size: medium | xx-large, smaller 等多个关键字 |

- 建议使用关键字在`body`中定义页面的默认大小 
- 在其他元素中使用相对方式定义字体大小
- 关键字与相对大小都是为了避免用户缩放页面时出现问题
- 默认字体大小取决于浏览器，一般情况下：
	- `<body>` 为 16px
	- `<h>`依次为 200%, 150%, 120%, 100%, 90%, 60%
	- 在`<body>`中使用`em`、`%`，即相对于默认`16px`的大小

## color 为文本添加颜色
**Add color to your text with the color property.**
```css
body {
    color: silver;
}
```

## font-weight 影响字体粗细
**Affect the weight of your fonts with the font-weight property.**
```css
body {
    font-weight: bold;
}
```
- 可选属性：`bold`, `normal`, `lighter`, `bolder`

## font-decoration 为文本增加样式
**Add even more style to your text with the text-decoration property.**
```css
body {
    text-decoration: underline;
}
```

| ---- | ---- | ---- |
| italic | 斜体 | 斜体是人为设计的一种风格，并非所有字体都支持 |
| oblique | 倾斜 | 倾斜只是浏览器将正常文字倾斜了，不支持斜体则为倾斜 |
| overline | 上划线 |  |
| underline | 下划线 |  |
| line=through | 删除线 |  |

- `<em>`与斜体
	- `<em>`用来指定结构，表示需要强调的文字， 默认表现为斜体
	- 正因如此，`<em>`的重点在于强调，而非斜体
	- 所以避免使用`<em>`来将文字变成斜体
	- 通过 CSS 指定`<em>`的样式，可使其表现为其他形式

###### Reference
[1] **Head First HTML and CSS, 2nd Edition**
