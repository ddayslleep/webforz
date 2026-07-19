

## Ajax

特点：在==不刷新==的情况下就可以实现效果

![image-20260520232251192](https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260520232251192.png)

用户要看就请求，不看就不请求——提高页面加载速度

### XML简介

![image-20260520233047587](https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260520233047587.png)

![image-20260520233542453](https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260520233542453.png)

![image-20260520234724527](https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260520234724527.png)

名字 空格 内容

![image-20260520234958846](https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260520234958846.png)

**怎么查看响应报文和请求报文**

![image-20260520235058627](https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260520235058627.png)

header中注意看响应头和请求头

响应行在response

### express框架

```js
// 引入express
const express = require('express')
const { request } = require('node:http')
// 创建应用对象
const app = express()
// 创建路由规则 request是对请求报文的封装，response是对响应报文的封装
app.get('/server',(request,response)=>{
    // 设置响应头
    response.setHeader('Access-Controll-Allow-Origin','*')//*代表所有的响应头都能使用，设置允许跨域
    //设置响应体
    response.send('hello')
});
// 监听端口启动服务
app.listen(8000,()=>{
    console.log('1')
})

```

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    
</head>
<body>
    
</body>
</html>
<script>
    //创建对象
    const xhr = new XMLHttpRequest();
    //初始化 设置请求方法和url
    xhr.open('GET','http://127.0.0.1:8000/server')
    //发送
    xhr.send()
    //事件绑定 处理服务端返回的结果 on when 当...时候
    //readystate 是 xhr对象中的属性 ，表示状态
    //0——未初始化 1——open方法调用完毕 2——send方法调用完毕 3——服务端返回部分接口 4——服务端返回所有接口
    //change 改变
    xhr.onreadystatechange = function(){
        //判断
        if(xhr.readyState === 4){
            //判断响应状态码 200 404 403 401 500
            //2开头都代表成功
            if(xhr.status >= 200 && xhr.status <300){
                //处理结果 行 头 空行 体
                //响应行
                console.log(xhr.status)//状态码
                console.log(xhr.statusText) //状态字符串
                console.log(xhr.getAllResponseHeaders())//所有响应头
                console.log(xhr.response)//响应体
                //设置result的文本
                result.innerHTML = xhr.respnse
            }
        }
    }
</script>
```

### 怎么设置ajax的参数？

用&连接 ？分割  `?` 就是用来在 URL 后面拼接参数的——http协议的标准写法
`地址?参数名=值`

`http://127.0.0.1:8000/server?a=200&b=300`

### ajax发送post请求

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        #result {
            width: 200px;
            height: 100px;
            background: pink;
        }
    </style>
</head>
<body>
      <div id="result"></div>
</body>
</html>
<script>
    //获取对象
    const result = document.getElementById('result')
    //绑定事件
    result.addEventListener("mouseover",function(){
        //创建对象
        const xhr = new XMLHttpRequest()
        //初始化 设置类型与url
        xhr.open('POST','http://127.0.0.1:8000/server')
        xhr.send()
    xhr.onreadystatechange = function(){
        //判断
        if(xhr.readyState === 4){
            if(xhr.status >= 200 && xhr.status <300){
                //处理结果
                result.innerHTML = xhr.response
            }
        }
    }
    })
</script>
```

```js
const express = require('express')
const app = express()

app.get('/server', (request, response)=>{
    response.setHeader('Access-Control-Allow-Origin','*')
    response.send('hello 成功啦！')
})

app.post('/server', (request, response)=>{
    response.setHeader('Access-Control-Allow-Origin','*')
    response.send('hello 成功啦！post')
})


app.listen(8000, ()=>{
    console.log('服务启动成功')
})
```

### post怎么设置参数

` xhr.send('a:100&b:200')`

`xhr.send('a=100&b=200')`

`xhr.send('123')`
非常灵活，只要服务器能处理即可，以第一种居多

### 设置请求头信息

在open后面设置

```js
//xhr.setRequestHeader('头的名字','头的值')
        xhr.setRequestHeader('Content-Type','applicication/x-www-form-urlencoded')
        //Content-Type 设置请求体类型  applicication/x-www-form-urlencoded 设置参数查询字符串的类型，固定写法
