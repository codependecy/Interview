第 1 题
填空

var object = {}
object.__proto__ ===  ????填空1????  // 为 true

var fn = function(){}
fn.__proto__ === ????填空2????  // 为 true
fn.__proto__.__proto__ === ????填空3???? // 为 true

var array = []
array.__proto__ === ????填空4???? // 为 true
array.__proto__.__proto__ === ????填空5???? // 为 true

Function.__proto__ === ????填空6???? // 为 true
Array.__proto__ === ????填空7???? // 为 true
Object.__proto__ === ????填空8???? // 为 true

true.__proto__ === ????填空9???? // 为 true

Function.prototype.__proto__ === ????填空10???? // 为 true
学生的回答
Object.prototype
Function.prototype
Object.prototype
Array.prototype
Object.prototype
Function.prototype
Function.prototype
Function.prototype
Boolean.prototype
Object.prototype
评分
评语
well done.~

参考答案
var object = {}
object.__proto__ ===  Object.prototype  // 为 true

var fn = function(){}
fn.__proto__ === Function.prototype  // 为 true
fn.__proto__.__proto__ === Object.prototype // 为 true

var array = []
array.__proto__ === Array.prototype // 为 true
array.__proto__.__proto__ === Object.prototype // 为 true

Function.__proto__ === Function.prototype // 为 true
Array.__proto__ === Function.prototype // 为 true
Object.__proto__ === Function.prototype // 为 true

true.__proto__ === Boolean.prototype // 为 true

Function.prototype.__proto__ === Object.prototype // 为 true
第 2 题
function fn(){
    console.log(this)
}
new fn()
new fn() 会执行 fn，并打印出 this，请问这个 this 有哪些属性？这个 this 的原型有哪些属性？

学生的回答
这个this没有属性，除了公共隐藏的 proto
因为是通过new关键字来创建的
new 操作为了记录我们的临时对象是由哪个函数构成的，所以给这个原型 加上了一个constructor属性
这个属性里面记录了一些关于我们这个函数的特征，比如说name什么的。

评分
评语
well done.~ 很不错

参考答案
this 自身没有属性（只有一个隐藏的 __proto__ 属性）
this 的原型是 fn.prototype，只有一个属性 constructor，且 constructor === fn（另外还有一个隐藏属性 __proto__，指向 Object.prototype）

第 3 题
JSON 和 JavaScript 是什么关系？
JSON 和 JavaScript 的区别有哪些？

学生的回答
json和JavaScript有什么关系
json是一门新的语言，json是抄袭JavaScript的

json和JavaScript的区别是什么
这是两门语言。并不相同
json带来了一个全新的数据格式，json有他自己的格式，其中有一种表现为键值对的方式，其中键必须加双引号 {"name": "he"}.
而JavaScript则是一门语言，其中JavaScript对象也可以通过键值对的形式表现出来，{"name": "he"}这就让人对这两种东西产生了误解。

评分
评语
well done.~

参考答案
关系：JSON 是一门抄袭/借鉴 JavaScript 的语言，同时也是一种数据交互格式，JSON 是 JavaScript 的子集（或者说 JSON 只抄袭了一部分 JavaScript 语法，而且没有新增任何原创的语法）

区别：JSON 不支持函数、undefined、变量、引用、单引号字符串、对象的key不支持单引号也不支持不加引号、没有内置的 Date、Math、RegExp 等。
而 JavaScript 全都支持。

第 4 题
前端 MVC 是什么？（10分）
请用代码大概说明 MVC 三个对象分别有哪些重要属性和方法。（10分）

学生的回答
前端MVC是什么
m代表 Model 操作数据
v代表 View 视图
c代表 controller 控制器
model数据和服务器交互，model可以将从服务器获取到的数据传给我们的controller，然后controller再把数据填充到view视图中，controller会一直监视view视图，如果用户操作了view，controller就会接收到信号，然后去调用我们的model，这样一层层下去。
简单点来说就是专门的人做专门的事，处理数据的就让他处理数据，展示数据的就让数据进行展示，结构化我们的代码，就像html开发中，css样式就放在css文件中，不要在html中随意的改动css样式，这样代码逻辑清晰，也为其他人看懂你的代码做了铺垫。

