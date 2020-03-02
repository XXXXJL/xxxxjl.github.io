---
layout: post
title: Activity 和Fragment 学习笔记
date: 2018-01-05 15:07:00.000000000 +09:00
---

# Activity 生命周期  

Activity 是Android 四大组件之一，也是日常开发过程中最最常用的组件了。

 ![avatar](https://github.com/XXXXJL/xxxxjl.github.io/raw/master/assets/blog_images/2019-01/2019010502.png?raw=true)

**Activity生命周期的7个方法说明：**  
onCreate(), onStart(), onResume(), onPause(), onStop(), onRestart(), onDestory()  

方法名称 | 描述 | 用途举例 | 下一方法
 :----- |  :----- | :-: | :-:
onCreate() | 当Activity第一次创建时调用。该方法（如果有）会提供给你一个包含之前<br>活动的冻结状态信息bundle. | 进行一系列初始化的操作时。例如：创建View，加载视频数据等等。 | onStart()
onRestart() | 当Activity 状态为onStop()重新唤起后调用的方法 | 当活动停止后重新启动该活动时调用（不常用），针对停止后重启操作。 |  onStart()
onStart() | 该方法代表Activity正在被启动，此时Activity已经可见，但是此时Activity还未到前台，因此用户还无法看到，无法响应用户的交互互动作。 | - | onResume()
onResume() | 当Activity将开始与用户进行交互时调用。在这个时间点你的活动将会在活动堆栈的顶端，用户输入将会访问它。 | 暂停后恢复我们会在该方法中进行一些操作，例如视频继续播放 |  onPause()
onPause() | onPause方法表示Activity正在暂停，正常情况下，onStop紧接着就会被调用。| 该方法十分重要，用来做信息持久化存储操作以及停止消耗CPU资源操作，如记录视频播放进度时间，以及暂停视频播放操作等。 |  onStop()或onResume()
onStop() | 表示Activity即将停止，可以做一些稍微重量级的资源回收工作等，同样也不能太耗时。 | 界面将会隐藏或销毁，做一些重要信息或未被存储的信息的存储操作。但也不要太耗时。如存储用户信息等操作，以及用户此次观看的视频地址以及时间，便于下次打开该界面时继续播放。 |  onDestory或onRestart()
onDestory() | Activity被销毁钱最后一个被调用的方法。这个方法将会发生因为活动将会结束（在活动中调用finish()方法，或者系统临时销毁该实例节约空间。你可以使用isFinishing()方法区别这两种场景）。 | 界面将要销毁，释放一些实例节约空间，如置空List集合等。 | -   

**Activity 阶段状态：**  
 ![Activity 四种主要状态](https://github.com/XXXXJL/xxxxjl.github.io/raw/master/assets/blog_images/2019-01/2019010503.png?raw=true)  

 一个Activity 从本质上讲拥有4种状态：

 * 运行：如果当前Activity 在前台界面(堆栈栈顶)
 * 暂停：当ActivityA 被另一个非全屏ActivityB（如一个对话框） 覆盖时，ActivityA将会暂停，一个暂停的Activity也是可以货源的（他的成员和成员信息将会保留），当在内存资源缺乏时将会被系统回收。  
 * 停止： 当ActivityA 被另一个全屏ActivityB 覆盖时，那么ActivityA将处于停止状态，该活动也仍保留全部的状态和成员信息，但将会被隐藏起来不再展示给用户，并且当内存在其他地方被需要时该活动就将会被系统杀死。  
 * 重启：如果activity处于暂停或者停止状态，系统将会在内存中终止该活动无论是结束活动或者杀死进程。当它再一次展示给用户时，它必须是完全重启并且恢复到之前的状态。  

 **状态转换：**  

 ![Activity 状态转换](https://github.com/XXXXJL/xxxxjl.github.io/raw/master/assets/blog_images/2019-01/2019010504.png?raw=true)  