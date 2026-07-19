## API

### 1. 作用和分类

作用：使用js去操作html和浏览器

分类：DOM（文档对象模型）、BOM（浏览器对象模型）

## DOM

定义：用来呈现以及与任意HTML或XML文档交互的API

作用:开发网页内容特性和实现用户交互

### 1. DOM树

定义：将HTML文档以树状结构直观的表现出来，描述网页内容关系的名词

作用：直观体现了标签与标签间的关系

### 2. DOM对象

定义：浏览器根据html标签生成的==js对象==

所有的标签属性都可以在这个对象上面找到，修改这个对象的属性会自动映射到标签身上

**核心思想**：把网页内容当作对象来处理

**document对象**
DOM里提供的一个对象。它提供的属性和方法都是用来访问和操作网页内容的，例如`document.write()` ，网页所有内容都在document里面

### 3. 获取DOM对象

查找元素DOM就是利用JS选择页面中标签元素

#### 3.1 根据CSS选择器来获取DOM元素

1. 选择匹配的第一个元素
   语法：

   ````js
   document.querySelctor(`CSS选择器`)
   ````

**该怎么获取ul下的第一个li呢？**

```js
const li = document.querySelctor('ul li:first-child')
```

参数：包含一个或多个有效的CSS选择器字符串

返回值：CSS选择器匹配的第一个元素，一个HTMLElement对象，如果没返回值，返回到null

2. 选择匹配的多个元素

语法：
```js
document。querySelectorAll('css选择器')
```

参数：包含一个或多个有效的CSS选择器字符串

返回值：CSS选择器匹配的NodeList 对象集合、

结果：是一个伪数组：有长度有索引好的数组，但是没有pop() push()等数组方法
想要得到里面的每一个对象，则需要遍历for的方式得到
==哪怕只有一个元素，用这种方式得到的也是伪数组==

**该怎么选择ul里的所有li呢？**

```js
const lis = document.querySelctorAll('ul li')
```

**获取多个DOM元素时，能直接修改吗？**
不能，因为获取的是数组，只能通过遍历的方式一次给里面的元素做修改

#### 3.2 其他获取DOM元素的方法

```js
document.getElementById('nav')//根据id获取一个元素
document.getElementsByTagName('div')
//根据标签获取一类元素，获取页面所有div
document.getElementsByClassName('w')
//根据类名获取元素，获取页面所有类名为w的
```

后两种获取的都是伪数组，前一个是单个元素

### 4. 操作元素内容

#### 4.1 元素.innerText 属性

将文本内容添加/更新到任意标签位置；显示纯文本，不解析标签——添加strong标签等，不会出现文字加粗的效果

语法： `box.innerText = 'this is a sentence' `

#### 4.2 元素.innerHTML属性

将文本内容添加/更新到任意标签位置，会解析标签，多标签建议使用模板字符

````html
<span>好的</span>
````

![image-20260513103856673](https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260513103856673.png)

```js
const p = document.querySelector('span')
p.innerHTML = '<strong>这是第一个</strong>'
```

![image-20260513103913253](https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260513103913253.png)

------

#### 年会抽奖案例

```html
<style>
        .wrapper {
            width: 840px;
            height: 420px;
            /*background:url() no-repeat center / cover;*/
            background-color: #c09393;
            padding: 100px 250px;
            box-sizing: border-box;
        }
    </style>
<div class="wrapper">
        <strong>年会抽奖</strong>
        <h1>一等奖：<span id="one">?</span></h1>
        <h2>二等奖：<span id="two">?</span></h2>
        <h4>三等奖：<span id="three">?</span></h4>
    </div>
    <script>
        //声明数组
        const personArr = ['在玹','道英','朝了个朝','辰乐','志晟',]
        //随机数（一等奖）
        const random = Math.floor(Math.random() * personArr.length)
        const one = document.querySelector('#one')
        one.innerHTML = personArr[random]
        //中奖之后删除这个人的名字
        personArr.splice(random,1)
        //二等奖
        const random2 = Math.floor(Math.random() * personArr.length)
        const two = document.querySelector('#two')
        two.innerHTML = personArr[random2]
        personArr.splice(random2,1)
        //三等奖
        const random3 = Math.floor(Math.random() * personArr.length)
        const three = document.querySelector('#three')
        three.innerHTML = personArr[random3]
        personArr.splice(random3,1)
    </script>
```



### 5. 操作元素属性

#### 5.1 操作元素常用属性

语法：对象.属性 = 值 

------

#### 页面刷新，图片随机更换案例

