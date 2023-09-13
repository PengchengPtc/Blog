---
title: 安卓开发之微信UI设计-MyApplycation
date: 2022-03-21 16:39:37
summary: 你不能只问顾客要什么，然后想法子给他们做什么。等你做出来，他们已经另有新欢了。
categories: 安卓开发
tags:
	- 安卓开发
---

# 微信UI设计

## 实现四个页面的布局

## 环境

1. java

2. 安卓虚拟机

   > 编辑器使用Android Studio

### 布局列表

布局文件均存在与res的layout文件夹中

[![qnIhVJ.png](https://s1.ax1x.com/2022/03/21/qnIhVJ.png)](https://imgtu.com/i/qnIhVJ)

### 各Tab页面的实现

此处要建xml文件写xml，类似于html的文件，是页面的“骨架”。

#### 头部标题

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="65dp"
    android:background="#000000"
    android:orientation="vertical">

    <TextView
        android:id="@+id/textView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_gravity="center"
        android:text="@string/app_name"
        android:textColor="#ffffff"
        android:textSize="20sp" />
</LinearLayout>
```

#### 底部导航

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:layout_width="match_parent"
    android:layout_height="80dp"
    android:background="@drawable/bottom_bar"
    android:orientation="horizontal"
    android:baselineAligned="false">

    <LinearLayout
        android:id="@+id/id_tab_weixin"
        android:layout_width="0dp"
        android:layout_height="match_parent"
        android:layout_gravity="center"
        android:layout_weight="1"
        android:orientation="vertical">

        <ImageButton
            android:id="@+id/id_tab_weixin_img"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:background="#000000"
            android:clickable="false"
            android:contentDescription="@string/app_name"
            app:srcCompat="@drawable/tab_weixin_pressed" />

        <TextView
            android:id="@+id/textView1"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="微信"
            android:textColor="#ffffff"
            android:gravity="center"
            android:clickable="false"
            android:textSize="15sp" />
    </LinearLayout>

    <LinearLayout
        android:id="@+id/id_tab_frd"
        android:layout_width="0dp"
        android:layout_height="match_parent"
        android:layout_gravity="center"
        android:layout_weight="1"
        android:orientation="vertical">

        <ImageButton
            android:id="@+id/id_tab_frd_img"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:background="#000000"
            android:clickable="false"
            android:contentDescription="@string/app_name"
            app:srcCompat="@drawable/tab_find_frd_normal" />

        <TextView
            android:id="@+id/textView2"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="朋友"
            android:textColor="#ffffff"
            android:gravity="center"
            android:clickable="false"
            android:textSize="15sp" />
    </LinearLayout>

    <LinearLayout
        android:id="@+id/id_tab_contact"
        android:layout_width="0dp"
        android:layout_height="match_parent"
        android:layout_gravity="center"
        android:layout_weight="1"
        android:orientation="vertical">

        <ImageButton
            android:id="@+id/id_tab_contact_img"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:background="#000000"
            android:clickable="false"
            android:contentDescription="@string/app_name"
            app:srcCompat="@drawable/tab_address_normal" />

        <TextView
            android:id="@+id/textView3"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="通讯录"
            android:textColor="#ffffff"
            android:gravity="center"
            android:clickable="false"
            android:textSize="15sp" />
    </LinearLayout>

    <LinearLayout
        android:id="@+id/id_tab_settings"
        android:layout_width="0dp"
        android:layout_height="match_parent"
        android:layout_gravity="center"
        android:layout_weight="1"
        android:orientation="vertical">

        <ImageButton
            android:id="@+id/id_tab_settings_img"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:background="#000000"
            android:clickable="false"
            android:contentDescription="@string/app_name"
            app:srcCompat="@drawable/tab_settings_normal" />

        <TextView
            android:id="@+id/textView4"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="设置"
            android:textColor="#ffffff"
            android:gravity="center"
            android:clickable="false"
            android:textSize="15sp" />
    </LinearLayout>
</LinearLayout>

```

#### 第一个页面

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">

    <TextView
        android:id="@+id/textView5"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:gravity="center"
        android:layout_gravity="center"
        android:layout_weight="1"
        android:text="这是微信界面"
        android:textSize="30sp"
        android:textStyle="bold"/>
</LinearLayout>

```

#### 第二个页面

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">

    <TextView
        android:id="@+id/textView5"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:gravity="center"
        android:layout_gravity="center"
        android:layout_weight="1"
        android:text="这是微信朋友圈界面"
        android:textSize="30sp"
        android:textStyle="bold"/>

</LinearLayout>

```

#### 第三个页面

```xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent">


    <androidx.recyclerview.widget.RecyclerView
        android:id="@+id/tab03_1"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:overScrollMode="never"
        android:scrollbars="none" />

    <include layout="@layout/tab03_include_recycle_item" />
</RelativeLayout>
```

#### 第四个页面

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">

    <TextView
        android:id="@+id/textView5"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:gravity="center"
        android:layout_gravity="center"
        android:layout_weight="1"
        android:text="这是设置界面"
        android:textSize="30sp"
        android:textStyle="bold"/>

</LinearLayout>

```

###  页面注册

所有页面需要在activity_main里面注册

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    tools:context=".MainActivity">

    <include layout="@layout/top"></include>

    <FrameLayout
        android:id="@+id/id_content"
        android:layout_width="match_parent"
        android:layout_height="0dp"
        android:layout_weight="1">

    </FrameLayout>

    <include layout="@layout/bottom" />
</LinearLayout>

```

> 1.include 相当于占位符，为头部布局和底部导航布局占位
>
> 2.FrameLayout则是四个页面的布局展位

至此微信UI静态布局已经实现，接下来是实现底部导航的点击效果，需要写java。

## 多个Fragment之间的跳转

### 实现方式

[![qnTONd.png](https://s1.ax1x.com/2022/03/21/qnTONd.png)](https://imgtu.com/i/qnTONd)

### 1、创建4个自定义Fragment类继承自Fragment，并且创建对应的布局文件，之后在Fragment类文件内部加载布局文件

[![qnHpGR.png](https://s1.ax1x.com/2022/03/21/qnHpGR.png)](https://imgtu.com/i/qnHpGR)

```java
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        requestWindowFeature(Window.FEATURE_NO_TITLE);
        setContentView(R.layout.activity_main);

        initView();
        initEvent();
        initFragment();
        setSelect(0);
    }
```

### 2、在MainAcitvity的布局文件下创建一个FrameLayout用来加载Fragment(上面已经实现)

```xml
 <FrameLayout
        android:id="@+id/id_content"
        android:layout_width="match_parent"
        android:layout_height="0dp"
        android:layout_weight="1">

    </FrameLayout>
```

### 3、在Main Activity创建对应的4个自定义Fragment对象，并进行初始化

```java
package com.example.mywechat;

import android.app.Activity;
import android.app.Fragment;
import android.app.FragmentManager;
import android.app.FragmentTransaction;
import android.os.Bundle;
import android.util.Log;
import android.view.View;
import android.view.Window;
import android.widget.ImageButton;
import android.widget.LinearLayout;

private void initFragment(){
        fm = getFragmentManager();
        FragmentTransaction transaction= fm.beginTransaction();
        transaction.add(R.id.id_content,mTab01);
        transaction.add(R.id.id_content,mTab02);
        transaction.add(R.id.id_content,mTab03);
        transaction.add(R.id.id_content,mTab04);
        transaction.commit();
    }

```

### 4.实现点击按钮切换Fragment的界面效果

```java
  @Override
    public void onClick(View view) {
        Log.d("OnClick","1");
        resetImgs();
        switch(view.getId()){
            case R.id.id_tab_weixin:
                Log.d("OnClick","2");
                setSelect(0);
                break;
            case R.id.id_tab_frd:
                setSelect(1);
                break;
            case R.id.id_tab_contact:
                setSelect(2);
                break;
            case R.id.id_tab_settings:
                setSelect(3);
                break;
            default:
                break;
        }
    }
```

## 实现效果

部分截图如下

[![qnHbYd.png](https://s1.ax1x.com/2022/03/21/qnHbYd.png)](https://imgtu.com/i/qnHbYd)

[![qnHvOf.png](https://s1.ax1x.com/2022/03/21/qnHvOf.png)](https://imgtu.com/i/qnHvOf)

## 总结

​	这学期选了移动开发这门课，因为之前对移动开发比较感兴趣，因为我们平时和手机打交道比较多，移动应用已经融入我们的日常生活。这次模仿微信，实现了一个简单的UI。总结了以下几点。

​	1.首先通过老师的讲解，学到了基础概论和实现的流程

​	2.通过之前学前端，发现有虽然框架不同，但又很多思想是类似，HTML类似于XML,JavaScript类似于Java

​	3.遇到问题，可以自行查阅资料，解决之后，收获还是蛮多的。
