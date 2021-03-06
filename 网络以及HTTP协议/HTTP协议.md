### HTTP协议

- **http版本**

>在HTTP1.0协议中，客户端与web服务器建立连接后，只能获得一个web资源。
>
>在HTTP1.1协议，允许客户端与web服务器建立连接后，在一个连接上获取多个web资源。
>
>https是九次握手

- 一个完整的HTTP请求包括如下内容：**一个请求行、若干消息头、以及实体内容**

**https必须是http/2.0协议的，http是http/1.1协议的**

```txt
浏览器默认发送get请求，想要post请求，可以使用表单提交

在开发过程中，如果希望服务器输出什么浏览器就能看到什么，那么在服务器端都要以字符串的形式进行输出。
```

##### HTTP请求的细节——消息头

```http
　HTTP请求中的常用消息头

　　accept:浏览器通过这个头告诉服务器，它所支持的数据类型
　　Accept-Charset: 浏览器通过这个头告诉服务器，它支持哪种字符集
　　Accept-Encoding：浏览器通过这个头告诉服务器，支持的压缩格式
　　Accept-Language：浏览器通过这个头告诉服务器，它的语言环境
　　Host：浏览器通过这个头告诉服务器，想访问哪台主机
　　If-Modified-Since: 浏览器通过这个头告诉服务器，缓存数据的时间
　　Referer：浏览器通过这个头告诉服务器，客户机是哪个页面来的  防盗链
　　Connection：浏览器通过这个头告诉服务器，请求完后是断开链接还是何持链接
```

##### HTTP响应细节——常用响应头

```http
　HTTP响应中的常用响应头(消息头)
　
　　Location: 服务器通过这个头，来告诉浏览器跳到哪里
　　Server：服务器通过这个头，告诉浏览器服务器的型号
　　Content-Encoding：服务器通过这个头，告诉浏览器，数据的压缩格式
　　Content-Length: 服务器通过这个头，告诉浏览器回送数据的长度
　　Content-Language: 服务器通过这个头，告诉浏览器语言环境
　　Content-Type：服务器通过这个头，告诉浏览器回送数据的类型
　　Refresh：服务器通过这个头，告诉浏览器定时刷新
　　Content-Disposition: 服务器通过这个头，告诉浏览器以下载方式打数据
　　Transfer-Encoding：服务器通过这个头，告诉浏览器数据是以分块方式回送的
　　Expires: -1  控制浏览器不要缓存
　　Cache-Control: no-cache  
　　Pragma: no-cache 
```

##### 解决乱码

```http
解决post提交方式的乱码：request.setCharacterEncoding("UTF-8");
解决get提交的方式的乱码：parameter = new String(username.getbytes("iso8859-1"),"utf-8");
```

##### servlet

```txt
由于客户端是通过URL地址访问web服务器中的资源，所以Servlet程序若想被外界访问，必须把servlet程序映射到一个URL地址上，这个工作在web.xml文件中使用<servlet>元素和<servlet-mapping>元素完成。
　　<servlet>元素用于注册Servlet，它包含有两个主要的子元素：<servlet-name>和<servlet-class>，分别用于设置Servlet的注册名称和Servlet的完整类名。
一个<servlet-mapping>元素用于映射一个已注册的Servlet的一个对外访问路径，它包含有两个子元素：<servlet-name>和<url-pattern>，分别用于指定Servlet的注册名称和Servlet的对外访问路径。
```

##### 状态码

```http
100系列
	需要下一步操作
200系列
	正确的操作
300系列
	重定向
400系列
	客户端错误
500系列
	服务器错误
成功代码
	200ok
	206只需要一部分数据（范围请求）
    301永久重定向
    302临时重定向
    304未修改
    307重定向保持原有的请求数据
失败代码
	400客户端错误
	401为鉴权
	403未获得文件系统的访问授权
	404找不到页面
	503服务器暂时不可用
	500服务器内部错误
```

## HTTP 状态码

1. (信息类)：表示接收到请求并且继续处理
2. ​    **100——客户必须继续发出请求**
3. ​    **101——服务器已经理解了客户端的请求，并将通过Upgrade 消息头通知客户端采用不同的协议来完成这个请求。在发送完这个响应最后的空行后，服务器将会切换到在Upgrade 消息头中定义的那些协议。**



