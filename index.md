请写出一个符合 W3C 规范的 HTML 文件，要求

页面标题为「我的页面」
页面中引入了一个外部 CSS 文件，文件路径为 /style.css
页面中引入了另一个外部 CSS 文件，路径为 /print.css，该文件仅在打印时生效
页面中引入了另一个外部 CSS 文件，路径为 /mobile.css，该文件仅在设备宽度小于 500 像素时生效
页面中引入了一个外部 JS 文件，路径为 /main.js
页面中引入了一个外部 JS 文件，路径为 /gbk.js，文件编码为 GBK
页面中有一个 SVG 标签，SVG 里面有一个直径为 100 像素的圆圈，颜色随意
注意题目中的路径



```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8">
        <title>我的页面</title>
        <link rel='stylesheet' href='/style.css'>
        <link rel='stylesheet' href='/print.css' media='print'>
        <link rel='stylesheet' href='/mobile.css' media='(max-width:500px)'>
    </head>
    <body>
        <svg xmlns='http://www.w3.org/2000/svg' version='1.1' width='500' height='500'>
            <circle cx='150' cy='150' r='50' fill='lightgreen' />
        </svg>
        <script src='/main.js'></script>
        <script src='/gbk.js' charset='GBK'></script>
    </body>
</html>
```





移动端是怎么做适配的？

回答要点：

meta viewport
媒体查询（CSS深入浅出第五课）
动态 rem 方案（CSS深入浅出第九课）



## meta-viewport
在移动设备上我们的网页会出现缩放的现象，因此就有了一种新方法，通过设置meta的viewport之后，移动端的浏览器就会将我们的页面放在一个虚拟的窗口中通过平移等操作来浏览网页，不会破坏网页原本的结构。
```
<meta name='viewport' content='width=device-width, initial-scale=1,maximum-scale=1'>
```
width：控制viewport的大小，device-width为设备的宽度
height：控制高度
maximum-scale：允许用户缩放到的最大比例
minimum-scale：允许用户缩放到的最小比例
user-scalable：用户是否可以手动缩放
## 媒体查询
> 媒体查询，添加自CSS3，允许内容的呈现针对一个特定范围的输出设备而进行裁剪，而不必改变内容本身。
媒体查询其实就是根据不同的条件来选择不同的css

比如说

```
<link rel='stylesheet' href='/mobile.css' media='(max-width:500px)'>
```
通过添加要求，max-width:500px  来让我们的页面在宽度小于500px的时候应用mobile.css
这是添加在link标签中的媒体查询，还有另外一种直接添加到style样式中的。
```
@media screen and (max-width: 300px) {
    body {
        background-color:lightblue;
    }
}
```
这里通过添加要求来让文档宽度小于300px的时候修改背景颜色
我们可以根据不同的要求来设定不同的样式，来让页面更为完美的在各个移动端显示。
## 动态rem方案
rem是CSS3新增的相对长度单位，它的值为我们页面根元素的font-size大小
媒体查询给我们提供了一种在不同设备中加载不同CSS样式的方法，但是当移动端页面大小不一，需要匹配的量很大的时候，这个时候一个个给定要求加载样式就变得相当麻烦了，所以需要我们做出改变。如何改变呢？我们需要按照比例来匹配我们的页面，不同的页面应用不同比例的宽度，这样就可以比较好的适配了。
因为rem值是可以根据页面大小来变化的，所以我们只需要在不同的页面宽度下应用不同的rem值，就可以根据屏幕的比例来实现我们的动态布局
```
<meta name="viewport" content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
 <script>
     var pageWidth = window.innerWidth
     document.write('<style>html{font-size:'+pageWidth/10+'px;}</style>')
 </script>
 ```
 我们rem的值始终是页面宽度的十等分，不同宽度页面下的显示比例都是一致的，也就实现了我们的动态布局。
 
 
 
 
 用过CSS3吗? 实现圆角矩形和阴影怎么做?
 
 
 
 ## CSS3实现圆角矩形
