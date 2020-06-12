### CSRF 简介
Cross Site RequestForgery(跨站点请求伪造)，简称CSRF。
攻击成功的原因，重要操作的所有参数都可以被攻击者猜测到，只有预测出URL和所有参数和参数值，才能构造一个伪造的请求

浏览器的cookie策略
- Session Cookie (临时的cookie)
- Third-party Cookie (本地Cookie)
区别在于Third-party Cookie是服务器在Set-Cookie时指定了Expire时间，只有到了Expire时间后Cookie才会失效。而Session Cookie没有指定时间，关闭浏览器，就失效了


#### 防御
#####  验证码
CSRF往往是用户不知情的情况下构造了网络请求，而验证码可以强制用户必须和应用进行交互，才能完成请求
##### Referer Check
用户检查请求是否来自于合法的“源”，通过页面与压面之间的逻辑关系，检查referer时候合法来判断用户是否被CSRF攻击
而缺点在于，服务器并非什么时候都能去到Referer，很多用户出于隐私的保护，也限制了Referer的发送。
##### Anti CSRF Token
在URL添加一个token参数，token参数是随机的，不可以预测的。
而Token通常可以放在用户的session中，或者浏览器的Cookie中。
在使用时，需要注意
- 生成的Token一定要足够随机
- Token应该保存在Cookie中，而不是服务器端的Session中。可以考虑生成多个有效的Token，解决页面共存的场景
- 使用Token应该注意Token的保密性，使用时应该把Token放在表单中，将敏感操作由Get改为Post，以form表单或者AJAX的形式提交，避免Token泄露
- 预防XSS或者一些跨域漏洞，让攻击者窃取Token的值
- XSS带来的问题。应该使用XSS防御方案解决，否则CSRF的Token防御就是空中楼阁。CSRF和XSS组合可以称为XSRF


