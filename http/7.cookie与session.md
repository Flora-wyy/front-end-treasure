### 什么是cookie？
  cookie是一段不超过4KB的小型文本数据，由一个名称（Name）、一个值（Value）和其它几个用于控制Cookie有效期、安全性、使用范围的可选属性组成。  
  cookie分为会话和持久性，会话cookie是一种临时的cookie，它记录了用户访问站点时的设置和偏好，退出浏览器时，会话cookie则删除，持久cookie的生存时间更长，它存储在硬盘上，浏览器退出，计算机重启时他们依旧存在，通常用持久cookie维护某个用户周期性访问的站点配置文件或登录名。  
会话cookie与持久cookie之间区别就是它们的过期时间，cookie通常由服务器Set-cookie首部贴到用户身上  
cookie规范正式名称叫做HTTP状态管理机制，cookie的基本思想是浏览器积累一组服务器特有的信息，每次访问服务器都将这些信息提供给它，不同的站点会使用不同的cookie  
  
Cookie 主要用于以下三个方面：  
1、会话状态管理（如用户登录状态、购物车、游戏分数或其它需要记录的信息）  
2、个性化设置（如用户自定义设置、主题等）  
3、浏览器行为跟踪（如跟踪分析用户行为等）  

### cookie的组成
|属性|描述|
|----|----|
|NAME=VALUE|强制的，除非包含双引号不然不包括分号、逗号、等号和空格。如Set-Cookie: name=zy|
|Expires|可选，指定一个日期字符串，用来定义cookie的实际生存期，格式为Weekday, DD-MON-YY HH:MM:SS GMT,唯一合法的时区为GMT,若没有设置该项则会话结束后过期，如Set-Cookie: name=zy; expires=Mon, 15-Feb-2021 07:15:20 GMT|
|Max-Age|在 cookie 失效之前需要经过的秒数。秒数为 0 或 -1 将会使 cookie 直接过期。一些老的浏览器（ie6、ie7 和 ie8）不支持这个属性。对于其他浏览器来说，假如二者 （指 Expires 和Max-Age） 均存在，那么 Max-Age 优先级更高|
|Domain|可选，浏览器指定域中服务器主机名发送cookie，这样就将服务器cookie限制在特定的域中，如果没有指定则默认生成响应服务器的主机名|
|Path|可选，这个属性是可以为服务器上特定的文档分配cookie，如果没有设置则默认生成产生cookie响应的url路径|
|Secure|可选，如果包含这个属性，就只有在HTTP使用SSL安全连接时才能发送cookie
|HttpOnly|设置了 HttpOnly 属性的 cookie 不能使用 JavaScript 经由  Document.cookie 属性、XMLHttpRequest 和  Request APIs 进行访问，以防范跨站脚本攻击（XSS）|
名称中包含 __Secure- 或 __Host- 前缀的 cookie，只可以应用在使用了安全连接（HTTPS）的域中，需要同时设置 secure 指令。另外，假如 cookie 以 __Host- 为前缀，那么 path 属性的值必须为 "/" （表示整个站点），且不能含有 domain 属性。对于不支持 cookie 前缀的客户端，无法保证这些附加的条件成立，所以 cookie 总是被接受的 

### 什么是Session？
Session是另一种记录客户状态的机制，不同的是Cookie保存在客户端浏览器中，而Session保存在服务器上。客户端浏览器访问服务器的时候，服务器把客户端信息以某种形式记录在服务器上。这就是Session。客户端浏览器再次访问时只需要从该Session中查找该客户的状态就可以了, 通常服务端执行session机制时候会生成session的id值，这个id值会发送给客户端，客户端每次请求都会把这个id值放到http请求的头部发送给服务端，而这个id值在客户端会保存下来，保存的容器就是cookie，因此当我们完全禁掉浏览器的cookie的时候，服务端的session也会不能正常使用
