# SuspendButtonLayout

## 一个带浮动按钮的布局，按钮可以展开

### 一.简介

一个轻量的带浮动按钮的布局。按钮可以随意展开关闭、显示隐藏，可以监听按钮打开、关闭、移动等状态，可以监听各个按钮的点击事件。无论你怎么拖动按钮，按钮最终都会停留在左边缘或右边缘。

### 二.效果图

![image](https://raw.githubusercontent.com/laocaixw/SuspendButtonLayout/master/screen/image1.gif)

### 三.Demo的Apk下载

[Apk](https://raw.githubusercontent.com/laocaixw/SuspendButtonLayout/master/screen/Demo_SuspendButtonLayout.apk)

### 四.用法

因为**SuspendButtonLayout**布局继承了RelativeLayout布局，且按钮在**SuspendButtonLayout**中，所以想让按钮浮在你的布局上方，应该把**SuspendButtonLayout**布局写在你的布局下面。（如果你无所谓按钮在什么位置，可以直接把**SuspendButtonLayout**当做RelativeLayout来用。）

##### 1.布局：

```

<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:suspend="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent">
    
    <RelativeLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent">
        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_centerInParent="true"
            android:text="Hello World!" />
    </RelativeLayout>

    <com.laocaixw.layout.SuspendButtonLayout
        android:id="@+id/layout"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        suspend:distance="80dp"
        suspend:imageSize="50dp"
        suspend:marginY="100dp"
        suspend:number="8"
        suspend:imageMainOpen="@mipmap/suspend_main_open"
        suspend:imageMainClose="@mipmap/suspend_main_close"
        suspend:image1="@mipmap/suspend_1"
        suspend:image2="@mipmap/suspend_2"
        suspend:image3="@mipmap/suspend_3"
        suspend:image4="@mipmap/suspend_4"
        suspend:image5="@mipmap/suspend_5"
        suspend:image6="@mipmap/suspend_6" />
</RelativeLayout>

```

如下图，绿色部分为按钮停留区域，各属性：

- distance="80dp" // 按钮打开后，主按钮和子按钮的距离
- imageSize="50dp" // 按钮大小，所占区域的边长
- marginY="100dp" // 与上下边缘距离，下图中黄色部分的高度
- number="8" // 展开的子按钮的数量，可以是3-6个
- imageMainOpen="@mipmap/suspendMainOpen" // 中间按钮展开时的图片资源
- imageMainClose="@mipmap/suspendMainClose" // 中间按钮关闭时的图片资源
- image1="@mipmap/suspend_1" // 子按钮的图片资源，image1~image6

![image](https://raw.githubusercontent.com/laocaixw/SuspendButtonLayout/master/screen/image2.jpg)

##### 2.使用方法：

```

SuspendButtonLayout suspendButtonLayout = (SuspendButtonLayout) findViewById(R.id.layout);

suspendButtonLayout.setOnSuspendListener(new SuspendButtonLayout.OnSuspendListener() {
    @Override
    public void onButtonStatusChanged(int status) {
        // 监听按钮状态：展开、关闭、移动等
    }

    @Override
    public void onChildButtonClick(int index) {
        // 监听子按钮的点击事件
    }
});

suspendButtonLayout.hideSuspendButton(); // 隐藏按钮
suspendButtonLayout.showSuspendButton(); // 显示按钮

suspendButtonLayout.openSuspendButton(); // 展开按钮
suspendButtonLayout.closeSuspendButton(); // 关闭按钮

suspendButtonLayout.setMainCloseImageResource(R.mipmap.suspend_main_close); //设置关闭时，主按钮的图片
suspendButtonLayout.setMainOpenImageResource(R.mipmap.suspend_main_open); //设置展开时，主按钮的图片

```

##### 3.*使用细节详见Demo。*

### 五.原理

1. SuspendButtonLayout布局继承了RelativeLayout，拥有RelativeLayout的一切属性，每个按钮都在SuspendButtonLayout中；
2. 按钮的拖动是在onTouch方法中对控件做Animator动画处理；
3. 悬浮按钮OnSuspendListener事件监听采用接口回调机制。