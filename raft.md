# 寻找一种更易于理解的一致性算法

Diego Ongaro and John OusterhoutStanford University

## 摘要

Raft是一种为了管理复制日志的一致性算法。它提供了和(multi-)Paxos等效且一致的结果，但结构不同于Paxos；这种不同的结构也使得Raft更加利于理解以及在构建实际系统时有更好的基础。为了更加方便的理解，Raft将一致性算法中的几个关键要素进行了分割，比如Leader选举，日志复制和安全性，同时限制了更强的一致性，来减少算法中需要考虑的状态。通过使用者学习Raft的过程说明了Raft对于学生来说比Paxos更加简单易懂。Raft同时引入了一种新的更换集群成员的机制，这种机制利用重叠的大多数来保证安全性。

## 介绍

一致性算法是一种可以让一个集群的机器当作一个整体来工作的同时能够容忍内部成员故障的算法。正因为一致性算法的这种功能，使得其在构建大规模高可用软件系统中十分关键。Paxos算法一直是过去十年间一致性算法的焦点：大部分的一致性算法都是基于或者受Paxos的影响，同时Paxos也成为了一致性算法教学中的主要手段。

然而，尽管有很多人尝试进行改进，Paxos算法还是非常不易于理解。为了构建实际的系统更需要做出很多复杂的变动。这就造成了教学和实际开发者对于Paxos都十分头疼。

