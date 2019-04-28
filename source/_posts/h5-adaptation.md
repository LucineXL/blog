---
title: 移动端适配问题 整理
date: 2019-04-28 17:59:50
tags: h5
cover: https://images.unsplash.com/photo-1437652010333-fbf2cd02a4f8?ixlib=rb-1.2.1&auto=format&fit=crop&w=800&q=60
---

![](https://images.unsplash.com/photo-1437652010333-fbf2cd02a4f8?ixlib=rb-1.2.1&auto=format&fit=crop&w=800&q=60)

<br>

#### 此文用来整理记录 在移动端开发过程中遇到的一些适配问题， 会一直更新~

1. ios 上input输入框disabled状态时背景颜色变灰

  原因：ios默认disabled属性时透明度为0.3

  解决方案： input:disabled  { opacity: 1}

