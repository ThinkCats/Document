OpenSSL + Nginx + Tomcat 构建 Https 
===
### 1. OpenSSL 证书制作
#### （1） 安装 OpenSSL 工具
  安装后将安装目录加入到环境变量中。
#### （2） 制作证书
   - A. 生成SSL 证书
 ```
 openssl genrsa -des3 -out mykey.pem 2048
 ```
 
  - B. 生成 CA 证书
```
openssl req -new -x509 -days 3650 -key mykey.key -out mykey.crt
```

### 2. Tomcat 配置
使用上一步生成的两个key，配置tomcat的 server.xml (此处是8443安全端口)
```
	<Connector 
	       SSLCertificateFile="F:\CA\mykey.crt"	
	       SSLCertificateKeyFile="F:\CA\mykey.pem" SSLPassword="123456"	       
	       SSLEnabled="true" URIEncoding="UTF-8" maxThreads="150" port="8443" protocol="HTTP/1.1"
		scheme="https" secure="true" sslProtocol="TLS" />
```

### 3. Nginx 配置
#### (1) 运行nginx (windows)
cmd 进入nginx目录，执行：
```
start  nginx.exe -c conf/nginx.conf
```
其他命令：
```
nginx -s stop	--fast shutdown
nginx -s quit	--graceful shutdown
nginx -s reload	--changing configuration, starting new worker processes with a new configuration, graceful shutdown of old worker processes
nginx -s reopen	--re-opening log files
```

#### (2) `TODO`