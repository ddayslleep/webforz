# JS基础

js：运行在浏览器的一门编程语言

### 一、JS 快速上手

#### 1.1 书写位置

1.内部

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>
<body>
  <p id="demo">JS输出</p>
  <script>
    a=5;
    b=6;
    c=a+b;
    console.log(c);
  </script>
</body>
</html>
```

2.外部

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>
<body>
  <p id="demo">JS输出</p>
  <script src=""></script>
</body>
</html>
```

如果我在外部引入的时候在标签中间写了代码，会执行吗？

3.内联

onclick =  ""

```javascript
<button onclick="alert('Hello, World!')">点击我</button>
```

#### 1.2 注释

##### 1.单行注释

符号：//

快捷键：ctrl+/

##### 2.块注释

符号：/* */

快捷键：shift+alt+a

##### 3.结束符

;

可写可不写

#### 1.3 输入输出语法

##### 1.输出语法

语法1：document.write('内容')

向html输出

```javascript
document.write('内容')
document.write('<h1>标题</h1>')
```

注：输入中文一定要加引号

语法2：alert('内容')

弹出对话框

注：在实际写项目的时候我们一般不采用alert对话框，因为`alert` 会破坏用户体验、阻塞交互流程、样式不可控，除了极简的调试场景外，应完全避免在实际项目中使用。

语法3：`console.log('内容')`

向控制台输出

##### 2.输入语法

语法：prompt('内容')

作用：显示一个对话框，对话框中包含一条文字信息，用来提示用户输入文字

### 二、变量与常量

#### 2.1 变量是什么？有什么作用？

是计算机存储数据的容器。存放数据。

#### 2.2 变量的基本使用

##### 1.声明变量

语法：let 变量名

注：

1.声明变量由两部分构成：声明关键字、变量名（标识）

2.let即关键字，所谓关键字是系统提供的专门用来声明（定义）变量的词语

==3.let不允许多次声明同一个变量==

##### 2. 变量赋值

如：age  =  18      注：‘=’    赋值运算符

##### 3. 更新变量

```javascript
let age;
age = 18;
age = 19;
console.log(age);
```

##### 4. 声明多个变量

```javascript
let age=18,uname='jiumeng'
console.log(age,uname);
```

注：为了代码易于可读，不推荐采用一行声明多个变量

#### 2.3 变量命名规则与规范

##### 1.规则

1.不能用关键字

2.只能用**下划线**、**字母**、**数字**、**$符号**组成，且数字不能开头

3.字母严格**区分大小写**，如Age与age是不同的变量

注：必须遵守，不遵守报错

##### 2. 规范

1.起名要有意义

2.遵守小驼峰命名法（第一个字母小写，后面每一个单词字母大写）

注：建议，不遵守不会报错

#### 2.4 const 常量

使用const声明

1.常量不允许再次赋值

2.常量声明的时候必须赋值

#### 2.5 let、var、const的区别

var声明：

1.可以先使用 再声明（不合理）

2.var声明过的变量可以重复声明（不合理）

3.比如变量提升、全局变量、没有块级作用域

##### 1. 作用域

**var**

(1)函数作用域

无论在函数内部哪个位置声明变量，这个变量的作用域都是整个函数，无论在函数哪个位置声明，都可以在函数的任何地方访问。

```javascript
function testVar() {
      x = 11
      if (false) {
        var x = 10;
      } else {
        console.log(x);
      }
    }
testVar();
```

(2)全局

如果在全局作用域中使用var声明变量，那么这个变量会成为全局变量，可以在整个脚本中访问。

var声明的变量会提升到作用域顶部，但赋值不会提升

```javascript
console.log(y); // 输出 undefined，因为变量 y 被提升，但赋值操作没有提升
var y = 20;
```

**let**

（1）块级作用域

let 声明的变量只在代码块中有效

```javascript
if (true) {
  let a = 10;
}
console.log(a); // 报错，a 不在当前作用域
```

（2）无变量提升

```javascript
console.log(a); // 报错，a 未声明
let a = 10;
```

**const**