```html
//假定所有的图片命名都是i.webp，i为任意正整数
    <img src="./images/1.webp" alt="">
    <script>
        //获取 N~M的随机整数
        function getRandom(N,M) {
            return Math.floor(Math.random()* (M - N+1))+N
        }
        const img = document.querySelector('img')
        const random = getRandom(1,4) //随机得到序号
        img.src = `./images/${random}.webp`
    </script>
```

------

#### 5.2 操作元素样式属性

##### 5.2.1 通过style来修改

语法：对象.style .样式属性 = '值'  ==不要忘记加单位==
也可以通过这样的方式添加样式

```html
<div class="box"></div>
```

```css
.box {
    width: 300px;
    height: 400px;
    background-color: pink;
}
```



```js
const box = document.querySelector('.box')
box.style.width = '400px'
// 遇到CSS里面有短横线的多组单词，就用小驼峰命名法，不然获取不到
box.style.backgroundColor = 'green'
```

<img src="https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260513110314276.png" alt="image-20260513110314276" style="zoom:50%;" /><img src="https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260513110238435.png" alt="image-20260513110238435" style="zoom:50%;" />

##### 5.2.2 通过类名改变属性

适用于修改的样式比较多的情况

语法：`元素.className = '类名'` 

注意：

1. 由于class是关键字，所以使用className去代替
2. className是使用新值换旧值，如果需要添加一个类，需要保留之前的类名 
   eg:`div.className = 'nav box'` 原类名是nav

##### 5.2.3 通过classList 操作类控制CSS

使用场景：由于className容易覆盖之前的类名，所以通过classList方式追加和删除类名
语法：

```js
// 追加一个类
元素.classList.add('类名')
// 删除一个类
元素.classList.remove('类名')
// 切换一个类，如果是原有的类名就删掉，没有就加上
元素.classList.toggle('类名')
```

类名不加点，并且是字符串

------

#### 随机轮播图案例

```html
<script>
        const sliderData = [
        { url:'',title:'',color:''},
        { url:'',title:'',color:''},
        { url:'',title:'',color:''},
        { url:'',title:'',color:''},
        ]
        /* <function getRandom(N,M) {
            return Math.floor(Math.random()*(M-N+1))+N
        }
        const random = getRandom() --> */
        const random = parseInt(Math.random()*sliderData.length)
        //把对应的数据渲染给标签
        const img = document.querySelector('存放图片的盒子')
        img.src = sliderData[random].url//修改图片路径 = 对象.url
        //获取p
        const p = document.querySelector('存放p的盒子 p')
        p.innerHTML = sliderData[random].title
        //修改背景颜色
        const footer = document.querySelector('存放p的盒子')
        footer.style.backgroundColor = sliderData[random].color
        //处理小圆点的高亮
        const circle = document.querySelector(`ul的类名 li:nth-child(${random + 1})`)//因为random是从0开始的
        li.classList.add('active')//active是高亮的li的类名
        
    </script>
```



------

#### 5.3 操作表单元素属性

正常的有属性有取值的，跟其他的标签属性没有任何区别
获取：DOM对象.属性名
设置：DOM对象.属性名 = 新值
获取表单里面的值 ： `表单.value`
设置表单的值： `表单.value = '新值'`
修改表单的类型： eg： `表单.type = 'password' `

表单属性中添加就有效果，移除没有效果，一律用布尔值表示，如果为 true 代表添加了该属性，如果是flase代表移除了该属性，==只接受布尔值==
eg ： disabled checked selected

**怎么设置单选和禁用按钮功能呢？**

```js
const ipt = document.querySelector('input')
//这里input是前面设置的一个复选框
ipt.checked = true
//不提倡加上引号的写法，会有隐式转换

const button = document.querySecletor('button')
button.disabled = ture
```

#### 5.4 自定义属性

**标准属性**
标签天生自带的属性，比如class id title 等，可以直接使用点语法操作，比如disabled

**自定义属性**
data-自定义属性，在标签上一律以data-开头，在DOM对象上一律以dataset对象方式获取

```html
<div class="box" data-id="10">this is a box</div>
    <script>
        const box = document.querySelector('.box')
        console.log(box.dataset.id)
    </script>
```

![image-20260514142407356](https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260514142407356.png)

如果定义了多个自定义标签的话，单独的dataset会得到一个集合，可以用 `box.dataset.id ` 得到某一个具体的

### 6. 定时器——间歇函数

#### 6.1 开启定时器

`setInterval(函数名，间隔时间) `
`setInterval(function(){ console.log('一秒执行一次')},1000) `
**注意函数名不用加括号，加了括号的话就会直接调用函数，不会传给定时器**

作用：每隔一段时间调用这个函数
间隔时间单位是毫秒

**定时器返回的是一个id数字**

#### 6.2 关闭定时器

