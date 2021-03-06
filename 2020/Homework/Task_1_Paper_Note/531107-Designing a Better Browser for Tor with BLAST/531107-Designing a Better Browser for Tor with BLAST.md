**论文标题**：Designing a Better Browser for Tor with BLAST

**论文作者**：Tao Wang Department of Computer Science and Engineering Hong Kong University of Science and Technology

**出处**：NDSS 2020

**简要信息**：Tor是一个非常成功的匿名网络，但使用Tor访问互联网时，速度非常缓慢，文章通过一系列的实验与分析指出，Tor之所以速度很慢是因为大量的时间被浪费在RTT上，因此文章提出了一系列的方案减少服务器与客户端的往返通信次数，并基于此得到了很好的加速效果

![image-20200407194110232](http://alioss.hiram.wang/img/image-20200407194110232.png)

## 内容笔记

**背景：**

①Tor是一个非常成功的匿名网络

②Tor的一个极其关键的缺点在于其打开页面的速度极其缓慢，往往打开一个页面需要16-19秒

**研究铺垫：**

①制作一个叫做BLAST的模拟工具，来模拟用户操作并进行数据统计，同时还能在条件改变的情况下预测新的页面加载时间，以便进行实验

②介绍了有关于Web资源、TCP链接、队列等计算机网络基础知识

③给出了Tor加载慢的可能原因分析：如资源分布在大量不同服务器上，浪费握手时间、大量以及深层次的Web资源等

④给出了加载时间的计算方法以及相关定义

**现有技术分析：**

一、PIPELINING

原理：并行请求资源

现状：曾经被使用，但由于效率提升不明显，且维护困难，后来被废除

效果：确实可以减少加载时间，可以增强资源加载能力

问题：

​	Head-of-line blocking：虽然浏览器并行请求，但Web服务器仍然只能一个个按照顺序回复，因此还是会造成延迟；

​	Pipelining Errors：大量服务器不兼容PIPELINING，因此会造成响应错误

​	Depth：选择好的并发数非常重要，过大的并发数会导致服务器响应错误和服务器端的延时，而过小的并发数又达不到效果

实验分析：经过带有PIPELINING请求的实验，大部分时间都消耗在了Quene Delay上，可能是由于PIPELINING的错误造成的

​	Head-of-line blocking：只有0.2%的数据包主要收到了该因素的影响，因此不是非常严重

​	Pipelining Errors：错误率非常高，以至于让这个方法几乎没有价值

​	Depth：选择不同的并发数似乎没有太大影响

总结：Pipelining可以极大提高浏览器的资源加载能力，但由于服务器的兼容性问题，最终效果并不理想

二、HTTP/2

原理：采用多路复用技术而不是仅仅建立多个链接

现状：HTTP/2已经替代了上面的Pipelining，并成为了Tor中正在使用的技术，但是虽然HTTP/2在网络中广泛使用，其在匿名网络中的表现没有得到验证

问题：

​	Head-of-line blocking：由于其传输层协议还是TCP，因此HTTP/2仍旧会受到该因素的影响

​	Transfer rate：由于HTTP/2的单链接特性，其更易受网络拥塞的影响，特别是像Tor这样糟糕的网络

​	Premature connection close：对于遇到错误的处理可能导致更严重的丢包

​	ALPN：由于会话前需要确认服务器是否支持HTTP/2，因此会增加一次RTT

实验分析：综合实验结果甚至比HTTP1.1+Pipelining更糟糕，这很让人惊讶

​	大部分服务器都支持HTTP2

​	经过具体分析，http2的确对资源加载时间有优化，但对于页面的整体加载时间，http2的优势却消失了，原因在于在加载一些分布在不同的服务器上的资源时，HTTP2的表现比较糟糕

总结：HTTP2甚至还不如刚刚的那个

**新技术提出：**

从上面的现有技术分析可以看出，现有的技术并不能解决Tor慢的问题

为什么呢？因为现有的技术提高的都是浏览器的资源加载能力，但目前拖慢Tor的并不是这个因素，而恰恰是RTT

因此我们要加快Tor的速度，就必须将RTT耗时降低到最低

因此作者主要提出了两个方面来降低RTT耗时

一、降低加载一个资源所需要耗费的RTT

​	TCP Fast Open：对于已经建立连接的服务器，在请求一个另外的资源的时候，无需再建立一个新的连接

​	Optimistic data：将以前需要两次请求才能完成的操作合并成一次请求，比如把TCP连接的建立请求和Request请求合并到一起，把TLS握手包和TCP握手包合到一起等等

​	0-RTT TLS：主要是为了降低TLS握手的耗时，也就是让客户端记住之前已经协商好的密钥，并直接在新的会话中使用

二、降低加载整个Web页面所需要耗费的RTT

​	Redirection database：维护一个跳转数据库，把所有相关的跳转记录下来，避免无谓的请求

​	HTTP/2 database：记录支持HTTP2的网站服务器，发起HTTP2的请求之前就无需再发ALPN包确认是否支持HTTP2

​	Prefetching database：记录常用网站需要加载的资源树，在拉取Web页面的同时就可以开始拉取资源，提高效率

实验结果表明这些措施可以将页面的平均加载时间降低61%

除了单纯加速，Tor作为一个匿名网络，作者还考虑到了这些措施对其匿名性的影响

值得称赞的是，这些措施不仅没有降低匿名性，反而更好的对抗了当前网站使用的用户指纹技术，进一步提升了匿名性，同时也加快了Tor的运行速度

最为重要的是，这些措施都不需要服务器端的升级，只需要更改客户端代码即可，使得其有很高的可行性。

**相关研究**：

作者指出对于改进浏览器设计的相关研究并不多，大部分研究都致力于通过改进拥塞控制，或者是带宽等条件来提升Tor的速度，这也是这篇文章重要的创新性所在

与此同时，作者还提出提升Tor的性能能吸引更多的用户，让网站对于使用Tor的用户追踪更加困难，让匿名网络更匿名；这篇文章提出的方法既可以对抗浏览器指纹，又可以提升加载速度，具有很强的实用性意义。



## **创新点**

这篇文章是比较偏向工程性的文章，因此其实本身创新点不是很明显。但这篇文章对于Tor网络速度慢的这个角度展开研究，和其他研究不同，文章并没有着重于提升网络带宽或者服务器性能，而是从浏览器本身的改进入手，通过一些简单的无需服务器端太多参与的改进，极大的提升了Tor匿名网络的效率，具有一定的创新性。



## 不足之处

本文也存在一些不足，主要如下：

①文章对于背景知识介绍得过多，导致文章本身比较冗长

②文章标题拟的不好，BLAST这个自定义名字的工具凭空出现在标题里面，让人不明所以

③文章摘要缺乏一定的逻辑性，与文章正文递进关系不符，文章正文先讨论了HTTP2和管道技术才引出RTT问题，但文章摘要中恰好相反，因此缺乏一定逻辑性

