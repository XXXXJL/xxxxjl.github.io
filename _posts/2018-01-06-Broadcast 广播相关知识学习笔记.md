---
layout: post
title: Broadcast 广播相关知识学习笔记
date: 2018-01-06 15:07:00.000000000 +09:00

---



 **Broadcast 的定义**

Broadcast 是Android 中广泛应用在应用程序之间传输信息的机制。发送的广播是一个Intent，这个Intent可以携带我们想要的数据。不同应用程序之间只要注册了和发送广播相同的action 的广播接收者，都可以收到这个广播。

**广播的使用场景**

* 同一App 中多个进程的不同组件之间的消息通信
* 不同App 的组件之间通信

**广播的种类**

* **普通广播：Context.sendBroadcast： **传给各个符合条件的receiver ，各个receiver 的接收顺序不被保证，广播不能被截获
* **有序广播：Context.sendOrderedBroadcast：** 按照优先级高低依次传给receiver ，优先级高的可以截获广播，使得优先级低的广播无法收到广播
* **本地广播：**只在自身App内传播，由LocalBroadcastManager完成

**广播的实现（receiver）**

* **静态注册：** 通过在`AndroidManifest.xml` 文件中使用`<receiver>` 进行注册，注册完成后就一直运行，静态注册的广播即使Activity 销毁了，甚至进程被杀掉了，还是可以收到广播。
* **动态注册：** 跟随Activity 的生命周期，是在代码中调用`registerReceiver()` 进行注册，会随着Activity 的销毁而销毁。

**广播的实现机制**

1. 自定义广播接收者Broadcast ，并复写`onReceive()` 方法；
2. 通过Binder 机制向AMS(Activity Manager Service ) 进行注册；
3. 广播发送者通过Binder 机制向AMS 发送广播；
4. AMS 查找符合相应条件的(IntentFilter/Permission 等) 的BroadcastReceiver，将广播发送到BroadcastReceiver(一般情况下是Activity) 相应的消息循环队列中；
5. 消息循环队列执行拿到此广播，回调BroadcastReceiver 中的`onReceive()` 方法。

**LocalBroadcastManager 详解**

* 使用LoacalBroadcastManager 发送的广播只在App 内部传播，不用担心泄露隐私数据；
* 其他App 无法对你的App 发送该广播，因为你的App 根本不可能接收到非自身应用发送的该广播，因为不用担心有安全漏洞；
* 比系统的全局广播更加高效；
* LocalBroadcastManager 高效的原因主要是它内部是通过Hander 实现的，其`sendBroadcast()` 方法含义并非和我们平时所用的一样，它的`sendBroadcast()` 方法是通过handler 发送一个Message 实现；
* 内部通过Handler 实现广播的发送，相比于系统的Binder 机制更加高效，通过handler发送，高效，同时也保证了在应用内使用，其他app无法利用漏洞。

**广播的使用简单举例**

* 发送方

  发送广播：

  ```kotlin
      val intent = Intent()
  	//设置广播的名字（设置Action）
      intent.action = "broadcast_action"
      sendBroadcast(intent)
  ```

* 接收方

  注册广播：

  ```kotlin
      var intentFilter = IntentFilter()
      intentFilter.addAction("")
      registerReceiver(bdReceiver, intentFilter)
  ```

  广播接收：

  ``` kotlin
  class bdReceiver: BroadcastReceiver(){
          override fun onReceive(context: Context?, intent: Intent?) {
              var action = intent!!.action
              if (action.equals("broadcast_action")){
                  Log.i("BroadcastReceiver", "收到广播消息")
              }
          }
      }
  ```

  **关于系统广播**

  系统会在发生各种系统事件时自动发送广播，例如当系统进入和退出飞行模式时，系统广播会发被发送给所有同意接收的应用。

