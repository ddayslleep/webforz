## 盒子模型

### 1. 组成

作用：布局网页，摆放盒子和内容

组成部分：

+ 内容区域 - width & height
+ 内边距 - padding （出现在**内容**和盒子边缘之间）
+ 边框线 - border
+ 外边距 - margin (出现在盒子外面，通常用来拉开两个盒子之间的距离)

> ```css
> div{
>             width: 200px;
>             height: 200px;
>             background: pink;
>             padding: 25px;
>             border: 2px solid black;
>             margin: 35px;
>          }
> ```

用浏览器的检查功能，效果如图所示：<img src="https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260408185349185.png" alt="image-20260408185349185" style="zoom: 50%;" />

页面显示：<img src="https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260408195708775.png" alt="image-20260408195708775" style="zoom:50%;" />

### 2. 边框线

属性名：border（bd）

属性值：边框线粗细 线条样式 颜色（不区分顺序）

常用线条样式：

+ solid - 实线
+ dashed - 虚线
+ dotted - 点线

**设置单方向边框线**

属性名： border-方位名词（bd+方位名词首字母）

属性值： 边框线粗细 线条样式 颜色（不区分顺序）

> ```css
> div{
>             width: 200px;
>             height: 200px;
>             background: pink;
>             border-top: 3px dotted #000;
>             border-bottom: 4px solid #a82c2c;
>             border-left: 5px dashed #39359f;
>             border-right: 6px solid #15883f;
>          }
> ```

效果如图：<img src="https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260408200259347.png" alt="image-20260408200259347" style="zoom:50%;" />

### 3.内边距

作用：设置内容与盒子边缘之间的距离

属性名：padding/padding-方位名词
**单独设置一个方向内边距的方法与边框线相同**

**多值写法**
作用规律：从上开始顺时针转一圈，如果当前方向没有数值，取值跟对面一样

| 取值个数 | 示例                            | 含义                                   |
| -------- | ------------------------------- | -------------------------------------- |
| 一个值   | `padding : 10px;`               | 四个方向内边距均为10px                 |
| 两个值   | `padding : 10px 80px; `         | 上下：10px    左右：80px               |
| 三个值   | `padding : 10px 40px 80px; `    | 上：10px   左右：40px  下：80px        |
| 四个值   | `padding : 10px 20px 40px 80px` | 上：10px  右：20px  下：40px  左：80px |

> ```css
> div{
>             width: 200px;
>             height: 200px;
>             background: pink;
>             padding: 10px 20px 40px 60px;
>          }
> 
> div{
>             width: 200px;
>             height: 200px;
>             background: pink;
>             padding: 10px 20px 40px ;
>          }
> ```

浏览器中元素检查，前后对比如下：

<img src="https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260408201418662.png" alt="image-20260408201418662" style="zoom:50%;" />

<img src="https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260408201534183.png" alt="image-20260408201534183" style="zoom:50%;" />

### 4. 尺寸计算

+ 默认情况
  盒子尺寸=内容尺寸+border尺寸+内边距尺寸
  <img src="https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260408201940565.png" alt="image-20260408201940565" style="zoom: 67%;" />

