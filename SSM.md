## catalog

ssm（spring，springMVC，MyBatis（持久化层））

mysql 读写分离

Nginx 负载均衡，动静分离

redis

阿帕奇active message queue（性能差的系统不能直接调用，建立一个单独系统*队列）

---

流行技术

前端，html5，jquery，Bootstrap，elementUI，**Echart**（图表），node.js（操作本地资源，趋近后端），**vue.js**（数据绑定，前端整体框架），MUI（统一pc，Android，IOS）

后端，spring，springBoot，springCloud（热部署，不用停机再部署，拆分模块开发，微服务）



```c++
dp[i][j]=min(max(dp[t][j-1],sum(a[t+1]~a[i]))
```



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



## xml

<![CDATA[]]>  中间可以还原&<>



## maven

配置功能的版本号，在pom.xml中，maven进行配置jar包



## i18n

把文字全部作为变量，对应值存在zh.CN.properties，en.US.properties中，可以同一逻辑，各自语言



