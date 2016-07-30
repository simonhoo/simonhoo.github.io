---
layout: post
title:  "解决Thrift Client大量句柄导至资源不够用的问题"
date:   2015-01-05
desc: "我的书单"
keywords: "Java,Thrift,句柄打开过多,系统架构,木偶人,胡登军,Simon"
categories: [Java,Architecture]
tags: [Java,Thrift,句柄打开过多,系统架构]
icon: fa-java
---

由于Thrift的RPC通讯走的是TCP/IP协议，而且是短连接，就意味着消费者端都不停的打开SOCKET连接和关闭SOCKET连接，如果该动作发生的频率过高，就会导至Client端有大量的TIME_WAIT状态的句柄，在Windows中，默认是有4份钟，也就是240秒的延迟，并且端口上限有限制。

为了解决这个问题除了修改操作系统配置之外，我们的应用也需要进行处理，在我们创建SOCKET时，需要做如下处理:

```
/**
 * 初始化，创建TTransport实例
 * 
 * @author Simon Hoo
 * @throws ThriftException
 */
public void init() throws ThriftException {
	try {
		Socket s = new Socket(hostIp, port);
		s.setReuseAddress(true);
		s.setSoTimeout(timeout);
		transport = new TSocket(s);
		if (!transport.isOpen()) {
			transport.open();
		}
	} catch (TTransportException e) {
		throw new ThriftException(e);
	} catch (SocketException e) {
		throw new ThriftException(e);
	} catch (UnknownHostException e) {
		throw new ThriftException(e);
	} catch (IOException e) {
		throw new ThriftException(e);
	} catch (Exception e) {
		throw new ThriftException(e);
	}
}
```

重点是下面这几行, 每次打开时，先进行判断:

```
if (!transport.isOpen()) {
	transport.open();
}
```
