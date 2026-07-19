## 基础语法

### 1.  简介

定义：是一种运行在浏览器的编程语言，实现人机交互效果。

作用：

+ 网页特效（如轮播图等)——监听用户的一些行为让网页作出对应的反馈
+ 表单验证——针对表单数据的合法性进行判断
+ 数据交互——获取后台的数据，渲染到前端
+ 服务器编程（node.js）

组成：

+ ECMAScript：规定了js基础语法核心知识（比如：变量、分支语句、循环语句、对象等）
+ Web APIs
  + DOM 操作文档，比如对页面元素进行移动、大小、添加删除等操作
  + BOM 操作浏览器，比如页面弹窗、检测窗口宽度、存储数据到浏览器等

### 2. 书写位置

**1. 内部JS**
直接写在html文件里，用 <script> 标签包裹住，写在 </body> 上面
原因：页面从上往下加载，防止html文件加载失败

拓展： alert('hello,js')——页面弹出警告对话框

**2. 外部JS**
代码写在以 .js结尾的文件里

语法：通过 <script> 标签，引入到html页面中

```html
<script src="./work.js"></script>
```

外部引入是 <script> 标签内写的代码会被忽略

**3. 内联JS**

代码写在标签内部
```html
 <button onclick="alert('this is a word')"></button>
```

### 3. 注释和结束符

#### 3.1 注释

+ 单行注释
  + 符号：//
  + 作用：//右边这一行的代码会被忽略
  + 快捷键 ：Ctrl+/
+ 块注释
  + 符号：/* */
  + 作用：在/* 和*/之间的所有内容都会被忽略
  + 快捷键： shift +alt +a

#### 3.2 结束符

+ 作用：使用英文的;代表语句结束、
+ 可写可不写，浏览器可以自动推断语句的结束位置

### 4. 输入与输出语法

#### 4.1 输出语法

```javascript
document.write('你需要输出的内容')
```

**作用**  向body内输出内容

**注意** 如果输出内容写的是标签，也会被解析成网页元素

```js
alert('你需要输出的内容')
```

**作用**：页面弹出警告框

```js
console.log('控制台')
```

**作用** ：控制台输出语法，程序员调试使用

![image-20260506204743625](https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260506204743625.png)

#### 4.2 输入语法

```js
prompt('输入的内容')
```

**作用**：显示一个对话框，对话框中包含一条文字信息，用来提示用户输入文字

![image-20260506204848913](https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260506204848913.png)

==prompt和alert会优先执行于其他的输入或输出，会跳过页面渲染先被执行==

### 5. 字面量

定义：在计算机中描述事/物 

分类：数字字面量，字符串字面量，数组字面量。对象字面量等

### 6.变量

定义：计算机中用来存储数据的“容器”

#### 6.1 变量的基本使用

**声明变量**

语法：

```js
let age
```

组成：变量关键字、变量名（标识）

**赋值变量**

```js
age = 17
```

```js
let age = 17
```

==字符串、汉字必须带引号==

**更新变量**

let不允许多次声明一个变量，更新变量直接重新赋值即可

**声明多个变量**

不同变量之间用逗号隔开即可

```js
let age = 17,name = '朝了个朝'
console.log(age,name)
```

为了更好的可读性，一行只声明一个变量

#### 6.2 变量的本质

内存：计算机中存储数据的地方，相当于一个空间

变量本质：程序在内存中申请的一块用来存放数据的小空间

#### 6.3 变量命名规则与规范

**规则**

+ 不能用关键字
  + 关键字：含有特殊含义的字符（js内置的一些英语词汇） 例如：let,var,if,for
+ 只能用下划线、字母、数字、$组成，且数字不能开头
+ 字母严格区分大小写

**规范**

+ 起名要有意义
+ 遵守小驼峰命名法：第一个单词首字母小写，后面每个单词首字母大写（userName）

#### let和var的区别

**var声明**（已经不再使用）

可以先使用再声明，可以重复声明，比如变量提升、全局变量、设有块级作用域等等

#### 6.4. 数组

**声明数组**

作用：将一组数据存储在单个变量名下

```js
let 数组名 = [数据1,数据2,...,数据n]
let number = [10,20,30]
```

数组是按顺序保存，如果要单独输出某一个值，直接加上索引号即可

**取值语法**

```js
数组名[下标]
let number = [10,20,30]
number[0]
```

**获取数组的长度（元素的个数）**

```js
let number = [10,20,30]
number[0]
let count = number.length
```

