#### XSS

##### 什么是XSS攻击
XSS(跨站脚本攻击)，通常指的是通过利用网页开发时留下的漏洞，通过巧妙的方法注入恶意指令代码到网页，使用户加载并执行攻击者恶意制造的网页程序。

##### XSS攻击原理
起因是网站没有对用户的输入进行严格的限制, 使得攻击者可以将脚本上传到帖子让其他人浏览到有恶意脚本的页面, 其注入方式很简单包括但不限于 JavaScript / VBScript / CSS / Flash 等.

当其他用户浏览到这些网页时, 就会执行这些恶意脚本, 对用户进行 Cookie 窃取/会话劫持/钓鱼欺骗等各种攻击. 其原理, 如使用 js 脚本收集当前用户环境的信息 (Cookie 等), 然后通过 img.src, Ajax, onclick/onload/onerror 事件等方式将用户数据传递到攻击者的服务器上. 钓鱼欺骗则常见于使用脚本进行视觉欺骗, 构建假的恶意的 Button 覆盖/替换真实的场景等情况 (该情况在用户上传 CSS 的时候也可能出现, 如早起淘宝网店装修, 使用 CSS 拼接假的评分数据等覆盖在真的评分数据上误导用户).

##### XSS攻击类型
- 反射型XSS:非持久化，欺骗用户去点击链接,攻击代码包含在url中,被用户点击之后执行攻击代码.

- 存储型XSS:持久型,攻击提交恶意代码到服务器，服务器存储该段代码,这样当其他用户请求后，服务器返回并发给用户，用户浏览此类页面时就可能受到攻击。例如:恶意用户的HTML或JS输入服务器->进入数据库->服务器响应时查询数据库->用户浏览器。

##### 防范与过滤

输入编码过滤:对于每一个输入，在客户端和服务器端验证是否合法字符，长度是否合法，格式是否正确,对字符进行转义.非法字符过滤.

输出编码过滤:对所有要动态输出到页面的内容，进行相关的编码和转义.主要有HTML字符过滤和转义,JS脚本转义过滤.url转义过滤.

设置http-only,避免攻击脚本读取cookie.