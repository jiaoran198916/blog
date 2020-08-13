---
title: PHP中 超全局变量 $_SERVER 详解
tags: Server
categories: PHP
abbrlink: adf01bc2
date: 2020-08-13 11:28:59
---
`$_SERVER`是PHP中超全局变量之一，存储的是服务器、请求和执行环境等的信息，包括 headers, paths, script locations.  
内容（entries）是由 web 服务器创建的，所以具体可能会有所不同，完整列表可参看 [» CGI/1.1 specification](http://www.faqs.org/rfcs/rfc3875.html).
<!-- more -->
下面列出一些常用的，有一些只在命令行模式下有效。

|  项 Entry | 描述 Description |
| ------------ | ------------ |
| PHP_SELF  | 当前运行脚本名，相对于文档根目录，如 http ://example.com/foo/bar.php -> /foo/bar.php.  |
| argv  | 命令行下，传递给脚本的参数数组，C风格  |
| argc  | 命令行下，传递给脚本的参数的个数  |
| GATEWAY_INTERFACE  | 使用的CGI和版本（revision）  |
| SERVER_ADDR  | 服务端IP  |
| SERVER_NAME  | 服务器名称，如果用虚拟主机则是配置的虚拟主机名  |
| SERVER_SOFTWARE  | 服务器使用的软件和版本  |
| SERVER_PROTOCOL  | 请求协议和版本  |
| REQUEST_METHOD  | 请求方法  |
| REQUEST_TIME  | 请求时间，时间戳格式  |
| REQUEST_TIME_FLOAT  | 请求时间，时间戳微秒（microsecond precision）  |
| QUERY_STRING  | 查询字符串  |
| DOCUMENT_ROOT  | 文档根目录  |
| HTTP_ACCEPT  | 请求接收的内容：Accept  |
| HTTP_ACCEPT_CHARSET  | 请求接收的字符集：Accept-Charset:'iso-8859-1,*,utf-8'  |
| HTTP_ACCEPT_ENCODING  | 请求接收的编码：Accept-Encoding:gzip  |
| HTTP_ACCEPT_LANGUAGE  | 请求接收的语言：Accept-Language:en  |
| HTTP_CONNECTION  | 请求连接类型：Connection:Keep-Alive  |
| HTTP_HOST  | 请求的主机：Host  |
| HTTP_REFERER  | 请求提交的页面  |
| HTTP_USER_AGENT  | 用户浏览器：User-Agent  |
| HTTPS  | 不为空如果是HTTPS访问  |
| REMOTE_ADDR  | 用户IP  |
| REMOTE_HOST  | 用户主机  |
| REMOTE_PORT  | 用户端口号  |
| REMOTE_USER  | 用户 The authenticated user.  |
| REDIRECT_REMOTE_USER  | The authenticated user if the request is internally redirected.  |
| SCRIPT_FILENAME  | 当前执行脚本的绝对路径  |
| SERVER_ADMIN  | 配置的管理员联系信息  |
| SERVER_PORT  | 服务器端口号  |
| SERVER_SIGNATURE  | 服务器签名信息，包含服务器软件版本和虚拟主机名  |
| PATH_TRANSLATED  | Filesystem  |
| SCRIPT_NAME  | 当前脚本路径  |
| PHP_AUTH_DIGEST  | When doing Digest HTTP authentication this variable is set to the 'Authorization' header  |
| PHP_AUTH_USER  | HTTP authentication ，用户  |
| PHP_AUTH_PW  | HTTP authentication ，密码  |
| AUTH_TYPE  | HTTP authentication ，类型  |
| PATH_INFO  | Contains any client-provided pathname information.  |
| ORIG_PATH_INFO  | PHP处理前的，PATH_INFO的最初状态  |
| HTTP_X_FORWARDED_FOR  | 用户加代理后的IP列表  |
| HTTP_CLIENT_IP  | 客户端IP  |
