# Online Cyber-Attack Detection in Smart Grid: A Reinforcement Learning Approach



## 论文信息

- 笔记作者：谢斯佳
- 原文作者： Mehmet Necip Kurt , Oyetunji Ogundijo, Chong Li,  Xiaodong Wang
- 原文题目：Online Cyber-Attack Detection in Smart Grid: A Reinforcement Learning Approach
- 原文来源：IEEE Transactions on Smart Grid, VOL. 10, NO. 5, SEPTEMBER 2019
- 原文链接：https://ieeexplore.ieee.org/abstract/document/8514804

## 主要内容

​		智能电网是建立在集成的、高速双向通信网络的基础上，通过先进的传感和测量技术、先进的设备技术、先进的控制方法以及先进的决策支持系统技术的应用，因此，为了保障智能电网的正常运行，尽早发现网络攻击对于智能电网的安全可靠运行至关重要。 这篇文章将在线攻击/异常检测问题表达为部分可观察的马尔可夫决策过程（POMDP）问题，并提出了一种使用无模型强化学习（RL）框架的POMDP通用鲁棒在线检测算法，可以准确地检测针对智能电网的网络攻击，具有广泛的用途，实用性高。

## 创新点

- 首次尝试使用RL技术在智能电网中进行在线网络攻击检测。
- 提出的算法是通用的，不需要攻击模型，可以广泛运用，检测到新的未知攻击类型。
- 对防御者进行低幅度的攻击训练以应对最坏的情况，因为这种攻击很难检测到，训练会使防御者变得敏感，可以检测到仪表测量值与正常系统操作之间的细微偏差，限制攻击者的攻击强度。

## 缺点

- 论文将在线网络攻击检测问题表述为POMDP问题，并提出了一种基于无模型RL的POMDP解决方案，可以准确地导出变化前模型，但是变化后模型是未知的，使得检测性能可能下降。
- 论文提出的解决方案在追求泛用性的同时，在对于特定攻击方法上检测的精确度会下降。
- 滑动窗口的大小有限，且存在着存储冗余，操作等待的问题，导致执行的效率不高。

## 改进方法

- 可以在获得真实的变更后数据(例如攻击/异常)，使用模拟数据进一步增强真实数据，并可以相应地进行训练，这将潜在地提高检测性能。
- 开发更复杂的存储技术，可以使用分块存储的滑动窗口数据重用技术，增大滑动窗口的数据吞吐量，通过并行存取窗口数据来减少存储器访问时间，提高效率。
- 还可以使用一种基于异常数据融合的智能电网攻击检测方法，通过入侵检测系统发现信息网络中的异常流量，利用标准化残差方法检测电力系统中的异常量测数据，通过关联信息网络和物理系统的异常报警数据来检测智能电网攻击事件。该方法可以消除入侵检测与标准化残差检测产生的大量错误报警，显著提高智能电网攻击的检测精度。

