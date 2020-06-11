[toc]
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

通常来说风险：存储型 > 反射性
攻击过程来说：反射性 > 存储型

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

#### 识别用户安装的软件
如识别firefox的拓展

#### 获取用户的真实IP地址
如果客户安装了Java环境，XSS就可以通过调用JavaApplet的接口获取本机IP地址


#### XSS构造技巧
- 利用字符编码
- 绕过长度限制
  - 利用 location,hash 藏代码
  - 远程加载JS
  - 利用注释符
- 使用\<base>标签
  - 作用是定义页面上所有使用相对路径标签的host地址
- window.name 实现跨域、跨页面请求数据


### XSS防御
XSS本质是“HTML 注入”
#### HTTP only
通过Set-Cookie给关键Cookie植入HTTPOnly标识，解决XXS后的Cookie劫持攻击
防御：
#### 输入检查
前后端都对输入进行检查，检查用户输入的数据是否包含一些特殊的字符。这种方式成为“XSS Filter”
#### 输出检查
变量输出到HTML页面时，可以使用编码或者转义的方式防御XSS
- 使用安全的编码函数，需要注意的是安全编码后的长度可能发生改变，影响某些功能
- 可以考虑不止使用一种编码

#### 处理富文本
禁止危险标签：\<iframe>,\<script>,\<base>,\<form>
标签应使用白名单，避免黑名单。如只允许使用\<a>,\<img>,\<div>等安全标签
白名单同时应用于属性与事件的选择

#### 防御DOM based XSS
尽量避免用户的输入，关注会修改HTML的语句，如
- xxx.innerHTML= 
- document.write .....






