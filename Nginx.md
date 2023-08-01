# Nginx简介

## 一、Nginx概述

> Nginx（engine x）是一个高性能的**HTTP**和**反向代理**web服务器，同时也提供了**IMAP/POP3**/SMTP服务。特点是**占有内存少**，**并发能力强**。
>
> 中国大陆使用nginx网站用户有：百度、京东、新浪、网易、腾讯、淘宝等。

### 1.Nginx作为Web服务器

Nginx可以作为静态页面的web服务器。同时还支持CGI协议的动态语言，比如perl、php等。但是不支持Java，Java程序只能通过tomcat配合完成。

Nginx专为性能优化而开发，性能是其最重要的考量，实现上非常注重效率，能经受高负载的考验。

https://lnmp.org/nginx.html

### 2.反向代理

#### 2.1 正向代理

**在客户端（浏览器）配置代理服务器**，通过代理服务器进行互联网访问。

![image-20230713143513868](https://gitee.com/v876774538/my-img/raw/master/image-20230713143513868.png)

#### 2.2 反向代理

反向代理，客户端对代理是无感知的，因为**客户端不需要任何配置**就可以进行访问：我们**只需要将请求发送到反向代理服务器，由反向代理服务器去选择目标服务器获取数据后，再返回给客户端**，此时反向代理服务器和目标服务器对外就是一个服务器，**暴露的是代理服务器地址，隐藏了真实服务器的IP地址**。

![image-20230713144410687](https://gitee.com/v876774538/my-img/raw/master/image-20230713144410687.png)

正向代理保护客户端，反向代理保护服务端。 

### 3.负载均衡

客户端发送多个请求到服务器，服务器处理请求，有一些可能需要与数据库进行交互，服务器处理完毕后，再将结果返回给客户端。

![image-20230713144738865](https://gitee.com/v876774538/my-img/raw/master/image-20230713144738865.png)

这种架构模式对于早期的系统相对单一、并发请求相对较少的情况下是比较合适的，成本也低。

但是随着信息数量的不断增长，以及系统业务复杂度的增加，这种架构会造成服务器相应客户端的请求日益缓慢，在并发量特别大的时候，还容易造成服务器直接崩溃。

这时候集群的概念产生了，单个服务器解决不了，我们可以**增加服务器的数量，然后将请求分发到各个服务器上，将负载分发到多个不同的服务器**，这就是我们所说的**负载均衡**。

![image-20230713145417183](https://gitee.com/v876774538/my-img/raw/master/image-20230713145417183.png)

### 4.动静分离

为了加快网站的解析速度，可以把动态页面和静态页面交由不同的服务器来解析，加快解析速度，降低原来单个服务器的压力。

#### 4.1 动静不分离

![image-20230713145923807](https://gitee.com/v876774538/my-img/raw/master/image-20230713145923807.png)

#### 4.2 动静分离

![image-20230713152942035](https://gitee.com/v876774538/my-img/raw/master/image-20230713152942035.png)

## 二、Nginx安装

1. 使用远程连接工具连接linux操作系统

   Xshell7中文破解版下载：http://www.itmind.net/118813.html

   ![image-20230713153704872](https://gitee.com/v876774538/my-img/raw/master/image-20230713153704872.png)

2. 安装pcre依赖

   - 联网下载pcre压缩文件依赖

     ```shell
     wget http://downloads.sourceforge.net/project/pcre/pcre/8.37/pcre-8.37.tar.gz
     ```

   - 解压压缩文件

     ```shell
     tar –xvf pcre-8.37.tar.gz
     ```

   - 配置

     ```shell
     ./configure
     ```

   - 编译

     ```shell
     make
     ```

   - 安装

     ```shell
     make install
     ```

   - 查看pcre依赖是否安装成功

     ```shell
     pcre-config --version
     ```

3. 安装openssl、zlib、gcc依赖

   ```shell
   yum -y install make zlib zlib-devel gcc-c++ libtool openssl openssl-devel
   ```

4. 安装nginx

   - 下载

     1. 官网下载.tar .gz安装包

        https://nginx.org/en/download.html

     2. wget命令下载，确保系统已经安装了wget，如果没有安装，执行` yum install wget `安装。

        ```shell
        wgte https://nginx.org/download/nginx-1.21.6.tar.gz
        ```

   - 解压

     ```shell
     tar xvf nginx-1.21.6.tar.gz
     cd nginx-1.21.6
     ```

   - 配置

     ```shell
     ./configure
     ```

   - 编译安装

     ```shell
     make && make install
     ```

     安装成功后，在usr多出一个文件夹local/nginx，文件夹下的**sbin**中有启动脚本

     启动：

     ```shell
     ./nginx
     ```

     ![image-20230713165834967](https://gitee.com/v876774538/my-img/raw/master/image-20230713165834967.png)

5. 安装后无法访问的，需要对防火墙进行设置，也可以直接关闭防火墙，并防止防火墙自启动（仅限练习）

   ```shell
   //关闭防火墙&&防火墙自启
   systemctl stop firewalld && systemctl disable firewalld
   
   //安装Iptables管理工具&&启动Iptables&&设为Iptables开机自启&&清空Iptables规则&&保存Iptables默认规则
   yum -y install iptables-services && systemctl start iptables && systemctl enable iptables&& iptables -F && service iptables save
   ```

   - 查看开放的端口

     ```shell
     firewall-cmd --list-all
     ```

   - 设置开放的端口

     ```shell
     firewall-cmd --add-service=http –permanent
     firewall-cmd --add-port=80/tcp --permanent
     ```

   - 重启防火墙

     ```shell
     firewall-cmd --reload
     ```

6. 访问成功

   ![img](https://img2018.cnblogs.com/blog/1455597/201910/1455597-20191029102622854-1627774877.png)

## 三、Nginx常用命令

注：使用nginx操作命令需要进入nginx的目录 `cd /usr/local/nginx/sbin`

### 1.查看nginx版本号

```shell
./nginx -v
```

### 2.启动nginx

```shell
./nginx	 //直接nginx启动，前提是配好nginx环境变量

systemctl start nginx.service //使用systemctl命令启动

// 查看是否启动成功
ps -ef|grep nginx
```

![img](https://img2018.cnblogs.com/blog/1455597/201910/1455597-20191029102726015-172811692.png)

### 3.停止nginx

```shell
./nginx -s stop
```

![image-20230713171443398](https://gitee.com/v876774538/my-img/raw/master/image-20230713171443398.png)

### 4.重新加载nginx

```shell
./nginx -s reload
```

### 5.查看nginx运行状态

```shell
./nginx -t
```

### 6.查看nginx配置文件位置

```shell
sudo find / -name nginx.conf
```



## 四、nginx.conf配置文件

### 1.位置

`/usr/local/nginx/conf/nginx.conf`

### 2.配置文件中的内容

#### 2.1 全局块

> 配置服务器整体运行的配置指令。

从配置文件到events块之间的内容，主要会设置一些影响nginx服务器整体运行的配置指令：包括**配置运行Nginx服务器的用户（组）**、**允许生成的worker process数**、**进程PID存放路径**、**日志存放路径和类型**，以及**配置文件的引入**等。

![img](https://gitee.com/v876774538/my-img/raw/master/1455597-20191029102802614-510328292.png)

```nginx
worker_processes	1;
```

这是Nginx服务器并发处理服务的关键配置。`worker_processes`的值越大，可以支持的并发处理量也越多，但是会受到硬件、软件等设备的制约。

#### 2.2 events块

> 影响Nginx服务器与用户的网络连接。

events块设计的指令主要影响Nginx服务器与用户的网络连接。常用的设置包括**是否开启对多work process下的网络连接进行序列化**，**是否允许同时接收多个网络连接**，**选取哪种事件驱动模型来处理连接请求**，**每个work process可以同时支持的最大连接数**等。

![img](https://gitee.com/v876774538/my-img/raw/master/1455597-20191029102827884-232471630.png)

```nginx
worker_connections	1024;
```

表示每个 work process 支持的最大连接数为 1024。

#### 2.3 http块

> 代理、缓存和日志定义等绝大多数功能和第三方模块的配置。

![img](https://gitee.com/v876774538/my-img/raw/master/1455597-20191029102837788-914776640.png)

1. http全局块

   http全局块配置的指令包括文件引入、MIME-TYPE定义、日志自定义、连接超时时间、单链接请求数上限等。

   ![img](https://gitee.com/v876774538/my-img/raw/master/1455597-20191029102851922-1592334025.png)

2. server块

   与虚拟主机密切相关。从用户角度看，虚拟主机和一台独立的硬件主机是完全一样的，该技术的产生是为了节省互联网服务器硬件成本。

   **每个http块可以包含多个server块，而每个server块就相当于一个虚拟主机。**

   ![image-20230718164943968](https://gitee.com/v876774538/my-img/raw/master/image-20230718164943968.png)

   ```nginx
   listen		80;			// 监听的端口号为80
   server_name	localhost;	// 主机名称
   ```

3. 全局server块

   本虚拟机主机的监听配置和本虚拟主机的名称或IP配置。

4. location块

   一个server块可以配置多个location块。

   主要作用是基于Nginx服务器接收到的请求字符串（如，`server_name/uri-string`），对虚拟主机名称（或IP别名）之外的字符串（`/uri-string`）进行匹配，**对特定的请求进行处理**。地址定向、数据缓存和应答控制等功能还有许多第三方模块的配置也在这里进行。

### 3.实例1

![image-20230718165530091](https://gitee.com/v876774538/my-img/raw/master/image-20230718165530091.png)

```nginx
server {
        listen       80;
        server_name  zjz.syy333.com;
        rewrite ^(.*) https://$server_name$1 permanent;
    }

 server {
        listen       443;
        server_name  zjz.syy333.com;
        access_log  /www/server/panel/logs/zjz.syy333.com.log;
        ssl_certificate   /www/server/panel/vhost/cert/zjz.syy333.com.pem;
        ssl_certificate_key  /www/server/panel/vhost/cert/zjz.syy333.com.key;
        ssl_session_timeout 5m;
        ssl_ciphers ECDHE-RSA-AES128-GCM-SHA256:ECDHE:ECDH:AES:HIGH:!NULL:!aNULL:!MD5:!ADH:!RC4;
        ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
        ssl_prefer_server_ciphers on;


        location /{
            proxy_pass   http://127.0.0.1:9000/;
	#    try_files $uri $uri/ /index.html;
        #    index  index.html index.html;
        }
        
        location /admin {
            alias  /usr/local/sarlisi/admin/;
            index  index.html index.htm;
        }
        
        location /main/ {
            proxy_pass  http://127.0.0.1:8088/;
        }
        
        location /api/ {
            proxy_pass  http://127.0.0.1:7010/;
        }
        
        location /file {
                alias /usr/local/sarlisi/file/;
        }

        #charset koi8-r;

        #location / {
        #    alias  /usr/local/sarlisicare/;
        #    index  index.html index.htm;
        #}

        #error_page  404              /404.html;

        # redirect server error pages to the static page /50x.html
        #
        #error_page   500 502 503 504  /50x.html;
        #location = /50x.html {
        #    root   html;
        #}

        }    
    
```

### 4.实例2

![image-20230801135852109](https://gitee.com/v876774538/my-img/raw/master/image-20230801135852109.png)

```nginx
server {
        listen       80;
        server_name  santime.co.jp www.santime.co.jp;
        rewrite ^ https://$http_host$request_uri? permanent;
        
        location /{
           alias   /usr/local/santime/santimeJapen/;
           add_header Access-Control-Allow-Origin *;
           add_header Access-Control-Allow-Headers X-Requested-With;
           add_header Access-Control-Allow-Methods GET,POST,OPTIONS;
           index  index.html index.htm;
        }
}

server {
		listen		443 ssl;
		server_name	santime.co.jp www.santime.co.jp;
		
		ssl_certificate   /usr/local/webserver/nginx/conf/cert/santime.co.jp_chain.crt;
        ssl_certificate_key  /usr/local/webserver/nginx/conf/cert/santime.co.jp_key.key;
        
        ssl_session_cache    shared:SSL:1m;
        ssl_session_timeout  5m;
        ssl_ciphers  HIGH:!aNULL:!MD5;
        ssl_prefer_server_ciphers  on;
        
        location /{
           alias   /usr/local/santime/santimeJapen/;
           add_header Access-Control-Allow-Origin *;
           add_header Access-Control-Allow-Headers X-Requested-With;
           add_header Access-Control-Allow-Methods GET,POST,OPTIONS;
           index  index.html index.htm;
        }
        
        location /api/ {
            proxy_pass  http://127.0.0.1:7010/;
        }
}

```



