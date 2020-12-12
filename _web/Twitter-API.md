---
layout: post
title: 关于 Twitter API
categories: miscs
summary: 
published: true
---

## 写在前面

看 Head First HTML5 Programming 2th ch.7 Twitter API：

```html
<scrit src="http://twitter.com/statuses/user_timeline/wickedsmartly.json?callback=updateTweets"></scrit>

```

但好像没有效果，稍微研究一下。Twitter [Developer](https://developer.twitter.com/en) 以及 [Document](https://developer.twitter.com/en/docs/twitter-api)。

## Getting started

### Using the Twitter API

*The **Twitter API** can be used to programmatically retrieve and analyze data, as well as engage with the conversation on Twitter.*

API 用于程序地获取和分析数据，或者与推特互动，并提供下述资源的访问：

- 推 Tweets
- 用户 Users
- 私信 Direct Messages
- 好友 Lists
- 热门 Trends
- 媒体 Media
- 地区 Places

目前 (2020/12/13) 提供两个版本，具体查看[这里](https://developer.twitter.com/en/docs/twitter-api/getting-started/guide)。

应该是要使用 **[Standard v1.1](https://developer.twitter.com/en/docs/twitter-api/v1)** 中的 Retrieve timelines。

### How to get access to the Twitter API

如何访问 Twitter API：
#### Step one: Apply and receive approval for a developer account

申请开发者账号并获得许可。其他看不懂，大概就是写份 200 字的英文申请，提交后给我邮箱发了封邮件让我确认。确认之后又一封邮件让我等审核，可能是我推调成日语了，邮件用的是日语。

```
I'm new to web development. Recently I'm reading Head First HTML5 Programming and learning web development. There is a project that used Twitter API to get user timeline then show on the page in this book. I want to try to implement this project as this book does. Please give me approval, thank you!
```

不知道能不能通过 (2020/12/13)。

#### Step two: Save your App's key and tokens and keep them secure

保存好你的 Key 和 token，并且要保密。 

#### Step three: Set up your access

#### Step five: Make your first request