```js
let 变量名 = setInterval(函数，间隔时间)
clearInterval(变量名)
```

一般不会刚创建就停止，而是满足一定条件再停止

------

#### **阅读注册协议（按钮60s之后才可以使用）**

button 按钮特殊，获取内容需要用innerHTML
```html
 <textarea name="" id="" cols="30" rows="30">
    用户注册协议
     ……
    </textarea>
    <br>
    <button class="btn" disabled>我已经阅读用户协议(60)</button>
    <script>
        //获取元素
        const btn = document.querySelector('.btn')
        //倒计时
        let i = 60
        let n = setInterval(function(){
            i--
            btn.innerHTML = `我已经阅读用户协议(${i})`
            if(i === 0) {
                //关闭定时器
                clearInterval(n)
                btn.disabled = false
                btn.innerHTML = '同意'
            }
        },1000)
    </script>
```

------

#### 轮播图定时版

```html
<script>
        const sliderData = [
        { url:'',title:'',color:''},
        { url:'',title:'',color:''},
        { url:'',title:'',color:''},
        { url:'',title:'',color:''},
        ]
        const img = document.querySelector('存放图片的盒子 img')
        const p = document.querySelector('存放p的盒子 p')
        let i = 0
        //开启定时器(1s切换一次)
        setInterval(function(){
            i++
            //无缝衔接位置
            if (i >= sliderData.length) { 
                i = 0
            }
            img.src = sliderData[i].url
            p.innerHTML = sliderData[i].title
            //小圆点也要切换，只让当前li高亮——删除以前的active
            document.querySelector('ul的类名 .active').classList.remove('active')
            document.querySelector(`ul的类名 li:nth-child(${i+1})`).classList.add('active')

        },1000)
        
    </script>
```



### 7. 事件监听

#### 7.1 事件监听

**什么是事件？**
定义：在编程时系统内发生的动作或者发生的事情，比如说用户单击一个按钮

**什么是事件监听**
让程序检测是否有事件发生，一旦有事件触发，就立即调用一个函数做出响应，也成为绑定/注册事件，比如点击可以播放轮播图等

语法：

`元素对象.addEventListener('事件类型',要执行的函数)`

事件监听三要素：

+ 事件源：哪个元素？要获取被事件触发的dom元素
+ 事件类型：用什么方式触发？eg:click(单击)、mouseover(鼠标经过)
+ 事件调用的函数：要做什么事？

**函数不会一写出来就执行，要等事件触发了才可以**

```html
<button class="btn">this is a button</button>
    <script>
        const btn = document.querySelector('.btn')
        //修改样式
        btn.addEventListener('click',function(){
            alert('已点击')
        })
    </script>
```

注意：事件类型要加引号，每次事件触发就会执行函数
**案例**

```html
<button>点击</button>
    <script>
        //需求：点击按钮之后弹出对话框
        //事件源——按钮   事件类型——点击鼠标   事件处理程序——弹出对话框  
        const btn = document.querySelector('button')
        btn.addEventListener('click',function(){
            alert('hello~')
        }) 
    </script>
```

#### 7.2 事件监听版本

+ DOM L0  事件源.on事件 = function(){ }
+ DOM L2  事件源.addEventListener(事件，事件处理函数)
+ 区别： on方式会被覆盖，后者方式可绑定多次，拥有事件更多特性——相当于写了两个对话框，前者只能弹出一次，后者可以弹出两次

#### 7.3 事件类型

1. 鼠标类型——鼠标触发
   click 鼠标点击   
   mouseenter 鼠标经过  
   mouseleave  鼠标离开

2. 焦点事件——表单获得光标  **用于表单**
   focus 获得焦点  
   blur 失去焦点

3. 键盘事件——键盘触发
   keydown  键盘按下触发
   keyup  键盘抬起触发

4. 文本事件——表单输入触发
   input 用户输入事件

   ```js
   input.addEventListener('input',function(){
       console.log(input.value)
   })
   ```

**如果有多个文本框，怎么获取呢？**

`<input type="search" placeholder=" ">`

`const input = document.querySelcetor('[type = search]')`

**怎么让文本框获得焦点的时候，文本框颜色发生变化呢？**
CSS中写一个目标颜色的类型的代码，获得焦点的时候就添加这个类名，失去焦点的时候就移除这个类名

**怎么获得焦点的时候CSS样式直接发生改变呢？**
用focus伪类选择器

```css
input {
    width:200px;
    transition:all 0.3s;
}
input:focus {
    width:300px;
}
```

**怎么获得用户输入的长度？**

```js
total.innerHTML = `${tx.value.length}/xx字`
```

#### 7.4 事件对象

