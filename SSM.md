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

log4j：rootLogger输出级别，DEBUG，INFO，WARNING，ERROR，由高到低，选择性输出，输出到文件

`import arpachi....log4j...`不是引用`common...`里的



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

