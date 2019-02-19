# Community-detection
复杂网络中的几种社区发现算法

## 构造问题及数据集toy
  网络中节点1，2，3，4都是用户，用户之间可能互相给对方发数据，每个人发不发和给谁发都是随机。
  假设我们认为谁收到的数据最多为胜者，那这个时候可能存在作弊的用户。
  一些作弊用户使用同一个ip地址通过一直互相发数据来取得比赛胜利。
  
  数据集如data.txt所示，解题思路如下：
  构建两个网络A，B，网络A以发数据作为edge，网络B以相同IP作为edge。
  即网络A中，edge的两端是发送方和接收方的关系，而在网络B中，edge的两端是两个IP相同的用户。
  根据community detection的思路，网络A的community是那些发数据较为频繁的用户集合，网络B中的community是IP较为集中的用户集合。
  如果A和B中community的重合率很高的话，那么它们就有可能是作弊用户。
  
  通过NetworkX构建有向图，那么网络A中edge的属性应该为count（连接次数）和amount（金额）。
  网络B中应该不带任何属性，只要两个节点曾经用过相同的IP，那么两者之间即有一条edge。
  利用NetworkX构建多重有向图，发送次数通过计算边的重数可得。
  构造网络具体说明：
  - 网络A（多重有向图）的节点为各用户，如果用户1以IP（255.255.255.0）向用户2发送金额为30的数据，那么添加一条有向边（用户1→用户2），边强度为30。
  - 网络B（多重无向图）的节点为各用户，如果用户1以IP（255.255.255.0）向其他用户发送了5次数据，用户2以同样IP（255.255.255.0）向其他用户发送了2次数据，那么添加一条无向边（用户1—用户2），边强度为min（5,2）=2。
  
## 应用各种社区发现算法  
  1. clique渗透算法
  2. louvain算法
  3. GN算法
