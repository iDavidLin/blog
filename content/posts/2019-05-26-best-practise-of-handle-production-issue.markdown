---
layout: post
title: "Best Practise of Handle Production Issue"
date: 2019-05-26
description: nil
tags: [production-issue]
---

这篇文章是读 左耳听风的 《故障处理最佳实践：应对故障》的读后笔记。  

## 故障发生时

在亚马逊，处理线上故障的方式比较特别，会把所有onCall的team都叫到（线上）一起。
工作流程是
1. 先签到；
2. 自检自己的服务；不是自己服务器的问题就stand by. （一边待命）

如果问题没有被及时解决，就会自动升级到高层，直到 SVP 级别。

因为现在大多数系统架构都是分布式服务化的。一个用户的请求可能会历经好几个service，开发和运维起来比较麻烦。因此需要有一套夸部门的开发和运维。

故障源团队通常会有以下几种手段来恢复系统。


> 重启和限流。重启和限流主要解决的是可用性的问题，不是功能性的问题。重启还好说，但是限流这个事就需要相关的流控中间件了。

> 回滚操作。回滚操作一般来说是解决新代码的 bug，把代码回滚到之前的版本是快速的方式。

> 降级操作。并不是所有的代码变更都是能够被回滚的，如果无法回滚，就需要降级功能了。也就是说，需要挂一个停止服务的故障公告，主要是不要把事态扩大。

> 紧急更新。紧急更新是常用的手段，这个需要强大的自动化系统，尤其是自动化测试和自动化发布系统。假如你要紧急更新 1000 多台服务器，没有一个强大的自动化发布系统是很难做到的。

也就是说，**出现故障时，最重要的不是 debug 故障，而是尽可能地减少故障的影响范围，并尽可能快地修复问题。**

## 故障前的准备工作

#### 1. 以用户功能为索引的服务和资源的全视图。
首先，我们需要一个系统来记录前端用户操作界面和后端服务，以及服务所使用到的硬件资源之间的关联关系。这个系统有点像 CMDB（配置管理数据库），但是比 CMDB 要大得多，是以用户端的功能来做索引的。然后，把后端的服务、服务的调用关系，以及服务使用到的资源都关联起来做成一个视图。
#### 2. 为地图中的各个服务制订关键指标，以及一套运维流程和工具，包括应急方案。
以用户功能为索引，为每个用户功能的服务都制订一个服务故障的检测、处理和恢复手册，以及相关的检测、查错或是恢复的运维工具。对于基础层和一些通用的中间件，也需要有相应的最佳实践的方法。

#### 3. 设定故障的等级。
还要设定不同故障等级的处理方式。比如，亚马逊一般将故障分为 4 级：1 级是全站不可用；2 级是某功能不可用，且无替代方案；3 级是某功能不可用，但有替代方案；4 级是非功能性故障，或是用户不关心的故障。
在我们公司则分根据影响的用户数以及对业务范围，分为Priority 1,Priority 2,Priority 3,和Priority 4。

#### 4. 故障演练。
故障是需要演练的。因为故障并不会时常发生，但我们又需要不断提升处理故障的能力，所以需要经常演练。一些大公司，如 Netflix，会有一个叫 Chaos Monkey 的东西，随机地在生产线上乱来。
#### 5. 灰度发布。

我们自己也是分布式架构。通过event的方式，从上游的service把数据分发给所有下游的services.而这个发事件的service是一个很老的项目，是一个monoliths。发布的流程非常复杂和漫长。
最近我们出来好几次线上issue。只能尽快修复bug，然后部署新的fix版本。这个项目比较庞大、复杂。整个部署流程（包括测试）至少要1.5个小时以上。  
我们最后怎么办呢？
我们在各个节点上加了feature toggle。可以随时控制整个事件流。
  
![Feature toggle](/image/feature-toggle.jpg)

