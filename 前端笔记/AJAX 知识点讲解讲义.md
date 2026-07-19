# AJAX 知识点讲解讲义

---

## 一、什么是 AJAX？

**AJAX** 全称 **Asynchronous JavaScript And XML**（异步 JavaScript 和 XML）。

简单说，它是一种**在不刷新整个页面的情况下，和服务器交换数据并更新部分网页**的技术。

传统网页交互模式：
- 用户操作 → 整个页面重新加载 → 服务器返回新页面。

AJAX 交互模式：
- 用户操作 → JavaScript 异步发送请求 → 服务器返回数据（常见为 JSON 或 XML） → JavaScript 拿到数据后，只更新页面的一小部分。

---

## 二、为什么需要 AJAX？

1. **提升用户体验**：页面不会因为一个请求而整体刷新、白屏、重新加载所有资源。
2. **节省带宽**：只传输需要的数据，而不是整个 HTML 页面。
3. **实现前后端分离**：前端专注 UI 交互，后端专注提供 API 数据接口。

常见应用场景：
- 搜索引擎的搜索提示（输入时下拉提示）
- 表单的局部校验（用户名是否已占用）
- 无限滚动加载更多内容
- 实时聊天消息展示

## 三.同步与异步的本质区别

**同步请求**（不推荐）：

- 发送请求后，浏览器会“卡死”，直到服务器返回结果才继续执行后续代码。
- 用户体验极差，可能造成页面假死。

**异步请求**（默认）：

- 请求发出后，浏览器继续执行后续代码，不会等待。
- 当响应返回时，通过回调、Promise 等方式处理结果。

深入理解异步：JavaScript 是单线程的，依靠 **事件循环** 机制来处理异步任务。AJAX 请求交给浏览器的网络线程处理，完成后将回调放入任务队列，等待主线程空闲时执行。

```js
console.log('1');
const xhr = new XMLHttpRequest();
xhr.open('GET', '/api/delay', true);
xhr.onreadystatechange = function() {
  if (xhr.readyState === 4) console.log('3');
};
xhr.send();
console.log('2');
// 输出顺序：1 → 2 → 3
```

## 四、AJAX 的核心工作流程

一次完整的 AJAX 请求包含以下四个阶段：

1. 创建 XMLHttpRequest 对象
2. 配置请求（设置请求方式、URL、是否异步等）
3. 发送请求
4. 监听状态变化，处理服务器返回的数据

---

## 五、原生 AJAX —— XMLHttpRequest 对象

### 5.1 创建对象
```js
const xhr = new XMLHttpRequest();
```

### 5.2 配置请求 —— `open` 方法
```js
xhr.open(method, url, async);
```
- `method`：请求方式，常见为 `"GET"` 或 `"POST"` 等
- `url`：请求的地址
- `async`：是否异步，默认 `true`

示例：
```js
xhr.open('GET', '/api/users', true);
```

### 5.3 设置请求头（可选）
```js
xhr.setRequestHeader('Content-Type', 'application/json');
```

### 5.4 发送请求 —— `send` 方法
- GET 请求：不需要发送请求体
  ```js
  xhr.send();
  ```
- POST 请求：需要将数据放入 `send()` 中
  ```js
  xhr.send(JSON.stringify({ name: 'Tom', age: 20 }));
  ```

### 5.5 监听响应 —— `onreadystatechange` 事件
`XMLHttpRequest` 对象有一个 `readyState` 属性，表示请求的状态：

| readyState | 含义                           |
| ---------- | ------------------------------ |
| 0          | 未初始化，尚未调用 open()      |
| 1          | 已调用 open()，尚未调用 send() |
| 2          | 已调用 send()，尚未收到响应    |
| 3          | 正在接收响应数据               |
| 4          | 响应数据接收完毕               |

我们一般只关心 `readyState === 4` 的情况。

同时还有一个 `status` 属性，表示 HTTP 状态码（如 200 成功，404 未找到等）。

