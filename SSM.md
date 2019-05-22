## catalog

ssm（spring，springMVC，MyBatis（持久化层））

mysql 读写分离

Nginx 负载均衡，动静分离

redis

阿帕奇active message queue（性能差的系统不能直接调用，建立一个单独系统*队列）

------

流行技术

前端，html5，jquery，Bootstrap，elementUI，**Echart**（图表），node.js（操作本地资源，趋近后端），**vue.js**（数据绑定，前端整体框架），MUI（统一pc，Android，IOS）

后端，spring，springBoot，springCloud（热部署，不用停机再部署，拆分模块开发，微服务）







string a="abc", b="abc";一开始a和b都在栈里，且地址相同，a==b

string a = new String ("abc")声明在堆里，地址不同

string 不可变对象，的变化会创建一个新的对象，在复制给他，for循环里会不停创建

stringBuffer可变字符串对象，在原来上进行修改，循环用回高，线程安全

stringBuilder=stringBuilder，线程不安全



请求转发（站内）让A将内容站内跳转到B上，getRequestDispatcher()，共享request和response对象

请求重定向，A返回给浏览器，让浏览器重新访问B，sendRedirect()，对象不共享。



JSP首先会翻译成java代码，翻译成servlet，tomcat把翻译以后的文件编译成class文件再执行



## Spring

Ioc，控制反转，让框架来创建新的类

tomcat是一个web容器，所有的servlet是由tomcat创建，释放，调用的

spring是管理java的bin（类对象）的，创建，销毁，调用由spring执行



#### IoC

- bean作用域（创建类方式与生命周期）

  单例：`<bean id="userDao" class="com.ioc.UserDaoImpl" scope="singleton"/>`

  原型，每次实例化一个`scope="prototype"·`



- 注解`@component` 让spring把其视为管理的bean

  xml配置文件

  `<context:component-scan base-package="...">< /context:component-scan>``

- 自动装载 ``@autowired`，把类里的别的类上声明，测试类也要

  `@autowired(required=false)`找不到不抛异常

  基本数据类型不是bean，不能装载，包括String

- `@qualifier("..")`用名字装配，填写component后面的名字，通常用不上

- `@configuration`加载framework提供功能时使用，或者`@bean`手动提供new的类，安全过滤器使用


依赖注入是通过ioc来实现的



#### AOP

重复代码写一次

切面类`@Component @Aspect`,方法前面加`@Before("excution(* package.class.*(..))")`

持久化层上加处理

```Java
Logger log = Logger.getLogger(Advice.class);

@Before("excution(* package.class.*(..))")
(JointPoint joinPoint) { // 支持就给你赋值，参数可以不添加
    log.info(joinPoint.getSignature().getName());
    // 获得参数
    log.info(joinPoint.getArgs()[0].toString());
}

@After("excution(* package.class.*(..))")

// 环绕
@Around("excution(* package.class.*(..))")
public void circle(ProceedingJoinPoint proceedingJoinPoint) {
    log.info(proceedingJoinPoint.getSignature().getName());
    Object o;
    try { // have to be done 
        o = proceedingJoinPoint.proceed(proceedingJoinPoint.getArgs());
    } catch(Throwable throwable) {
        
    }
    // after
    log.info(o.toString());
    return o;
} 

// 
@AfterReturning(value = "excution(* package.class.*(..))", returning = "o")
public Object afterReturn(Object o) {
	log.info(o.toString());
    return o;
}

@AfterThrowing(value = "excution(* package.class.*(..))", throwing = "e")
public void afterThrowing(Exception e) {
    log.info(e.getMessage());
}

// (..) -> ((int), (int))
// (..) -> (.User*.insert*((int), (int)))
p1 = b/(b+w),  (b+d)/(b+w+d)
    
<aop:aspect-autoproxy proxy-target-class="true">
```

切点：注解（@before..）



#### 库

+ log4j：rootLogger输出级别，DEBUG，INFO，WARNING，ERROR，由高到低，选择性输出，输出到文件

`import arpachi....log4j...`不是引用`common...`里的

+ pagehelper



#### 测试

测试类和框架一起运行`@runWith(SpringJUNIT4ClassRunner.class)`

配置文件`@ContextConfiguration(locations = "classpath:applicationContext.xml")`





## xml