（1）块级作用域

（2）没有变量提升

（3）必须初始化

**声明的变量必须在声明时初始化，且不能重新赋值。**

```javascript
const a = 10;
a = 20; // 报错，不能重新赋值
```

##### 2. 重复声明

在同一个作用域内可以重复使用 `var` 声明同一个变量，但只有第一次声明会真正创建变量，后续的声明会被忽略。

```javascript
var b = 50;
var b = 60;
console.log(b); // 输出 60，只有第一次声明创建了变量，后续的声明只是重新赋值
```

在同一个作用域内不能重复使用 `let`和**`const`** 声明同一个变量，否则会报错

```javascript
let c = 70;
let c = 80; // 报错：
const b = 10;
const b = 20; // 报错，重复声明
```

### 三、数据类型

#### 3.1 基本数据类型

number数字型，string字符串型，boolean布尔型，undefined未定义型，null空类型

##### 1. 数字类型

可以使整数、小数、正数、负数等统称为数字类型

**算术运算符**：+ - * / %

注：NaN代表一个计算错误，他是一个不正确的或者一个未定义的数字操作所得到的结果，NaN是粘性的，对NaN的操作都会返回NaN

##### 2. 字符类型

通过   “      ’      或  `  包裹的数据都叫字符串（单引号、双引号、反引号），单引号和双引号没有本质区别，但推荐使用单引号

**注意事项**：

1.无论单引号还是双引号必须成对使用

2.单引号/双引号可以相互嵌套，但是不可以自己嵌套自己（口诀：外双内单，或者外单内双）

3.必要时可以使用转义字符\，输出单引号或双引号

**字符串拼接**

console.log('aaa' + 'bbb')

**模版字符串**：

语法：

1.``   必须是反引号

2.在英文输入模式下按键盘的tab间上方的那个键（1左边）

3.内容拼接变量时，在${}内部写变量

```javascript
let age = 18
document.write(`我今年${age}岁了`)
```

##### 3. 布尔型

true    false

##### 4. 未定义

undefined：只声明，未赋值

##### 5. 空

null

如果一个变量里确定存放的是对象，如果还没准备好对象，可以放个null

检测数据类型：

```javascript
typeof x
typeof(x)
```

#### 3.2 引用数据类型

object对象

#### 3.3 类型的转换

##### 1. 隐式转换

某些运算符被执行时，系统内部自动将数据类型进行转换，这种方法被称为隐式转换

规则：

1.+两边只要有一个是字符串，就会把另一个也转化为字符串

2.除了+以外的运算符都会把数据转换成数字类型

小技巧：

==1.+作为正号解析可以转换成数字型==

2.任何数据和字符串相加结果都是字符串

```javascript
console.log(1+1);//2
console.log('pink' + 1);//pink1
console.log(typeof +'123');//Number
console.log(+'123' + 123);//246
```

##### 2. 显式转换

1.转换为数字型

Number(数据)

```javascript
let str = '456'
console.log(Number(str));
```

parseInt(数据)      

注：只能变成整数

```console.log(parseInt('12.34px'));```

parseFloat(数据)    

```console.log(parseFloat('12.34px'));```

### 四、数组

#### 4.1 创建数组

是一种可以按是顺序保存数据的数据类型

1.使用数组字面量语法

```javascript
let arr = [数据1，数据2，......数据n]

例：
let names = ['小明' ,  '小刚' ,  '小红' ,  '小丽']
```

- 语法简洁，易于理解和编写。
- 可以直接在数组中添加各种类型的元素（字符串、数字、布尔值、对象、数组等）。
- 适合快速创建数组，尤其是数组元素已知且数量较少时。

2.构造函数方法

```javascript
let arr = new Array(元素1, 元素2, 元素3, ...);
                    
