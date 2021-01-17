# Servlet
## Servlet 规范
1. Servlet规范是JavaEE规范的一种
2. 作用
   1. 在Servlet规范中，指定**动态资源文件**的开发步骤
   2. 在Servlet规范中，指定Http服务器调用动态资源文件的规则
   3. 在Servlet规范中，指定Http服务器管理动态资源文件的规则(如何管理servlet)

## Servlet 接口实现类
1. 在Servlet规范中认为，Http能调用的动态资源文件必须是Servlet接口的实现类，也就是说，只有Servlet接口的实现类才是动态资源文件
2. Servlet接口是Servlet规范下的一个接口，这个接口存在于Http服务器提供的jar包
3. 在Tomcat服务器下的lib文件中，有一个servlet-api.jar的jar包，里面存放着Servlet接口


## Servlet的生命周期
1. 网站中所有的Servlet接口实现类的实例对象，只能由Http服务器来创建，程序员不能手动创建
2. 在默认的情况下，Http服务器接收到对于当前Servlet接口实现类第一次请求时自动创建这个Servlet接口实现类的实例对象
3. 在手动配置的情况下，可以要求Http服务器在启动时自动创建某个Servlet接口实现类的实例对象

## HttpServletResponse接口和HttpServletRequest接口
- 两者接口皆来自于Servlet规范中
- 两者接接口实现类由Http服务器负责提供
- HttpServletResponse接口负责将doGet/doPost方法执行结果写入到【响应体】交给浏览器，HttpServletRequest接口负责在doGet()，doPost()等方法运行时读取Http请求协议包中信息
- 习惯于将HttpServletResponse接口对象称为响应对象，HttpServletRequest接口修饰的对象称为【请求对象】

### HttpServletResponse功能
1. 将执行结果以二进制形式写入到响应体
2. 设置响应头content-type属性值，从而控制浏览器使用对应编译器将响应体二进制数据编译为【文字，图片，视频，命令等】
3. 置响应头【location】属性值，将一个请求地址赋值给location，从而控制浏览器向指定服务器发送请求（setRedirect()）

### HttpServletRequest功能
1. 可以读取Http请求协议包中请求行信息
2. 可以读取保存在Http请求协议包中请求头或者请求体中参数信息
3. 可以替代浏览器向Http服务器申请资源文件调用
   
### 请求对象和响应对象的生命周期
1. 在Http服务器接收到浏览器发送的Http请求协议包之后，会自动为当前请求协议包生成一个请求对象和响应对象
2. 在Http服务器调用doGet或doPost方法时，负责将请求对象和响应对象作为参数传递进去
3. 在Http服务器准备推送Http响应包之前，负责将本次请求关联的请求对象和响应对象销毁
注：请求对象和响应对象生命周期贯穿一次请求的处理过程始末

## 监听器
1. 监听器接口用于监控【作用域对象生命周期变化时刻】以及【作用域对象共享数据变化时刻】
2. 作用域对象：在Servlet规范中，认为在服务端内存中可以在某些条件下认为两个Servlet之间提供数据共享方案，被称为【作用域对象】
   1. ServletContext： 全局作用域对象
   2. HttpServlet：会话作用域对象
   3. HttpServletRequest：请求作用域对象

## 过滤器
1. Filter接口在Http服务器调用资源文件之前，对Http服务器进行拦截
2. 具体作用：
   1. 拦截Http服务器，帮助Http服务器检测当前请求合法性
   2. 拦截Http服务器，对当前请求进行增强操作

https://qiankunli.github.io/2019/11/26/tomcat_source.html#%E4%BB%8E%E5%90%84%E4%B8%AA%E8%A7%86%E8%A7%92%E7%9C%8Btomct