## DNS概念
域名解析服务器
### 流程（无LocalDNS缓存命中）
1、访问域名时，向localDNS 查询IP
2、无缓存命中，转向rootDNS查询域名授权DNS
3、rootDNS将授权DNS访问记录回应LocalDNS
4、LocalDNS向授权DNS查询ip
5、域名授权DNS查询记录返回LocalDNS
6、LocalDNS回应IP给客户端
7、客户端访问IP地址
8、服务返回内容

## CDN概念
内容分发网络
### 流程（无LocalDNS缓存命中）

1、访问域名时，向localDNS 查询IP，
2、无缓存命中，转向rootDNS查询域名授权DNS
3、rootDNS将授权DNS记录回应LocalDNS
4、LocalDNS向授权DNS查询ip
5、授权DNS返回CNAME域名（Canonical name别名 ）的ip
6、LocalDNS 将请求发送到域名调度DNS，并为请求分配最佳节点IP地址
7、LocalDNS返回IP给客户端
8、客户端访问IP地址
9、服务器（命中缓存返回，未命中回源并缓存）返回内容