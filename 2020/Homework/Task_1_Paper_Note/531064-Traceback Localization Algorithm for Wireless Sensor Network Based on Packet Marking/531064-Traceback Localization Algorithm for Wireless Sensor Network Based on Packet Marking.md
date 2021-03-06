# 论文笔记-基于包标记的无线传感器网络溯源定位算法
## 论文基本信息
* 标题
    Traceback Localization Algorithm for Wireless Sensor Network Based on Packet Marking
* 作者
    LI Peng-fei, LIU Ping, YI Ting, YUAN Hong-wei
* 刊物出处:
    Computer Engineering, VOL.40, 2014
* 链接
    http://www.wanfangdata.com.cn/details/detail.do?_type=perio&id=jsjgc201402023
## 论文主要内容
* 无线传感器网络（WSN）由于缺乏防火墙等边界安全设施、计算能力有限等特点易受到攻击。因此，在网络受到攻击时逆向查找攻击源位置十分重要。本文在对比了目前已有的基于概率包标记算法的溯源定位方案，在此基础上提出了一种层次式混合概率包标记算法（LMPPM），该算法实现简单、提高收敛性，从而提高无线传感网络的溯源效率。
## 论文创新点
* 本论文中提出一种新型基于包标记的层次式混合概率包标记算法。根据WSN中的标记特点，通过提高上游节点的标记概率，降低下游结点的标记概率即减少下游节点标记覆盖率，从而提高算法的收敛性。而提高标记上游节点标记概率，则是通过扩大上下游节点之间的相对距离来实现的。该算法降低了节点的负担和算法的复杂度，实现了优化。
## 论文缺点
* **攻击路径长度影响算法效率**
当攻击路径变长时，数据包的数量也随之增大，当数据包数量达到一定程度时，LMPPM算法的性能提升幅度趋近于零。
* **算法受分簇规模影响**
虽然说分簇的目的是为了减少节点的计算量，降低存储负担，但是当簇特别特别小时，簇根节点的轮换就会变得十分频繁，节点消耗能量变快，会使簇开始重新调整并重新划分，导致簇根节点的计算数量增加，又会提高存储负担，与算法最初的设计目的矛盾。

## 改进办法
本人在查找相关资料及论文后，对上述缺点提供以下可能的解决思路：
* 对攻击路径进行预测
由于对于不同长度的攻击路径存在不同的最优算法，是否可以基于传统的也贝斯网络攻击图的攻击路径预测方法，实现一种WSN内的网络攻击路径预测方法。从而在已有的LMPPM、APPM、BPPM算法的基础上，进一步提高无线传感网络的溯源效率。
* 寻找合适的分簇规模
由于不当的分簇方法，会增加额外的计算量从而加大网络负担。因此，在该算法应用之前，需要经过大量的测试，选取最佳的分簇规模，统筹好性能提升与网络负担之间的关系，才能利用本文所提出的方法，实现无线传感网络溯源的最优化。