```

自定义的头名字，浏览器会有保护机制

**all是可以接收任意类型的请求**

****

```js
app.all('/server', (request, response)=>{
    response.setHeader('Access-Control-Allow-Origin','*')
    response.send('hello 成功啦！post')
})
```

### 服务端响应json数据

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        #result {
            width: 200px;
            height: 100px;
            background: pink;
        }
    </style>
</head>
<body>
      <div id="result"></div>
      <script>
    const result = document.getElementById('result')
    //绑定键盘按下事件
    window.onkeydown = function(){
        //向后端发送请求
        const xhr = new XMLHttpRequest()
        xhr.responseType = 'json'
        //初始化
        xhr.open('GET','http://127.0.0.1:8000/json-server')
        //发送
        xhr.send()   
        //事件绑定
        xhr.onreadystatechange = function(){
            if(xhr.readyState === 4){
                if(xhr.status >= 200 &&xhr.status <300){
                    //result.innerHTML = xhr.response 
                    //在ajax中用字符串转换，得到的是一个数组，对于多组数据，想要得到其中的数据特别不方便
                    //1.手动对数据转换
                    //let data = JSON.parse(xhr.response)
                    //result.innerHTML = data.name
                    //2.自动转换
                    //通过设置响应体数据的类型，写在了发送请求的后面
                    result.innerHTML = xhr.response.name
                    
                }
            }
        }
    }
</script>
</body>

```

```js
const express = require('express')
const app = express()

app.all('/json-server', (request, response)=>{
    response.setHeader('Access-Control-Allow-Origin','*')
    // 响应一个数据
    const data = {
        name:'abc'
    }
    // 对对象进行字符串转换
    let str = JSON.stringify(data)
    //设置响应体
    response.send(str)
})


app.listen(8000, ()=>{
    console.log('服务启动成功')
})
```

### ajax-ie缓冲问题

ie浏览器会对ajax的响应做一个缓存，导致第二次响应是本地的缓存而非最近的数据，时效性不强
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        #result {
            width: 200px;
            height: 100px;
            background: pink;
        }
    </style>
</head>
<body>
    <button>点击发送请求 </button>
      <div id="result"></div>
      <script>
        const btn = document.getElementsByTagName('button')[0]
        const result = document.querySelector('#result ')
        btn.addEventListener('click',function(){
            const xhr = new XMLHttpRequest()
            //xhr.open('GET','http://127.0.0.1:8000/ie')
            xhr.open('GET','http://127.0.0.1:8000/ie?t='+Date.now())
            //推荐带时间戳的方式，这样使每次的url都不一样，浏览器就会发送新请求，不会发送本地缓存
            xhr.send()
            xhr.onreadystatechange = function(){
                 if(xhr.readyState === 4){
                if(xhr.status >= 200 &&xhr.status <300){
                    result.innerHTML = xhr.response
                    
                }
            }
            }
        })
</script>
</body>

```

```js
const express = require('express')
const app = express()

//针对IE缓存
app.all('/ie', (request, response)=>{
    response.setHeader('Access-Control-Allow-Origin','*')
    response.send('hello ie！!')
})

app.listen(8000, ()=>{
    console.log('服务启动成功')
})
```

### AJAX请求超时和网络异常处理

作用：保证后端内容可以及时响应

比方说设置了2s，但是2s后没有反应，我们就要给后端一个提醒，告诉他超时了

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        #result {
            width: 200px;
            height: 100px;
            background: pink;
        }
    </style>
</head>
<body>
    <button>点击发送请求 </button>
      <div id="result"></div>
      <script>
        const btn = document.getElementsByTagName('button')[0]
        const result = document.querySelector('#result')
        btn.addEventListener('click',function(){
            const xhr = new XMLHttpRequest()
            //超时设置(以两秒为例)
            xhr.timeout = 2000
            //超时回调
            xhr.ontimeout = function(){
                alert("网络异常，请稍后重试")

            } 
            // 网络异常回调
            xhr.onerror = function(){
                alert("你的网络似乎出了一些问题")
            }
            //浏览器中检查——网络中选择脱机可以测试
            xhr.open('GET','http://127.0.0.1:8000/delay')
            xhr.send()
            xhr.onreadystatechange = function(){
                 if(xhr.readyState === 4){
                if(xhr.status >= 200 &&xhr.status <300){
                    result.innerHTML = xhr.response
                    
                }
            }
            }
        })
</script>
</body>

```

