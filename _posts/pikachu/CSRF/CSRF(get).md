# 皮卡丘靶场-CSRF(get)

## 一、基本信息

- 漏洞模块：CSRF
- 子漏洞：CSRF(get)
- 工具：Burp Suite、浏览器
- 目的：复现漏洞，通过复现漏洞了解CSRF(get)的原理和完整流程

## 二、漏洞原理

  当在一个浏览器中一个网站登录时，cookie会保存在浏览器中，如果在外部服务器中有一个构造好的访问该网站的请求，在同一个浏览器中访问该请求，浏览器同样会将cookie携带在该请求中，此时不需要知晓账号密码去登陆，就能够访问网站，甚至修改用户的信息。

## 三、复现步骤

1. Burp Suite中输入账号密码登录
2. 修改个人信息，Burp Suite中捕获到请求
3. Burp Suite中生成CSRF PoC，复制生成的HTML代码
4. 在Apache服务器WWW根目录下建立evil.html，将复制的HTML代码写入evil.html中
5. 在浏览器中访问Apache服务器中的evil.html，点击发送请求
6. 能看到pikachu平台中CSRF(get)页面个人信息被修改

## 四、结果与总结

- **结果**：成功复现漏洞，得到预取结果。
- **总结**：GET型CSRF，攻击者构造恶意页面，诱导登录后的受害者访问，利用浏览器自动携带Cookie的特性，发起伪造的请求，修改用户信息。

## 五、步骤截图

![步骤截图](/assets/images/pikachu/CSRF/CSRF(get)1.png)



  输入账号密码登录

![步骤截图](/assets/images/pikachu/CSRF/CSRF(get)2.png)

 

  能看到登录后的页面

![步骤截图](/assets/images/pikachu/CSRF/CSRF(get)3.png)



  修改个人信息

![步骤截图](/assets/images/pikachu/CSRF/CSRF(get)4.png)



  Burp Suite中捕获请求

![步骤截图](/assets/images/pikachu/CSRF/CSRF(get)5.png)

![步骤截图](/assets/images/pikachu/CSRF/CSRF(get)6.png)

  

  构造CSRF PoC，复制构造好的HTML代码

![步骤截图](/assets/images/pikachu/CSRF/CSRF(get)7.png)



  在Apache根目录WWW中建立evil.html，内容为复制的HTML代码

![步骤截图](/assets/images/pikachu/CSRF/CSRF(get)8.png)



  在浏览器中访问evil.html

![步骤截图](/assets/images/pikachu/CSRF/CSRF(get)9.png)

![步骤截图](/assets/images/pikachu/CSRF/CSRF(get)10.png)



  事先修改个人信息，点击构造的请求，能看到pikachu中个信息被修改