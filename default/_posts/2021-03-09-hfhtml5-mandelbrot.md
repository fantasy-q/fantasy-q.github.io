---
layout: post
title: Web 工作线程 — Mandelbrot
date: 2021-03-09 18:00:00 +0800
categories: note
summary: 以计算 Mandelbrot 集为例，了解 Web 工作线程。
published: false
---

《Head First HTML5 Programming》第 10 章讲工作线程，使用 **Mandelbrot 集** 作为例子。

按书上的话来说，**Mandelbrot** 的公式非常简单，但需要大量计算，非常适合作为 Web 工作线程的例子。

感觉有点复杂又有点意思，单独记录一下。

## 目录
- [目录](#目录)
- [计算 Mandelbrot 集](#计算-mandelbrot-集)
- [使用多个工作线程](#使用多个工作线程)
- [变量](#变量)
  - [全局变量](#全局变量)
- [mandel.js](#mandeljs)
  - [startWorkers()](#startworkers)
- [mandellib.js](#mandellibjs)
  - [setupGraphics()](#setupgraphics)
  - [makePalette()](#makepalette)
  - [createTask()](#createtask)
- [worker.js](#workerjs)
- [workerlib.js](#workerlibjs)

## 计算 Mandelbrot 集

先看看简单的伪代码：

```js
// 循环处理图像的每一行
for (i = 0; i < numberOfRows; i++) {
/* 计算像素 */ const row = computeRow(i);
/* 逐行绘制 */ drawRow(row);
}

for (i = 0; i < numberOfRows; i++) {
/* 所需行数据 */ const taskForRow = createTaskForRow(i);
/* 计算行像素 */ const row = computeRow(taskForRow);
/* 逐行绘制 */  drawRow(row);
}
```

接下来需要修改，将计算分解到多个工作线程。

## 使用多个工作线程

将图像按**行**分解为多个小区域，由多个工作线程负责计算。

每个线程独立处理，完成后将结果打包发回。

直到计算完成，工作线程空闲，等待下一次点击放大。

但工作线程不希望被大量使用，因为需要额外的内存和操作系统线程。

## 变量

### 全局变量

| Variable        | Initialization | setupGraphics()                    |
| --------------- | -------------- | ---------------------------------- |
| numberOfWorkers | 8              |                                    |
| workers         | [ ]            |                                    |
| canvas          |                | getElementById("fractal")          |
| ctx             |                | getContext("2d")                   |
| canvas.width    |                | window.innerWidth                  |
| canvas.height   |                | window.innerHeight                 |
| rowData         |                | Uint8ClampedArray(canvas.width*4)  |
|                 |                |                                    |
| i_max           | 1.5            |                                    |
| i_min           | -1.5           |                                    |
| r_max           | 1.5            | [r_mid](#setupgraphics) - width/2; |
| r_min           | -2.5           | r_mid + width/2;                   |
| max_iter        | 1024           |                                    |
| escape          | 100            |                                    |
| palette         | [ ]            |                                    |

## mandel.js

跳转 [worker.js](#workerjs)

```js
let numberOfWorkers = 8;
let workers = [];

window.onload = init;
function init() {
  /* mandellib.js */ setupGraphics();
  for (var i = 0; i < numberOfWorkers; i++) {
    /* 创建线程 */ var worker = new Worker("worker.js");
    /* 设置事件 */ worker.onmessage = function(event) {
      processWork(event.target, event.data);
    }
    worker.idle = true;
    workers.push(worker);
  }
  startWorkers();
}
```

代码顺序 init():
- setupGraphics()
  - makePalette()
- worker.onmessage = processWork(event.target, event.data);
- startWorkers() 
  - createTask()
  - worker.postMessage(task)
    - workerResult = computeRow(task.data)
    - postMessage(workerResult)
      - processWork(workerResult.target, workerResult.data)
        - drawRow(workerResults)
        - 
        - reassignWorker(worker)

### startWorkers()

```js
function startWorkers() {
  generation++;
  nextRow = 0;
  for (let i = 0; i < workers.length; i++) {
    let worker = workers[i];
    if (worker.idle) {
      let task = createTask(nextRow);
      worker.idle = false;
      worker.postMessage(task);
      nextRow++;
    }
  }
}
```

## mandellib.js

第 10 章源码，包含所有数值计算和一些图形处理

### setupGraphics()

`setupGraphics` 设置用于计算 Mandelbrot 的变量的初始值

以及将 `canvas` 的尺寸置为 window 的尺寸

| Variable | Initialization                   |     |
| -------- | -------------------------------- | --- |
| width    | 3 * canvas.width / canvas.height |     |
| r_mid    | -0.5                             |     |

### makePalette()

```js
function makePalette() {
	function wrap(x) {
		x = ((x + 256) & 0x1ff) - 256;
		if (x < 0) x = -x;
		return x;
	}
	for (i = 0; i <= this.max_iter; i++) {
		palette.push([wrap(7 * i), wrap(5 * i), wrap(11 * i)]);
	}
}
```

做了一个 `palette` 数组的[图表](https://fantasy-q.github.io/web-demo/chartjs/palette/index.html)。

### createTask()

| task       |                     | Value                              |
| ---------- | ------------------- | ---------------------------------- |
| row        | createTask(nextRow) | startWorkers(){ nextRow++ }        |
| width      | rowData.width       | canvas.width === window.innerWidth |
| generation | global              | startWorkers(){ generation++ }     |
| r_min      | global              | setupGraphics()                    |
| r_max      | global              | setupGraphics()                    |
| max_iter   | global              | 1024                               |
| escape     | global              | 100                                |
| **i**      | **Native**          | 3 * row / canvas.height            |

## worker.js

```js
importScripts("workerlib.js");

onmessage = function (task) {
	var workerResult = computeRow(task.data);
	postMessage(workerResult);
}
```

## workerlib.js

计算**分形**的一行，返回到 `manager` 代码的 `values` **数组**对于一行中每个像素都包含一个**数**

```js
function computeRow(task) {
  let iter = 0;
  let c_i = task.i;
  let max_iter = task.max_iter;
  let escape = task.escape * task.escape;
  task.values = [];
  // Loop 1: 对应行中每个像素
  for (let i = 0; i < task.width; i++) {
    let c_r = task.r_min + (task.r_max - task.r_min) * i / task.width;
    let z_r = 0;
    let z_i = 0;
    // Loop2: 查找该像素适当的值
    for (iter = 0; z_r*z_r + z_i*z_i < escape && iter < max_iter; iter++) {
      // z -> z^2 + c
      let tmp = z_r*z_r - z_i*z_i + c_r;
      z_i = 2 * z_r * z_i + c_i;
      z_r = tmp;
    }
    if (iter == max_iter) {
      iter = -1;
    }
    // 最终计算结果
    task.values.push(iter);
  }
  return task;
}
```

