### 点击劫持
ClickJacking(点击劫持)是一种是觉得欺骗手段。攻击者使用一个透明的、不可见的iframe，覆盖在一个网页上，然后诱使用户在该网页上进行操作，用户将在不知情的情况下点击透明的iframe页面。

与CSRF一样，都是在用户不知情的情况下诱使用户完成一些动作，不同的是，点击劫持利用的是与用户交互产生的页面

例子：
- 图片覆盖攻击
- 拖拽劫持
- 触屏劫持


#### 防御
##### frame busting
即禁止iframe嵌套，
##### X-Frame-Options
在HTTP头中添加X-Frame-Options
X-Frame-Options 有三个值可选
- DENY：浏览器会拒绝当前页面加载任何frame页面
- SAMEORIGIN：则frame页面的地址只能为同源域名下的页面
- AL-LOW-FROM: 允许frame加载的页面地址

Firefox的“Content Security Police”以及No-Script扩展也能够有效防御ClickJacking