```js
const express = require('express')
const app = express()
//延时响应
app.all('/delay', (request, response)=>{
    response.setHeader('Access-Control-Allow-Origin','*')
    setTimeout(()=>{
    response.send('hi~')
    },3000)

})
app.listen(8000, ()=>{
    console.log('服务启动成功')
})
```

### ajax取消请求

适用场景：发送请求后，没有得到结果之后，手动取消请求

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <button>点击发送</button>
    <button>点击取消</button>
      <script>
        const btns = document.querySelectorAll('button')
        let x =null//注意不同的函数里，只有全局
        btns[0].onclick = function(){
            x = new XMLHttpRequest()
            x.open("GET","http://127.0.0.1:8000/delay")
            x.send()
        }

        //abort (属于x对象的)
        btns[1].onclick = function(){
            x.abort()
        }
</script>
</body>

```

```js
const express = require('express')
const app = express()
//延时响应
app.all('/delay', (request, response)=>{
    response.setHeader('Access-Control-Allow-Origin','*')
    setTimeout(()=>{
    response.send('hi~')
    },3000)

})
app.listen(8000, ()=>{
    console.log('服务启动成功')
})
```

### ajax请求重复发送请求

适用场景：响应很慢的时候，用户不断发送请求，那么浏览器就会不断接收请求，服务器压力就很大

思路：取消最新请求之前的所有请求，让服务器可以接收到最新的请求

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <button>点击发送</button>
      <script>
        const btns = document.querySelectorAll('button')
        let x =null//注意不同的函数里，只有全局
        //标识变量
        let isSending = false //是否正在发送ajax请求
        btns[0].onclick = function(){
            //判断标识变量
            if(isSending) x.abort()//如果正在发送，则取消发送，创建一个新的请求
            x = new XMLHttpRequest()
            //修改标识变量的值
            isSending = true
            x.open("GET","http://127.0.0.1:8000/delay")
            x.send()
            x.onreadystatechange = function(){
                if(x.readyState === 4){
                    //修改标识变量
                    isSending = false
                }
            }
        }

        //abort (属于x对象的)
        btns[1].onclick = function(){
            x.abort()
        }
</script>
</body>

```

```js
const express = require('express')
const app = express()
//延时响应
app.all('/delay', (request, response)=>{
    response.setHeader('Access-Control-Allow-Origin','*')
    setTimeout(()=>{
    response.send('hi~')
    },3000)

})
app.listen(8000, ()=>{
    console.log('服务启动成功')
})
```

## jQuery 中的Ajax

### get请求和post请求

![image-20260521140650564](https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260521140650564.png)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script src="https://cdn.bootcdn.net/ajax/libs/jquery/3.7.1/jquery.js"></script>
</head>
<body>
    <div class="container">
        <h2 class="page-header">jQuery发送AJAX请求</h2>
        <button class="btn btn-primary">GET</button>
        <button class="btn btn-danger">POST</button>
        <button class="btn btn-info">通用型方法ajax</button>
    </div>
      <script>
        //1.发送get请求
      $('button').eq(0).click(function(){
        $.get('http://127.0.0.1:8000/jquery-server',{a:100,b:200},function(data){
            console.log(data)
        })
        //第一个是给谁发请求,第二个是发什么请求（参数对象），第三个是回调
      })
      //2.发送post请求
      $('button').eq(1).click(function(){
        $.post('http://127.0.0.1:8000/jquery-server',{a:100,b:200},function(data){
            console.log(data)
        })
        //post的请求并不会像get一样，在网络中的请求中可见
      })
        //3.响应体类型
      $('button').eq(0).click(function(){
        $.get('http://127.0.0.1:8000/jquery-server',{a:100,b:200},function(data){
            console.log(data)
        },'json')
        //加了json是一个对象，不加json是一个参数
      })
</script>
</body>

