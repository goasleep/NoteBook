### XSS简介

Cross-Site Scripting（跨站脚本攻击）简称 XSS。攻击者往Web页面里插入恶意的Script代码，当用户浏览该页之时，嵌入其中Web里面的Script代码会被执行，从而达到恶意攻击用户的目的。

本质：恶意代码未经过滤，与网站正常的代码混在一起；浏览器无法分辨哪些脚本是可信的，导致恶意脚本被执行。

分类：存储型XSS,反射型XSS,DOM型XSS

#### 反射性XSS
将用户输入的数据“反射”给浏览器。往往需要诱使用户点击一个恶意链接，才能攻击成功。又称“非持久性XSS”

#### 存储型XSS
将用户输入的数据“存储”在服务器端。如写下一篇包含恶意JavaScript代码的博客

#### DOM 型XSS
类似于反射性XSS，用户点击时，修改页面的DOM节点形成XSS 


### XSS攻击进阶
#### XSS Payload
XSS Payload：攻击者能够对用户当前浏览器的页面植入恶意脚本，进而控制用户的浏览器。这种恶意脚本就称为"XSS Payload"

常见的 XSS Payload: 读取浏览器的cookie对象，从而发起“Cookie劫持”攻击

#### 构造GET 和POST请求
通过JavaScript 模拟浏览器发包
通过GET执行某些操作
通过JavaScript发出Post请求，通过提交表单或者通过XMLHttpRequest

#### XSS钓鱼
XSS的攻击都是通过浏览器的JavaScript脚本自动进行的，缺少和用户交互的过程。
比如：修改用户密码时需要用户输入旧密码，这样就可以通过钓鱼 

#### 识别用户浏览器
``` js
alert(navigator.userAgent);
```
更高级的识别技巧：利用不同浏览器之间的是独有的对象判断



防御：
- 通过Set-Cookie给关键Cookie植入HTTPOnly标识
- 将Cookie和用户IP绑定