例如：
let fruits = new Array("apple", "banana", "cherry");
let numbers = new Array(1, 2, 3, 4, 5);
let mixed = new Array(1, "hello", true, null);
```

- 使用 new Array() 创建数组，语法相对复杂，但功能强大。
- 如果只传入一个数字参数，Array 构造函数会将该数字视为数组的长度，而不是数组的元素。

- 如果传入多个参数，这些参数将作为数组的元素。

```javascript
let arr = new Array(3,5,789,131,1656,13156,1)
console.log(arr);
```

![image-20250415154942804](https://join-std.oss-cn-beijing.aliyuncs.com/chenweiqi2023012226/202504151549975.png)

- 数组是按顺序保存的，所以每个数据都有自己的编号
- 计算机中的编号从0开始
- 在数组中，数据的编号也叫索引或下标
- 数组可以存储任意类型的数据

```javascript
let names = ['a','b','c','d']
console.log(names[0]);
```

元素：数组中保存的每个数据都叫数组元素

下标：数组中数据的编号

长度：数组中数据的个数，通过length属性获得

#### 4.2 增删改查

##### 1.新增元素

语法：

`arr.push(元素1，元素2，元素n)`

将元素添加至数组末尾，并返回**数组长度**

`arr.unshift()`

将数添加至开头，返回**数组长度**

##### 2.删除元素

`arr.pop()`从数组中删除最后一个元素，并返回该**元素的值**

`arr.shift()`从数组中删除第一个元素，返回值是**删除元素**

`arr.splice(起始位置,删除几个元素)`，返回值是被**删除的元素（数组）**

起始位置：指定修改的开始位置（从0开始）

删除几个元素：表示要移除元素的个数，如果省略则默认从所选位置开始删除到最后

### 五、运算符与流程控制

#### 5.1 常用运算符

##### 1.赋值运算符

对变量进行赋值的运算符

=     +=    -=    *=   /=

##### 2.自增运算符

符号：++

1）前置自增

2）后置自增 

两者的区别？

##### 3.比较运算符

<   >   >=   <=

==:判断左右两边的值是否相当

===:左右两边是否类型和值都相等

!==：左右两边是否不全等

注：

- 字符串比较，是比较ascll码的值
- NaN不等于任何值，包括他自己

- 尽量不要比较小数，小数有精度问题

- ==不同类型之间比较会发生隐式转换==

##### 4.一元运算符

如：+  -

##### 5.逻辑运算符

###### 1）介绍

&& 		||     		！

###### 2）运算优先级

1.小括号

2.一元运算符

3.算术运算符

4.关系运算符

5.相等运算符

6.逻辑运算符（&&>||）

7.赋值运算符

8.逗号运算符

###### 3）逻辑中断

前面的成立，就不会运行后面的式子

```javascript
let x = 0;
	if (x++ === 0 && x++ === 0 && x++ === 2) {
    	console.log('条件成立');
}
console.log(x);//打印：2
```

#### 5.2 表达式，语句

区别：

表达式：可被求值

语句：不一定有值

##### 1.顺序语句

##### 2.分支语句

###### 1）if

```javascript
if(条件1){
	满足条件的代码
}
else if(条件2) {
	不满足条件1，但是满足提条件2的代码
}
else {
	不满足条件的代码
}
```

注：

- 数字中除了0，所有数字都为真，

- 字符串中，除了 ' '（空字符串） 所有字符串都为真


###### 2）三元运算符

语法：条件?满足条件执行的代码 : 不满足条件执行的代码

###### 3）switch

```javascript
switch:(数据){
	case 值1：
        代码1
        break
	case 值2：
        代码2
        break
	case 值3：
        代码3
        break
	default:
		代码4
}
```

##### 3.循环语句

###### 1）while循环

```javascript
while(循环条件){
	要重复执行的代码(循环体)
}
```

三要素：

1.变量起始值

2.终止条件

3.变量变化量

###### 2）for循环	

```javascript
for(变量起始值;终止条件;变量变化量){
	循环体
}
```

###### 3）循环退出

1.break,结束循环

2.continue,结束本次循环，进行下一次循环

### 六、函数

#### 6.1 声明与调用

##### 1.函数声明语法

```javascript
function 函数名( ){
	函数体
}
```

```javascript
function sayhi(){
	console.log('hi~~~');
}
sayhi()
```

##### 2. 函数命名

- 建议使用驼峰命名法

- 准确反映函数的功能


##### 3. 函数调用

函数名( )

#### 6.2 参数与返回值

##### 1. 函数传参

function 函数名(参数列表){

​	函数体

}

```javascript
function getHe(a,b){
    let c = a + b
    console.log(c)
}
getHe(10,2)