典型监听写法：
```js
xhr.onreadystatechange = function() {
  if (xhr.readyState === 4) {
    if (xhr.status === 200) {
      // 成功获取数据
      const data = JSON.parse(xhr.responseText);
      console.log(data);
    } else {
      // 请求失败
      console.error('请求失败，状态码：' + xhr.status);
    }
  }
};
```



### 补充：

   const res = JSON.parse(xhr.responseText);  为何一定要转为对象？

==**服务器返回的是字符串**，不是对象==

服务器返回的（字符串）

```
"{ \"name\": \"张三\", \"age\": 20 }"
```

这就是 `xhr.responseText` 的真实内容 —— **纯文本字符串**。

```js
{ name: "张三", age: 20 }
```

这才是 JS 能直接用的**对象**。

**为什么服务器不直接返回对象？**

✅ **HTTP 协议只能传输文本、二进制，不能传输对象**

✅ 对象是 JS 内存里的东西，无法在网络上传输

✅ 所以必须先转成字符串发过来，你再转回去





## 六、现代方案：Fetch API

Fetch API 是浏览器原生提供的更简洁、基于 Promise 的异步请求方法，已逐渐取代 `XMLHttpRequest`。

### 6.1 基本语法
```js
fetch(url, options)
  .then(response => {
    // 处理响应
  })
  .catch(error => {
    // 处理错误
  });
```

### 6.2 GET 请求示例
```js
fetch('/api/products')
  .then(response => {
    if (!response.ok) {
      throw new Error('网络响应不成功');
    }
    return response.json();   // 解析成 JSON
  })
  .then(data => {
    console.log(data);
  })
  .catch(error => {
    console.error('请求失败:', error);
  });
```

### 6.3 POST 请求示例
```js
fetch('/api/login', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({
    username: 'admin',
    password: '123456'
  })
})
.then(response => response.json())
.then(data => {
  console.log('登录结果:', data);
})
.catch(error => console.error('错误:', error));
```

---



## 七、XMLHttpRequest vs Fetch 对比

| 特性            | XMLHttpRequest           | Fetch                            |
| --------------- | ------------------------ | -------------------------------- |
| 语法复杂度      | 较复杂，基于事件回调     | 简洁，基于 Promise               |
| 支持同步        | 支持（但不推荐）         | 不支持                           |
| 默认携带 Cookie | 默认携带同源 Cookie      | 默认不携带，需设置 `credentials` |
| 进度监控        | 支持 `onprogress`        | 目前不直接支持                   |
| 错误处理        | 仅网络层级错误触发 error | 需手动检查 `response.ok`         |
| 浏览器兼容      | 几乎所有浏览器都支持     | IE 不支持，现代浏览器均支持      |

---

## 八、常见问题与陷阱

### **1. 跨域问题（CORS）**

#### 报错 1：跨域 Cookie 不生效（登录态丢失）
你看到的现象：

- 请求发出去了
- 后端**收不到 Cookie**
- 接口返回“未登录”“请先登录”
- 控制台**没有红色报错**，但就是不生效

根本原因

**浏览器的同源安全策略：默认禁止跨域请求自动携带 Cookie**

浏览器规则：
- 同域请求：自动带 Cookie
- **跨域请求：默认不带 Cookie**

你必须主动开启：
```js
xhr.withCredentials = true;
```
不开 = 浏览器**主动不帮你带 Cookie** → 后端认不出你 → 登录态失效。

---

#### 报错 2：控制台红标报错
`Credentials flag is 'true', but the 'Access-Control-Allow-Credentials' header is ''`

你看到的报错原文

```
Access to XMLHttpRequest at 'xxx' from origin 'xxx' has been blocked by CORS policy:
Credentials flag is 'true', but the 'Access-Control-Allow-Credentials' header is ''.
It must be 'true' to allow credentials.
```

根本原因

**前端开了凭证，后端没允许 → 浏览器直接拦截请求**

流程：
1. 前端：`withCredentials: true`（我要带 Cookie）
2. 浏览器：向后端发预检 OPTIONS
3. 后端：没返回 `Access-Control-Allow-Credentials: true`
4. 浏览器：**前后端不一致，不安全，直接拒绝请求**

