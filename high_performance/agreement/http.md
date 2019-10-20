# http

## 简介

http协议是Hyper Text Transfer Protocol\(超文本传输协议\)的缩写，用于从万维网  
服务器传输超文本到本地浏览器的传送协议。  
  Http是一个属于应用层的面向对象的协议，于1990年提出，现在迭代到2.0版本，并有  
诸如Quic协议等还在发展中的协议。

## URL

HTTP使用同一资源标识符（uniform resource identifiers uri）来建立连接和传输数据，url是一种特殊的  
uri，全程是uniform resource locator，中文名称是统一资源定位符，是互联网上用来标识某一处资源的地址。  
一个完整的URL包括以下几部分：  
1.协议部分：该URL的协议部分为“http：”，这代表网页使用的是HTTP协议。在Internet中可以使用多种协议，如HTTP，FTP等等本例中使用的是HTTP协议。在"HTTP"后面的“//”为分隔符

2.域名部分：该URL的域名部分为“www.aspxfans.com”。一个URL中，也可以使用IP地址作为域名使用

3.端口部分：跟在域名后面的是端口，域名和端口之间使用“:”作为分隔符。端口不是一个URL必须的部分，如果省略端口部分，将采用默认端口

4.虚拟目录部分：从域名后的第一个“/”开始到最后一个“/”为止，是虚拟目录部分。虚拟目录也不是一个URL必须的部分。本例中的虚拟目录是“/news/”

5.文件名部分：从域名后的最后一个“/”开始到“？”为止，是文件名部分，如果没有“?”,则是从域名后的最后一个“/”开始到“\#”为止，是文件部分，如果没有“？”和“\#”，那么从域名后的最后一个“/”开始到结束，都是文件名部分。本例中的文件名是“index.asp”。文件名部分也不是一个URL必须的部分，如果省略该部分，则使用默认的文件名

6.锚部分：从“\#”开始到最后，都是锚部分。本例中的锚部分是“name”。锚部分也不是一个URL必须的部分

7.参数部分：从“？”开始到“\#”为止之间的部分为参数部分，又称搜索部分、查询部分。本例中的参数部分为“boardID=5&ID=24618&page=1”。参数可以允许有多个参数，参数与参数之间用“&”作为分隔符

## 请求格式

![http请求格式](https://github.com/whodarewin/knowledge_hierarchy/blob/master/high_performance/agreement/http_request.md)  
由上图可以看到，协议分为三个部分，  
请求行  
请求头  
请求数据

```
GET /562f25980001b1b106000338.jpg HTTP/1.1
Host    img.mukewang.com
User-Agent    Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/51.0.2704.106 Safari/537.36
Accept    image/webp,image/*,*/*;q=0.8
Referer    http://www.imooc.com/
Accept-Encoding    gzip, deflate, sdch
Accept-Language    zh-CN,zh;q=0.8
```

## 返回格式

图片稍后加

```
HTTP/1.1 200 OK
Server: nginx
Date: Mon, 20 Feb 2017 09:13:59 GMT
Content-Type: text/plain;charset=UTF-8
Vary: Accept-Encoding
Cache-Control: no-store
Pragrma: no-cache
Expires: Thu, 01 Jan 1970 00:00:00 GMT
Cache-Control: no-cache
Content-Encoding: gzip
Transfer-Encoding: chunked
Proxy-Connection: Keep-alive

{"code":200,"notice":0,"follow":0,"forward":0,"msg":0,"comment":0,"pushMsg":null,"friend":{"snsCount":0,"count":0,"celebrityCount":0},"lastPrivateMsg":null,"event":0,"newProgramCount":0,"createDJRadioCount":0,"newTheme":true}
```

第一行是状态行，最后一行是响应报文，中间是消息报头，注意，中间的消息报头和响应报文之间有空行。

## 数据传输

http协议是1990年提出的，伴随着网络的发展，最初的协议及传输方式已经不能满足现在的需求了，尤其是  
数据传输方面，经过了非常大的改动。

### 1.0
缺点：
1. 短连接，每个链接只能请求一次，链接无法复用，一个单独包含多个请求的网页加载速度会比较慢。
2. 每个域名每次只能同时建立一定数量的链接（建立多了有损性能）
### 1.1
优点：
1. 支持持久连接，
2. 使用pipline技术，一个连接可以发送多个请求（仅限于一个网页），一个请求发送出去以后，不用等待应答的到来，便可发送下一个请求。
缺点：
1. 使用pipline技术，如果先请求的数据没有返回，后续数据先于先请求的数据，则后续请求不会被处理，即仍然存在head of blocking问题。
2. 针对同一域名下的请求仍然有一定数量限制。
### 2.0
优点：
1. 多路复用，在应用层真正解决了head of blocking 问题（传输层仍然会存在这样的问题）。
2. 在应用层和传输层之间增加了二进制分帧层，将http的请求再次打散，支持了首部压缩和首部只发送一次的优化。
3. 在协议层面支持了服务端推送。

### quic
解决的问题：
1. 低延迟连接的建立。
2. 改进的拥塞控制
3. 基于udp，在tcp层面上避免了head of blocking 问题。