```

```js
const express = require('express')
const app = express()
//jQuery服务
/* app.all('/jquery-server', (request, response)=>{
    response.setHeader('Access-Control-Allow-Origin','*')
    response.send('nct in the house')

}) */
//jQuery服务(响应体)
app.all('/jquery-server', (request, response)=>{
    response.setHeader('Access-Control-Allow-Origin','*')
    const data = {name:'hi'}
    response.send(JSON.stringify(data))

})
//写all的话get和post都能发，单独的get就不能发post
app.listen(8000, ()=>{
    console.log('服务启动成功')
})
```

![image-20260521142705137](https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260521142705137.png)

**有json是对象，没加json是参数**

### 通用方法发送请求

**功能性更强,适用于个性化处理**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script src="https://cdn.bootcdn.net/ajax/libs/jquery/3.7.1/jquery.js"></script>
</head>
<body>
    <div class="container">
        <h2 class="page-header">jQuery发送AJAX请求</h2>
        <button class="btn btn-primary">GET</button>
        <button class="btn btn-danger">POST</button>
        <button class="btn btn-info">通用型方法ajax</button>
    </div>
      <script>
      $('button').eq(2).click(function(){
        $.ajax({
            //url
            url:'http://127.0.0.1:8000/jquery-server',
            //参数
            data:{a:100,b:200},
            //请求类型
            type:'GET',
            //响应体结果
            dataType:'json',
            //成功的回调
            success:function(data){
                console.log('hi')
            },
            //超时事件
            timeout:2000,
            //失败的回调
            error:function(){
                console.log('出错了')
            },
            //头信息
            headers:{
                c:300,
                d:400
            }
            //头信息是自定义，不是预定义，所以需要做一个设置
      })
      })
</script>
</body>

```

```js
const express = require('express')
const app = express()
//jQuery服务
app.all('/jquery-server', (request, response)=>{
    response.setHeader('Access-Control-Allow-Origin','*')
    response.setHeader('Access-Control-Allow-Headers','*')
    //第二个是给自定义头文件设置的
    // response.send('nct in the house')
    const data = {name:'hi'}
    response.send(JSON.stringify(data))

})
app.listen(8000, ()=>{
    console.log('服务启动成功')
})
```

## Axios

### Axios发送AJAX请求

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
</head>
    <body>
    <div class="container">
        <button>GET</button>
        <button>POST</button>
        <button>ajax</button>
    </div>
     <script>
        const btns = document.querySelectorAll('button')
        //配置baseURL
        axios.defaults.baseURL = 'http://127.0.0.1:8000'
        btns[0].onclick = function(){
            //GET 请求
            axios.get('/axios-server',{
                //url 参数
                params:{
                    id:100,
                    vip:7
                },
                //请求头信息
                headers: {
                    name:'hi',
                    age:20
                }
            }).then(value=> {
                console.log(value)
            })
        }
        btns[1].onclick = function(){
            axios.post('/axios-server',{
                //url
                params: {
                    id:200,
                    vip:9
                },
                //请求头参数
                headers: {
                    height:180,
                    weight:180,
                },
                //请求体
                data: {
                    username:'admin',
                    password:'admin'
                }
            })
        }
     </script>
</body>
</html>

```

```js
const express = require('express')
const app = express()
//axios服务
app.all('/axios-server', (request, response)=>{
    response.setHeader('Access-Control-Allow-Origin','*')
    response.setHeader('Access-Control-Allow-Headers','*')
    //第二个是给自定义头文件设置的
    // response.send('nct in the house')
    const data = {name:'hi'}
    response.send(JSON.stringify(data))

})
app.listen(8000, ()=>{
    console.log('服务启动成功')
})
```

### Axios函数发送AJAX请求

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
</head>
    <body>
    <div class="container">
        <button>GET</button>
        <button>POST</button>
        <button>ajax</button>
    </div>
     <script>
        const btns = document.querySelectorAll('button')
        //配置baseURL
        axios.defaults.baseURL = 'http://127.0.0.1:8000'
        btns[0].onclick = function(){
            //GET 请求
            axios.get('/axios-server',{
                //url 参数
                params:{
                    id:100,
                    vip:7
                },
                //请求头信息
                headers: {
                    name:'hi',
                    age:20
                }
            }).then(value=> {
                console.log(value)
            })
        }
        btns[1].onclick = function(){
            axios.post('/axios-server',{
                //url
                params: {
                    id:200,
                    vip:9
                },
                //请求头参数
                headers: {
                    height:180,
                    weight:180,
                },
                //请求体
                data: {
                    username:'admin',
                    password:'admin'
                }
            })
        }
        btns[2].onclick = function(){
            axios({
                //请求方法
                method:'POST',
                //url
                url:'/axios-server',
                //url参数
                params: {
                    vip:10,
                    level:30
                },
                //头信息
                headers: {
                    a:100,
                    b:200
                },
                //请求体参数
                data:{
                    username:'admin',
                    password:'admin'
                }
            }).then(response=>{
                console.log(response);
                //响应状态码
                console.log(response.status)
                //响应状态字符串
                console.log(response.statusText)
                //响应头信息
                console.log(response.headers)
                //响应体
                console.log(response.data)
            })
        }
     </script>
</body>
</html>

```