CSS3中可以通过border-radius这个属性来设置矩形四个角的半径
```
border-radius: 20px;
```
## CSS3实现阴影
CSS3中我们可以直接用box-shadow来实现阴影
```
box-shadow: 10px 10px 5px #000000;
```
![](//video.jirengu.com/xdml/image/91c35d38-8030-4d6c-85c6-4c25319570a2/2018-11-28-23-6-12.png)







什么是闭包，闭包的用途是什么？


# 什么是闭包
函数和这个函数内部能访问到的变量的总和就是闭包
代码表示
```
var local = '变量'
function fn(){
    console.log(local)
}
```
因为fn这个函数可以访问我们的local变量，所以他们一起被称为闭包。
# 闭包的用途
闭包的用处就是让一个私密的变量可以通过某种方法在别处被间接访问。
有的时候重要的变量不想让别人进行修改，于是就会将它放在一个函数中做成一个局部变量，这样在函数外部，就不能直接访问了
```
function fn(){
    var local = '重要的变量'
}
console.log(local) //报错
```
但是放在函数内部，满足了私密性，但是当我们想用的时候怎么用呢？就像你把钱放在保险柜里了，你不找个'钥匙'怎么开锁呢？
这个时候我们就需要来用'钥匙'来开锁取钱了。
```
!function(){
    var money = 100
    window.showMoney = function(){
        console.log(money)
    }
}()
showMoney()   // 100
```
这样我们就可以间接来通过钥匙打开保险柜来看看我们的钱了。
这里的变量money以及在函数内部能访问到变量money的函数showMoney共同组成了一个闭包。





call、apply、bind 的用法分别是什么？


## call()
用来改变this的指向
```
function.call(thisArg,arg1,arg2,...)
//可以通过改变thisArg这个参数来改变this的指向
```
举个例子
```
window.color = 'red'
document.color = 'yellow'
var s1 = {color: 'blue'}
function changeColor(){
    console.log(this.color)
}
changeColor() // red
changeColor.call() //red
changeColor.call(window) //red
changeColor.call(document) //yellow
changeColor.call(this) //red
changeColor.call(s1) //blue
```
我们可以通过改变call()方法中的thisArg参数从而改变this的指向。
## apply()
也是用来改变this的指向，只是和call()有略微的不同
```
function.apply(thisArg,[arg1,arg2,...])
//可以通过改变thisArg这个参数来改变this的指向
function.apply(thisArg,arg1,arg2,...)
//会报错
```
和call()最大的不同就是apply()传的是参数数组，而call()则是参数列表
```
function add(c,d){
    return this.a + this.b + c + d
}
var s = {a:1,b:2}
add.call(s,3,4) //10
add.apply(s,[3,4]) //10
```
除了传入参数的区别，apply()和call()用法都是基本一致的。
## bind()
bind()也可以改变this的指向，只不过bind()方法会创建一个新的函数，不会和apply(),call()方法一样立即被调用
```
fun.bind(thisArg[, arg1[, arg2[, ...]]]) //bind()语法

function add(c,d){
    return this.a + this.b + c + d
}
var s = {a:1,b:2}
add.bind(s,3,4)   //会返回一个函数实例，但是不会和上面apply(),call()一样直接弹出10
add.bind(s,3,4)() //10  被调用之后，就会给我们一个10了
```
### 总结
- call(),apply(),bind()都可以改变this的指向
- call()传入参数列表，apply()传入参数数组
- 相比于call()和apply()的立即调用，bind()会创建一个函数实例，便于以后调用





请说出至少 8 个 HTTP 状态码，并描述各状态码的意义。



HTTP状态码分为5种类型
1** 服务器收到请求，需要请求者继续操作
2** 操作被成功接收并处理
3** 重定向，需要进一步的操作来完成请求
4** 客户端错误，请求包含语法错误或无法完成请求
5** 服务器错误，服务器在处理请求的过程中发生了错误
状态码 404 服务器无法根据客户端的请求找到网页
状态码 403 服务器理解客户端的请求，但拒绝执行
状态码 301 被请求的资源已永久移动到新位置
状态码 400 客户端请求的语法错误，服务器无法理解
状态码 500 服务器内部错误，无法完成请求
状态码 401 请求要求用户的身份验证
状态码 202 已接受请求，但未处理完成
状态码 201 成功请求并创建了新的资源





请写出一个 HTTP post 请求的内容，包括四部分。
其中
第四部分的内容是 username=ff&password=123
第二部分必须含有 Content-Type 字段
请求的路径为 /path




```
POST /path HTTP/1.1
Host: www.baidu.com
User-Agent: curl/7.54.0
Accept: */*
Content-Length: 24
Content-Type: application/x-www-form-urlencoded

username=ff&password=123
``` 





请说出至少三种排序的思路，这三种排序的时间复杂度分别为

O(n*n)
O(n log2 n)
O(n + max)



## 冒泡排序
从数组的头部开始，每次比较两个元素，满足条件就交换位置，逐次比较，一直比较到数组的尾部，不能再比较了就说明排序完成了。
## 堆排序
1. 从数组中随机选择一个数作为基准元素
2. 小于基准元素的放在基准的左边，大于基准元素的放在基准元素的右边
3. 在基准元素的左边和右边分别重复1，2过程，这样数组就会不停的进行分割，直到不能再分也就是排序完成了
## 计数排序
1. 找出数组中的最大值和最小值，创建一个Max-Min+1的辅助空间
2. 给辅助空间中的每个数值创建一个新的空数组
2. 将原数组中的数一个个放进辅助空间相对应的位置，相同的数字出现就在辅助空间相对应的数组上+1
3. 遍历辅助空间，去除大小为0的空数组，辅助空间里数组的大小则对应着原数组中数值出现的次数，这样排序就完成了









著名前端面试题：
一个页面从输入 URL 到页面加载显示完成，这个过程中都发生了什么？

这一题是在挖掘你的知识边界，所以你知道多少就要答多少。

可以先查阅一些资料再查，但是不要把自己不懂的东西放在答案里，面试官会追问的。

你的回答




1. 查找URL所对应的资源的位置
不同的URL对应着不同的资源，但是浏览器本身并不能识别我们的URL到底是什么，于是就用到了DNS解析
- DNS解析
DNS解析的过程就是将要请求的域名还原成ip地址
2. 找到了这个资源所对应的ip之后，浏览器就会将用户发起的http请求发送给服务器，发送http请求之前需要与对方建立连接
- TCP连接
通过TCP协议我们可以在两个主机之间建立可靠的连接服务。
TCP连接一般会通过三次握手来建立连接。第一次握手：主机说：服务器你收到了吗？第二次握手：服务器说：主机我收到了，你说吧。第三次握手：主机说：那我要给你东西了。
3. 浏览器向服务器发送HTTP请求
浏览器会按照请求的格式来发送HTTP请求，举个例子
```
POST /path HTTP/1.1
Host: www.baidu.com
User-Agent: curl/7.54.0
Accept: */*
Content-Length: 24
Content-Type: application/x-www-form-urlencoded

username=ff&password=123
``` 
4. 服务器开始处理HTTP请求，并且根据HTTP请求来给浏览器一个响应
不同的状态码代表着不同的意义。状态码200就表示响应成功
5. 浏览器根据不同的响应来做出不同的应对，响应成功就会开始获取服务器发过来的数据。
如果状态码为404 服务器找不到浏览器想要的网页。
6. 浏览器开始渲染页面，解析html代码，解析css,js文件
7. 渲染完成，连接结束




著名面试题：
如何实现数组去重？
假设有数组 array = [1,5,2,3,4,2,3,1,3,4]
你要写一个函数 unique，使得
unique(array) 的值为 [1,5,2,3,4]
也就是把重复的值都去掉，只保留不重复的值。

要求：

不要做多重循环，只能遍历一次
请给出两种方案，一种能在 ES 5 环境中运行，一种能在 ES 6 环境中运行（提示 ES 6 环境多了一个 Set 对象）




## 第一种： ES5
``` 
var array = [1,5,2,3,4,2,3,1,3,4]
function unique(arr){
    var newArr = []
    var hash = {}
    for(var i=0;i<arr.length;i++){
        if(!hash[arr[i]]){
            hash[arr[i]] = 1
            newArr.push(arr[i])
        }
    }
    return newArr
}
unique(array)
```
## 第二种： ES6
``` 
var array = [1,5,2,3,4,2,3,1,3,4]
function unique(arr){
      return Array.from(new Set(arr))
  }
unique(array)
``` 