1.   2**(响应成功)：表示动作被成功接收、理解和接受
2.   ​    200——表明该请求被成功地完成，所请求的资源发送回客户端
3.   ​    201——提示知道新文件的URL
4.   ​    202——接受和处理、但处理未完成
5.   ​    203——返回信息不确定或不完整
6.   ​    **204——请求收到，但返回信息为空**
7.   ​    205——服务器完成了请求，用户代理必须复位当前已经浏览过的文件
8.   ​    **206——服务器已经完成了部分用户的GET请求**
9.   
10.   3**(重定向类)：为了完成指定的动作，必须接受进一步处理
11.   ​    **300——请求的资源可在多处得到**
12.   ​    **301——本网页被永久性转移到另一个URL**
13.   ​    **302——请求的网页被转移到一个新的地址，但客户访问仍继续通过原始URL地址，重定向，新的URL会在response中的Location中返回，浏览器将会使用新的URL发出新的Request。**
14.   ​    **303——建议客户访问其他URL或访问方式**
15.   ​    **304——自从上次请求后，请求的网页未修改过，服务器返回此响应时，不会返回网页内容，代表上次的文档已经被缓存了，还可以继续使用**
16.   ​    305——请求的资源必须从服务器指定的地址得到
17.   ​    306——前一版本HTTP中使用的代码，现行版本中不再使用
18.   ​    307——申明请求的资源临时性删除（保护重定向中的资源 常用于POST）



1.   4**(客户端错误类)：请求包含错误语法或不能正确执行
2.   ​       **400——客户端请求有语法错误，不能被服务器所理解**
3.   ​       **401——请求未经授权，这个状态代码必须和WWW-Authenticate报头域一起使用**
     ​     1. HTTP 401.2 - 未授权：服务器配置问题导致登录失败
     ​         2. HTTP 401.3 - ACL 禁止访问资源
     ​         3. HTTP 401.4 - 未授权：授权被筛选器拒绝
     ​         4. HTTP 401.5 - 未授权：ISAPI 或 CGI 授权失败
     ​         5. 402——保留有效ChargeTo头响应
     ​         6. **403——禁止访问，服务器收到请求，但是拒绝提供服务**
     ​         7. HTTP 403.1 禁止访问：禁止可执行访问
     ​         8. HTTP 403.2 - 禁止访问：禁止读访问
     ​         9. HTTP 403.3 - 禁止访问：禁止写访问
     ​         10. HTTP 403.4 - 禁止访问：要求 SSL
     ​         11. HTTP 403.5 - 禁止访问：要求 SSL 128
     ​         12. HTTP 403.6 - 禁止访问：IP 地址被拒绝
     ​         13. HTTP 403.7 - 禁止访问：要求客户证书
     ​         14. HTTP 403.8 - 禁止访问：禁止站点访问
     ​         15. HTTP 403.9 - 禁止访问：连接的用户过多
     ​         16. HTTP 403.10 - 禁止访问：配置无效
     ​         17. HTTP 403.11 - 禁止访问：密码更改
     ​         18. HTTP 403.12 - 禁止访问：映射器拒绝访问
     ​         19. HTTP 403.13 - 禁止访问：客户证书已被吊销
     ​         20. HTTP 403.15 - 禁止访问：客户访问许可过多
     ​         21. HTTP 403.16 - 禁止访问：客户证书不可信或者无效
     ​         22. HTTP 403.17 - 禁止访问：客户证书已经到期或者尚未生效
4.   ​    404——一个404错误表明可连接服务器，但服务器无法取得所请求的网页，请求资源不存在。输入了错误的URL
5.   ​    **405——用户在Request-Line字段定义的方法不允许**
6.   ​    **406——根据用户发送的Accept头发现无法响应用户发送的数据，请求资源不可访问、无法接受。**
7.   ​    407——类似401，用户必须首先在代理服务器上得到授权
8.   ​    408——客户端没有在用户指定的时间内完成请求
9.   ​    409——对当前资源状态，请求不能完成
10.   ​    410——服务器上不再有此资源且无进一步的参考地址
11.   ​    411——服务器拒绝用户定义的Content-Length属性请求
12.   ​    412——一个或多个请求头字段在当前请求中错误
13.   ​    413——请求的资源大于服务器允许的大小
14.   ​    414——请求的资源URL长于服务器允许的长度
15.   ​    415——请求资源不支持请求项目格式
16.   ​    416——请求中包含Range请求头字段，在当前请求资源范围内没有range指示值，请求也不包含If-Range请求头字段
17.   417——服务器不满足请求Expect头字段指定的期望值，如果是代理服务器，可能是下一级服务器不能满足请求长。
      2. 5**(服务端错误类)：服务器不能正确执行一个正确的请求
18.   HTTP 500 - 服务器遇到错误，无法完成请求
   19.   HTTP 500.100 - 内部服务器错误 - ASP 错误
   20.   ​    　　HTTP 500-11 服务器关闭
   21.   ​    　　HTTP 500-12 应用程序重新启动
   22.   ​    　　HTTP 500-13 - 服务器太忙
   23.   ​    　　HTTP 500-14 - 应用程序无效
   24.   ​    　　HTTP 500-15 - 不允许请求 global.asa
   25.   ​    　　Error 5 01 - 未实现
26.   **HTTP 502 - 网关错误**
27.   **HTTP 503：由于超载或停机维护，服务器目前无法使用，一段时间后可能恢复正常**