```js
const express = require('express')
const app = express()
//axios服务
app.all('/axios-server', (request, response)=>{
    response.setHeader('Access-Control-Allow-Origin','*')
    response.setHeader('Access-Control-Allow-Headers','*')
    //第二个是给自定义头文件设置的
    // response.send('nct in the house')
    const data = {name:'hi'}
    response.send(JSON.stringify(data))

})
app.listen(8000, ()=>{
    console.log('服务启动成功')
})
```

### fetch函数发送AJAX函数

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
</head>
    <body>
    <div class="container">
        <button>AJAX</button>
    </div>
     <script>
        const btn = document.querySelector('button')
        btn.onclick = function(){
            fetch('http://127.0.0.1:8000/fetch-server',{
                //请求方法
                method:'POST',
                //请求头
                headers:{
                    name:'hi'
                },
                //请求体
                body:'username=admin&password=admin'
            }).then(response =>{
                //return response.text()
                return response.json()
            })
        }
     </script>
</body>
</html>

```

```js
const express = require('express')
const app = express()
//fetch服务
app.all('/fetch-server', (request, response)=>{
    response.setHeader('Access-Control-Allow-Origin','*')
    response.setHeader('Access-Control-Allow-Headers','*')
    //第二个是给自定义头文件设置的
    // response.send('nct in the house')
    const data = {name:'hi'}
    response.send(JSON.stringify(data))

})
app.listen(8000, ()=>{
    console.log('服务启动成功')
})
```

### 同源策略

浏览器的一种安全策略

同源：协议、域名、端口号必须完全相同

违背同源策略就是跨域

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <h1>hi~</h1>
    <button>获取用户数据</button>
    <script>
        const btn = document.querySelector('button')
        btn.onclick = function(){
            const x = new XMLHttpRequest()
            //因为这里是满足同源策略的，所以url可以简写
            x.open("GET",'/data')
            x.send()
            x.onreadystatechange = function(){
                if(x.readyState === 4){
                    if(x.status >=200 && x.status <300){
                        console.log(x.response)
                    }
                }
            }
        }
    </script>
</body>
</html>
```

```js
const express = require('express')
const app = express()
app.get('/home',(request,response)=>{
    //响应一个页面
    response.sendFile(__dirname+'/index.html')
})
app.get('/data',(request,response)=>{
    response.send('用户数据')
})
app.listen(9000,()=>{
    console.log("成功启动")
})
```

### jsonp

![image-20260521194133585](https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260521194133585.png)

script标签本身就具有跨越属性

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        #result{
            width: 300px;
            height: 100px;
            border: solid 1px #78a;
        }
    </style>
</head>
<body>
    <div id="result"></div>
    <script>
        //处理数据
function handle(data){
    //获取元素
    const result = document.getElementById('result')
    result.innerHTML = data.name
}
</script>
    <script src="http://127.0.0.1:8000">
    </script>
</body>
</html>
```

```js
const express = require('express')
const app = express()
//jsonp服务
app.all('/jsonp-server', (request, response)=>{
    // response.send('hello')
    const data = {
        name:'hi'
    }
    //将数据转化成字符串
    let str = JSON.stringify(data)
    //返回结果
    response.end(`handle(${str})`)
})
app.listen(8000, ()=>{
    console.log('服务启动成功')
})
```

### 原生jsonp实验

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    用户名：<input type="text" id="username">
    <p></p>
    <script>
        //获取input元素
        const input = document.querySelector('input')
        const p = document.querySelector('p')
        //声明handle函数
        function handle(data){
            input.style.border = "solid 1px #f00"
            //修改p标签的提示文本
            p.innerHTML = data.msg
        }
        //绑定事件
        input.onblur = function(){
            //获取用户的输入值
            let username = this.value
            //向服务端发送请求，检测用户名是否存在
            //1.创建 script 标签
            const script = document.createElement('script')
            //2.设置标签的src属性
            script.src = 'http://127.0.0.1:8000/check-username'
            //3.将script 插入到文档中
            document.body.appendChild(script)
        }   
    </script>
</body>
</html>
```

