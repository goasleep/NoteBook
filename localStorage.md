### localStorage

#### localStorage 和 sessionStorage不同点

- localStorage 是没有时间限制的，永久的。除非特定的清除localStorage或者通过浏览器来清除
- sessionStorage 生命周期为当前窗口或者标签页，当窗口或者标签页被清除时，sessionStorage就会被清空。（页面及标签页仅指顶级窗口，如果一个标签页包含多个iframe标签且他们属于同源页面，那么他们之间是可以共享sessionStorage）

#### localStorage的优点：

1. localStorage拓展了cookie的4K限制，扩展到5M
2. localStorage会可以将请求的数据直接存储到本地
3. 遵循同源策略，不同的网站直接是不能共用相同的localStorage

#### localStorage的缺点：

1. 浏览器的localStorage大小不统一，只有IE8以上的IE版本才支持localStorage这个属性
2. localStorage的值类型限定为string类型。即使你存储的是数组和对象，localStorage也会将数组和对象以字符串的形式存储。
3. localStorage在浏览器的隐私模式下面是不可读取的
4. localStorage过大会导致页面卡顿
5. localStorage不能被爬虫爬取

参考

http://www.manongjc.com/article/35746.html