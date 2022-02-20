---
title: Python scrapy自动切换HTTP代理
tags: [python,scrapy]
categories: Python
date: 2021-8-20 10:27:28
---

使用Scrapy中间件动态修改代理IP



### 常见的反爬虫及应对策略

1. 通过检查Headers中的User-Agent或者Referer（为了防止盗链）值，应对策略：

	- `在请求的时候动态修改User-Agent值，或者将Referer设置为目标网站的域名地址`

2. 基于用户行为进行反爬虫，同一个IP很短的时间内多次进行访问，应对策略：

	- `爬取页面的时候设置阈值，每次抓取完页面sleep一段时间`

	- `使用IP代理，在抓取页面的时候动态的切换IP`

	- `只抓取动态请求的数据，不直接抓取整个页面`



### Scrapy中间件的使用

1.创建一个中间件对象，并实现`process_request(request, spider)`方法：

``` python
class HttpProxyMiddleware(object):
	def process_request(self, request, spider):
    	proxy = HttpProxy()
		#这里可以设置请求的user-agent
		#request.headers.setdefault('User-Agent', "Your user agent!")
		request.meta["proxy"] = proxy.get_random_ip()
```

这里的HttpProxy是写好的获取代理IP的工具类，返回代理格式：`[协议]://[IP]:[PORT]`

2.在setting.py中配置创建的中间件

``` python
DOWNLOADER_MIDDLEWARES = {

	'myprojects.middlewares.HttpProxyMiddleware': 300

}
```

#### 参考资料：

[github上的HttpProxyMiddleware](https://github.com/kohn/HttpProxyMiddleware)





