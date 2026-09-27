# 皮卡丘靶场-CSRF(token)

## 一、基本信息

- 漏洞模块：CSRF
- 子模块：CSRF(token)
- 工具：Burp Suite、浏览器
- 目的：了解CSRF(token)的原理

## 二、漏洞原理

  CSRF-token是用来防御CSRF攻击的，通过设置token，token明文显示在页面代码中，每次请求必须携带当前页面中的token，后端校验token，且请求完旧token被销毁并产生新token，普通的CSRF恶意页面是无法读取页面内部的token的，因此普通CSRF攻击失效，但如果网站存在存储型xss，可以通过JS读取token，再发起请求，绕过token防护。

## 三、总结

  CSRF-token本身不是漏洞，而是一种CSRF防护机制，可以抵挡普通的跨站伪造请求攻击，但是不能应对xss漏洞带来的风险，要同时做好xss过滤，多层防护。

## 四、步骤截图

![步骤截图](/assets/images/pikachu/CSRF/CSRF(token)1.png)

![步骤截图](/assets/images/pikachu/CSRF/CSRF(token)2.png)

  

  登录后能看到个人信息，修改个人信息

![步骤截图](/assets/images/pikachu/CSRF/CSRF(token)3.png)



  能看到Burp Suite中捕获的请求中携带了token

![步骤截图](/assets/images/pikachu/CSRF/CSRF(token)4.png)



  看到页面中隐藏了下次请求的token

![步骤截图](/assets/images/pikachu/CSRF/CSRF(token)5.png)



  将请求发送到重放器

![步骤截图](/assets/images/pikachu/CSRF/CSRF(token)6.png)

![步骤截图](/assets/images/pikachu/CSRF/CSRF(token)7.png)

![步骤截图](/assets/images/pikachu/CSRF/CSRF(token)8.png)



  尝试能不能复用token，或者删除token参数，发送请求结果信息未被修改

![步骤截图](/assets/images/pikachu/CSRF/CSRF(token)9.png)

![步骤截图](/assets/images/pikachu/CSRF/CSRF(token)10.png)



  看到token是动态生成的，修改后就生成新的token，销毁旧token

![步骤截图](/assets/images/pikachu/CSRF/CSRF(token)11.png)

  

  输入框中写入`<img src="#" onerror="(function(){alert(documnt.cookie;)})">`，能看到弹出提示框，存在xss漏洞

  