`<![CDATA[]]> ` 中间可以还原&<>



## maven

配置功能的版本号，在pom.xml中，maven进行配置jar包



## i18n

把文字全部作为变量，对应值存在zh.CN.properties，en.US.properties中，可以同一逻辑，各自语言



## Mybaties

utf-8 --- utf8-generate-ci

数据库连接都是通过网络连接的

当多个客户端访问数据库时，（Oracle默认20），当连接的进程句柄装载在连接池中，超过的将被拒绝。用完访问后需要close。

连接池：原先每次访问，需要分配资源需要耗时，现在直接取连接池的已经访问DB的资源，类似进程池，无需创建和释放。数据源中设置：UNPOOLED,POOLED,JDNI



**基本要素** sqlMapConfig.xml 全局配置文件，Mapper.xml 核心映射文件，SqlSessionFactory 接口



jar包 ： MyBatis Spring Maven; 

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<!--通过这个配置文件，完成mybatis与数据库的连接  -->
<configuration>
    <!-- 注意此配置文件内的元素的  -->
    <!-- 引入database.properties文件 -->
    <properties resource="database.properties"/>
    <!--配置mybatis的log实现为LOG4J  -->
    <!-- 配置后，后台就会有sql
    
    
    SqlMapConfig.xml
    
    
driver=com.mysql.cj.jdbc.Driver
url=jdbc:mysql://localhost:3306/world?characterEncoding=utf-8&serverTimezone=GMT%2B8
username=root
password=123456

database.properties
```



`<set>`可以把语句中多余逗号去除

`<where>`可以把里面的`and`多余去掉



+ 指向redis集群，让缓存数据一直存在，即使mybatis关闭



+ 一级缓存&二级缓存

  需要`session.commit();`

  二级缓存，协调不同的缓存速度

## MySql

select * from X limit 40, 10

pagehelper/5.1.8

## SpringMVC

http:\\localhost:8080/taobao/dir......

端口为 80 为HTTP默认端口，绑定它可以不输入端口号

MVC - Model-View-Controller

+ Model（模型）表示应用程序核心（比如数据库记录列表）。

+ View（视图）显示数据（数据库记录）。

+ Controller（控制器）处理输入（写入数据库记录）。

MVC 模式同时提供了对 HTML、CSS 和 JavaScript 的完全控制。

Model（模型）是应用程序中用于处理应用程序数据逻辑的部分。
　　通常模型对象负责在数据库中存取数据。

View（视图）是应用程序中处理数据显示的部分。


　　通常视图是依据模型数据创建的。
Controller（控制器）是应用程序中处理用户交互的部分。
　　通常控制器负责从视图读取数据，控制用户输入，并向模型发送数据。

REST（当前流行）： 模式，把请求通过url展示出来，比如 ?id=1001:size=1  =>  /id/1001/size/1

web.xml 是所有网站的入口  （servlet，servletmapping（"/"所有请求，进行统一处理））

<load-on-startup> 表示servlet的启动顺序

servlet-mapping 中表示拦截所有请求 ：<url-pattern> *.form</url-pattern> 改成 <url-pattern> /</url-pattern> 

settings-> application servers 配置

add configruation



包导入的正确性很重要



---

## 问题

reference: <https://www.cnblogs.com/hfblogs/p/5345497.html>

`<association> <collection>` 需要在对应的类中包括对应的属性，不然会提示ambiguous

一对一，一对多，多对多  https://blog.csdn.net/qq_42780864/article/details/81429114



---

request 在一次连接之后就消失了

session 存储登录消息，一般维护时间为半小时，每一次request重新计时，让sessionID在response返回，并在之后登录之后由request发送至服务器

contacts对象在服务器一直存在，直到网站关闭，存储网站的整体配置，提示信息，不适合频繁调度

page生命周期最短，相当于成员变量，请求转发不会到下一个页面上

return “a.jsp”实际是请求转发



DTO 是继承了 bean类后，还包含其他额外功能属性的类，可以直接替代bean进行传递交互

`SimpleDateFormat ("yyyy-MM-dd HH:mm:ss")` 时间转换

`simpleDataFormat.format(new Date())`

选择`java.util.date`， `org.springframework.core.convert...`

配置

![1557887635928](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\1557887635928.png)

ServiceFactoryBean