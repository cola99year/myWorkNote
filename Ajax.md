2022.7.24

原视频链接：[【尚硅谷】3小时Ajax入门到精通_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1WC4y1b78y?p=23&vd_source=69efaf6a51aef1bb532cc0757188528d)；

参考文章:[【3小时入门Ajax】](https://blog.csdn.net/weixin_44972008/article/details/113772348)，文章有参考代码哦！

官网文档：[axios中文文档|axios中文网 | axios (axios-js.com)](http://www.axios-js.com/zh-cn/docs/#axios-post-url-data-config)；



# 1. HTTP 请求

>ajax请求 是一种特别的 http请求

## 1.1 HTTP 请求交互的基本过程

<img src="https://i0.hdslb.com/bfs/album/fa2fa18bdf71f83f9d954bc0027bc633bd7da8e2.png" alt="image-20220724123051221" style="zoom: 67%;" />

---







## 1.2 HTTP请求-客户端

> 图下`XHR`即`XMLHTTPRequest`，对Ajax筛选的分类。即下面的链接**都是Ajax请求**

<img src="https://i0.hdslb.com/bfs/album/f1f7fbcec0fc3805457140f3c263f25bbd8ad42e.png" alt="image-20220724162447221" style="zoom: 67%;" />

---



### 1. 请求行：即URL链接

都是键值对：

即   ①显示的GET还是POST的方法 ，②**URL链接**；二者归属于请求行；如下图所示：

<img src="https://i0.hdslb.com/bfs/album/45463686de2a2dd51756fdd091e346b577b31395.png" alt="image-20220724170717107" style="zoom: 67%;" />

---









### 2. 请求头：有很多

> 都是键值对：比如携带有客户端的浏览器版本信息
>
> 携带用户自定义请求头数据

Host: www.baidu.com
Cookie: BAIDUID=AD3B0FA706E; BIDUPSID=AD3B0FA706;
Content-Type: application/x-www-form-urlencoded 或者application/json

<img src="https://i0.hdslb.com/bfs/album/5f487505cf6e0fcbfaa78c31afb17fcd4126cc2c.png" alt="image-20220724170641795" style="zoom: 67%;" />



> **请求头设置**：Content - Type是用来设置==客户端请求体的类型==

如：**a=190&b=290&c=300**的类型为**x-www-form-urlencoded**；

<img src="https://i0.hdslb.com/bfs/album/7da6a7d27996f14beda5a1ad3757909a81e1c0bf.png" alt="image-20220724170907232" style="zoom: 50%;" />

---



### 3.空行

空行无实际意义



### 4. 请求体

> **get**的请求体一般都是空的
>
> **post**就有请求体：例如包含了账号+密码的请求体

username=tom&pwd=123

**Post请求才有的请求体**：

{"username": "tom", "pwd": 123}





**查看字符串参数：**

<img src="https://i0.hdslb.com/bfs/album/8b3305542520d2fb1cc378a5058535581ed3b024.png" alt="image-20220724162333351" style="zoom: 67%;" />

---



## 1.3 HTTP响应-服务器端

### 1. 响应行

响应行包括    **HTTP协议版本+状态码**

### 2. 响应头（多个）

作用：比如设置响应头，告诉浏览器数据类型是`HTML类型数据`，这样浏览器才会解析HTML**标签**

response.setContentType("text/html;charset=utf-8");

<img src="https://i0.hdslb.com/bfs/album/8d6a0a15bcdfc35653f4a0179eadd1ba4427b247.png" alt="image-20220724163313969" style="zoom:80%;" />

---



![image-20220724163141288](https://i0.hdslb.com/bfs/album/8d6a0a15bcdfc35653f4a0179eadd1ba4427b247.png)

### 3.空行

空行无实际意义

---

![image-20220724162122309](https://i0.hdslb.com/bfs/album/8d6a0a15bcdfc35653f4a0179eadd1ba4427b247.png)

---



### 4. 响应体

> **响应体**设置即为后端要返回给前端的信息。
>
> 如@ResponseBody注解，把数据放到响应体中！

```html
<html>
    <head/></head>   
    <body>
        .......
	</body>
</html>  
```

<img src="https://i0.hdslb.com/bfs/album/498f85e6d46c5ebaa1a9f16706af251df4cc0c16.png" alt="image-20220724160723922" style="zoom: 50%;" />



# 2. Ajax请求

## 2.1 GET请求

下面为GET请求的大体步骤，POST请求同理之！

### 1. GET请求三步骤

> 客户端Ajax的GET请求：

<img src="https://i0.hdslb.com/bfs/album/364c2c7eb17467f4cdbcc0358e4e95ea76a671e9.png" alt="image-20220724163645717" style="zoom: 67%;" />

> 这是**服务端**处理匹配客户端的GET请求

<img src="https://i0.hdslb.com/bfs/album/fb4034853ad99e038af2e86498ba4eef60be1542.png" alt="image-20220724165031995" style="zoom:50%;" />

> 控制台打印输出如下：

<img src="https://i0.hdslb.com/bfs/album/ff1f9666b6460b3163d8c0863927b4ce086d1a9c.png" alt="image-20220724163827820" style="zoom:80%;" />

### 2. GET携带参数

GET请求携带参数如下：

<img src="https://i0.hdslb.com/bfs/album/730ca7c6b96afab8f630429550cd6b0a3bf95954.png" alt="image-20220724164526021" style="zoom: 67%;" />



## 2.2 响应JSON数据

> 转来转去都是因为：JavaWeb就学过，响应**只会有字符串和流**，怎么会响应json?对象？？

服务端发送JSON数据，把JSON数据用`JSON.stringify()`转换为字符串，如下图所示：

<img src="https://i0.hdslb.com/bfs/album/bc14157a787e6a3cf9cf19f0ed4fdbff294d3a8d.png" alt="image-20220724171610438" style="zoom:67%;" />

---

客户端再用`JSON.parse()`把字符串转换为JSON就可以使用了。

<img src="https://i0.hdslb.com/bfs/album/a5872eaec9dedab234cf58ddca99474bf5f99b50.png" alt="image-20220724171815529" style="zoom:50%;" />

或者设置响应的类型：

```js
//设置响应体数据的类型
xhr.responseType 'json';
```

---





# 3. axios请求

官网文档：[axios中文文档|axios中文网 | axios (axios-js.com)](http://www.axios-js.com/zh-cn/docs/#axios-post-url-data-config)；

### 1. axios的get请求+传参

> axios.get(url[, config])

<img src="https://i0.hdslb.com/bfs/album/77a6a56bc7e6b8f05dfacb58f8a72f9d1815b9f6.png" alt="image-20220724173752904" style="zoom: 40%;" />

官网演示：

```js
// 为给定 ID 的 user 创建请求
axios.get('/user?ID=12345')
  .then(function (response) {
    console.log(response);
  })
  .catch(function (error) {
    console.log(error);
  });

// 上面的请求也可以这样做
axios.get('/user', {
    params: {
      ID: 12345
    }
  })
  .then(function (response) {
    console.log(response);
  })
  .catch(function (error) {
    console.log(error);
  });
```



---





### 2.  axios的post请求+传参(即请求体)

> axios.post(url[, data[, config]])

<img src="https://i0.hdslb.com/bfs/album/be34dd25595061c002f97bbc610999ed84d9819f.png" alt="image-20220724174233041" style="zoom:50%;" />

官网演示：

```js
axios.post('/user', {
    firstName: 'Fred',
    lastName: 'Flintstone'
  })
  .then(function (response) {
    console.log(response);
  })
  .catch(function (error) {
    console.log(error);
  });
```



### 3. axios函数写法

官网：

```js
// 发送 POST 请求
axios({
  method: 'post',
  url: '/user/12345',
  data: {
    firstName: 'Fred',
    lastName: 'Flintstone'
  }
});
```



# 4. 设置CORS响应头实现跨域





# END