//函数参数默认值
function getHe2(a = 0, b = 0){
    let c = a + b  
    console.log(c)
}
getHe2()
```

##### 2. 函数返回值

语法：return   数据

```javascript
function getHe(){
    return 20
}
console.log(getHe());
```

返回值的细节：

- return 后面的代码不会被执行，故 return 后面的数据不要换行写
- 没有 return 时函数默认返回值为 undefined

返回多个数据

```javascript
function getArrValue(arr = []){
	let max = arr[0]
	let min = arr[0]
	for(let i = 1; i < arr.length; i++){
		if(max < arr[i]){
			max = arr[i]
		}
		if(min > arr[i]){
			min = arr[i]
		}
	}
	return [max, min]
}

let newArr = getArrValue([11, 3, 55, 7, 29])
```

#### 6.3 作用域

1）全局作用域：全局变量

2）局部作用域：局部变量

特别的，局部变量或者块级变量没有let声明直接赋值时把它当作全局变量来看==（强烈不提倡！）==

变量访问原则：

在能够访问到的情况下，先局部，局部没找到在全局找

```javascript
let i = 1
function test() {
    if(true) {
        let i = 2 
        console.log(i);//2
    }
    console.log(i);//1
}
test()
```

#### 6.4 匿名函数

```javascript
function (){}
```

函数表达式

将匿名函数赋值给一个变量，并且通过变量名进行调用

**语法：**

```javascript
let fn = function (x, y) { 
	//函数体
}

fn(1, 2)
```

注：具名函数的调用可以写在任何位置，==函数表达式必须先声明后调用==

**立即执行的匿名函数**

方式1：

```javascript
(function ( ) {  }) ( );
```

方式2：

```javascript
( function ( ) {  } ( ) );
```

==立即执行函数必须加分号==

**无参**

```javascript
(function(){
    console.log(122);
})();
```

**实参**

```javascript
(function(x,y){
    console.log(x+y);
})(1,2);
```

### 七、对象

- 对象是一种数据类型

- 可以理解为一种无序的数据集合

- 由**属性**和**方法**组成


#### 7.1 创建对象

let   对象名   =   { }

let   对象名   =   new  Object( )

let   对象名   =   {

​	属性名 : 属性值 ，

​	方法名 : 函数

}

```javascript
let jm ={
    uname : 'aaa',
    age:18,
    gender: '男'
}
console.log(jm);
```

#### 7.2 属性的增删改查

##### 1. 查

对象.属性

对象名[ '属性名' ]

##### 2. 改

对象.属性 = 新值

##### 3. 增

对象.属性 = 新值

##### 4.删

delate 对象.属性

```javascript
let jm ={
    uname : 'aaa',
    age:18,
    gender: '男'
}
jm.gender = '女'
jm.hobby = '足球'
console.log(jm.age);//18
console.log(jm['gender']);//女
console.log(jm.hobby);//足球
```

#### 7.3 对象的方法

写法：	

方法名:function( ) {

​	方法体

}

```javascript
const person = {
    name: "jm",
    age: 25,
    sayHello: function () {
        console.log(1);
    }
};
person.sayHello(); //1
```

#### 7.4 遍历对象

for( let k in object){}

注：k是属性名

```javascript
let jm ={
    uname : 'aaa',
    age:18,
    gender: '男'
}
for(let k in jm){
    console.log(jm[k]);
}
```

为什么是`jm[k]`而不是`jm.k` ？

答案：因为k是加引号的属性名

### 八、内置对象

#### 8.1 Math

##### 1. Math对象包含的方法：

random:生成0-1之间的随机数

ceil：向上取整

floor：向下取整

round：四舍五入

max：找最大值

min：找最小值

pow：幂运算

abs：绝对值

##### 2. random()

[0,1) 浮点数

```javascript
console.log(Math.random() * 10);
```

```javascript
 let arr = ['red','green','blue']
 let random = Math.floor(Math.random()*arr.length)
 console.log(arr[random]);
