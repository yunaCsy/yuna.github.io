---
title: css笔记
date: 
---


[TOC]

# html中引入css的方法
行内样式、嵌入式、导入式、 链接式

```css
<style type="text/css">
	@import="mystyle.css";
</style>
```

**如果仅需要引入一个css文件，则使用链接方式，如果需要多个css文件，则首先用链接方式引入一个"目录"css文件，这个"目录"css文件中在使用导入式引入其他css文件**

## link与@import的区别
+ @import只能导入样式，link可以定义RSS，rel连接属性，引入网站图标等。
+ 加载顺序区别，link标签引入的css被同时加载，@import引入的css将在页面加载完毕后再加载
+ 兼容性区别

> 使用链接方式时, 会在装载页面主体部分之前装载css文件, 这样显示出来的页面从一开始就是带有样式效果的, 而使用导入式时,会在整个页面装载完成之后再装载css文件, 对于有的浏览器来说, 在一些情况下, 如果网页文件的体积比较大,则会出现先显示无样式的页面,闪烁一下之后再出现设置样式后的效果.从浏览器的感受来说, 这是使用导入式的一个缺陷.




# 布局
盒模型：content、padding、border、margin

+ 元素垂直对齐 vertical-alige 仅适用行内元素
+ 宽高自适应
    - max-content 采用内部元素宽度值最大的那个元素的宽度作为最终容器的宽度
    - min-content 采用内部元素最小宽度值的那个元素的宽度作为最终容器的宽度
    - fit-content 将宽度收缩为内容宽度，加margin：auto实现内容自适应的居中效果，类似高度也有此特性
    - fill-available 撑满可用空间，可以实现等高布局


```css
/* 清除浮动 */
.clearfix::before, .clearfix::after {
    conetne: "",
    display: table;
}
.clearfix::after {
    clear: both;
}

.clearfix {
    *zoom: 1;
}
```




# CSS选择器

**这就是一种"内容"与"表现形式"的对应关系**

+ 群组选择器用“，”隔开  
+ 后代选择器用 空格 隔开


## 权重
+ id 0100
+ class 0010
+ 标签 0001
+ 行内 最高
+ 继承权重为null, *权重0, 0 > null
+ !important > 行内

## 伪类，伪元素
+ 伪类， 应用于一组html元素，而你无需在html中用类标记他们 
    - ::first-child
    - ::link
    - ::hover
+ 伪元素，是html中并不存在的元素，如定义第一个字母或第一行文字
    - ::first-letter
    - ::first-line
    - ::before
    - ::after
+ 链接多种状态定义顺序 link，visited，focus，hover，active
    

## 后代级别选择器
+ div p
+ div > p
+ p:only-child
+ p:nth-child(2)
+ p:nth-last-child(2)
+ p:first-child
+ p:last-child
+ :root
+ p:empty


## 同辈级别选择器
+ div + p
+ p ~ ul
+ p:first-of-type
+ p:last-of-type
+ p:only-of-type
+ p:nth-of-type(2)
+ p:nth-last-of-type(2)

## 属性选择器
+ [attribute] 匹配指定属性，不论具体值是什么
+ [attribute="value"] 完全匹配指定属性值
+ [attribute~="value"] 属性值是以空格分割的多个，其中一个完全匹配指定值
+ [attribute|="value"] 已value-打头
+ [attribute^="value"] 已value开头，value为完整单词或单词一部分
+ [attribute$="value"] 已value结尾，value为完整单词或单词一部分
+ [attribute*="value"] 属性值为指定值得子字符串


## UI伪类选择器
+ :enabled input上作用
+ :disabled input上作用
+ :checked   input上作用
+ :not(select) 
+ ::selection  选中



# 介绍下BFC及其应用

BFC（Block Format Context）块级格式化上下文，是页面盒模型中的一种css渲染模式。相当于`一个独立的容器，里面的元素和外部的元素相互不影响`。


创建BFC的方式有：
+ html根元素
+ float浮动
+ 绝对定位
+ overflow不为visible
+ display为表格布局或者弹性布局

主要的作用是：
+ 清除浮动
+ 防止同一BFC容器中的相邻元素－的外边距重叠问题



#  响应式web设计
针对任意设备对网页内容进行完美布局的一种显示机制

## 媒体设备 
+ screen
+ print

`media="screen"`


## 响应式布局

+ 要指定的宽度（以像素为单位）/ 容器宽度（以像素为单位） = 值
+ 优点：在各个设备显示更舒服的样式
+ 缺点：兼容各种设备工作量大，效率低下，代码累赘