定义：也是对象，这个对象里有事件触发时的相关信息

使用场景：判断用户按下哪个键，比如说按下回车键发布；可以判断鼠标点击了哪个元素，从而做出相应的操作

**怎么获取？**
在事件绑定的回调函数的第一个参数就是事件对象，一般命名为event、ev、e

```js
元素.addEventListener('click',function(e){
            
        })
```

**常见事件对象属性**

+ type
  获取当前的事件类型
+ clientX/clientY
  获取光标相对于浏览器可见窗口左上角的位置
+ offsetX/offsetY
  获取光标相对于当前DOM元素左上角的位置
+ key
  用户按下的键盘键的值 ==现在不提倡使用keyCode==

**怎么控制只有按了某个键才能触发呢？**

```js
if (e.key === 'Enter'){
    console.log('')
}
```

**怎么处理字符串多余的左右侧空格?**

```js
const str = ''
str.trim()
```

==`tx.value.trim() !== ' ' 等价于 ' '`==

#### 7.5 环境对象

定义：指的是函数内部特殊的变量this，它代表着当前函数运行时所处的环境

每个函数里面都会有this，普通函数里面this指向的是window，谁调用的函数就指向谁

适用的环境：五个对象，有相同的触发条件时，他们的样式发生相同的变化，就可以用this来弄

#### 7.6 回调函数

定义：如果将函数A作为参数传递给函数B时，我们称函数A为回调函数

```js
function fn(){

        }
        setInterval(fn,1000)
```

### 随机点名案例

![image-20260517153936236](https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260517153936236.png)

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <style>
    *{
      margin:0;
      padding: 0;
    }
    h2{
      text-align: center;
    }
    .box {
      width: 600px;
      margin: 50px auto;
      display: flex;
      font-size: 25px;
      line-height: 40px;
    }
    .qs {
      width: 450px;
      height: 40px;
      color: red;
    }
    .btns {
      text-align: center;
    }
    .btns button {
      width: 130px;
      height: 35px;
      margin: 0 50px;
    }
  </style>
</head>
<body>
  <h2>随机点名</h2>
  <div class="box">
    <span>字母是：</span>
    <div class="qs">这里是姓名</div>
  </div>
  <div class="btns">
    <button class="start"></button>
    <button class="end"></button>
  </div>
  <script>
    //准备数组
    const arr = [' ',' ']
    let timeID = 0
    const random
    //开始按钮
    const qs = document.querySelector('.qs')
    const start = document.querySelector('.start')
    start.addEventListener('click',function(){
     timeID = setInterval(function(){
      random = parseInt(Math.random()*arr.length)
      qs.innerHTML = arr[random]
    },1000)
      })
      if(arr.length === 1){
        start.disabled = true
        end.disabled = true
      }
    const end = document.querySelector('.end')
    end.addEventListener('click',function) {
      clearInterval(timeID)
      arr.splice(arr[random],1)
    }
  </script>
</body>
</html>
```



### tab切换案例

需求：鼠标经过不同的选项卡，底部可以显示不同的内容

**原理**
能显示的盒子写一个active

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <style>
    //这样写类名
    .tab-content .item {
      display: none;
    }
    .tab-content .item.active {
      display: block;
    }
  </style>
</head>
<body>
  <div class="tab">
    <div class="tab-nav">
      <ul>
        //小圆点的做法
        <li><a class="active" href="javascript:;"></a></li>
        <li><a href="javascript:;"></a></li>
        <li><a href="javascript:;"></a></li>
        <li><a href="javascript:;"></a></li>
        <li><a href="javascript:;"></a></li>
      </ul>
    </div>
    <div class="tab-content">
      <div class="item acitve"><img src="" alt=""></div>
      <div class="item"><img src="" alt=""></div>
      <div class="item"><img src="" alt=""></div>
      <div class="item"><img src="" alt=""></div>
      <div class="item"><img src="" alt=""></div>
    </div>
  </div>
  <script>
    // a模块制作——给5个链接绑定鼠标经过事件
    const as = document.querySelectorAll('.tab-nav a')
    for(let i = 0;i<as.length;i++){
      as[i].addEventListener('mouseenter',function(){
        //移除上一个，添加下一个
        document.querySelector('.tab-nav .active').classList.remove('active')
        //当前这个就是this
        this.classList.add('active')
      })
    }
    //5个盒子对应item
    document.querySelector('.tab-content .active').classList.remove('active')
    document,querySelector(`.tab-content .item:nth-child(${i+1})`).classList.add('active')
  </script>
</body>
</html>
```



### 表单反选案例

需求：点击全选，下面的复选框全部选择，取消全选则全部取消
![image-20260517151800041](https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260517151800041.png)

