## 预防跨站脚本攻击攻击`XSS`

`XSS`最常见的就是网站输入框可以执行Javascript，这样别人可以构建一个网站执行javascript的链接群发，利用`Document.cookie`盗取别人的cookie

Javascript `Docuemnt.cookie` 无法访问带有HttpOnly属性的cookie，此类cookie仅作用于服务器

    Set-Cookie: id=a3fWa; Expires=Wed, 21 Oct 2015 07:28:00 GMT; HttpOnly

## 预防`man-in-the-middle`攻击

标记为 Secure 的 Cookie 只应通过被 HTTPS 协议加密过的请求发送给服务端

    Set-Cookie: id=a3fWa; Expires=Wed, 21 Oct 2015 07:28:00 GMT; Secure

## 预防阻止跨站请求伪造攻击`CSRF`

SameSite Cookie 允许服务器要求某个 cookie 在跨站请求时不会被发送

    Set-Cookie: key=value; SameSite=Strict

SameSite 可以有下面三种值：

* None。浏览器会在同站请求、跨站请求下继续发送 cookies，不区分大小写。

* Strict。浏览器将只在访问相同站点时发送 cookie。（在原有 Cookies 的限制条件上的加强，如上文 “Cookie 的作用域” 所述）

* Lax。与 Strict 类似，但用户从外部站点导航至URL时（例如通过链接）除外。 在新版本浏览器中，为默认选项，Same-site cookies 将会为一些跨站子请求保留，如图片加载或者 frames 的调用，但只有当用户从外部站点导航到URL时才会发送。如 link 链接

> [Cookies](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Cookies)

> [SameSite](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Set-Cookie/SameSite)

> [cookie not found](https://cloud.tencent.com/developer/article/1704653)