### 7.常量

概念：使用const声明的变量称为“常量”

使用场景：某个变量永远不会改变时

命名规范：和变量一致

**不允许重新赋值，声明的时候必须赋值（初始化）**

```js
const = F
```

### 8. 数据类型

#### 1. 数字类型(Number)

js是弱数据类型，变量类型只有等赋值之后才能确认

算术运算符的主要类型与C语言一样

```js
console.log(1 + 1)
```

![image-20260507125936117](https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260507125936117.png)

优先级：相同时，按照从左到右执行

+ 乘、除、取余优先级相同，大于加减
+ 加、减优先级相同
+ 使用括号可提升优先级

**补充**

NaN(Not a Number)代表一个计算错误，是一个不正确的或者一个未定义的数学操作所得到的结果，是粘性的，任何对NaN的操作都会返回NaN

#### 2. 字符串类型

用单引号、双引号、反引号包裹的数据都是字符串类型，单双引号没有特别的区别。
引号中间没有数据——空字符串

**注意**

1. 无论是单引号还是双引号必须成对使用
2. 单引号/双引号可以相互嵌套，但不能自己嵌套自己
3. 必要时可以使用转义符\，输出单引号或双引号

**字符串拼接**

使用：+ 运算符

```js
let name = 'Mike'
let age = '17'
document.write(name + age)
```

![image-20260507131739173](https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260507131739173.png)

也可以写成

```js
let name = 'Mike'
let age = 17
document.write(name+age)
document.write(name + '今年' + age + '岁了')
```

**模板字符串**

使用场景：拼接字符串和变量

语法
![image-20260507133826690](https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260507133826690.png)

```js
let age = 18
document.write(`我今年${age}岁了`)
```

![image-20260507134023799](https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260507134023799.png)

#### 3. 布尔类型

表示肯定或否定时在计算机中对应的是布尔类型数据。有两个固定的值true和false。

#### 4. 未定义类型

未定义只有一个值underfined

**什么情况出现未定义类型**

只==声明变量，不赋值==的情况下，变量的默认值为undefined,一般很少==直接==为某个变量为undefined
如果一个变量是需要我们等待传送过来的数据，可以通过检测这个变量是不是undefined，就判断用户是否有数据传递过来

```js
let age
document.write(age)
```

![image-20260507135153842](https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260507135153842.png)

#### 5. null(空类型)

js中的null仅是一个代表“无”、“空”或“值未知”的特殊值

**null和undefined区别**

+ undefined 表示没有赋值
+ null表示赋值了，但是内容为空

```js
let number = null
console.log(number)
```

![image-20260507135640964](https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260507135640964.png)

**null在开发中的使用场景**

如果变量里面存放的是一个对象，但对象还没创建好，可以给个null，可以将null作为尚未创建的对象

```js
console.log(undefined + 1)
console.log(null + 1)
```

#### ![image-20260507135943799](https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260507135943799.png)

#### 控制台输出语句和检测数据类型

**控制台输出语句**

根据颜色判断数据类型

**通过typeof 关键字检测数据类型**

typeof 运算符可以返回被检测的数据类型。支持两种语法形式（结果都是一样的）：

1. 作为运算符： typeof x (常用的写法)
2. 函数形式： typeof(x)

```js
let count = 18
document.write(typeof count)
```

![image-20260507140528429](https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260507140528429.png)

### 9. 类型转换

原因：使用表单、prompt获取的数据默认是字符串类型的，此时不能直接进行简单的加法运算

#### 9.1 隐式转换

定义：某些运算符被执行时，系统内部自动将数据类型进行转换

规则：

1. +号两边只要有一个是字符串，都会把另外一个换成字符串

2. 除了+以外的算术运算符，比如 - * / 等都会把数据换成数字类型

**转换类型不明确，需要依靠经验**

技巧：

+ +号作为正号解析可以转换成数字型
+ 任何数据和字符串相加结果都是字符串

#### 9.2 显式转换

概念：自己写代码告诉系统该转成什么类型

**转换为数字型**
Number(数据)

NaN也是number类型的数据，代表非数字；如果字符串内容里有非数字，转换失败时结果为NaN

parselnt（数据）——只保留整数

parseFloat（数据）——可以保留小数

```js
console.log(parseInt('6.24px'));
console.log(parseFloat('7.23555px'));
```

![image-20260507142626165](https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260507142626165.png)

### 10. 运算符

#### 10.1 赋值运算符

![image-20260507143049473](https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260507143049473.png)