![image-20260517153315897](https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260517153315897.png)

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <style>
    /*选择被勾选的复选框*/
    .ck:checked {

    }
  </style>
</head>
<body>
  <table>
    <tr>
      <th class="allcheck">
        <input type="checkbox" name="" id="checkALL"> <span class="all">全选</span>
      </th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
    <tr>
      <td>
        <input type="checkbox" name="check" class="ck">
      </td>
      <td>
        <input type="checkbox" name="check" class="ck">
      </td>
      <td>
        <input type="checkbox" name="check" class="ck">
      </td>
      <td>
        <input type="checkbox" name="check" class="ck">
      </td>
    </tr>
  </table>
  <script>
    const checkall = document.querySelector("#checkAll")
    const cks = document.querySelectorAll('.ck')
    checkall.addEventListener('click',function(){
      //得到的全选的checked是true或者false状态
      //遍历所有小复选框
      for (let i = 0;i<cks.length;i++){
        cks[i].checked = this.checked
      }
    })
    //小复选框控制大复选框
    for(let i = 0;i<cks.length;i++) {
      cks[i].addEventListener('click',function(){
        checkALL.checked = document.querySelectorAll('.ck:checked').length === cks.length//后面得到的是true或false
      })
    }
  </script>
</body>
</html>
```



### 8. 事件流

#### 8.1 事件流和两个阶段说明

定义：时间完整执行过程中的流动路径

当触发事件时，会经历两个阶段——捕获阶段、冒泡阶段

捕获阶段——从父到子  冒泡阶段——从子到父  一般都是使用事件冒泡为主

#### 8.2 事件捕获

概念：从DOM的根元素开始执行对应的事件（从外到里）
事件捕获需要写对应代码才能看到效果

代码：
`DOM.addEventListener(事件类型,事件处理函数,是否使用捕获机制)`

说明：
第三个参数传入true代表的是捕获阶段触发（很少用）；若传入false代表冒泡阶段触发，默认就是false；若是用L0事件监听，则只有冒泡阶段，没有捕获

#### 8.3 事件冒泡

概念：当一个元素的事件被触发时，同样的事件将会在该元素的所有祖先元素中依次被触发——依次向上调用所有父级元素的同名事件
事件冒泡是默认存在的
L2事件监听第三个参数是false，或者默认都是冒泡

#### 8.4 阻止冒泡

适用需求：想把事件就限制在当前元素内，阻止事件冒泡需要拿到事件对象

语法：`事件对象.stopPropagation( )`

**此方法可以阻断事件流动传播，在冒泡/捕获阶段都有效**

#### 8.5 解绑事件

**on事件方式**
直接使用null覆盖偶就可以实现事件的解绑

```js
btn.onclick = function() {
    
}//绑定事件
btn.onclick = null //解绑事件
```

**addEventListener方式**
`removeEventListener(事件类型，事件处理函数，[获取捕获或者冒泡阶段])`

注意：匿名函数无法解绑

#### 鼠标经过事件的区别

鼠标经过事件：

+ mouseover 和mouseout 会有冒泡效果
+ mouseenter 和 mouseleave 没有冒泡效果（推荐）

#### 两种注册事件的区别

+ 传统on注册（L0）
  + 同一个对象，后面注册的事件会覆盖前面注册（同一个事件）
  + 直接使用null覆盖偶就可以实现事件的解绑
  + 都是冒泡阶段执行的
+ 事件监听注册（L2）
  + 语法：`addEventLisener(事件类型,事件处理函数,是否使用捕获) `
  + 后面注册的事件不会覆盖前面注册的事件（同一个事件）
  + 可以通过第三个参数确定是在冒泡还是捕获阶段执行
  + 必须使用removeEventListener(事件类型，事件处理函数，获取捕获或者冒泡阶段)
  + 匿名函数无法被解绑

### 9. 事件委托

适用于同时给多个元素注册事件，相比于for循环注册实践，这个只需要注册一次就能实现效果
原理:利用事件冒泡的特点

+ 给父元素注册事件，当我们触发子元素的时候，会冒泡给父元素身上，从而触发父元素的事件

**怎么精准地弄到事件触发的对象呢？**
`e.targret` ——但是也不太好，如果ul里面既有li又有p 的话，无法精准到li
`事件对象.target.tagName` 可以获得真正触发事件的元素 ——用if来判断

#### 9.1 阻止事件默认行为

例如阻止链接的跳转，表单域跳转

语法：`e.preventDefault() `

### 10. 其他事件

#### 10.1 页面加载事件

加载外部资源（如图片、外联CSS和JS等）加载完毕时触发的事件

事件名：load

监听页面所有资源加载完毕：给window 添加 load 事件

```js
window.addEventListener('load',function(){
    //执行的操作
})
```

针对某个特定的资源，就把window替代成该资源就行

当初始的HTML文档被完全加载和解析完成之后，DOMContentLoaded 事件被触发，无需等待样式表、图像等完全加载

事件名：DOMContentLoaded

监听页面DOM加载完毕：给document添加DOMContentLoaded事件

`document.addEventListener('DOMContentLoaded',function(){}) `

#### 10.2 页面滚动事件

滚动条在滚动的时候持续触发的事件，比如说回到顶部

事件名： scroll

监听整个页面滚动：
`window.addEventListener('scroll',function( ){ })`
给window或document添加都可以

适用场景：检测滚动的意义

##### 获取位置

**scrollLeft 和scrollTop 属性**
获取被卷去的大小，获取元素内容向左、向上滚出去看不到的距离，这两个值是可读写的 

![image-20260516134350551](https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260516134350551.png)

获取html元素写法
`document.documentElement.scroll
``document.documentElement.scrollTop`

```js
const n = document.documentElement.scrollTop
        if(n >=100) {
            div.style.display = 'block'
        }
        else {
            div.style.display = 'none'
        }