```

```javascript
let uname=['y','c','b','a','x']
console.log(uname[Math.floor(Math.random()*uname.length)]);
```

```javascript
let uname=['y','c','b','a','x']
let random = Math.floor(Math.random()*uname.length)
document.write(uname[random])
uname.splice(random,1)
console.log(uname)
```

#### 8.2 数组高阶方法

##### 1. map

**map**（对数组中的每个元素执行某种操作并返回一个新数组）

```javascript
array.map(function(currentValue, index, array) {
    // 返回新数组的元素
})
currentValue：当前正在处理的元素
index（可选）：当前元素的索引
array（可选）：调用 map 的数组本身

let numbers = [1, 2, 3, 4, 5];
let doubled = numbers.map(function(num) {
    return num * 2;
}); // [2, 4, 6, 8, 10]
```

特点：

- 不会改变原数组，而是返回一个新数组
- 新数组的长度和原数组相同

##### 2. join

**join** 方法将数组中的所有元素连接成一个字符串，并返回这个字符串。

```javascript
array.join(separator)
eparator（可选）：指定分隔符，默认为逗号

let arr = ['苹果', '香蕉', '橘子'];
console.log(arr.join());      // 输出："苹果,香蕉,橘子"
console.log(arr.join('-'));   // 输出："苹果-香蕉-橘子"
console.log(arr.join(''));    // 输出："苹果香蕉橘子"

// 空数组返回空字符串
let empty = [];
console.log(empty.join('-')); // 输出：""
```

特点：

- 如果分隔符是空字符串（''），元素之间没有任何字符
- 返回一个拼接后的字符串

##### 3. map 和 join 配合使用

**map** 和 **join** 经常配合使用，将数组快速转换为HTML字符串：

```javascript
// 图书数据
let books = [
    { name: 'JavaScript高级程序设计', author: 'Nicholas' },
    { name: 'CSS揭秘', author: 'Lea Verou' },
    { name: 'HTML5权威指南', author: 'Adam Freeman' }
];

// 使用 map + join 生成列表HTML
let html = books.map(function(book, index) {
    return `<li>${book.name} - ${book.author}</li>`;
}).join('');

console.log(html);
// 输出：
// <li>JavaScript高级程序设计 - Nicholas</li>
// <li>CSS揭秘 - Lea Verou</li>
// <li>HTML5权威指南 - Adam Freeman</li>
```

##### 4. filter

**filter**根据条件过滤数组中的元素并返回一个新数组

```javascript
let numbers = [1, 2, 3, 4, 5];
let even = numbers.filter(function(num) {
    return num % 2 === 0;
}); // [2, 4]
```

##### 5. reduce

**reduce** 方法对数组中的每个元素执行一个累加函数，最终返回一个累计结果。

```javascript
array.reduce(function(accumulator, currentValue, currentIndex, array) {
    // 返回累计的结果
}, initialValue)

accumulator：累积器，存储每次累加后的结果
currentValue：当前正在处理的元素
currentIndex（可选）：当前元素的索引
array（可选）：调用 reduce 的数组本身
initialValue（可选）：累积器的初始值

let numbers = [1, 2, 3, 4, 5];
let sum = numbers.reduce(function(acc, curr) {
    return acc + curr;
}, 0);
console.log(sum); // 输出：15
```

**特点：**

- 不会改变原数组
- 最终返回一个累计值

### 九、拓展

#### 1.   .trim()

- **作用**：.trim() 是一个字符串方法，用于去除字符串两端的空白字符（包括空格、制表符、换行符等），但不会改变原字符串，而是返回一个新的字符串。
- **语法**：string.trim()
- **返回值**：返回一个去掉两端空白字符的新字符串。

```javascript
let str = "   Hello World   ";
let trimmedStr = str.trim();
console.log(trimmedStr); // 输出："Hello World"
```

#### 2.foreach

除了使用for循环遍历数组，还可以用foreach

语法：

```javascript
array.forEach(function(currentValue, index, array){
    //函数体
});
currentValue：当前正在处理的元素的值。
index（可选）：当前正在处理的元素的索引。
array（可选）：调用 forEach的数组本身。