`弹性网格布局，弹性图片，媒体和媒体查询整合起来`

```css
@media screen and (max-width: 960px) {
    div {}
}
```

```html
<link rel="stylesheet" media="not screen and (max-width: 960px) and (orientation:portrait) " href="800width-potrtrait-screen.css"/>
```




# 字体
倾斜的字体本身是一种独立存在的字体, 对应于操作系统中的某一个字体库文件  

font-style：italic | oblique
+ italic 是使用当前字体的斜体字体
+ oblique 是单纯地让文字（形状）倾斜


# 单位em、rem、dpr、ppi、设备独立像素
+ em: 尺寸跟父级的字号建立关连
+ rem: 尺寸跟根级(html元素的字号)相关联
+ 设备像素: 物理像素，一般手机的分辨率值得就是设备像素，一个设备的设备像素是不可变的
+ dpr 是设备像素和设备独立像素的比值, 一般pc dpr=1 iphone7 dpr=2
+ ppi 每英寸的物理像素的密度
+ 在所有现代浏览器中，其默认的字体大小就是16px，默认1em=16px。




# css编码技巧
+ currentColor
+ 继承

```css
input, select, button {font: inherit}
a {color: inherit}
```


## width
+ width:auto 会使元素撑满整个元素，margin、border、padding、content区域会自动分配水平空间。




## 背景与边框
+ box-sizing: border-box
+ outline 外边框不会占据空间位置
+ background-position扩展语法方案

```css
.eg {
    background: url(img.png) no-repeat #58a;
    background-position: right 20px bottom 10px;
}
```

+ background-origin 方案 

`background-position:top left`,这个top left到底是哪个左上角？ 每个元素身上都存在的三个矩形框 border box（边框的外沿框）、padding box（内边距的外沿框）、content box（内容去的外沿框。background-position默认是以padding box为准。 background-origin可以用来改变这种行为。

```css
.eg {
    padding: 10;
    background: url(img.png) no-repeat bottom right #58a;
    /* 背景的偏移量与容器的内边距一致 */
    background-origin: content-box;
}
```

## 定位
`position: sticky; top:0px`, 粘性定位

+ 同级会叠加
+ 不同级会把上面的顶走


## font-size: 0
line-block的元素之间会有空白区域的影响，元素之间差不多会有一个字符的间隙。最简单有效的方法是设置父元素的font-size属性为0。

## ios
+ 自带的click点击效果`-webkit-tap-highlight-color: rgba(0,0,0,0)`
+ 控制元素在移动设备上是否使用滚动回弹效果`-webkit-overflow-scrolling: touch | auto;`


## flex

+ `flex-grow: 1 | 2 | 3 ...`  可用空间分配
+ `flex-shrink: 0 | 1 | 2 ...`  动态缩小 空间分配
+ min-width >  flex-basis (主轴尺寸) > width
+ `flex： 0 0 100px`分别对应 放大（flex-grow），缩小（flex-shrink），轴尺寸（flex-basis）
+ order 排序
+ 使用margin自动撑满空间


## scroll
overflow：scroll 时不能平滑滚动，添加-webkit-overflow-scrolling：touch启用了硬件加速特性，所以滑动很流畅。


## 几何图形
+ clip-path
+ shape-outside 的本质其实是生成几何图形，并且裁剪掉其几何图形之外周围的区域，让文字能排列在这些被裁剪区域之内。

```css
{
    /* keyword values */
    clip-path: none;

    /* image values */
    clip-path: url(resources.svg);

    /* box values */
    clip-path: fill-box;
    clip-path: stroke-box;
    clip-path: view-box;
    clip-path: margin-box;
    clip-path: padding-box;
    clip-path: content-box;

    /* geometry values */
    clip-path: inset(100px 50px);
    clip-path: circle(50px at 0 100px);
    /* 可以生成任意多边形 */
    clip-path: polygon(50% 0, 100% 50%, 50% 100%, 0 50%);

    /* box and geometry values combined */
    clip-path: padding-box circle(50px at 0 100px);

    /* global values */
    clip-path: inherit;
    clip-path: initial;
    clip-path: unset;
}
```

## 文本省略
```css
/* 文本省略 */
overflow: hidden;
white-space: nowrap;
text-overflow: ellipsis;

/* 单词换行 非中日韩文本的换行规则 */
word-break: break-all | normal | keep-all

/* 允许长的不可分割的单词进行分割并换行, 长单词或url换行 */
word-wrap: normal | break-wrod
```
