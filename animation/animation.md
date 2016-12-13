# Android动画

### 概述

Android的animation由四种类型组成：alpha，scale，translate，rotate，对应官方文档地址[《Animation Resources》](http://developer.android.com/guide/topics/resources/animation-resource.html)


1. XML配置文件中

| 名称	        |描述           		| 
| ------------- |:--------------------- |
| alpha         | 渐变透明度动画效果 	|
| scale      	| 渐变尺寸伸缩动画效果  |
| translate 	| 画面转换位移动画效果  |
| rotate 		| 画面转移旋转动画效果	|

2、 动作文件存放位置

在res文件夹下创建anim文件夹，可将动画文件存在此处。

### Alpha动画

	Alpha 是Android透明度渐变动画，其基类为Animation类。

属性：

```xml
<?xml version="1.0" encoding="utf-8"?>
<alpha
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:fromAlpha="1.0"            #起始透明度，取值范围0.0--1.0 ，从完全透明到完全不透明
    android:toAlpha="0.1"              #结束透明度，取值范围同上

    android:duration="700"             #动画持续时间，毫秒为单位
    android:fillAfter="true"           #动画结束后，保持结束时的状态
    android:fillBefore="true"          #动画结束后，恢复为初始状态
    android:fillEnabled="true"         #效果同上
    android:repeatCount="5"            #重复次数,取值为-1时无限重复，默认动画执行一次
    android:repeatMode ="reverse"      #重复模式，有reverse和restart两个值，前者为倒序回放，后者为重新开始
    
/>

```

### Scale动画
	
	Scale是Android的尺寸缩放动画，集成自基类Animation类。

属性

```xml
<?xml version="1.0" encoding="utf-8"?>
<scale xmlns:android="http://schemas.android.com/apk/res/android"
	android:fromXScale="0.0"	# 起始X尺寸比例
	android:toXScale="1.4"		# 最终x尺寸比例
	android:fromYScale="0.0"	# 起始Y尺寸比例
	android:toYScale="1.4"		# 最终Y尺寸比例
	android:pivotX="50%"		# 缩放起点X轴坐标，取值可以是数值(50),百分数(50%),
								  百分数p(50%p),当取值为数值时，缩放七点为View左上角坐标加
								  具体数值像素，当取值为百分数时，表示在当前的View左上角坐
								  标加上View宽度的具体百分比，当数值为百分数p时，表示在View
								  左上角坐标加上父控件宽度的具体百分比
	android:pivoY="50%"
	android:duration="700"
	android:fillAfter="true"
	android:fillBefore="true"
	android:fillEnabled="true"
	android:repeatMode="reverse"
	android:interpolator="@android:anim/accelerate_decelerate_interpolator"
```