这是浏览器的 CORS 强制安全检查，不通过就完全不让请求成功。

---

#### 报错 3：跨域被拒绝
`The value of the 'Access-Control-Allow-Origin' header in the response must not be the wildcard '*'`

你看到的报错原文

```
Access to XMLHttpRequest at 'xxx' from origin 'xxx' has been blocked by CORS policy:
The value of the 'Access-Control-Allow-Origin' header in the response must not be the wildcard '*' when the request's credentials mode is 'include'.
```

根本原因

**一旦你要携带 Cookie（凭证），就绝对不能用 `*` 允许所有域**

为什么？
- `*` = 允许任何网站来请求
- 如果你还允许带 Cookie
- → **任何网站都能偷偷拿你的用户身份发请求**（巨大安全漏洞）
- 浏览器直接禁止这种组合

所以规则是：
```
withCredentials: true
 ↓ 必须配套
Access-Control-Allow-Origin: 具体域名（不能是 *）
```



1. **不带 withCredentials** → 跨域请求**不会带 Cookie** → 登录态没了
2. **前端开了 withCredentials**，但**后端没开 Allow-Credentials** → 浏览器直接拦请求
3. **带凭证时用 Origin:*** → 浏览器认为不安全，直接拒绝

---

最终正确组合（缺一不可）

前端

```js
xhr.withCredentials = true;
```

后端响应头

```
Access-Control-Allow-Origin: https://你的前端域名
Access-Control-Allow-Credentials: true
```

---

#### 总结
- **Cookie 不生效** = 前端没开 `withCredentials: true`
- **Credentials flag 报错** = 后端没开 `Allow-Credentials: true`
- **不能用 * 报错** = 带凭证时不允许开放所有域，必须写具体前端域名

### **2.忘记解析 JSON**

- 无论 XHR 的 `responseText` 还是 Fetch 的 `response.json()`，数据接收后需转换为 JS 对象才能使用

- . 忘记解析 JSON —— 数据在手里，却读不出来

  **典型错误**

  你收到响应了，`console.log` 也打印了内容，但试图取 `result.data` 却得到 `undefined`。控制台输出的数据看起来像字符串，而不是可展开的对象。

  #### **场景重现**（实验一登录接口）

  ```js
  xhr.onreadystatechange = function() {
      if (xhr.readyState === 4 && xhr.status === 200) {
          const result = xhr.responseText;   // 这是字符串！
          console.log(result.data);          // 永远是 undefined
          // 你以为 result 是对象，其实是字符串，.data 不存在
      }
  };
  ```

  

  此时，把 `result` 打印出来会看到 `"{"data":"eyJhbGci...","message":"登陆成功!","status":200}"`——它被双引号包裹，本质是文本。

  ==**为什么出错**==

  `xhr.responseText` 永远是字符串。服务器返回的 JSON 格式文本不会自动变成 JS 对象。

  正确做法

  ==**要么**用 `JSON.parse`：==

  ```
  const result = JSON.parse(xhr.responseText);
  console.log(result.data);  // 正确输出 token
  ```

  

  ==**要么**在 `open` 之前设置 `xhr.responseType = 'json'`，然后使用 `xhr.response` 直接得到对象：==

  ```js
  xhr.responseType = 'json';
  xhr.onload = function() {
      if (xhr.status === 200) {
          console.log(xhr.response.data); // xhr.response 已经是对象
      }
  };
  ```

  

  

### **3.错误处理不够完整**

