### HTML5 安全
#### 新的标签
HTML5 定义了很多先标签和新事件，可能会带来新的XSS攻击。如果建立一个黑名单的话，则可能不会覆盖到HTML5新增的标签和功能，从而发生XSS

##### iframe 的sandbox
HTML5专门为iframe定义新的属性，叫sandbox。使用这一个属性，iframe标签加载的内容将会被视为一个独立的源，其中的脚本被静置执行，表单被禁止提交，插件被禁止加载，指向其他浏览器对象的链接也被禁止

- allow-same-origin：允许同源访问
- allow-top-navigation:允许访问顶层窗口
- allow-forms：允许提交表单
- allow-scripts:允许执行脚本

##### Link Types:noreference 
为\<a>和\<area>标签定义一个新的LinkTypes:noreference
标签指定noreference后，浏览器在请求该标签指定的地址时将不在发送Referer。
这是出于保护敏感信息和隐私考虑。因为通过Refer，可能会泄露一些敏感信息

##### Canvas 破解验证码
可以通过JavaScript操作Canvas中的每个像素点，成功自动化识别验证码


##### Origin Header
Origin Header 用户标记HTTP发起的源，服务器通过识别浏览器自动带上的这个OriginHeader，来判断浏览器的请求是否来自一个合法的源，这样可以用来防御CSRF，它也不想Referer那么容易被清空

##### WEB Storage
浏览器存储的信息方法有三种
- Cookie : 用户保存登录凭证和少量信息。有长度限制不能够存储太多信息
- Flash Shared Object 和 IE userDate： 并非一个通用化的标准
- Web Storage

Web Storage 分为Session Storage 和 LocalStorage。
Session Storage 会在关闭浏览器的时候失效，而LocalStorage则一直会存在
Web Storage就像一个非关系型数据库，由Key-Value对组成，可以通过JavaScript对戏进行操作
Web Storage也会受到同源策略的约束，每个域所拥有的信息只会保存在自己的域下

而攻击者可能将而已代码保存在Web Storage 中，从而实现跨页面攻击
