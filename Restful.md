### Restful 设计
-  资源
- 表现层：资源的表现形式：如以json表现。HTTP请求头中的accept和content-type字段控制
- 状态转化(get,post,put,delete)
原则：
- 每一种URI 代表一种资源
- 服务器和客户端之间传递的资源的表现层
- 客户端通过四个HTTP动词，对服务器词源进行操作，实现表现层状态转化 
#### 设计误区
1. URI出现动词。
### Hypermedia API(HATEOAS)
简单来讲就是告诉别人有什么API可以调用
