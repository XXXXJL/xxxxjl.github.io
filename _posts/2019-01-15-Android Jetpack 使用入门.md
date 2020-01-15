---
layout: post
title: Android Jetpack 使用入门
date: 2018-01-09 08:00:00.000000000 +08:00
---
#Android Jetpack 使用入门

##Jetpack简介
***Jetpack是谷歌在Google I/O 大会上推出的帮助Android 开发者快速开发出优质应用的组件，下面内容是节选自[Android Developer]("https://developer.android.com/jetpack")官网的介绍：***  

Jetpack 是一套库、工具和指南，可帮助开发者更轻松地编写优质应用。这些组件可帮助您遵循最佳做法、让您摆脱编写样板代码的工作并简化复杂任务，以便您将精力集中放在所需的代码上。

Jetpack 包含与平台 API 解除捆绑的[androidx.*](https://developer.android.com/jetpack/androidx) 软件包库。这意味着，它可以提供向后兼容性，且比 Android 平台的更新频率更高，以此确保您始终可以获取最新且最好的 Jetpack 组件版本。

###使用Jetpack的优势：  
**加速开发：** 组件可单独采用（不过这些组件是为协同工作而构建的），同时利用Kotlin 语言能帮助您提高工作效率。

**消除样板代码：**Android Jetpack 可以很方便的管理Activity（例如后台任务、导航和生命周期管理），便于您快速高效的开发。

**构建高质量的强大应用：** Android Jetpack 组件围绕现代化设计实践构建而成，具有向后兼容性，可以减少崩溃和内存泄漏。

##在Android Studio 中引入Jetpack
打开**Module**中的`build.gradle`中添加`google()`代码库：

``` 
allprojects { 
    repositories { 
        google()
        jcenter()
    }
} 

```
