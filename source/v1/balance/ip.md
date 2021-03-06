---
title: 负载均衡-IP负载
---

## TCP/IP协议

- 首先让我们来看看下面这张大家都非常熟悉的TCP/IP协议族的分层图：

<div style="padding-left:30%"><img src="../../../images/balance/ip.jpg" style="max-width:500px;"></div>

- 关于每层在网络数据包传输过程中所起到的作用不是本文的重点，本文主要是讲解如何在网络层中使用IP来做服务器集群的负载均衡，为什么可以在这一层来做负载均衡。下面在来看IP协议的报头格式：

<div style="padding-left:30%"><img src="../../../images/balance/ip-2.png" style="max-width:500px;"></div>

- 内红色框内的源地址和目的地址是IP负载均衡功能的关键所在，IP负载均衡又可以称之为网络层负载均衡，其核心原理就是通过内核驱动更改IP的目的地址来完成数据负载均衡的，如下图：

<div style="padding-left:30%"><img src="../../../images/balance/ip-3.png" style="max-width:500px;"></div>

- 如上图所示，用户请求数据包（源地址为200.110.50.1）到达负载均衡服务器114.100.20.200后，负载均衡服务器在内核进程获取网络数据包，根据一定的负载均衡算法得到一台内部的真实服务器192.168.1.1，然后将数据包的目的IP修改为192.168.1.1，此后数据包将会被发往192.168.1.1的服务器上，服务器处理完后，将向负载均衡服务器返回相应的数据包，负载均衡服务器在把源地址修改为114.100.20.200后将数据包传输给用户浏览器。在这一整个过程中，数据包没有通过用户的应用进程，因此该负载均衡的性能是非常之高的。

- 根据以上的图和上文的讲解，大家可能会觉得这很容易实现，其实不然，在这里需要处理关键的地方就是如何将集群内部服务器处理完后的数据返回给负载均衡服务器。因为，用户请求的数据包到达负载均衡服务器前的目的地址是114.100.20.200，源地址是200.110.50.1，通过负载均衡服务器修改后的目的地址是192.168.1.1，源地址还是200.110.50.1，所以处理后返回的数据包目的地址将是200.110.50.1，源地址是192.168.1.1，最终返回的数据包要回到负载均衡服务器就成了问题。

- 解决的办法大概有如下两种：
1)、负载均衡服务器使用双网卡，一个对内一个对外，在修改请求数据包的目的IP的同时也修改源地址，将源地址设为自身的IP，即源地址转换（SNAT），这样内部集群服务器响应会再回到负载均衡服务器；
2)、将负载均衡服务器作为真实物理服务器集群的网关服务器，这样所有的响应都将通过负载均衡服务器。

- IP负载均衡在内核进程完成数据分发，处理性能得到了很好的提高。但是由于所有请求和响应都要经过负载均衡服务器，集群的最大响应数据吞吐量将受到负载均衡服务器网卡带宽的限制，对于提供下载服务或者视频服务等需要大量传输数据的站点而言，这是难以满足需求的。要是能让响应数据包绕过负载均衡服务器直接发往用户机器上就好了，有什么办法可以做到呢？当然有，那就是链路层的负载均衡，这将在下一博文中讲解。
