---
layout: post
title: Flexbox Froggy
date: 2021-02-13 02:30:00 +0800
categories: note
summary: a game where you help Froggy and friends by writing CSS code!
published: true
---

## [Flexbox Froggy](http://flexboxfroggy.com/)

|      |      |      |      |
| ---- | ---- | ---- | ---- |
| [Level 1](#level-1) | [Level 2](#level-2) | [Level 3](#level-3) | [Level 4](#level-4) |
| [Level 5](#level-5) | [Level 6](#level-6) | [Level 7](#level-7) | [Level 8](#level-8) |
| [Level 9](#level-9) | [Level 10](#level-10) | [Level 11](#level-11) | [Level 12](#level-12) |
| [Level 13](#level-13) | [Level 14](#level-14) | [Level 15](#level-15) | [Level 16](#level-16) |
| [Level 17](#level-17) | [Level 18](#level-18) | [Level 19](#level-19) | [Level 20](#level-20) |
| [Level 21](#level-21) | [Level 22](#level-22) | [Level 23](#level-23) | [Level 24](#level-24) |

### Level 1

属性 `justify-content` 可以水平对齐元素：

- `flex-start`: Items align to the **left** side of the container.
- `flex-end`: Items align to the **right** side of the container.
- `center`: Items align at the **center** of the container.
- `space-between`: Items display with equal spacing between them.
- `space-around`: Items display with equal spacing around them.

```css
#pond {
  display: flex;
  justify-content: flex-end;
}
```

### Level 2

```css
#pond {
  display: flex;
  justify-content: center;
}
```

### Level 3

```css
#pond {
  display: flex;
  justify-content: space-around;
}
```

### Level 4

```css
#pond {
  display: flex;
  justify-content: space-between;
}
```

### Level 5

属性 `align-items` 可以纵向对齐元素：

- `flex-start`: Items align to the **top** of the container.
- `flex-end`: Items align to the **bottom** of the container.
- `center`: Items align at the vertical center of the container.
- `baseline`: Items display at the baseline of the container.
- `stretch`: Items are stretched to fit the container.

```css
#pond {
  display: flex;
  align-items: flex-end;
}
```

### Level 6

```css
#pond {
  display: flex;
  align-items: center;
  justify-content: center;
}
```

### Level 7

```css
#pond {
  display: flex;
  align-items: flex-end;
  justify-content: space-around;
}
```

### Level 8

属性 `flex-direction` 定义了元素在容器里摆放的方向：

- `row`: Items are placed the same as the text direction.
- `row-reverse`: Items are placed opposite to the text direction.
- `column`: Items are placed top to bottom.
- `column-reverse`: Items are placed bottom to top.

```css
#pond {
  display: flex;
  flex-direction: row-reverse;
}
```

### Level 9

```css
#pond {
  display: flex;
  flex-direction: column;
}
```

### Level 10

```css
#pond {
  display: flex;
  flex-direction: row-reverse;
  justify-content: flex-end;
}
```

### Level 11

```css
#pond {
  display: flex;
  flex-direction: column;
  justify-content: flex-end;
}
```

### Level 12

```css
#pond {
  display: flex;
  flex-direction: column-reverse;
  justify-content: space-between;
}
```

### Level 13

```css
#pond {
  flex-direction :row-reverse;
  align-items: flex-end;
  justify-content: center;
}
```

### Level 14

有时候仅仅调转行或列的方向是不够的。在这些情况，我们可以设置单个元素的`order`属性。元素的属性默认值为0，但是我们设置这个属性为正数或负数。

```css
#pond {
  display: flex;
}

.yellow {
  order: 2;  /* any number >= 1 */
}
```

### Level 15

```css
#pond {
  display: flex;
}

.red {
  order: -1;
}
```

### Level 16

另一个你可以使用的控制单个元素的属性是`align-self`。这个属性接受和`align-items`一样的那些值。

```css
#pond {
  display: flex;
  align-items: flex-start;
}

.yellow {
  align-self: flex-end;
}
```

### Level 17

```css
#pond {
  display: flex;
  align-items: flex-start;
}

.yellow {
  align-self: flex-end;
  order: 1;
}
```

### Level 18

用 `flex-wrap` 属性把它们分散看看：

- `nowrap`: Every item is fit to a single line.
- `wrap`: Items wrap around to additional lines.
- `wrap-reverse`: Items wrap around to additional lines in reverse.

```css
#pond {
  display: flex;
  flex-wrap: wrap;
}
```

### Level 19

```css
#pond {
  display: flex;
  flex-direction: column;
  flex-wrap: wrap;
}
```

### Level 20

`flex-direction` 和 `flex-wrap` 两个属性经常会一起使用，所以有缩写属性 `flex-flow`。这个缩写属性接受两个属性的值，两个值中间以空格隔开。

举个例子，你可以用 `flex-flow: row wrap` 去设置行并自动换行。

试着用 `flex-flow` 来重复上一关的任务。

```css
#pond {
  display: flex;
  flex-flow: column wrap;
}
```

### Level 21

你可以使用 `align-content` 来决定行与行之间隔多远：

- `flex-start`: Lines are packed at the top of the container.
- `flex-end`: Lines are packed at the bottom of the container.
- `center`: Lines are packed at the vertical center of the container.
- `space-between`: Lines display with equal spacing between them.
- `space-around`: Lines display with equal spacing around them.
- `stretch`: Lines are stretched to fit the container.

这可能有些容易混淆，但 `align-content` 决定行之间的间隔，而`align-items`决定元素整体在容器的什么位置。只有一行的时候 `align-content` 没有任何效果。

```css
#pond {
  display: flex;
  flex-wrap: wrap;
  align-content: flex-start;
}
```

### Level 22

```css
#pond {
  display: flex;
  flex-wrap: wrap;
  align-content: flex-end;
}
```

### Level 23

```css
#pond {
  display: flex;
  flex-wrap: wrap;
  flex-direction: column-reverse;
  align-content: center;
}
```

### Level 24

Bring the frogs home one last time by using the CSS properties you've learned:

- `justify-content`
- `align-items`
- `flex-direction`
- `order`
- `align-self`
- `flex-wrap`
- `flex-flow`
- `align-content`

```css
#pond {
  display: flex;
  flex-direction: column-reverse;
  flex-wrap: wrap-reverse;
  justify-content: center;
  align-content: space-between;
}
```
