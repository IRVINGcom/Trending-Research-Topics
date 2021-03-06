# Smart Grid Security 笔记

* 论文标题 Achieving Efficientand Secure Data Acquisition for Cloud-supported Internet of Things in Smart  Grid
* 作者Zhitao Guan, Jing Li, Longfei Wu, Yue Zhang, Jun Wu, Xiaojiang Du 
* 出处 [IEEE Internet of Things Journal]('https://ieeexplore.ieee.org/abstract/document/7891593')
* 笔记：程明浩 2018141531078

## 论文内容

###  Problem

云物联网已经广泛运用与智能电网。物联网前端主要负责数据获取和状态监督，存储大量数据并发往云服务器管理。数据安全性与传输效率有很大挑战。

### Work

本文提出一种CP-ABE（基于密文策略属性加密），主要是从终端获取的数据划分为块，并行依次使用访问子树加密。这个方案有效降低时间成本流行的方法。

* 提出一种并行处理方法:数据从终端划分为块，依次对应访问子树加密，并行处理数据加密与传输。
* 约定双重秘钥共享方案保护访问树信息。只有合并密钥，加密数据才能被恢复。每一块数据都会有一个密钥。最后一个密钥由其他数据保护。

### solve

* 解决数据安全和细粒度的访问控制的问题。
* 保持数据安全性同时提高传输效率。


## 思考

###  创新点

* 文章提出许多算法理论，并分点一一证明。
* 引用基于属性的ABE加密
* 通过阈值密钥共享，提高数据安全性。

### 缺点

* 实验只是与以往方案对比，并未验证是否可以完全保证安全性。
* 该方案可能并不能阻止DDoS攻击。
* 是否可阻止重放攻击。
* 用户隐私问题解决。

### 改进

​	可以依靠防火墙基础、虚拟专用网络 PKI+SSL机制保证。建立可靠通信网络，对新的配置。固件和指令进行加密和签名，以验证数据来源可靠性。现场保护密钥。采用匿名认证对用户信息保护，匿名认证技术是指利用匿名、假名技术对用户的真实身份进行隐藏，用户在不泄露任何与自己真 实身份有关信息的条件下，向验证方证明自己身份 的合法性。由于整个过程并没有泄露敏感信息，所以攻击方也无法推算用户的真实身份，在一定程度 上保护了用户隐私。所以说匿名认证技术成为了隐私保护系统中使用较为广泛的技术。国内外对匿名技术也提出了相应的认证方案，主要可分为基 于公钥技术的匿名认证、基于群签名的匿名认证、 基于盲签名的匿名认证。
