# AJAX

## 一、AJAX是什么

- `Ajax` = 异步 `JavaScript` 和 `XML`。
- AJAX = Asynchronous Javascript And XML。
- `Ajax`是一种用于创建快速动态网页的技术。
- 通过在后台与服务器进行少量数据交换，`Ajax`可以使网页实现异步更新。这意味着可以在不重新加载整个网页的情况下，对网页的某部分进行更新。
- 传统的网页（不使用 Ajax）如果需要更新内容，必需重载整个网页面。
- （注意：`Ajax` 不是一种新的编程语言，而是一种用于创建更好更快以及交互性更强的`Web应用`程序的技术。）

## 二、ajax的使用及实现步骤

+ 1、 创建XMLHttpRequest对象,也就是创建一个异步调用对象. 

+ 2、 创建一个新的HTTP请求,并指定该HTTP请求的方法、URL及验证信息. 
+ 3、设置响应HTTP请求状态变化的函数. 
+ 4、发送HTTP请求. 
+ 5、获取异步调用返回的数据. 

### 示例:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
    <div id="div1">
        这是div的数据
    </div>
    <div>这是不变的数据</div>
    <button id="button">点我</button>
    <script>
    button.addEventListener('click', function(){
        // 1. 创建XMLHttpRequest对象
        var request = new XMLHttpRequest()   
        // 2. 监听 onreadystatechange 事件
        request.onreadystatechange = function(){
            if(request.readyState === 4){
                if(request.status >= 200 && request.status <= 300){
                    var string = request.responseText
                    var data = JSON.parse(string)
                    console.log(data)
                    console.log(data.name)
                    console.log(data.age)
                    div1.innerText = data.name + '---' + data.age
                }
            }
        }
        // 3. 设置请求的方法及url
        request.open('get', '/db')
        // 4. 发送请求
        request.send()
    })
    </script>
</body>
</html>

```

# 同源策略

Same-origin Policy

在需要做出一个技术决定时，我们常常需要给出适当的理由。就CORS而言，使用它的根本原因就是要完成资源的跨域访问，也就是如何绕过Same-origin Policy。

　　那么什么是Same-origin Policy呢？简单地说，在一个浏览器中访问的网站不能访问另一个网站中的数据，除非这两个网站具有相同的Origin，也即是拥有相同的协议、主机地址以及端口。一旦这三项数据中有一项不同，那么该资源就将被认为是从不同的Origin得来的，进而不被允许访问。

　　但是这个限制的确过于严格了：一个大型网站常常拥有一系列子域。在这些域之间交换数据就会受到Same-origin Policy的限制。为了绕过该限制，业界提出了一系列解决该问题的方法，例如更改document.domain属性，跨文档消息，JSONP以及CORS等。这些解决方案各有各的长处，因此我们需要根据需求的不同来对这些方案进行选择。



# CORS



## CORS 定义

Cross-Origin Resource Sharing（CORS）跨来源资源共享是一份浏览器技术的规范，提供了 Web 服务从不同域传来沙盒脚本的方法，以避开浏览器的同源策略，是 JSONP 模式的现代版。与 JSONP 不同，CORS 除了 GET 要求方法以外也支持其他的 HTTP 要求。用 CORS 可以让网页设计师用一般的 XMLHttpRequest，这种方式的错误处理比 JSONP 要来的好。另一方面，JSONP 可以在不支持 CORS 的老旧浏览器上运作。现代的浏览器都支持 CORS。

> **CORS**是W3c工作草案，它定义了在跨域访问资源时浏览器和服务器之间如何通信。CORS背后的基本思想是使用自定义的HTTP头部允许浏览器和服务器相互了解对方，从而决定请求或响应成功与否。[W3C CORS 工作草案](http://www.w3.org/TR/cors/)
> **同源策略**：是浏览器最核心也最基本的安全功能；同源指的是：同协议，同域名和同端口。精髓：认为自任何站点装载的信赖内容是不安全的。当被浏览器半信半疑的脚本运行在沙箱时，它们应该只被允许访问来自同一站点的资源，而不是那些来自其它站点可能怀有恶意的资源；[参考:JavaScript 的同源策略](https://developer.mozilla.org/zh-CN/docs/Web/Security/Same-origin_policy)
> **JSON & JSONP**:JSON 是一种基于文本的数据交换方式，或者叫做数据描述格式。JSONP是资料格式JSON的一种“使用模式”，可以让网页从别的网域要资料，由于同源策略，一般来说位于server1.example.com的网页无法与不是 server1.example.com的服务器沟通，而HTML的script元素是一个例外。利用script元素的这个开放策略，网页可以得到从其他来源动态产生的JSON资料，而这种使用模式就是所谓的JSONP

## CORS 对比 JSONP

都能解决 Ajax直接请求普通文件存在跨域无权限访问的问题

1. JSONP只能实现GET请求，而CORS支持所有类型的HTTP请求
2. 使用CORS，开发者可以使用普通的XMLHttpRequest发起请求和获得数据，比起JSONP有更好的错误处理
3. JSONP主要被老的浏览器支持，它们往往不支持CORS，而绝大多数现代浏览器都已经支持了CORS

## 使用

nodejs中只需在路由中设置响应头

```javascript

res.header("Access-Control-Allow-Origin", "*");

```





