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
成功代码
	200ok
    301永久重定向
    302临时重定向
    304未修改
    307重定向保持原有的请求数据
失败代码
	400客户端错误
	404找不到页面
	503服务器暂时不可用
	500服务器内部错误
```

