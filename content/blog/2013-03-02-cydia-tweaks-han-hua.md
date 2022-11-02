---
title: 【Cydia 插件汉化教程】 两种方法图文视频详细教程
author: Q
type: post
date: 2013-03-02T06:29:14+00:00
url: /blog/466
views:
  - 4032
categories:
  - iOS
  - Jailbreak
tags:
  - iOS
  - 汉化插件
  - 越狱

---
* 转载请标明出处：<https://xingxiang.me/blog/466>

* 请大家支持正版，使用正版软件，插件

deb制作教程：<https://xingxiang.me/blog/463/>

在ios上的制作方法 ：<https://xingxiang.me/blog/465/> 

* 总共有两个方法，废话不多说，开始…… 

## * 插件常放置文件的目录（也可以到Cydia里查看目录）

//Library/PreferenceBundles

//Library/PreferenceLoader/Preferences

//Library/MobileSubstrate/DynamicLibrarie

//System/Library/PreferenceBundles

//Library/Weeloader

//System/Library/WeeAppPlugins  
一般所有的插件都能在其中一个目录里进行汉化 ，大家可以像我一样在iFile创建一个收藏夹…

![][1]

## 方法一：

（优点: 较方便。缺点：更新插件会丢失汉化，有的菜单二级目录无法汉化。so 不推荐）

* 已Zephyr为例：

1. 首先看到的界面当然是英文的

![][2]

2. 然后打开iFile，定位到//Library/PreferenceLoader/Preferences （就是上面给出的目录）

![][3]

3. 找到Zephyr.plist

![][4]

4. 点击，选择使用文本编辑器打开

![][5]

5. 然后我们先汉化第一个 文本 ：Enabled

点击搜索，输入Enabled

![][6]

6. 然后选择这个单词 注意：旁边的标点别乱删

![][7]

7. 改成 开关

![][8]

8. 保存

9. 杀掉设置后台

10.回到设置里一看

![][9]

Finally 成功了!!!!!!

但是在此不推荐第一种，因为一些多二级菜单的插件汉化不彻底，而且容易丢失。

## 方法一 视频演示：

【简版 v2.0】youku链接：[http://v.youku.com/v\_show/id\_XNTMwODYxNTY4.html][10]

【详细有声版 v2.0】youku: [http://v.youku.com/v\_show/id\_XNTMxMDYwNzk2.html][11]  

## 第二种方法：

（极为推荐，I prefer this）  
* 废话不多说，还是以Zephyr为例……

![][12]

1. 打开iFile，定位到//Library/PreferenceLoader/Preferences （就是上面给出的目录）

![][13]

2. 在此目录创建语言包

简体：zh_CN.lproj

繁体：zh_TW.lproj

![][14]

## 3. 找到Zephyr.plist

4. 然后在zh_CN.lproj里创建 Zephyr.strings （文件名与你想修改的plist相同）

一定要 选 常规文件

![][15]

5. 点击这个strings

选择属性表编辑器，打开是空白的

![][16]![][17]</figure> 

6. 点击+

直接输入你在设置里看到的文字，注意大小写

![][18]

7. 然后按 完成

8. 然后再按你创建的属性表

![][19]

9. 输入你想汉化的内容

![][20]

10.杀掉设置后台

Finally 看到效果了吧

全面汉化效果:

![][21]

Zephyr 的 strings 全部:

![][22]

还是推荐这种方法!!!!

## 方法二 视频演示：

【简版 v2.0】youku链接：[http://v.youku.com/v\_show/id\_XNTMwODYzMDg0.html][23]  

【详细有声版 v2.0】 youku链接:[http://v.youku.com/v\_show/id\_XNTMxMDY0MDUy.html][24]

 [1]: /images/HanHua/1.png
 [2]: /images/HanHua/2.png
 [3]: /images/HanHua/3.png
 [4]: /images/HanHua/4.png
 [5]: /images/HanHua/5.png
 [6]: /images/HanHua/6.png
 [7]: /images/HanHua/7.png
 [8]: /images/HanHua/8.png
 [9]: /images/HanHua/9.png
 [10]: http://v.youku.com/v_show/id_XNTMwODYxNTY4.html
 [11]: http://v.youku.com/v_show/id_XNTMxMDYwNzk2.html
 [12]: /images/HanHua/10.png
 [13]: /images/HanHua/11.png
 [14]: /images/HanHua/12.png
 [15]: /images/HanHua/13.png
 [16]: /images/HanHua/14.png
 [17]: /images/HanHua/15.png
 [18]: /images/HanHua/16.png
 [19]: /images/HanHua/17.png
 [20]: /images/HanHua/18.png
 [21]: /images/HanHua/19.png
 [22]: /images/HanHua/20.jpg
 [23]: http://v.youku.com/v_show/id_XNTMwODYzMDg0.html
 [24]: http://v.youku.com/v_show/id_XNTMxMDY0MDUy.html