+ 结论：给盒子加 border /padding 会撑大盒子（外边距不会撑大盒子）
+ 解决方法
  + 手动做减法，减掉border/padding的尺寸
  + 內减模式(加border/padding不会撑大盒子）：box-sizing：border-box

以內减模式为例：

> ```css
> div{
>             width: 200px;
>             height: 200px;
>             background: pink;
>             padding: 10px ;
>             box-sizing: border-box;
>          }
> div{
>             width: 200px;
>             height: 200px;
>             background: pink;
>             padding: 10px ;
>          }
> ```
>
> 

<img src="https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260408202350844.png" alt="image-20260408202350844" style="zoom:67%;" />

<img src="https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260408202429137.png" alt="image-20260408202429137" style="zoom:67%;" />

### 5. 外边距

作用：拉开两个盒子之间的距离

属性名：margin

**与padding属性值写法、含义相同**

**版心居中**
` margin: 0 auto;`
浏览器将窗口的宽减去盒子的宽，然后除以2，是盒子在正中间；==此时盒子必须要有宽度==

#### 5.1 合并现象

场景：垂直排列的兄弟元素，上下margin会合并

现象：取两个margin中的较大值生效
**写垂直排列的盒子，就不要写两个外边距了**

#### 5.2 塌陷问题

场景：父子级的标签，子级的添加 上外边距（margin-top）会产生塌陷问题

现象：导致父级一起向下移动

解决办法：

+ 取消子级margin，父级设置padding——只要隔开父子级盒子顶端就行
+ 父级设置：overflow：hidden——浏览器去找父级正确的底部和顶端，将超出范围删除
+ 父级设置：border-top——让浏览器找到父级的正确边缘

### 6.清除标签默认样式

清除文件内所有的默认样式

> ```css
> *{
>     margin: 0;
>     padding: 0;
>     box-sizing: border-box;
>     /* 不用担心之后的盒子会被撑大*/
> }
> ```

清除列表的项目符号

> ```css
> li {
>             list-style: none;
>          }
> ```

### 7. 元素溢出

作用：控制溢出元素的内容的显示方式

属性名：overflow

| 属性值 | 效果                                       |
| ------ | ------------------------------------------ |
| hidden | 溢出隐藏                                   |
| scroll | 溢出滚动（无论是否溢出，都显示滚动条位置） |
| auto   | 溢出滚动（溢出才显示滚动条位置）           |

以scroll为例，效果如下：
<img src="https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260408235519978.png" alt="image-20260408235519978" style="zoom:50%;" />

<img src="https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260408235541914.png" alt="image-20260408235541914" style="zoom:67%;" />

### 8. 行内元素—内外边距问题

场景：行内元素添加 margin 和 padding，无法改变元素垂直位置

解决办法：给行内元素添加 line-height 可以改变垂直位置（相当于div的边距）

### 9.盒子模型 

#### 9.1 圆角

作用：设置元素的外边框为圆角

属性名：border-radius

属性值：数字+px/百分比

**怎么实现让四个角的圆角不一样？**

将 `border-radius: ;`写多个，从左上角开始顺时针赋值，没有取值的角与对角取值相同

> ```css
> div {
>             margin: 50px auto;
>             width: 200px;
>             height: 200px;
>             background-color: pink;
>             border-radius: 20px;
>          }
> 
> div {
>             margin: 50px auto;
>             width: 200px;
>             height: 200px;
>             background-color: pink;
>             border-radius: 20px 10px 40px 50px;
>          }
> ```

效果如图：<img src="https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260409002122804.png" alt="image-20260409002122804" style="zoom:50%;" /><img src="https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260409002425789.png" alt="image-20260409002425789" style="zoom:50%;" />

**常见应用**

+ 正圆形状

  + 给==正方形==盒子设置圆角属性为宽高的一半或50%
    圆角最大时50%，超过50%没有效果

    > ```CSS
    > div {
    >             margin: 50px auto;
    >             width: 200px;
    >             height: 200px;
    >             background-color: pink;
    >             border-radius: 100px;
    >          }
    > ```

    <img src="https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260409002903228.png" alt="image-20260409002903228" style="zoom:50%;" />

+ 胶囊形状

  + 给==长方形==盒子设置圆角属性值为盒子高度的一半

#### 9.2 阴影

作用：给元素设置阴影效果

属性名：box-shadow

属性值： X轴偏移量 Y轴偏移量 模糊半径 扩散半径 颜色 内外阴影

注意：

+ x轴偏移量和y轴偏移量必须书写
+ 默认是外阴影，内阴影需要添加**inset**

> ```css
> div {
>             margin: 50px auto;
>             width: 200px;
>             height: 100px;
>             background-color: pink;
>            box-shadow: 10px 20px 10px 10px rgba(1,1,1,0.5);
>          }
> ```
>
> 

<img src="https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260409003800322.png" alt="image-20260409003800322" style="zoom: 50%;" />

### 案例总结

CSS书写顺序

1. 盒子模型属性
2. 文字样式
3. 圆角、阴影等修饰属性

## 浮动

**标准流**

标签中默认的排布规则

### 1.基本使用与布局

#### 1.1 基本知识

作用：让块元素水平排列（实现图文混排效果）

属性名：float

属性值

+ left 左对齐
+ right 右对齐
  <img src="https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260409140646653.png" alt="image-20260409140646653" style="zoom:50%;" />

<img src="https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260409140720725.png" alt="image-20260409140720725" style="zoom: 50%;" />

**特点**
顶对齐：具备行内块显示模式特点
浮动流的盒子会脱离标准流的盒子
具备行内块特点
父级宽度不够，浮动的子级会换行

#### 1.2 产品区域布局

**怎么解决浮动的盒子可能掉下来的问题？**

调整父级或子级的宽度，每一排的最边缘的 li ，可以去掉左/右侧的margin

#### 1.3 清除浮动

场景：浮动元素会脱标，如果父级没有高度，子级无法撑开父级高度（可能导致页面布局错乱）

**1. 额外标签法**

在父元素内容的最后添加一个块级元素，设置CSS属性 clear:both
一般都用clearfix 做类选择器的标签名

会导致页面不清晰

**2. 单伪元素法**

依旧是在父元素内容的最后添加一个类选择器，必须添加content属性

> ```css
> .clearfix::after {
>             content: "";
>             display: block;
>             clear: both;
>         }
> ```

**3. 双伪元素法**

> ```css
> .clearfix::before,
>         .clearfix::after {
>             content: "";
>             display: table;
>         }
> 
>         .clearfix::after {
>             clear: both;
>         }
> ```

before 解决外边距塌陷的问题         after  清除浮动

**4. overflow**

父元素添加CSS属性 overflow: hidden

## flex布局

**定义**
也叫弹性布局，是浏览器提倡的布局模型，适合结构化布局，提供了强大的空间布局和对齐能力
不会产生浮动布局中脱标现象，布局网页更简单、灵活

### 1. 组成

设置方式：给父元素设置 `display:flex`,子元素可以自动挤压或拉伸

组成部分：弹性容器     弹性盒子     主轴：默认在==水平==方向       侧轴/交叉轴：默认在==垂直==方向

> ```css
> <style>
>         .number{
>             display: flex;
>             height: 300px;
>             border: 5px solid #000;
>         }
> 
>         .number div {
>             width: 200px;
>             height: 100px;
>             background-color: greenyellow;
>         }
>     </style>
> ```

> ```html
> <div class="number">
>         <div>1</div>
>         <div>2</div>
>         <div>3</div>
>     </div>
> ```

效果如图：弹性盒子都是沿主轴排列的（此时的主轴是水平的，侧轴是垂直的）

<img src="https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260409202610808.png" alt="image-20260409202610808" style="zoom: 50%;" />

边框包裹的盒子为弹性容器，有颜色的为弹性盒子
将CSS属性中的高注释掉后，黄绿色的弹性盒子将充满容器——拉伸

将子级盒子个数增多之后的==挤压==效果如图：
<img src="https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260409203016182.png" alt="image-20260409203016182" style="zoom:67%;" />

### 2. 布局

#### 2.1 主轴对齐方式

属性名：justify-content

| 属性值        | 效果                                                         |
| ------------- | ------------------------------------------------------------ |
| flex-start    | 默认值，弹性盒子从**起点**开始依次排列                       |
| flex-end      | 弹性盒子从**终点**开始依次排列                               |
| center        | 弹性盒子沿主轴**居中**排列                                   |
| space-between | 弹性盒子沿主轴均匀排列，空白间距均分在弹性盒子**之间**，父级剩余的尺寸分配成间距，弹性盒子之间的间距相等 |
| space-arround | 弹性盒子沿主轴均匀排列，空白间距均分在弹性盒子**两侧**，视觉效果为弹性盒子之间的间距是两端间距的两倍 |
| space-evenly  | 弹性盒子沿主轴均匀排列，弹性盒子与容器之间间距相等（**各个**间距都相等） |

以space-between为例：

> ```css
> .number{
>             display: flex;
>             height: 300px;
>             border: 5px solid #000;
>             justify-content: space-between;
>         }
> ```
>
> 

<img src="https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260409223350537.png" alt="image-20260409223350537" style="zoom: 33%;" />

#### 2.2 侧轴对齐方式

属性名

+ align-items   当前弹性容器内**所有**弹性盒子的侧轴对齐方式，**针对弹性容器**
+ align-self   单独控制**某个**弹性盒子的侧轴对齐方式，**针对弹性盒子**

| 属性值     | 效果                                                         |
| ---------- | ------------------------------------------------------------ |
| stretch    | 弹性盒子沿着侧轴线被拉伸至**铺满**容器（弹性盒子没有设置侧轴方向尺寸，则默认拉伸） |
| center     | 弹性盒子沿侧轴**居中**排列                                   |
| flex-start | 弹性盒子从**起点**开始依次排列                               |
| flex-end   | 弹性盒子从**终点**开始依次排列                               |

**弹性盒子在侧轴方向没有尺寸才能拉伸**

> ```css
>  .number{
>             display: flex;
>             height: 300px;
>             border: 5px solid hsl(0, 0%, 0%);
>             display: flex;
>             align-items: stretch;
>         }
> 
>         .number div {
>             width: 200px;
>             background-color: greenyellow;
>         }
> ```
>
> 

<img src="https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260409224638370.png" alt="image-20260409224638370" style="zoom: 33%;" />

控制单独的弹性盒子

> ```css
> .number{
>             display: flex;
>             height: 300px;
>             border: 5px solid hsl(0, 0%, 0%);
>             display: flex;
>             align-items: flex-end;
>         }
> 
>         .number div {
>             width: 200px;
>             height: 100px;
>             background-color: greenyellow;
>         }
> 
>         .number div:nth-child(2) {
>             align-self: center;
>         }
> ```
>
> 

<img src="https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260409224920197.png" alt="image-20260409224920197" style="zoom:33%;" />

#### 2.3 修改主轴方向

主轴默认在水平方向，侧轴默认在垂直方向

属性名：flex-direction（修改主轴方向，侧轴自动变换到水平方向）

| 属性值         | 效果                       |
| -------------- | -------------------------- |
| row            | 水平方向，从左到右（默认） |
| column         | 垂直方向，从上向下         |
| row-reverse    | 水平方向，从右向左         |
| column-reverse | 垂直方向，从下向上         |

>```css
>.number{
>            display: flex;
>            height: 300px;
>            border: 5px solid hsl(0, 0%, 0%);
>            display: flex;
>            align-items: center;
>            flex-direction: column-reverse;
>        }
>
>        .number div {
>            width: 200px;
>            height: 100px;
>            background-color: greenyellow;
>
>        }
>```

<img src="https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260409225826407.png" alt="image-20260409225826407" style="zoom:33%;" />

#### 2.4 弹性伸缩比

作用：控制弹性盒子的主轴方向的尺寸

属性名：flex

属性值：整数数字，表示占用父级剩余尺寸的份数

**默认情况下，主轴方向尺寸是靠内容撑开，侧轴默认拉伸**

> ```css
> .number{
>             display: flex;
>             height: 200px;
>             border: 5px solid hsl(0, 0%, 0%);
>         }
> 
>         .number div {
>             background-color: greenyellow;
> 
>         }
> 
>         .number div:nth-child(2) {
>             width: 100px;
>             background-color: red;
>             flex: 2;
>         }
> 
>         .number div:nth-child(3) {
>             flex: 1;
>             background-color: pink;
> 
>         }
> ```

<img src="https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260409230753026.png" alt="image-20260409230753026" style="zoom:33%;" />

#### 2.5 弹性盒子换行

弹性盒子可以自动挤压或拉伸，默认情况下，所有弹性盒子都在一行显示

属性名：flex-wrap

属性值

+ wrap：换行（用于父级宽度不够换行，这样就不会挤压）
+ nowrap：不换行（默认）

#### 2.6 行对齐方式

**对单行弹性盒子不生效**

属性名：align-content

| 属性名        | 效果                                                   |
| ------------- | ------------------------------------------------------ |
| flex-start    | 默认值，弹性盒子从**起点**开始依次排列                 |
| flex-end      | 弹性盒子从**终点**开始依次排列                         |
| center        | 弹性盒子沿主轴**居中**排列                             |
| space-between | 弹性盒子沿主轴均匀排列，空白间距均分在弹性盒子**之间** |
| space-around  | 弹性盒子沿主轴均匀排列，空白间距均分在弹性盒子**两侧** |
| space-evenly  | 弹性盒子沿主轴均匀排列，弹性盒子与容器之间间距相等     |

##  定位

灵活的改变盒子在网页中的位置，可以改变标签位置

实现方式：

1. 定位模式：position
2. 边偏移：设置盒子的位置（left，right，top，bottom）

### 1. 相对定位

`position:relative`

1. 改变位置的参照物是自己原来的位置
2. 不脱离标准流，占位（相当于图片往下移，但只有它在动，会有一段空白区域）
3. 只有position：relative，不会发生偏移，必须要加上位置
4. 标签显示模式特点不变

<img src="https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260410130012311.png" alt="image-20260410130012311" style="zoom: 50%;" />

<img src="https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260410130143062.png" alt="image-20260410130143062" style="zoom: 50%;" />

一般不直接使用相对位置，而是用相对位置配合其他使用

### 2. 绝对定位

`position：absolute`

使用场景：子级绝对定位，父级相对定位（子绝父相）

特点：

1. 脱离标准流，不占位
2. 参照物：先找最近的已经定位的祖先元素，如果祖先元素都没有定位，参照浏览器可视区域改位置
3. 显示模式特点改变：宽高生效（即使没有 `display:block`，也具备了行内块的特点）

**定位居中**

实现步骤：

1. 绝对定位
2. 水平，垂直边偏移为50%
3. 子级向左、上移动自身尺寸的一半
4. `transform:translate(-50%,-50%)`(前者指水平方向，宽的50%，后者指垂直方向，高的50%）

>```css
>img {
>            height: 300px;
>            width: 400px;
>    		/*缩放图片*/
>            position: absolute;
>            left: 50%;
>            top: 50%;
>            margin-left: -200px;
>            margin-top: -150px;
>       }
>		
>body {
>        background-color: pink;
>       }
>```
>
>

<img src="https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260411014101026.png" alt="image-20260411014101026" style="zoom: 33%;" />

### 3.固定定位

`postion:fixed`

场景：元素的位置在网页滚动时不会改变

需要添加边偏移

特点：

1. 脱标，不占位
2. 参照物是浏览器窗口
3. 显示模式特点：具备行内块特点

### 4. 黏性定位

position-sticky

### 4. 堆叠层级 z-index

默认效果：按照标签书写顺序，后来者居上（适用于多个标签）

作用：设置定位元素的层级顺序，改变定位元素的显示顺序

> ```CSS
> div {
>         position: absolute;
>         width: 200px;
>         height: 200px;
>        }
> 
>        .box1 {
>         background-color: greenyellow;
>        }
> 
>        .box2 {
>         background-color: palevioletred;
>         left: 100px;
>         top: 100px;
>        }
> ```
>
> ```html
> <div class="box1">one</div>
>    <div class="box2">two</div>
> ```
>
> <img src="https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260411015716411.png" alt="image-20260411015716411" style="zoom: 50%;" />

**怎么实现黄绿色盒子在上面？**

给希望在上的盒子加上 `z-index`

> ```css
>  .box1 {
>         background-color: greenyellow;
>         z-index: 1;
>        }
> ```
>
> <img src="https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260411015945944.png" alt="image-20260411015945944" style="zoom:50%;" />

`z-index`==取值是整数，默认是0，取值越大显示顺序越靠上==

**轮播图的箭头怎么在图片上方？**

用“子绝父相”

### 5. CSS 精灵

**定义**
也叫CSS Sprites，是一种网页图片应用处理方式，把网页中一些背景图片整合到一张图片文件中，再background-position 精确地定位出背景图片的位置

**优点** 减少服务器被请求次数，减轻服务器的压力，提高页面加载速度

**实现步骤**

1. 创建盒子，盒子尺寸与小图尺寸相同
2. 设置盒子背景图为精灵图
3. 添加 background-position 属性，改变背景图位置
   1. 使用PxCook测量小图片左上角坐标
   2. 取==负数==坐标为background-position 属性值（向==左上==移动图片位置）

## 字体图标

### 1. 基础知识

展示的是图标，本质是字体

作用：在网页中添加简单的、颜色单一的小图标

优点 

+ 灵活性  灵活地修改样式，如尺寸、颜色等
+ 轻量级  体积小、渲染快、降低服务器请求次数
+ 兼容性  几乎兼容所有主流浏览器
+ 使用方便  先下载再使用

### 2. 下载和使用

#### 2.1 下载字体

+ iconfont 图标库 [iconfont-阿里巴巴矢量图标库](https://www.iconfont.cn/)
+ 下载字体

![image-20260411023010059](https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260411023010059.png)

#### 2.2 使用字体

1. 引入字体样式表（iconfont.css）
   用link引，引入iconfont.css
2. 标签使用字体图标类名
   1. iconfont  字体图标基本样式（字体名，字体大小等等）
   2. icon-xxx  图标对应的类名（压缩包里html文件中会写）

> ```html
> <span class="iconfont icon-xxx"></span>
> ```

**用font-size调整大小，注意选择器的优先级要高于iconfont类**

### 3. 上传矢量图

作用： 项目特有的图标上传到iconfont图标库，生成字体

将小图做成后缀名为.svg 的文件，在平台上传，选择去除颜色并提交，方便后续调整

## 其他属性

### 1. 垂直对齐方式

属性名 vertical-align

| 属性值   | 效果                                   |
| -------- | -------------------------------------- |
| baseline | 基线（小写字母上下的距离）对齐（默认） |
| top      | 顶部对齐                               |
| middle   | 居中对齐                               |
| bottom   | 底部对齐                               |

**内容中，谁占的高度最高，就给谁加属性**

> ```css
>  div {
>         border: 2px solid #000;
>       }
> 
>       img {
>         vertical-align: middle;
>       }
> ```
>
> <img src="https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260411025127007.png" alt="image-20260411025127007" style="zoom:50%;" />

**不按基线对齐后，图片下面的小空隙也没有了**

**还有方法去除图片下方和盒子边缘的空白吗？**

给图片加 `display block` 属性，将其转化为行内块，就不是基线对齐了。因为浏览器把行内块，行内标签当作文字处理，默认按基线对齐
适用于没有文字，只有图片的情况

### 2. 过渡

作用：可以为一个元素在不同状态（通常指默认状态和鼠标悬停状态）之间切换的时候添加过渡效果

属性名 transition （复合属性）

属性值 过渡的属性 花费时间 (s)

提示：

+ 过渡的属性可以是具体的CSS属性
+ 也可以为all（两个状态属性值不同的所有属性，都产生过渡效果）
+ transition 设置给**元素本身**

### 3. 透明度

作用：设置整个元素的透明度（包含背景和内容）
`background-color` 只能让背景变透明

属性名 opacity

属性值 0-1

+ 0  完全透明（元素不可见）
+ 1 不透明
+ 0-1之间小数  半透明

> ```css
>  div {
>         width: 300px;
>         height: 300px;
>         background-color: gold;
>         opacity: 0.4;
>       }
> ```
>
> 

<img src="https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260411030857526.png" alt="image-20260411030857526" style="zoom:50%;" />



### 4. 光标类型

作用：鼠标悬停在元素上时指针显示样式

属性名：cursor

| 属性值  | 效果                         |
| ------- | ---------------------------- |
| default | 默认值，通常是箭头           |
| pointer | 小手效果，提示用户可以点击   |
| text    | 工字型，提示用户可以选择文字 |
| move    | 十字光标，提示用户可以移动   |

> ```css
> div {
>         width: 300px;
>         height: 300px;
>         background-color: gold;
>         cursor: pointer;
>       }
> 
> ```

移动需要配合js使用

##  grid 布局

作用：将网页划分成一个个网格，可以任意组合不同的网格，做出各种各样的布局

**与flex布局的区别**

+ flex布局是轴线布局，只能只能指定"项目"针对轴线的位置，可以看作是一维布局
+ grid布局是将容器划分成“行”和“列”，产生单元格，然后指定“项目所在”的单元格，可以看作是二维布局，比flex强大

### 1. 基本概念

**容器和项目**

容器：采用网格布局的区域，如下面的最外层的<div>元素
项目：容器内部采用网格定位的子元素，如下面的内层的三个<div>元素

==项目只能是容器的顶层子元素，不包含项目的子元素，grid布局只对项目生效==

> ```html
> <div>
>   <div><p>1</p></div>
>   <div><p>2</p></div>
>   <div><p>3</p></div>
> </div>
> ```
>
> 

**行和列**

水平区域——行  垂直区域——列

**单元格**

行和列的交叉区域

一般 n行和m列会产生 n*m 个单元格

 **网格线**

划分网格的线，称为"网格线"。水平网格线划分出行，垂直网格线划分出列。

一般n行有n + 1根水平网格线，m列有m + 1根垂直网格线

### 2. 容器属性

#### 2.1 display属性

`display: grid`指定一个容器采用网格布局。

默认情况下，容器元素都是块级元素，但也可以设成行内元素。

> ```css
> div {
>     display: inline-grid;
> }
> ```

**设为网格布局后，项目的`float`、`display:inline-blcok`等设置都失效**

#### 2.2 定义列宽、列高grid-template-columns 属性， grid-template-rows 属性

grid-template-columns 属性  定义每一列的列宽

 grid-template-rows 属性  定义每一行的行高

可以使用绝对单位或百分比

> ```css
> #container{
>       display: grid;
>       grid-template-columns: 100px 100px ;
>       grid-template-rows: 100px 100px ;
>         }
> 
>     .item {
>       font-size: 4em;
>       text-align: center;
>       border: 1px solid #e5e4e9;
>     }
> 
>     .item-1 {
>       background-color: #ef342a;
>     }
> 
>     .item-2 {
>       background-color: #f68f26;
>     }
> 
>     .item-3 {
>       background-color: #4ba946;
>     }
> 
>     .item-4 {
>       background-color: #0376c2;
>     }
> 
>     .item-5 {
>       background-color: #c077af;
>     }
> 
>     .item-6 {
>       background-color: #f8d29d;
>     }
> 
>     .item-7 {
>       background-color: #b5a87f;
>     }
> 
>     .item-8 {
>       background-color: #d0e4a9;
>     }
> 
>     .item-9 {
>       background-color: #4dc7ec;
> }
> ```
>
> <img src="https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260411034751967.png" alt="image-20260411034751967" style="zoom:50%;" />

**repeat()**

适用于网格很多的情况，简化重复的值

> ```css
> .container {
>   display: grid;
>   grid-template-columns: repeat(3, 33.33%);
>   grid-template-rows: repeat(3, 33.33%);
> }
> ```

接受两个参数 1.重复的次数 2. 重复的值

重复某种模式

> ```css
> #container{
>       display: grid;
>       grid-template-columns: repeat(2, 100px 20px 80px);
>       grid-template-rows: repeat(3, 100px);
>     }
> ```

重复 100px，20px，80px的规律
<img src="https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260411042335550.png" alt="image-20260411042335550" style="zoom:50%;" />

**auto-fill 关键字**

情况：每一行/列容纳尽可能多的单元格

含义：自动填充

> ```css
> .container {
>   display: grid;
>   grid-template-columns: repeat(auto-fill, 100px);
> }
> ```

表示每列100px，然后自动填充，知道容器装满

**与auto-fit区别**

行为基本相同。但当容器足够宽时，可以在一行容纳所有单元格，并且单元格宽度不固定的时候，`auto-fill`会用空格子填满剩余宽度，`auto-fit`会尽量扩大单元格的宽度

**fr 关键字**

`grid-template-columns: 1fr 1fr;` 
表示后者是前者的两倍，表示一种==比例==关系，常与绝对长度的单位结合使用，如px

```css
.container {
  display: grid;
  grid-template-columns: 150px 1fr 2fr;
}
```

<img src="https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260411042440964.png" alt="image-20260411042440964" style="zoom:50%;" />

**minmax()**

minmax()函数产生一个长度范围，表示长度就在这个范围中，接受两个参数，前者指不小于……，后者指不大于……

**auto 关键字**

表示由浏览器自己决定长度

若有单元格,则该列/行的宽度/高度基本上等于该列单元格的最大宽度，除非单元格内容设置了`min-width`，且这个值大于最大宽度。

**网格线名称**

在属性里，使用方括号，指定每一根网格线的名字
网格布局允许同一根线有多个名字，比如`[fifth-line row-5]`

**两栏式布局怎么写？**

> ```css
> .wrapper {
>   display: grid;
>   grid-template-columns: 70% 30%;
> }
> ```

表示左边栏为70%，右边栏为30%

#### 2.4 设置行、列间距 row-gap 属性， column-gap 属性， gap 属性

`row-gap`用于设置行间距，`column-gap`用于设置列间距。

> ```css
> #container{
>   display: grid;
>   grid-template-columns: 100px 100px 100px;
>   grid-template-rows: 100px 100px 100px;
>   grid-row-gap: 20px;
>   grid-column-gap: 20px;
> }
> ```

<img src="https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260411042600798.png" alt="image-20260411042600798" style="zoom: 33%;" />

`gap`属性是`column-gap`和`row-gap`的合并简写形式

> ```css
> gap: <row-gap> <column-gap>;
> ```

如果`gap`省略了第二个值，浏览器认为第二个值等于第一个值

#### 2.5 定义区域 grid-template-areas 属性

`grid-template-areas`属性用于定义区域。区域由一个或多个单元格组成

多个单元格合并成一个区域的写法如下。

> ```css
> grid-template-areas: 'a a a'
>                      'b b b'
>                      'c c c';
> ```

如果某些区域不需要利用，则使用"点"（`.`）表示，指没有用到该单元格，或者该单元格不属于任何区域

**注意**
区域的命名会影响到网格线。每个区域的起始网格线，会自动命名为`区域名-start`，终止网格线自动命名为`区域名-end`

#### 2.6 放置容器中子元素的位置  grid-auto-flow 属性

划分网格以后，容器的子元素会按照顺序，自动放置在每一个网格
这个顺序由`grid-auto-flow`属性决定，默认值是`row`，即"先行后列"。也可以将它设成`column`，变成"先列后行"

> ```css
> #container{
>   display: grid;
>   grid-template-columns: 100px 100px 100px;
>   grid-template-rows: 100px 100px 100px;
>   grid-auto-flow: column;
> }
> ```
>
> <img src="https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260411042704616.png" alt="image-20260411042704616" style="zoom: 50%;" />

`grid-auto-flow`属性除了设置成`row`和`column`，还可以设成`row dense`和`column dense`。这两个值主要用于，某些项目指定位置以后，剩下的项目怎么自动放置

> ```css
> #container{
>   display: grid;
>   grid-template-columns: 100px 100px 100px;
>   grid-template-rows: 100px 100px 100px;
>   grid-auto-flow: row;
> }
> ```

<img src="https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260411042833252.png" alt="image-20260411042833252" style="zoom:50%;" />

#### 2.7 设置单元格内容位置  justify-items 属性， align-items 属性， place-items 属性

`justify-items`属性设置单元格内容的水平位置（左中右），`align-items`属性设置单元格内容的垂直位置（上中下）

这两个属性的写法完全相同

属性值

> - start：对齐单元格的起始边缘
> - end：对齐单元格的结束边缘
> - center：单元格内部居中
> - stretch：拉伸，占满单元格的整个宽度（默认值）

> ```css
> #container{
>   display: grid;
>   grid-template-columns: 100px 100px 100px;
>   grid-template-rows: 100px 100px 100px;
>   justify-items: start;
> }
> ```

<img src="https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260411043011899.png" alt="image-20260411043011899" style="zoom:50%;" />

`place-items`属性是`align-items`属性和`justify-items`属性的合并简写形式

> ```css
> place-items: <align-items> <justify-items>;
> ```

如果省略第二个值，则浏览器认为与第一个值相等

#### 2.8设置整个内容区域在容器里的位置   justify-content 属性， align-content 属性， place-content 属性

`justify-content`属性是整个内容区域在容器里面的水平位置（左中右），`align-content`属性是整个内容区域的垂直位置（上中下）

这两个属性的写法完全相同

属性值

> - start - 对齐容器的起始边框
> - end - 对齐容器的结束边框
> - center - 容器内部居中
> - stretch - 项目大小没有指定时，拉伸占据整个网格容器
> - space-around - 每个项目两侧的间隔相等。所以，项目之间的间隔比项目与容器边框的间隔大一倍
> - space-between - 项目与项目的间隔相等，项目与容器边框之间没有间隔
> - space-evenly - 项目与项目的间隔相等，项目与容器边框之间也是同样长度的间隔

`place-content`属性是`align-content`属性和`justify-content`属性的合并简写形式

> ```css
> place-content: <align-content> <justify-content>
> ```

如果省略第二个值，浏览器就会假定第二个值等于第一个值

#### 2.9设置浏览器自动创建的多余网格的列宽和行高 grid-auto-columns 属性， grid-auto-rows 属性

`grid-auto-columns`属性和`grid-auto-rows`属性用来设置，浏览器自动创建的多余网格的列宽和行高
它们的写法与`grid-template-columns`和`grid-template-rows`完全相同
如果不指定这两个属性，浏览器完全根据单元格内容的大小，决定新增网格的列宽和行高。

#### 2.10 grid-template 属性， grid 属性

`grid-template`属性是`grid-template-columns`、`grid-template-rows`和`grid-template-areas`这三个属性的合并简写形式。

`grid`属性是`grid-template-rows`、`grid-template-columns`、`grid-template-areas`、 `grid-auto-rows`、`grid-auto-columns`、`grid-auto-flow`这六个属性的合并简写形式。
**不建议使用**

### 3.项目属性

#### 3.1 指定项目的四个边框  grid-column-start 属性， grid-column-end 属性， grid-row-start 属性， grid-row-end 属性

指定项目位置的方法就是指定项目的四个边框，分别定位在哪根网格线

- `grid-column-start`属性：左边框所在的垂直网格线
- `grid-column-end`属性：右边框所在的垂直网格线
- `grid-row-start`属性：上边框所在的水平网格线
- `grid-row-end`属性：下边框所在的水平网格线

> ```css
> .item-1 {
>   background-color: #ef342a;
>   grid-column-start: 2;
>   grid-column-end: 4;
> }
> ```
>
> <img src="https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260411043202561.png" alt="image-20260411043202561" style="zoom:50%;" />

这四个属性的值还可以使用`span`关键字，指左右边框（上下边框）之间跨越多少个网格

如果产生了项目的重叠，则使用`z-index`属性指定项目的重叠顺序

#### 3.2 grid-column 属性， grid-row 属性

`grid-column`属性是`grid-column-start`和`grid-column-end`的合并简写形式
`grid-row`属性是`grid-row-start`属性和`grid-row-end`的合并简写形式

> ```css
> .item {
>   grid-column: <start-line> / <end-line>;
>   grid-row: <start-line> / <end-line>;
> }
> ```

<img src="https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260411043318661.png" alt="image-20260411043318661" style="zoom: 50%;" />

这两个属性之中，可以使用`span`关键字，表示跨越多少个网格
斜杠以及后面的部分可以省略，默认跨越一个网格

#### 3.3指定项目放在哪一个区域   grid-area 属性

`grid-area`属性指定项目放在哪一个区域

> ```css
> #container{
>   display: grid;
>   grid-template-columns: 100px 100px 100px;
>   grid-template-rows: 100px 100px 100px;
>   grid-template-areas: 'a b c'
>                      'd e f'
>                      'g h i';
> 			}
> .item-1 {
>   background-color: #ef342a;
>   grid-area: e;
> 		}
> ```
>
> <img src="https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260411043452501.png" alt="image-20260411043452501" style="zoom:50%;" />

`grid-area`属性还可用作`grid-row-start`、`grid-column-start`、`grid-row-end`、`grid-column-end`的合并简写形式，直接指定项目的位置

> ```css
> .item {
>   grid-area: <row-start> / <column-start> / <row-end> / <column-end>;
> ```

#### 3.4 设置单元格内容的位置  justify-self 属性， align-self 属性， place-self 属性

`justify-self`属性设置单元格内容的水平位置（左中右），跟`justify-items`属性的用法完全一致，但只作用于==单个==项目

`align-self`属性设置单元格内容的垂直位置（上中下），跟`align-items`属性的用法完全一致，也是只作用于==单个==项目

属性值

- start：对齐单元格的起始边缘
- end：对齐单元格的结束边缘
- center：单元格内部居中
- stretch：拉伸，占满单元格的整个宽度（默认值）

`place-self`属性是`align-self`属性和`justify-self`属性的合并简写形式

> ```css
> place-self: <align-self> <justify-self>;
> ```

如果省略第二个值，`place-self`属性会认为这两个值相等