- **Fetch 的错误写法**：

  ```js
  fetch(url, { headers: { token } })
      .then(res => res.json())
      .then(data => renderArticle(data))
      .catch(err => console.log('网络错误'));
  ```

  

  当 Token 过期，`res.status` 为 401，但 `fetch` 并没有 reject，它依然会去解析 JSON，然后 `renderArticle` 拿到的是一个错误对象。那个 `.catch` 根本抓不到这个错误。

  **==正确做法==**

  XHR 严格检查状态码

  ```
  xhr.onreadystatechange = function() {
      if (xhr.readyState === 4) {
          if (xhr.status === 200) {
              // 成功
              const article = JSON.parse(xhr.responseText);
              renderArticle(article);
          } else if (xhr.status === 401) {
              // Token 过期，跳转到登录
              alert('登录已过期，请重新登录');
          } else {
              // 其他错误
              alert('请求失败，状态码：' + xhr.status);
          }
      }
  };
  ```

  

  **Fetch 检查 `response.ok`**

  `response.ok` 为 `true` 仅当状态码在 200~299 之间。

  ```
  fetch(url, { headers: { token } })
      .then(res => {
          if (!res.ok) {
              if (res.status === 401) throw new Error('未登录');
              throw new Error(`服务器错误 ${res.status}`);
          }
          return res.json();
      })
      .then(article => renderArticle(article))
      .catch(err => {
          console.error(err.message);
          // 显示错误提示
      });
  ```

---

## 九.实验思考题

### 1. POST请求和GET请求的区别

| 维度         | GET                                            | POST                                                         |
| :----------- | :--------------------------------------------- | :----------------------------------------------------------- |
| HTTP规范定义 | 获取资源，不改变服务器状态                     | 提交数据，可能导致资源创建或修改                             |
| 参数传递方式 | 拼接在URL查询字符串中，`send()` 为空           | 参数放入 `send(请求体)` 中                                   |
| 数据可见性   | 明文暴露在URL中，不适合传输密码                | 数据不显示在URL中                                            |
| 数据量限制   | URL长度通常限制在2KB-8KB，适合少量参数         | 请求体无大小限制，适合上传文件                               |
| 缓存机制     | 会被浏览器主动缓存，可能导致数据不新鲜         | 不会被缓存，每次都发起新请求                                 |
| Content-Type | 不需要设置（无请求体）                         | 通常需要设置 `application/json` 或 `application/x-www-form-urlencoded` |
| 浏览器回退   | 无害                                           | 会再次提交请求，可能导致重复操作                             |
| 参数编码     | 只接受ASCII字符，需手动 `encodeURIComponent()` | 无字符类型限制                                               |

```js
// get请求
xhr.open('GET','http://xxx.com/api/user?name=小明&age=20')
-----------------------------------------------------------------------
//post请求
xhr.open('POST','/api/user')
xhr.setRequestHeader('Content-type','application/json')
xhr.send(JSON.stringify({name:'小明',age:20}))
```



### 2. Token的作用

- **身份识别凭证**：替代每次都传用户名密码，避免密码频繁暴露。
- **无状态认证**：服务器无需维持Session会话，Token自身就携带了用户标识、角色权限、过期时间等信息（标准JWT结构：头部、载荷、签名）。
- **分布式友好**：微服务、跨域、移动端等场景都能统一鉴权，只需共享密钥即可验证Token真实性。
- **安全控制**：可设置过期时间 `exp`，服务端可撤销或拒绝已过期的Token；前端存储也需注意HTTPS加密传输、避免XSS攻击。

### 3. 发起请求时，每一个参数都必须携带吗？

**不是**。具体看接口文档的约定：

- **必填参数**：缺少会直接导致请求失败或返回错误（如实验一的 `email`、`password`）。
- **可选参数**：不传服务器会使用默认值（如天气预报接口的 `unescape` 若不传，可能默认不给转义数据）。
- **无参数请求**：某些 GET 接口可能默认返回数据全集。
- **请求头参数**：Token是可选的（仅受保护接口必填）；`Content-Type` 在GET请求中不需要设置，在POST请求中建议设置以避免解析异常。

**⚠️ 安全风险提示**：以上实验接口均为演示用例，你在实际开发中，**绝不能将明文密码、appsecret等敏感信息硬编码在前端代码中**，否则一旦代码被反编译或被中间人截获，将造成严重的安全泄露。

### 选做实践：封装自己的 Ajax 函数
