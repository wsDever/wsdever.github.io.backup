---
title: 用纯CSS3实现三角或箭头
categories:
  - css
tags:
  - css3
  - css
comments: true
date: 2017-02-15 18:28:03
---
### 简单介绍
三角形、箭头在页面菜单、导航、甚至进度条上使用的非常多。
今天在这里给出几种用css3做出来的样式

### 原理
元素的border属性，两端拐角其实是梯形连接，当元素的高与宽相等时可以明显看到四个梯形，当元素的高与宽相等且为0是，就形开了四个三角形，当设置其中一边与其它三条边不同颜色时（其它三边一般设置为透明或者同背景然），就可以看到一个三角形
<div style="display:inline-block;border: 20px solid blue;border-left-color: #f00;width: 20px;height: 20px;margin-right:40px;box-sizing: content-box"></div>
<div style="display:inline-block;border: 20px solid blue;border-left-color: #f00; width: 0px;height: 0px;margin-right:40px;"></div>
<div style="display:inline-block;border: 20px solid transparent;border-left-color: #f00; width: 0px;height: 0px;"></div>

代码分别为：
```
梯形：border: 20px solid blue;border-left-color: #f00; width: 20px;height: 20px;
三角形：border: 20px solid blue;border-left-color: #f00; width: 0px;height: 0px;
三角：border: 20px solid transparent;border-left-color: #f00; width: 0px;height: 0px;
```
可以看到，只要修改border-@-color，就可以得到一个对应方向的三角，@ 可以为top，left，right，bottom

### 任意的三角
通过上面的方法可以得到一个对应方向的三角，但是可以看到三角的顶角都是90度，那么只要改变三角形的三边就可以改变角度了，在这里只需要修改对应边的长度，如下：
<div style="display:inline-block;border: 20px solid transparent;border-left:80px solid #f00; width: 0px;height: 0px;"></div>
代码分别为：
```
border: 20px solid transparent;border-left:80px solid #f00; width: 0px;height: 0px;
```
可以看到，只要修改border-@，对应的宽度，就可以得到一个对应方向的三角，@ 可以为top，left，right，bottom

### 使用css伪类三角
通过 :after 伪类来实现，<a style="color:red" href="http://wshome.bid/main/shows/css3-arrow.html" target="" _blank="">点击此处</a>演示，实现如下：
```
.left-ang{
  position: relative;
}
.left-ang:after {
  border: 10px solid transparent;
  border-left: 10px solid #f00;
  width: 0;
  height: 0;
  position: absolute;
  content: ' '
}
```
也可以达到相同的效果。

### 实现箭头
方法也是通过伪类：after 不过要配合：before来实现，原理就是将：after与：before形成的三角形使用margin进行平移不同的数值。<a style="color:red" href="http://wshome.bid/main/shows/css3-arrow.html" target="" _blank="">点击此处</a>演示，实现如下：
```
.left_ang{
  position: relative;
}
.left_ang:after, .left_ang:before {
  border: 10px solid transparent;
  border-left: 10px solid #fff;
  width: 0;
  height: 0;
  position: absolute;
  top: 0;
  right: -20px;
  content: ' '
}

.left_ang:before {
  border-left-color: #f00;
  right: -21px;
}
```
可以看出，将：after和：before先均向右移动20px,然后把：before重新设置成移动21px，这样就形成了1px的差值。

### 实际应用
1、<a style="color:red" href="http://wshome.bid/main/shows/css3-arrow.html" target="" _blank="">进度条</a>
2、<a style="color:red" href="http://wshome.bid/main/shows/css3-arrow.html" target="" _blank="">仿对话框</a>

### 注意事项
由于IE8上不支持rgba，所以如果要兼容到IE8，那么颜色值不能设置成rgba。