let names = ['小明', '小刚', '小红'];
names.forEach(function(name, index) {
    console.log(index + ': ' + name);
});

输出
0:小明
1:小刚
2:小红
```

特点：

- 没有返回值
- 不能中断遍历：forEach 方法没有中断（break）或跳过（continue）的机制


```javascript
let fruits = ['apple', 'banana', 'cherry'];
fruits.some(function(fruit, index) {
    console.log(index + ': ' + fruit);
    return fruit === 'banana'; // 当遇到 'banana' 时中断遍历
});

输出
0: apple
1: banana
```

- 不会遍历新增的元素：如果在 **forEach**遍历过程中向数组中添加新元素，新增的元素不会被遍历到。


```javascript
let arr = [1, 2, 3];
arr.forEach(function(item, index) {
    console.log(item);
    if (index === 1) {
        arr.push(4); // 新增元素 4
    }
});
console.log(arr);
输出
1
2
3
[1,2,3,4]
```

- 被删除元素之后、原本还未遍历到的元素，不会被遍历到


```javascript
let arr = [1, 2, 3];
arr.forEach(function(item, index) {
    console.log(item);
    if (index === 1) {
        arr.splice(index, 1); 
    }
});
console.log(arr);
输出
1
2
[1,3]

迭代1: index=0  arr=[1,2,3] → 输出1
迭代2: index=1  arr=[1,2,3] → 输出2 → 删除索引1 → arr=[1,3]
迭代3: index=2  arr=[1,3]   → 索引2不存在 → 跳过回调
结束 → 输出 [1,3]
```

#### 3.箭头函数

**箭头函数**实例化的**函数对象**与正式的函数表达式创建的函数对象行为是相同的。任何可以使用函数表达式的地方，都可以使用箭头函数

```javascript
// 普通函数
let sum = function(a, b) {
	return a + b;
}

// 箭头函数
let sum1 = (a, b) => {
	return a + b;
}

// 箭头函数的语法
( 参数 ) => { 函数体 }
// 1. 当参数只有一个的时候可以省略掉小括号(),当没有参数或者有多个参数的时候一定要有括号
// 2. 当函数体只有一句话的时候可以省略掉{}，省略大括号的时候，默认返回这一条语句的值，且不能写return语句
```

使用场景：

充当回调函数：在使用数组的某些方法（map,filter）或者异步操作

```javascript
const numbers = [1, 2, 3, 4];
const doubled = numbers.map((num) => num * 2);
console.log(doubled); // 输出：[2, 4, 6, 8]

const numbers = [1, 2, 3, 4, 5];
const evenNumbers = numbers.filter((num) => num % 2 === 0);
console.log(evenNumbers); // 输出：[2, 4]
```

#### s4.函数的arguments对象

`arguments` 是函数内部的一个特殊对象，用来**获取调用函数时传入的所有参数**。

```javascript
function test() {
    console.log(arguments);
    console.log(arguments[0]); // 第一个参数
    console.log(arguments[1]); // 第二个参数
    console.log(arguments.length); // 参数个数
}

test('苹果', '香蕉', '橘子');
// 输出：['苹果', '香蕉', '橘子']
// 输出：'苹果'
// 输出：'香蕉'
// 输出：3
```

**特点：**

- 即使函数定义时没有写参数，也能通过 `arguments` 获取到传入的值

```javascript
function sum() {
    let total = 0;
    for (let i = 0; i < arguments.length; i++) {
        total += arguments[i];
    }
    return total;
}

