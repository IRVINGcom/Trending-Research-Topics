- 原文题目：Data Security and Trading Framework for Smart Grids in Neighborhood Area Networks 
- 原文作者：Jayme Milanezi Junior , João Paulo C. L. da Costa...
- 原文链接：https://www.mdpi.com/1424-8220/20/5/1337/htm
- 笔记作者：赵振宇 2017141411124

# 研究内容 #
本文提出了一个框架，该框架保留了生产者身份的保密性，并在竞争激烈的邻域网（NAN）的竞争性市场中提供了针对流量分析攻击的保护。此外，该框架还向恶意攻击者隐藏了投标者和中标者的数量。由于投标人需要小的数据吞吐量，因此框架的通信链路基于专有的通信系统。不过，在数据安全性方面，由于采用了XOR密钥的高级加密标准（AES）128位，因为它们降低了计算复杂性，可以实现快速处理。框架在逐个消费者的设计中在隐私保护和交易灵活性方面优于最新的解决方案。
# 创新点 #
## 面向隐私的数据安全系统 ##
- 提供一种低功耗处理解决方案。
- 避免生成密钥对
- 为TTP解决安全分配给每个设备一个硬编码AES密钥的任务

## 交易系统框架 ##
主要算法如下图：

![](https://pic.downk.cc/item/5ea9511fc2a9a83be538932c.png)

# 缺点 #
我认为该文章提出的框架中，恶意观察者可能会通过流量分析或地址匿名化来识别利益相关方，即观察者可以通过此类攻击识别参与者的角色。