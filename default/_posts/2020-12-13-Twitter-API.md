---
layout: post
title: 关于 Twitter API
date: 2020-12-13 02:30:00 +0800
categories: note
summary: 学习使用 Twitter API
published: true
---

## 写在前面

看 Head First HTML5 Programming 2th ch.7 里用到了 Twitter API：

```html
http://twitter.com/statuses/user_timeline/wickedsmartly.json?callback=updateTweets
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

目前提供两个版本，具体查看[这里](https://developer.twitter.com/en/docs/twitter-api/getting-started/guide)。

应该是要使用 **[Standard v1.1](https://developer.twitter.com/en/docs/twitter-api/v1)** 中的 Retrieve timelines。

### How to get access to the Twitter API

如何访问 Twitter API：
#### Step one: Apply and receive approval for a developer account

申请开发者账号并获得许可。其他看不懂，大概就是写份 200 字符长的英文申请，提交后给我邮箱发了封邮件让我确认。确认之后又一封邮件让我等审核，可能是我推调成日语了，邮件用的是日语，不知道能不能通过。

```
I'm new to web development. Recently I'm reading Head First HTML5 Programming 
and learning web development. There is a project that used Twitter API to get 
user timeline then show on the page in this book. I want to try to implement 
this project as this book does.
```
提交时间 (12:49AM) 回复时间 (4:51AM) 第一次审核没通过，而且不让我这个号继续申请了。我换了个号，居住国家选了个日本，用途选择学生，都没要审核，直接进去了……

不管那么多了，过了就行。进去给了我三个东西，API Key、API seret key、Bearer token。说是只能看一次，让我好好保存起来。

#### Step two: Save your App's key and tokens and keep them secure

保存好 Key 和 token，並且要保密。

###### API key

Your key is like your username. It is used to verify who you are to Twitter.

###### API secret key

Your secret key is used like a password. It identifies your account. Keep this safe!

###### Bearer token

An access token used in authentication that allows you to pull specific data.

然后给了我三个测试用例，纯文字，带图片，投票。列个最简单的在这里：

###### Request
Test this in your terminal by replacing <BEARER TOKEN> (including the < >) with your bearer token.

```
curl -X GET -H "Authorization: Bearer <BEARER TOKEN>" "https://api.twitter.com/2/tweets/20"
```

###### Response
```json
{
  "data": {
    "id": "20",
    "text": "just setting up my twttr"
  }
}
```
当然这里要挂代理：
```
set http_proxy=http://127.0.0.1:PORT
set https_proxy=http://127.0.0.1:PORT
```

一开始我用 ping 测试，发现一直不通。查了下说是 ping 使用 ICMP 协议，blabla，但是代理是 TCP、UDP，所以挂上代理也 ping 不通，这方面以后慢慢了解，反正挂上代理就能获取数据了。

#### Step three: Set up your access

搞完就跳到 Dashboard 页面了，这部分貌似是设置访问权限等级 (tier)？不理解，先跳过。

#### Step five: Make your first request

官网原文就没有 Step four，不知是否故意为之。教程套娃好麻烦啊，还是自己一个个搜吧。

## 写在最后

需要在 header 里添加一个 BEARER TOKEN 才能获取数据，不清楚能不能直接在 url 里添加 header，不编写程序，直接用浏览器的那种。