###

window.View = function(selector){
    return document.querySelector(selector)  //返回被操作的View视图
}
window.Model = function(){
    return {
        init: function(){}, //初始化数据
        fetch: function(){}, // 获取数据
        save: function(){} //保存数据
    }
}
//Controller会一直监视View视图，并且负责调用model，所以需要init。
//之后再去进行model的调用以及执行绑定的函数bindEvents
window.Controller = function(options){
    var init = options.init
    let object = {
        view: null,
        model: null,
        init: function(view,model){
            this.view = view
            this.model = model
            this.model.init()
            init.call(this,view,model)
            this.bindEvents(this)
        },
    }
    //遍历传入的参数，开始处理业务。
    for(let key in options){
        if(key !== 'init'){
            object[key] = options[key]
        }
    }
    return object
}
评分
评语
well done.~

参考答案
MVC 是什么
MVC 是一种设计模式（或者软件架构），把系统分为三层：Model数据、View视图和Controller控制器。
Model 数据管理，包括数据逻辑、数据请求、数据存储等功能。前端 Model 主要负责 AJAX 请求或者 LocalStorage 存储
View 负责用户界面，前端 View 主要负责 HTML 渲染。
Controller 负责处理 View 的事件，并更新 Model；也负责监听 Model 的变化，并更新 View，Controller 控制其他的所有流程。

代码说明

var model = {
    data: null,
    init(){}
    fetch(){}
    save(){}
    update(){}
    delete(){}
}
view = {
    init() {}
    template: '<h1>hi</h1'>
}
controller = {
    view: null,
    model: null,
    init(view, model){
        this.view = view
        this.model = model
        this.bindEvents()
    }
    render(){
        this.view.querySelector('name').innerText = this.model.data.name
    },
    bindEvents(){}
}
第 5 题
在 ES5 中如何用函数模拟一个类？（10分）

学生的回答
通过new关键字来模拟

function Human(hp,mp){
    this.hp = hp
    this.mp = mp
}
Human.prototype.name = function(){}
var human = new Human('he')
//Human这个构造函数创建的对象有着自身的hp以及mp属性，在其原型上则有着我们之后设置的name属性
评分
评语
well done.~

参考答案
ES 5 没有 class 关键字，所以只能使用函数来模拟类。

function Human(name){
    this.name = name
}
Human.prototype.run = function(){}

var person = new Human('frank')
上面代码就是一个最简单的类，Human 构造函数创建出来的对象自身有 name 属性，其原型上面有一个 run 属性。

第 6 题
用过 Promise 吗？举例说明。
如果要你创建一个返回 Promise 对象的函数，你会怎么写？举例说明。

学生的回答
用过，在Ajax中。
在使用Promise之后我们会先执行Ajax，而不会去在意结果，之后再根据结果的成功或者失败来执行resolve或者reject函数。



https://github.com/codependecy/JSONP/blob/master/ajaxpromise.html
function fn(){
    return new Promise(function(resolve,reject){
        setTimeout(function(){
            // 成功就调用resolve，失败就调用 reject
        },3000)
    })
}
评分
评语
well done.~ 作业完成的很赞

参考答案
用过 Promise，比如 jQuery 或者 axios 的 AJAX 功能，都返回的是 Promise 对象。

$.ajax({url:'/xxx', method:'get'}).then(success1, error1).then(success2, error2)
如果我自己创建 Promise 对象，我会这么写

function asyncMethod(){
    return new Promise(function (resolve, reject){
        setTimeout(function(){
            成功则调用 resolve
            失败则调用 reject
        },3000)
    })
}
