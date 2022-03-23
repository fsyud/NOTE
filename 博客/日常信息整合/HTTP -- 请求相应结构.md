# 一：一个HTTP请求报文由四个部分组成：请求行、请求头部、空行、请求数据。

## 1.请求行

　　1.请求方法：GET POST

　　2.URL字段

　　3.HTTP版本字段

## 2.请求头

　　1.Accept：浏览器可接受的mime类型。

　　2.Accept-Charset：浏览器可接受的字符集。

　　3.Accept-Encoding：浏览器能够进行解码的方式。

　　4.Content-Length：表示请求消息的长度。

　　5.Host：　客户端告诉服务器，想访问的主机名。

　　6.Cookie：客户端可以向服务器带数据，只是非常重要的信息之一。

## 3.空行

　　1.他的作用是告诉服务器 请求头部信息到此为止。

## 4.请求的数据

　　1.若方法是 GET，则该项为空。（数据都在url 地址栏里面）

　　2.若方法是 post 字段，则通常放置的是要 提交的数据。

# 二：响应报文  ： 响应头，响应行，响应主体。

## 1.响应行

　　1.协议版本

　　2.状态码

## 2.响应头

　　1.Allow  （支持那些请求的方法。如：get post）

　　2.Content- Type：表示属于什么类型文档。一般默认是 text/plain.通常指定为 text/html

　　3.Date：当前的GMT时间。

　　4.Expires：告诉浏览器把回送的资源缓存多长时间，-1或0则是不缓存。

　　5.Last-Modified：文档的最后改动时间。客户可以通过If-Modified-Since请求头提供一个日期，该请求将被视为一个条件GET，只有改动时间迟于指定时间的文档才会返回，否则返回一个304(Not Modified)状态。

　　6.Location：这个头配合302状态码使用，用于重定向接收者到一个新URI地址。表示客户应当到哪里去提取文档。Location通常不是直接设置的，而是通过HttpServletResponse的sendRedirect方法

　　7.Refresh：告诉浏览器隔多久刷新一次，以秒计。

　　8.Server：服务器通过这个头告诉浏览器服务器的类型。

　　9.Set-Cookie：设置和页面关联的Cookie。Servlet不应使用response.setHeader(“Set-Cookie”, …)，而是应使用HttpServletResponse提供的专用方法addCookie。

　　10.Transfer-Encoding：告诉浏览器数据的传送格式。

　　11.WWW-Authenticate：客户应该在Authorization头中提供什么类型的授权信息?在包含401(Unauthorized)状态行的应答中这个头是必需的。

　　12.setDateHeader方法和setIntHeadr方法专门用来设置包含日期和整数值的应答头，前者避免了把Java时间转换为GMT时间字符串的麻烦，后者则避免了把整数转换为字符串的麻烦。

　　13.setContentType：设置Content-Type头。大多数Servlet都要用到这个方法。

　　14.setContentLength：设置Content-Length头。对于支持持久HTTP连接的浏览器来说，这个函数是很有用的。

　　15。addCookie：设置一个Cookie(Servlet API中没有setCookie方法，因为应答往往包含多个Set-Cookie头)。

## 3.响应体

　　1.可能是纯数据

　　2.可能是 HTML 页面。
  
  Cache-Control：
  Cache-Control是最重要的规则。常见的取值有private、public、no-cache、max-age，no-store，默认为private。

（1） max-age：用来设置资源（representations）可以被缓存多长时间，单位为秒；
（2） s-maxage：和max-age是一样的，不过它只针对代理服务器缓存而言；
（3）public：指示响应可被任何缓存区缓存；
（4）private：只能针对个人用户，而不能被代理服务器缓存；
（5）no-cache：在发布缓存副本之前，强制要求缓存把请求提交给原始服务器进行验证(协商缓存验证)。
（6）no-store：禁止一切缓存（这个才是响应不被缓存的意思）,缓存不应存储有关客户端请求或服务器响应的任何内容，即不使用任何缓存。