```

**尽量在scroll事件里面获取被卷去的距离，得到的值是数字型的，不带单位**

#### 10.3 页面尺寸事件

在窗口尺寸改变的时候触发事件：resize
`window.addEventListener('resize',function( ){ } )`
检测屏幕宽度：

`document.documentElement.clientWidth`

##### 获取宽高

获取元素的可见部分宽高（不包含边框，margin，滚动条等）

clientWidth 和clientHeight

### 11. 页面尺寸与位置

适用场景：元素滚到到某个位置，自动实现效果

**获取宽高**：
获取元素自身的宽高、包含元素自身设置的宽高、padding、border
offsetWidth 和 offsetHeight
获取的是数值，方便计算
获取的是可视宽高，如果盒子是隐藏的，获取的结果是0

**获取位置**

获取元素距离自己==定位父级元素==的左、上距离

offsetLeft 和offsetTop 注意是只读属性
检测盒子的位置，距离最近的祖先元素

### 12.日期对象

定义：表示时间的对象
作用：可以得到当前系统的时间

#### 12.1 实例化

定义：在代码中发现了new关键字的操作

创建一个事件对象并获取时间
获取当前时间 `const date = new Date( ) `
获取指定时间 `const date = new Date('2026-6-24 8:30:00')

#### 12.2 日期对象方法

<img src="https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260516141020604.png" alt="image-20260516141020604" style="zoom:67%;" />

月份要记得加1

**怎么补0？**
` h = h < 10 ? '0' + h : h`

#### 12.4 时间戳

使用场景：计算倒计时效果，单位是毫秒数

算法：

+ 将来的时间戳 - 现在的时间戳 = 剩余时间毫秒数
+ 剩余时间毫秒数 转换为 剩余时间的 年月日时分秒就是倒计时时间

**获取时间戳的方法**

1. 使用getTime( )方法
   ```js
   const date = new Date()
   console.log(date.getTime())
   ```

2. 简写 +new Date( )

`console.log(+new Date())`

3. Date.now() 方法

`console.log(Date.now())`

后面两个无需时间戳，前面两个可以返回指定日期的时间戳

### 13. 节点操作

#### 13.1 DOM节点

定义：DOM树里每一个内容

节点类型：

+ 元素节点：所有的标签，html是根节点
+ 属性节点：所有的属性
+ 文本节点：所有的文本
+ 其他

#### 13.2 查找节点

**父节点查找**

parentNode属性，返回最近一级的父节点，找不到返回为null

`子元素.parentNode` 多弄几个就可以回到更前面的父节点

**子节点查找**
childNodes：获得所有子节点、包括文本节点（空格、换行）、注释节点等

children属性：仅获得所有元素节点，返回的还是一个伪数组 `父元素.children`

**兄弟关系查找**

下一个兄弟节点：nextElementSibling 属性

上一个兄弟节点：previousElementSibling 属性

#### 13.3 增加节点

##### 1. 创建节点

创造出一个新的网页元素，然后再添加到网页内，一般先创建节点，然后再插入节点

创建方法： `document.createElement('标签名') `

##### 2. 追加节点

需要插入到某个父元素才可以在页面上看到

插入到父元素的最后一个子元素：`父元素.appendChild(要插入的元素) `

插入到父元素中某个子元素的前面 `父元素.insertBefore(要插入的元素，在哪个元素前面) `

特殊情况下：复制一个原有的节点，把复制的节点放入到指定的元素内部