```js
const express = require('express')
const app = express()
//用户名检测是否存在
app.all('/check-username', (request, response)=>{
    const data = {
        exist:1,
        msg:'用户名已经存在'
    }
    //将数据转化成字符串
    let str = JSON.stringify(data)
    //返回结果
    response.end(`handle(${str})`)
})
app.listen(8000, ()=>{
    console.log('服务启动成功')
})
```

### jQuery发送jsonp请求

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        #result{
            width: 300px;
            height: 100px;
            border: solid 1px #089;
        }
    </style>
    <script src="https://cdn.bootcdn.net/ajax/libs/jquery/3.7.1/jquery.js"></script>
</head>
<body>
    <button>点击发送jsonp请求</button>
    <div id="result"></div>
    <script>
        $('button').eq(0).click(function(){
            $.getJSON('http://127.0.0.1:8000/jquery-jsonp-server?callback=?',function(data){
                $('#result').html(`
                名称：${data.name}<br>
                校区：${data.city}
                `)
            })
        })
    </script>
</body>
</html>
```

```js
const express = require('express')
const app = express()
//fetch服务
app.all('/fetch-server', (request, response)=>{
    response.setHeader('Access-Control-Allow-Origin','*')
    response.setHeader('Access-Control-Allow-Headers','*')
    //第二个是给自定义头文件设置的
    // response.send('nct in the house')
    const data = {name:'hi'}
    response.send(JSON.stringify(data))

})
//fetch服务
app.all('/jsonp-server', (request, response)=>{
    // response.send('hello')
    const data = {
        name:'hi'
    }
    //将数据转化成字符串
    let str = JSON.stringify(data)
    //返回结果
    response.end(`handle(${str})`)
})
//用户名检测是否存在
app.all('/jquery-jsonp-server', (request, response)=>{
    const data = {
        name:'hi',
        city:['1','2','3']
    }
    //将数据转化成字符串
    let str = JSON.stringify(data)
    //接收 callback 参数
    let cb = request.query.callback
    //返回结果
    response.end(`${cb}(${str})`)
})
app.listen(8000, ()=>{
    console.log('服务启动成功')
})
```

### CORS

![image-20260521203209523](https://team-image-zhuoyin.oss-cn-beijing.aliyuncs.com/2025013816/image-20260521203209523.png)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        #result{
            width: 300px;
            height: 100px;
            border: solid 1px #089;
        }
    </style>
    <script src="https://cdn.bootcdn.net/ajax/libs/jquery/3.7.1/jquery.js"></script>
</head>
<body>
    <button>发送请求</button>
    <div id="result"></div>
    <script>
        const btn = document.querySelector('button')
        btn.onclick = function(){
            //1.创建对象
        const x = new XMLHttpRequest
        //2.初始化设置
        x.open("GET","http://127.0.0.1:8000/cors-server")
        //3.发送
        x.send()
        //4.绑定事件
        x.onreadystatechange = function(){
            if(x.readyState === 4){
                if(x.status >=200 && x.status <300){
                    //输出响应体
                    console.log(x.response)
                }
            }
        }
        }
    </script>
</body>
</html>
```

```js
const express = require('express')
const app = express()
//fetch服务
app.all('/fetch-server', (request, response)=>{
    response.setHeader('Access-Control-Allow-Origin','*')
    response.setHeader('Access-Control-Allow-Headers','*')
    //第二个是给自定义头文件设置的
    // response.send('nct in the house')
    const data = {name:'hi'}
    response.send(JSON.stringify(data))

})
//fetch服务
app.all('/jsonp-server', (request, response)=>{
    // response.send('hello')
    const data = {
        name:'hi'
    }
    //将数据转化成字符串
    let str = JSON.stringify(data)
    //返回结果
    response.end(`handle(${str})`)
})
//用户名检测是否存在
app.all('/jquery-jsonp-server', (request, response)=>{
    const data = {
        name:'hi',
        city:['1','2','3']
    }
    //将数据转化成字符串
    let str = JSON.stringify(data)
    //接收 callback 参数
    let cb = request.query.callback
    //返回结果
    response.end(`${cb}(${str})`)
})
app.all('/cors-server', (request, response)=>{
    //设置响应头
    response.setHeader("Access-Control-Allow-Origin","*")
    response.send('hello')
})
app.listen(8000, ()=>{
    console.log('服务启动成功')
})
```

