# 浅谈Spring IOC
## 如何创建对象
在Java中，我们通常创建对象都是通过new Object 的形式来创建一个新的对象的，然后通过这个对象的set方法对一个对象里面的属性进行赋值。
譬如
``` java
 User user = new User()
 user.setName = 'Liming'
```
除了通过new的方式以外，我们也可以通过反射的方法创建对象。
``` java
Class<?> clz = Class.forName("User");
Constructor<?> constructor = clz.getConstructor(String.class, String.class);
Object object = constructor.newInstance("Liming");

```

我们可以拆解这个步骤，可以分为实例化和初始化两步：
1. 实例化：所谓的实例化就是new Object()这种这一种操作，这一行为在内存中为开辟了创建对象的空间
2. 初始化：所谓的初始化，就是对已经实例化的对象，填充其内部的属性。

每一次都需要这么创建，那么有没有什么方式可以帮助我们创建对象呢？Spring IOC就是为了解决我们这个难点的

## Spring IOC 是如何创建对象的
Spring 是如何帮我们创建对象的？使用过spring的都应该有过一个这样的体会，我们通过xml或者是注解来描述一个Bean,就像这样。
``` xml
<bean id="appConfig" class="com.test.AppConfig"></bean>
```
``` java
@Component
public class AppConfig{
}
```
Spring 根据我们对Bean的描述，转换成统一的Bean定义信息，然后根据这些信息创建一个对应的对象。如果我们需要使用这个对象，我们就可以通过getBean的方法，获取到这个对象。这样子就不用重新创建了，同时也省下了我们写一大串创建对象的方式

整一个流程可以简化成下图
![IOC1](..\image\IOC1.png)


对于一个对象是如此，对于多个不同对象而言，我们就需用引入工厂模式来解决这个问题。所有的对象由工厂统一生产。在这里回到我们上述说的Java中创建的方法，一是new，二是反射，而针对不同对象的创建，最好的方式就是通过反射的方式创建对象，而spring里面也同样是通过这种方式的

同时我们也将对Bean的不同描述，抽象出转换层。这样如果以后出现XML，注解外其他的Bean描述形式，我们只需接入这个转换层就可以了。

整一个流程可以如下图所示
![IOC2](..\image\IOC2.png)

## Spring IOC对对象进行操作
从spring IOC创建的流程我们可以发现，对象创建的流程变长了，从new然后set value的两步，引申出了Bean的定义信息，实例化和初始化。那么我们可以在如此长的flow当中对对象进行不同的操作。
1. 首先我们可以在Bean定义信息到BeanFactory的时候进行处理。此时，对象并没有被创建，我们可以对Bean的定义信息进行处理，比如修改Bean定义信息里面的属性值。
在Spring中，这一步是使用一个BeanFactoryPostProcessor(后置处理器/增强器)进行处理。

2. 当对象创建完以后，我们但是仍然还没有初始化以前，我们也可以对其进行操作。在初始化前和初始化后，我们都可以对创建完的对象进行处理。Spring这一步使用的是BeanPostProcessor进行处理。

整一个流程可以如下图所示
![IOC3](..\image\IOC3.png)