**克隆节点**
`元素.cloneNode(布尔值) `

cloneNode 会克隆出一个跟原标签一样的元素，括号内传入布尔值
若为true，则代表会包含后代节点一起克隆；若为false，则代表克隆时不包含后代节点，默认为false

#### 13.4 删除节点

删除元素，必须通过父元素删除（如果不存在父子关系则删除不成功）
语法 ：`父元素.removeChild(要删除的元素) `

删除节点和隐藏节点（display：none）的区别：
隐藏节点还是存在，删除节点就不存在了

### 14.M端事件

![image-20260516151550299](https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260516151550299.png)

### 15.swiper插件

多个swiper使用的时候，给每个轮播容器设置不同的类名，然后分别初始化，避免配置冲突

## Window对象

### 1. BOM

定义：浏览器duixiangmox

window对象是一个全局对象，是js中的顶级对象，像document等和基本BOM的属性和方法都是window的。所有通过var定义在全局作用域中的变量、函数都会变成window对象的属性和方法。window对象下的属性和方法调用的时候可以省略window

### 2.定时器——延时函数

语法：`setTimeout(回调函数,等待的毫秒数)`
==仅执行一次==

清除：

```js
let timer = setTimeout(回调函数,等待的毫秒数)
clearTimeout(timer)
```

延时器需要等待，所以后面的代码先执行，每一次调用延时器都会产生一个新的延时器

### 3. JS执行机制

Js是单线程，一个任务结束之后才会执行后一个任务

**同步**

程序的执行顺序和任务的 排列顺序是一致的、同步的

同步任务都在主线程上执行，形成一个执行栈

**异步**

可以在一个程序执行中，执行其他任务，通过回调函数实现

![image-20260516153211771](https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260516153211771.png)

1. 先执行执行栈中的同步任务
2. 异步任务放入任务队列中
3. 一旦执行栈中的所有同步任务执行完毕，系统就会按次序读取任务队列中的异步任务，被读取的异步任务结束等待状态，进入执行栈，开始执行

![image-20260516153402961](https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260516153402961.png)

事件循环：主线程不断地重复获得、执行、再获得、再执行任务的机制

### 4. location对象

数据类型是对象，拆分并保存了url地址的各个组成部分
作用：操作当前页面url

| 方法/属性         | 作用                                  | 示例                                    |
| ----------------- | ------------------------------------- | --------------------------------------- |
| location.href     | 获取 / 修改完整 URL（跳转页面）       | location.href = 'https://www.baidu.com' |
| location.search   | 获取 URL 中的查询参数（`?key=value`） | console.log(location.search             |
| location.reload() | 刷新页面                              | location.reload()                       |
| location.hash()   | 获取url中的哈希值                     | location.hash = '#section1'             |

### 4. navigator对象

作用：获取浏览器/设备信息，用于panduanhuanj

属性：

`navigator.userAgent` 用户代理字符串，包含浏览器、系统信息

`navigator.platform` 获取操作系统平台

### 5. history 对象

作用：操作浏览器的历史记录栈

| 方法               | 作用                                     |
| ------------------ | ---------------------------------------- |
| history.back()     | 相当于后退按钮                           |
| history.forward（) | 相当于前进按钮                           |
| history.go(n)      | 跳转到指定历史记录。-1后退，1前进，0刷新 |

## 本地存储

作用：将数据永久存储在用户的电脑，除非手动删除，否则关闭页面也会存在

特性：可以多窗口共享，同一浏览器可以共享；以键值对的形式存储使用

```js
// 1. 存储数据
localStorage.setItem('key', 'value');
// 2. 获取数据
localStorage.getItem('key');
// 3. 删除单个数据
localStorage.removeItem('key');
// 4. 清空所有数据
localStorage.clear();
```

**只能存字符串，如果要存对象/数组，需要转成json字符串**

```js
// 存储对象
const user = { name: '小明', age: 18 };
localStorage.setItem('user', JSON.stringify(user));

// 读取对象
const userData = JSON.parse(localStorage.getItem('user'));

```

## map方法和join方法

### 1. map方法

使用场景：遍历数组处理数据，并且返回新的数组

有返回值,map又称映射，一 一对应

```js
const arr = ['red','blue','green']
const newArr = arr.map(function(ele,index){
                       return 
                       })
```

### 2. join方法

把数组转换成字符串

`newArr.join()` 下括号为空则逗号分割，下括号是空字符串，则元素之间没有分隔符

## 正则表达式

定义：用于匹配字符串中字符组合的模式，在js中，正则表达式也是对象

通常用来查找、替换那些符合正则表达式的文本
使用场景： 验证表单（用户只能输入英文字母等） 过滤掉页面内容的一些敏感词，或从字符串中获取我们想要的特定部分