console.log(sum(1, 2, 3));      // 输出：6
console.log(sum(1, 2, 3, 4, 5)); // 输出：15
```

- `arguments` 是一个**伪数组**，它没有 `push`、`pop`、`forEach` 等数组方法

**ES6 推荐写法：Rest 参数**

用 `...args` 代替 `arguments`，得到的是真正的数组，可以直接使用数组方法。

```javascript
// Rest 参数写法（推荐）
function sum(...nums) {
    return nums.reduce((acc, num) => acc + num, 0);
}

console.log(sum(1, 2, 3)); // 输出：6
```

#### 5. 扩展运算符

扩展运算符（`...`）可以将一个**数组**或**伪数组**展开成一个个独立的元素。

```javascript
...数组

// 1. 展开数组
let arr = [1, 2, 3];
console.log(...arr);        // 输出：1 2 3（不是数组，是三个独立的数字）

// 2. 合并数组
let arr1 = [1, 2];
let arr2 = [3, 4];
let newArr = [...arr1, ...arr2];
console.log(newArr);        // 输出：[1, 2, 3, 4]

// 3. 复制数组
let original = [1, 2, 3];
let copy = [...original];
console.log(copy);          // 输出：[1, 2, 3]

// 4. 将伪数组转换成真数组
function test() {
    let trueArray = [...arguments];
    console.log(trueArray);           // 输出：[1, 2, 3]
    console.log(trueArray.push(4));   // 4（说明已经是真数组，可以用push方法）
}
test(1, 2, 3);
```

**注意：** 只有**可迭代对象**（如数组、伪数组等）才能使用扩展运算符展开。

#### 6. Array.from

`Array.from()` 是一个静态方法，用于将**伪数组**或**可迭代对象**转换成一个真正的数组。

```javascript
Array.from(伪数组)

// 1. 将 arguments 转换成真数组
function test() {
    let args = Array.from(arguments);
    console.log(args);              // 输出：[1, 2, 3]
    console.log(args.push(4));      // 4（说明可以用数组方法）
}
test(1, 2, 3);

// 2. 转换字符串
let str = 'hello';
let arr = Array.from(str);
console.log(arr);  // 输出：['h', 'e', 'l', 'l', 'o']
```

**扩展运算符 vs Array.from()：**

| 方法         | 写法              | 特点                         |
| :----------- | :---------------- | :--------------------------- |
| 扩展运算符   | `[...arr]`        | 更简洁，但只能用于可迭代对象 |
| Array.from() | `Array.from(arr)` | 功能更强大，还可以做数据转换 |

**推荐：** 将伪数组转换成真数组时，两种方法都可以，但 `Array.from()` 更语义化，见名知义。

#### 7.伪数组

伪数组就是**长得像数组，但不是真正的数组**的对象。

**伪数组的特征：**

- 有 `length` 属性
- 可以通过索引访问元素（如 `arr[0]`）
- 不能使用数组方法（如 `push`、`pop`、`forEach`）

**常见的伪数组：**

- 函数的 `arguments` 对象
- `document.querySelectorAll('div')` 返回的节点集合

| 特性                   | 伪数组           | 真数组 |
| ---------------------- | ---------------- | ------ |
| 通过索引访问           | 可以             | 可以   |
| 有 length 属性         | 有               | 有     |
| 能用 forEach/ push/pop | 不能（有些例外） | 能     |

**为什么有些伪数组能用 forEach？**

现代浏览器对 `document.querySelectorAll` 返回的伪数组添加了 `forEach` 方法，但这不是标准，所以最好先转换成真数组。

```javascript
let divs = document.querySelectorAll('div');
// 情况1：部分浏览器可以直接用 forEach
divs.forEach(div => console.log(div));

// 情况2：保险的做法，先转换成真数组
let divArray = Array.from(divs);
divArray.forEach(div => console.log(div));
```

**如何把伪数组转换成真数组？**

```javascript
// 方法一：Array.from()（推荐）
let trueArray = Array.from(arrayLike);

// 方法二：扩展运算符
let trueArray2 = [...arrayLike];
```

伪数组能用 `[索引]` 访问，也有 `length`，但不能直接用数组的方法，先用 `Array.from()` 转换一下再操作。