#### 10.2 一元运算符

自增：
符号：++  作用：让变量的值+1

自减：

符号：-- 作用：让变量的值-1

**前置自增和后置自增的区别**

单独使用没有区别，参与运算就有区别
前置自增：先自加再使用
后置自增：先使用再自加

#### 10.3 比较运算符

![image-20260507144645985](https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260507144645985.png)

比较结果为==布尔类型==，即只会得到ture或false
===是全等 = 单等是赋值 ==是判断

比较运算符有隐式转换 把'2' 转换成2，所以2 == '2' 返回值是true

==NaN== 不等于任何数值，包括它自己

小数有精度问题，所以尽量不比较小数

不同类型的比较涉及隐式转换，把数据转换成number类型才能使用

字符串比较，是比较字符对应的ASCII码

**!=和!==的区别**

!=  非严格不等号：只比值，会自动类型转换

规则：会对两边做隐式类型转换，把它们换成同一类型，再比较转换后的值是否不同

!== 严格不相等运算符：既比值，也比类型

规则：先判断两边的数据类型是否相同，类型不同直接判定为true，类型相同再比较值是否不同

#### 10.4 逻辑运算符

使用场景：解决多重条件判断

| 符号 | 特点                   | 口诀     |
| ---- | ---------------------- | -------- |
| &&   | 两边都为真，结果才为真 | 一假则假 |
| \|\| | 两边有一个真，结果为真 | 一真为真 |
| ！   | 真变假，假变真         |          |

#### 10.5 运算符优先级

![image-20260507183247978](https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260507183247978.png)

### 11. 语句

**表达式和语句的区别**

表达式：可以被求值的代码，js引擎会将其计算出一个结果

语句：一段可以被执行的代码

表达式可被求值，所以可以写在赋值语句的==右侧==；语句不一定有值，比如for alert()等语句就不能被用于赋值

#### 1. 分支语句

选择性地执行想要的代码

**if语句**

分类：单分支、双分支、多分支

使用语法与C语言相同，如果小括号内的结果不是布尔类型的话，会发生隐式转换

==除了0，所有数字都为真；除了空字符串，所有字符串都为真==

#### 2. 三元运算符

符号：？和 : 配合使用

作用：一般用于取值

```js
条件 ？ 满足条件执行的代码 ： 不满足条件执行的代码
```

#### 3. switch分支语句

```js
switch(数据) {
    case 值1:
        代码1
        break
    case 值2:
        代码2
        break
    default :
        代码n
        break
}
```

找到跟小括号里数据==全等==的case值，并执行对应语句。如果没有全等，则执行default里的语句

一般用于等值判断，不适合用于区间判断，需要配合break使用，否则会穿透

适用于case为比较确定值的情况，分支比较多的时候，该语句执行效率高

#### 断点测试

作用：更好地理解代码运行，找到bug
![image-20260507185131897](https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260507185131897.png)

**设置断点后一定要刷新浏览器**

#### 3. 循环结构

while循环，语法与C语言相同

需要具备三要素：变量起始值**（单独写在外面）**，终止条件（没有终止条件，循环会一直执行，造成死循环），变量变化量（用自增或自减）

**退出循环**

break：退出循环

continue ：退出本次循环，进入下一次循环

```js
let i = 1
while(i <= 5) {
    if(i ===3) {
        continue
    }
    console.log(`这是第${i}次`)
    i++
}
// 这是个死循环，修改如下

let i = 1
while(i <= 5) {
    if(i ===3) {
        i++
        continue
    }
    console.log(`这是第${i}次`)
    i++
}
```

