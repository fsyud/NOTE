# 一、XSS

## 1、概述
Cross-Site Scripting（跨站脚本攻击）简称 XSS，是一种代码注入攻击。攻击者通过给目标网站注入脚本，诱导用户点击，使得脚本最终在用户的浏览器上执行。为了和 CSS区分，改名为 XSS。

利用注入的脚本，能干的坏事有：

- 注入脚本获取信息
- 窃取用户Cookie，为接下来的CSRF做准备
- 绕过网页过滤进行攻击
- 劫持流量，实现恶意跳转


## 2、XSS 分类
### 2.1、 存储型 XSS（持久型XSS）

攻击步骤：

1. 恶意代码被攻击者提交到目标网站上，最终存储在目标网站的数据库中。
2. 用户打开网站后，网站服务器从数据库中返回拼接在 HTML 中的恶意代码，被用户执行。
3. 最终导致，恶意代码窃取用户数据发送给攻击者或者在当前浏览器上，利用用户数据，直接冒充用户行为，调用目标网站接口完成攻击者的指定操作。


### 2.2 反射型 XSS（非持久型XSS）

攻击步骤：

1. 攻击者构造含有恶意代码的 URL，诱导用户点击
2. 用户点击 URL 后，向服务器发起请求，服务器将恶意代码从URL中取出，拼接在 HTML里返回给浏览器
3. 用户浏览器接收到响应后，直接执行恶意代码
4. 会导致的后果同上
5. 
### 2.3 DOM型 XSS

攻击步骤：

1. 类似反射型 XSS。攻击者构造含有恶意代码的 URL，诱导用户点击
2. 用户点击后，此时没有向服务器发起请求，而是被前端的 Javascript 直接取出 URL 中的恶意代码并执行会导致的后果同上

## 3、防范
1. HTML 转义
2. CSP
3. 过滤能够注入脚本的标签，如 < script>、< img>、< a>等
4. 为防止 Cookie 盗用，在 http 响应头部设置 HttpOnly
5. 验证码
6. 输入内容长度控制，增加 XSS 攻击难度

# 二、CSP
## 1、概述
Content-Security-Policy（内容安全策略）简称 CSP，本质上是设立白名单，规定浏览器只能执行指定域名的代码，可防止 XSS 攻击。

## 2、使用方法
在 http 头部定义 Content-Security-Policy：

```js
Content-Security-Policy: default-src https://example.com https://example2.com; object-src 'none'

```

**或使用 meta 标签代替**

```js
<meta
  http-equiv="Content-Security-Policy"
  content="default-src https://example.net; child-src 'none'; object-src 'none'"
/>

```
可以看到服务器的响应，带有该头部信息：

![](https://img-blog.csdnimg.cn/2020122716382216.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0RyZWFteV9MSU4=,size_16,color_FFFFFF,t_70)

使用了 CSP 后，即便受到了 XSS 攻击，也不会加载不明来源的脚本。


# 三、CSRF


## 1、概述
Cross-site request forgery（跨站请求伪造）简称 CSRF，冒充用户在自动登录的网站上（带有Cookie），执行用户非本意的操作。

XSS 利用的是用户对网站的信任，CSRF 利用的是网站对用户的信任，进行攻击。

## 2、举例
- 第三方恶意网站自动提交跨域请求
一家银行的转账接口如下：

```js
http://example.com/withdraw?account=name&money=1000&for=name
```

第三方网站放置了如下代码：

```js
<img src="http://exampe.com/withdraw?account=Jack&money=1000&for=evil">
```

当用户点击了第三方网站，第三方网站向银行发起转账请求，由于之前已登录了银行，登录信息还未过期，便完成了转账。

现在银行会通过再次手动输入支付密码或短信验证，去防范。

- 结合 XSS 获取 Cookie
通过 XSS 获取了 Cookie后，打开网站登录界面，调出 Chrome dev tool，进入如下：

![](https://img-blog.csdnimg.cn/20201227175542744.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0RyZWFteV9MSU4=,size_16,color_FFFFFF,t_70)


新增 Cookie，设置更长的过期时间后，刷新页面，直接进入登录后页面，开始恶意操作。

## 3、防范
检查 referer 字段，只有在允许的地址下才能请求成功
添加校验 token，防止 XSS 攻击
更详细内容，可参看以下链接


转载: https://blog.csdn.net/Dreamy_LIN/article/details/111773344