### 1. 语法

#### 1.1 定义

`const 变量名 = /表达式/`

/ / 是正则表达式字面量

#### 1.2 判断是否有符合规则的字符串

test( ) 方法——用来查看正则表达式与指定字符串是否匹配

语法：`regObj.test(被检测的字符串)`
如果正则表达式与指定字符串匹配，返回true，否则false

## 轮播图案例

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>轮播图</title>
  <style>
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }
    .slider {
      width: 600px;
      height: 400px;
      overflow: hidden;
      margin: 0 auto;
    }

    .slider-wrapper {
      width: 100%;
      height: 300px;
    }

    .slider-wrapper img {
      width: 100%;
      height: 100%;
      object-fit: cover;
      display: block;
    }

    .slider-footer {
      height: 80px;
      background-color: rgba(102, 204, 102, 1);
      padding: 10px 10px 0 10px;
      position: relative;
    }

    .slider-footer .toggle {
      position: absolute;
      right: 0;
      top: 10px;
      display: flex;
    }

    .slider-footer .toggle button {
      margin-right: 10px;
      width: 28px;
      height: 28px;
      appearance: none;
      border: none;
      background: rgba(255, 255, 255, 0.3);
      color: #726585;
      border-radius: 4px;
      cursor: pointer;
    }

    .slider-footer .toggle button:hover {
      background: rgba(255, 255, 255, 0.2);
    }

    .slider-footer p {
      margin: 0;
      color: #a39db6;
      font-size: 20px;
      margin-bottom: 10px;
    }

    .slider-indicator {
      margin: 0;
      padding: 0;
      list-style: none;
      display: flex;
      align-items: center;
    }

    .slider-indicator li {
      width: 8px;
      height: 8px;
      margin: 4px;
      border-radius: 50%;
      background: #a39db6;
      opacity: 0.2;
      cursor: pointer;
    }

    .slider-indicator li.active {
      width: 12px;
      height: 12px;
      opacity: 1;
    }
  </style>
</head>
<body>
  <div class="slider">
    <div class="slider-wrapper">
      <img src="../img/01.jpg" alt="">
    </div>
    <div class="slider-footer">
      <p>浮光跃金，静影成壁</p>
      <ul class="slider-indicator">
        <li class="active"></li>
        <li></li>
        <li></li>
      </ul>
      <div class="toggle">
        <button class="prev">&lt;</button>
        <button class="next">&gt;</button>
      </div>
    </div>
  </div>

  <script>
    //初始数据
    const data = [
      { url: '../img/01.jpg', title: '浮光跃金，静影成壁', color: 'rgba(102, 204, 102, 1)' },
      { url: '../img/02.jpg', title: '大地沉韵，温厚内敛', color: 'rgba(102, 51, 0, 1)' },
      { url: '../img/03.jpg', title: '静水流深，澄澈庄重', color: 'rgba(0, 51, 102, 1)' },
    ]
    // 获取元素
    const img = document.querySelector('.slider-wrapper img')
    const p = document.querySelector('.slider-footer p')
    const footer = document.querySelector('.slider-footer')
    //左右按钮业务
    const next = document.querySelector('.next')
    let i = 0 //控制播放图片张数
    next.addEventListener('click',function(){
        i++
        //判断要写在i++后面，先判断再执行
         if(i >= 3){
          i = 0
        }
        //渲染数据
        img.src = data[i].url
        p.innerHTML = data[i].title
        footer.style.backgroundColor = data[i].color
        //更换小圆点
        document.querySelector('.slider-indicator .active').classList.remove('active')
        document.querySelector(`.slider-indicator li:nth-child(${i + 1})`).classList.add('active')
    })
    const prev = document.querySelector('.prev')
    prev.addEventListener('click',function(){
        i--
        if(i < 0){
          i = 3
        }
        //渲染数据
        img.src = data[i].url
        p.innerHTML = data[i].title
        footer.style.backgroundColor = data[i].color
        //更换小圆点
        document.querySelector('.slider-indicator .active').classList.remove('active')
        document.querySelector(`.slider-indicator li:nth-child(${i + 1})`).classList.add('active')
    })
    //设置自动播放
    let timeID = setInterval(function(){
      next.click()//利用js里的自动调用点击事件，一定要加小括号调用函数
    },1000)
    //设置鼠标经过/离开的效果
    const slider = document.querySelector('.slider')
    slider.addEventListener('mouseenter',function(){
      clearInterval(timeID)
    })
    slider.addEventListener('mouseleave',function(){
      timeID = setInterval(function(){
      next.click()
    },1000)
    })
  </script>
</body>
</html>

```



### 