**for循环(适用于明确循环次数）**

```js
for (变量起始值；终止条件；变量变化量) {
    // 循环体
}
```

可以用于遍历数组，注意数组的索引从0开始

while(true) 用于构造“无限”循环，和for( ; ; )需要使用break退出循环

==循环嵌套==

和C语言的大体相同

换行显示—— `document.write('<br>')`

## 数组

定义：一种可以按照顺序保存任意类型的数据的数据类型

### 1.基本使用

#### 1.1 声明语法

1. 字面量声明数组

```js
let 数组名 = [数据1,数据2,...,数据n]
```

2. 使用 new Array 构造函数声明

```js
let arr = new Array(1,2,3,4)
```

#### 1.2 取值语法

```js
数组名[下标]
```

取出来是什么类型的，就根据这种类型特点来访问

**相关术语**

元素：数组中保存的每个数据都叫数组元素

下标：数组中数据的编号

长度：数组中数据的个数，通过数组的length属性获取

#### 1.3 遍历数组

一般使用for循环

```js
for (let i = 0;i < 数组名.length;i++) {
    数组名[i]
}
```

### 2. 求数组的最大值和最小值

![image-20260508144045668](https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260508144045668.png)

### 3. 数组操作

#### 3.1 修改

直接对相应的元素进行修改，或者直接添加数据即可，类似于 `arr[i] = arr[i] + '老师' `

#### 3.2 新增

1. **数组.push()** 方法——将一个或多个元素添加到数组的**末尾**，==并返回该数组的新长度==

```js
arr.push(元素1,元素2,...,元素n)
```

```js
let arr = ['red','green']
console.log(arr.push('pink'))
```

![image-20260508153519042](https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260508153519042.png)

```js
let arr = ['red','green']
arr.push('pink')
console.log(arr)
```

![image-20260508153614179](https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260508153614179.png)

2. **arr.unshift(新增的内容）**方法将一个或多个元素添加到数组的**开头**，并返回==该数组的新长度==

```js
arr.unshift(元素1,元素2,...,元素n)
```

```js
let arr = ['red','green']
arr.unshift('pink')
console.log(arr)
```

![image-20260508154203722](https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260508154203722.png)

**筛选数组时，一定要是遍历完后再筛选**

#### 3.3 删除

1. **数组.pop() 方法** 从数组中删除最后一个元素，并返回该元素的值

```js
arr.pop()
```

需求使用场景：随机抽奖

2. **数组.splice()方法** 删除指定元素

```js
arr.splice(start,deleteCount)
```

start——起始位置：指定修改的开始位置(从0计数)

deleteCount——表示要移除的数组元素的个数。可选的，如果省略则默认从指定的起始位置删除到最后）

```js
let arr = ['red','green','pink']
arr.splice(1,1)
console.log(arr)
```

![image-20260508161914065](https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260508161914065.png)

```js
let arr = ['red','green','pink']
arr.splice(1)
console.log(arr)
```

![image-20260508161957611](https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260508161957611.png)

## 冒泡排序

![image-20260508162207310](https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260508162207310.png)

可以像C语言一样双重循环排序，也可以用 `arr.sort()`

```js
let arr = [1,4,6,8,3,5]
arr.sort()
document.write(arr)
```

![image-20260508162930363](https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260508162930363.png)

**sort()方法语法** 默认是升序排列

```js
let arr = [1,4,6,8,3,5]
// 升序排列
arr.sort(function(a,b){
    return a - b
})
document.write(arr)
document.write("<br>")
//html的标签必须在引号内
// 降序排列
arr.sort(function(a,b){
    return b - a
})
document.write(arr)
```

![image-20260508163357587](https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260508163357587.png)

## 函数及其细节补充

### 1. 函数

定义：function，是被设计为执行特定任务的代码块

#### 1.1 函数使用

**函数的声明语法**

```js
function 函数名(){
    函数体
}
```

函数名命名规范：与变量命名基本一致，尽量小驼峰式命名法，前缀应该为动词

常用命名建议
![image-20260508222828857](https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260508222828857.png)

**函数的调用语法**

```js
函数名()
```

#### 1.2 函数传参

```js
function 函数名(参数列表) {
    函数体
}

function getSum(num1,num2) {
    document.write(num1 + num2)
}
```

参数列表：传入数据列表，声明这个函数需要传入几个数据，多个数据用逗号隔开

**调用语法**

```js
函数名(传递的参数列表)
getSquare(8)
```

调用函数时，需要传入几个数据就写几个，用逗号隔开

形参：==声明==函数时写在函数名右边小括号里的参数（形式上的参数），可以理解为在这个函数内声明的变量

实参：==调用==函数时写在函数名右边的小括号里的参数（实际上的参数），可以理解为给这个函数赋值，==可以是变量==

**参数默认值**

设置了形参，但是调用时该变量不给值，默认是undefined，但赋值了的话，优先都是赋值的数据
可以给形参默认值，默认为0，这样程序更严谨

#### 1.3 函数返回值

当函数需要返回数据出去时，用return关键字
```js
return 关键字
return 20
```

**细节**
在函数体中使用return关键字能将内部的执行结果交给函数外部使用

return 后面的代码不会再被执行，会立即结束当前函数，所以==return后面的数据不换行写==

return函数可以没有return，这种情况函数默认返回值为undefined

#### 1.4 函数细节补充

两个相同的函数后面的会覆盖前面的函数

在js中，实参的个数和形参的个数可以不一致：如果形参过多，会自动填上undefined；如果实参过多，多余的实参会被省略

```js
// 实参多于形参
function fn(a,b) {
    console.log(a + b)
}
fn(1,2,3)
// 形参多于实参
function fun(a,b,c) {
    console.log(a + b + c)
}
fun(1,2)
```

![image-20260509102642422](https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260509102642422.png)

#### 1.5 作用域

定义：限定函数名的可用性的代码范围

作用：提高程序逻辑的局部性，增强程序的可靠性，减少了名字冲突

分类

+ 全局作用域：全局有效，作用于所有代码执行的环境，即整个script标签内部，或者一个独立的js文件
+ 局部作用域：作用于函数内的代码环境，也称为函数作用域

根据作用域的不同，变量可以分为两类

+ 全局变量：函数外部 let的变量。在任何区域都可以访问和修改
+ 局部变量:函数内部let的变量，只能在当前函数内部访问和修改

**特殊情况**
如果在函数内部的局部变量没有声明，直接赋值，也当全局变量来看
形参可以看作是函数的局部变量

**变量的访问原则**

+ 只要是代码，就至少有一个作用域
+ 写在函数内部的局部作用域
+ 如果函数中还有函数，那么在这个作用域中又可以诞生一个作用域
+ ==在能够访问到的情况下，先局部，局部没有再找全局==

#### 1.6 匿名函数

定义：没有名字的函数，无法直接使用

使用方式：
函数表达式
立即执行函数

**函数表达式**

定义：将匿名函数赋值给一个变量，并且通过变量名称进行调用

```js
let fn = function() {
    //函数体
}
```

```js
let num = function(){
    console.log('this is a number')
}
num()
//调用： 函数名()

let count = function(x,y){
    console.log(x + y)
}
count(1,2)
```

![image-20260509120431035](https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260509120431035.png)

其中函数的形参和实参使用跟具名函数一致

**与具名函数的区别**
具名函数的调用可以写在任何位置，但匿名函数的调用只能写在变量声明之后

**立即执行函数**

场景：避免全局变量之间的污染

语法：
```js
//方法1
(function(){
    
})();

(function(x,y){
    console.log(x + y)
})(1,2);

//方法2
(function(){
    
}());

(function(x,y) {
    console.log(x + y)
}(1,3));
```

不需要调用，立即执行

#### 1.7 逻辑中断

**逻辑运算符里的短路**

短路：只存在于&&和||中，当满足一定条件会让右边代码不执行

| 符号 | 短路条件          |
| :--- | ----------------- |
| &&   | 左边为false就短路 |
| \|\| | 左边为true就短路  |

原因：通过左边就得到整个式子的结果，没必要再判断右边

运算结果：运算结果都是最后被执行的表达式值，一般用在变量赋值

```js
function fn(x,y){
    x = x ||0
    y = y ||0
    
}
```



```js
let num = 624
console.log(false && num--)
console.log(num)
```

![image-20260509133159943](https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260509133159943.png)

若左右两边都是真值，&&返回最后一个真值，||返回第一个真值

```js
console.log(624 && 729)
console.log(624 || 729)
```

![image-20260509133722130](https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260509133722130.png)

**转换成布尔类型**

==显示转换==
Boolean(内容)
记忆：'' 、0、undefined、null、false、NaN 转换成布尔值后都是false，其余为true

==隐式转换==

1. 有字符串的加法 “ ” + 1，结果是“1”
2. 减法 - 只能用于数字，它会使空字符串 "" 转换成0
3. null 经过数字转换之后会变成0
4. undefined 经过数字转换之后会变成NaN

## 对象

定义：ja里的一种数据类型

可以理解为一种==无序==的数据集合，（数组为有序的数据集合），用来描述某个事物

```js
let obj = {
    uname:'朝了个朝'
    age:18
    gender:'女'
}
```

静态特征：用数字、字符串、数组、布尔类型等表示

动态行为：用函数表示

### 1. 对象使用

#### 1.1 对象声明语法

```js
let 对象名 = {}
//{} 是对象字面量
```

#### 1.2 对象由属性和方法组成

属性：信息或叫做特征（名词）

方法：功能或叫行为（动词）

```js
let 对象名 = {
    属性名: 属性值,
    方法名: 函数
}
```

**属性**

数据描述性的信息，一般为名词性词组

属性都是==成对==出现的，包括属性名和值，之间使用英文 :  分割

多个属性之间用英文 , 分隔

属性就是依附在对象上的变量（外面是变量，对象内是属性）

属性名可以用单双引号，==一般情况下省略==，除非名称遇到特殊符号，例如空格、中横线等

```js
let obj = {
    uname:'朝了个朝',
    age:18,
    gender:'女'
}
console.log(obj)
console.log(typeof obj)
```

![image-20260509140215693](https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260509140215693.png)

#### 1.3 对象使用

对象本质是无序的数据集合，也是增 删 改 查的语法

**属性-查**

+ 属性访问：声明对象，并添加了若干属性后，可以使用、获得对象属性对应的值
+ 语法：对象名.属性

```js
let obj = {
    uname:'朝了个朝',
    age:18,
    gender:'女'
}
console.log(obj.uname)
```

![image-20260509140528728](https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260509140528728.png)

==另一种方法==

对象名['属性名']

```js
let obj = {
    uname:'朝了个朝',
    age:18,
    gender:'女'
}
console.log(obj['age'])
```

![image-20260509141442055](https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260509141442055.png)

适用于属性名是字符串的，比如说"goods-name"，不然的话 - 会被当作减号，无法正确查询

**属性-改**

+ 语法：对象名.属性 = 新值

```js
let obj = {
    uname:'朝了个朝',
    age:18,
    gender:'女'
}
obj.age = 19
console.log(obj.age )
```

![image-20260509140752102](https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260509140752102.png)

**属性-增**

+ 语法： 属性名.新属性 = 值

```js
let obj = {
    uname:'朝了个朝',
    age:18,
    gender:'女'
}
obj.hobby = 'dancing'
console.log(obj)
```

![image-20260509141014846](https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260509141014846.png)

**属性-删**

+ 语法：delete 对象名.属性

```js
let obj = {
    uname:'朝了个朝',
    age:18,
    gender:'女'
}
delete obj.age
console.log(obj)
```

![image-20260509141144025](https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260509141144025.png)

**对象中的方法**
定义：数据行为性的信息，一般是动词性的，本质是函数

+ 方法是由方法名和函数两部分构成，它们之间使用 : 分隔
+ 多个属性之间使用英文 , 分隔
+ 方法是依附在对象中的函数
+ 方法名可以用双引号，==一般情况下省略==，除非名称遇到特殊符号，例如空格、中横线等

```js
let obj = {
    uname:'朝了个朝',
    age:18,
    gender:'女'
    hobby: function(){
        //函数体
    }
}
```

方面的调用： 对象名.方法名(),例如 `obj.hobby()`

方法调用：声明对象，并添加了若干方法，可以使用 . 调用对象中函数

也可以添加形参和实参

#### 1.4 遍历对象

用 for in 语句，不用for循环，因为不知道对象的长度，对象也没有下标

```js
let obj = {
    uname:'朝了个朝',
    age:18,
    gender:'女'
}
for(let k in obj){
    console.log(k)
    console.log(obj[k])//输出属性值，此时的k是字符串
}
```

![image-20260509143719643](https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260509143719643.png)

这种方法适用于遍历对象，这里的k是一个变量，在循环的过程中依次代表对象的==属性名==，所以必须用[]语法解析k

k是获得对象的属性名，对象名[k]是获得属性值

#### 1.5 内置对象

定义：js内部提供的对象，包含各种属性和方法给开发者调用

**Math**
定义：Math对象是js提供的一个"数学"对象

作用：提供了一系列做数学运算的方法

包含的方法：

| random   | 生成0-1之间的随机数（包含0不包含1）                     |
| -------- | ------------------------------------------------------- |
| ceil     | 向上取整                                                |
| floor    | 向下取整                                                |
| max      | 找最大数                                                |
| min      | 找最小数                                                |
| pow      | 幂运算                                                  |
| abs      | 绝对值                                                  |
| round    | 四舍五入后最接近的整数（若小数点后面是0.5，则往大了举） |
| parseInt | 取整函数                                                |

```js
console.log(Math.PI)
console.log(Math.ceil(1.1))
```

![image-20260509144656764](https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260509144656764.png)

```js
console.log(Math.round(-1.5))
console.log(Math.round(1.5))
```

![image-20260509145036137](https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260509145036137.png)

```js
console.log(Math.max(1,2,3,4,5))
console.log(Math.min(1,2,3,4,5))
console.log(Math.abs(-1))
```

![image-20260509145339059](https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260509145339059.png)
