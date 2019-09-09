---
title: 移动端适配问题 采坑记
date: 2019-04-28 17:59:50
tags: h5
cover: https://images.pexels.com/photos/2789165/pexels-photo-2789165.jpeg?auto=compress&cs=tinysrgb&dpr=2&w=500
---

#### 此文用来整理记录 在移动端开发过程中遇到的一些适配问题， 会一直更新~

1. ios 上input输入框disabled状态时背景颜色变灰

  原因：ios默认disabled属性时透明度为0.3

  解决方案： input:disabled  { opacity: 1}


2. 在使用 img标签渲染图片， ios图片不能正常显示， 安卓端可以正常显示

  效果如下:
  ![](https://user-gold-cdn.xitu.io/2019/7/8/16bd0b40b5d8178e?w=422&h=234&f=png&s=8535)

  解决办法： 在使用img标签时， img标签外套一个div标签， 使用方式和css如下

  ![](https://user-gold-cdn.xitu.io/2019/7/8/16bd0b659cb6d755?w=604&h=350&f=png&s=43368)
    css:

  ![](https://user-gold-cdn.xitu.io/2019/7/8/16bd0b6ca56eb99b?w=562&h=462&f=png&s=44561)


3. img 元素下方有间隙

  效果如图： 图片与下方文字之间有间隙

  ![](https://user-gold-cdn.xitu.io/2019/7/8/16bd0b7e3d0edbc3?w=338&h=224&f=png&s=23191)

  解决方式：

  1.将图片元素设置为块级元素， 即  {display: block}

  2.设置父元素 font-size 为0