---
layout: post
title: "SA到底是什么"
date: 2013-06-22 01:47
comments: true
categories: SA
---

*原谅我又拿考试复习的东西丢上来了 - -，而且这坑没填干净..*

*笔记而已，都是根据教材剖析出来的，加上一些自己的理解。*

##概念

- 软件
- 体系结构(Architecture)= 架构
- 设计元素 = 组件 or 连接件
- SA 包括 设计元素的描述、交互、组合的模式、模式中的约束。
- SA = 组件+连接件+约束
- 组件，连接件应该都是集合

##风格

###概念

- SA风格，是描述特定系统组织模式的惯用范例，强调**组织模式**跟**惯用范例**

###分类

1. 数据流系统(Data Flow)，就是数据顺序流过多个组件，如 批处理序列(batch sequential)，管道和过滤器(Pipes & Fliters)
1. 调用返回系统(Call/Return)，这个不用解释了吧~ 如 主/子程序(main program & subroutine)，面向对象系统(Object Oriented)，分层系统(layered)*这里把C/S归为分层，两层或三层(应用服务器)，B/S归为C/S的特例*
1. 数据中心系统(知识库，data-centered)，就是数据都放在中心节点，如 仓库(repository)，黑板(blackboard)
1. 虚拟机(Virtual Machine)，可以理解成一个模拟器，如 解释器(interpreter)，基于规则系统(rule-based system)
1. 独立构件(independent components)，**不知道在说什么..**，如 通信过程(communicating processes)，事件系统(event systems，分显式、隐式调用**？**)

这5种风格具体就先不介绍了。。*感觉书上的都是老的东西，以我在这个时代的认知读起来感觉很扯。。咱尽量不八股。。*

下面简单挑几个说一点，

###PS

黑板模式，就好像多位不同的专家在同一黑板上交流思想，每个专家都可以获得别的专家写在黑板上的信息，同时也可以用自己的分析去更新黑板上的信息，从而影响其它专家。

解释器，用来执行其他程序的程序，不单单指通常的编程语言解释器，也可以按大的理解，如浏览器（HTML、CSS、JS），通信协议（TCP/IP，socket），甚至是处理用户输入的一些Parser也可以算（parse了之后赋予语义）。

管道过滤器，这个挺好理解的，而且感觉挺有意思的，以后有机会可以找个项目实现一下。记得以前搞MVC.NET的时候看过那种Fliter。

##建模（Modeling）

###什么决定你的建模

架构师跟利益相关者，进行cost/benefit权衡。

简单说就是客户给基本需求，架构师进行分析，做权衡。

###建模什么

基本的架构元素(architectural elements)，

- Components（组件or构件）
- Connectors（连接件）
- Interfaces（接口）
- Configurations（配置？结构？）
- Rationale - reasoning behind decisions

###模型的要点

- 无歧义
- 准确且精确
*PS.准确指正确，接近目标；精确指不矛盾、无歧义，击中一个地方，但不一定正确*

###视图

View（视图）是一个subset-model(模型子集)，viewpoint（视点）是指关注点、标准(concern,criteria)。

这个学过数据库应该都知道，就是东西都放在一个模型里太复杂了，就分开放到多个视图里，每个视图只用说清楚一类事情，视图的划分由视点(viewpoint)来决定。

常用的viewpoints，

- Logical Viewpoints
- Physical Viewpoints
- Deployment Viewpoints
- Concurrency Viewpoints
- Behavioral Viewpoints

比方说，用deployment做视点，那可能整个model就被分为server、client两个视图。

###建模方法

####通常方法

- 自然语言
- PowerPoint-style modeling
- UML(the Unified Modeling Language)

####其他

- 早期的ADL(architecture description languages)
- Domain- and style-specific languages
- Extensible architecture description languages

##文档描述（Documenting）

###用途

正规的软件开发过程有很多角色参与，需要一个交流设计思想的媒介。

##架构设计（architecture design）

###架构模式

*没提到？感觉就是架构风格（Pattern = Style）*

###质量属性(Quality Attributes)

系统不仅需要满足功能特性(functionality)，还需要满足其他一些质量属性(QA)。功能特性跟质量属性是正交的，功能不会决定质量。

达到特定质量属性，需要考虑设计、实现、部署三方面。

质量属性本身是没有多大用的，需要在**明确**质量属性（specifying QA）的过程中来帮助架构设计。

常见的质量属性有6种（USTAMP），

- Usability（易用性），方便使用
- Security（安全性），入侵检测、入侵容忍、多机备份
- Testability（可测试性），单元测试、错误可复现、语句覆盖度(Path Coverage?)
- Availability（可用性），系统在任一时刻正常工作的概率
- Modifiability（可修改性），修改指采用新的算法、数据结构、UI等
- Performance（性能），系统响应时间，硬件资源的占用率

其他，

- Scalability（可伸缩性）
- Portability（可移植性）
- etc.


####质量属性场景(QAS)

所以，我们就需要 质量属性场景(QA Scenarios)。在特定场景中去明确质量属性。

一个场景分为6部分，

- source
- stimulus
- artifact
- environment
- response
- response measure

一句话说，就是 刺激源，在特定环境(条件、系统模式)下，用特定刺激(n.)去刺激(v.)制品(指系统或code)，然后获得反应，最后测量（度量）反应。

**来说明系统达到这个质量属性的程度。**

###战术(Tactics)

目前架构师主要工作是复用以前架构的方法（即很少凭空创造），这些方法（解决方案）大部分指 Patterns & Styles，小部分指 Tactics。

**疑问，架构模式(architectural patterns)跟架构风格(styles)基本是一个意思，那架构模式跟设计模式(design patterns)又有什么区别？**

而战术（Tactics），是用来实现质量属性反应（quality attribute response）的。它是影响控制质量属性反应的设计决策。我们又称一个战术集合为一个架构策略(architectural strategy)。

对6个常见的质量属性（USTAMP），相应地有6个战术，

- Usability Tactics（易用性战术），运行时战术(runtime tactics)、设计时战术(design-time tactics，包括MVC、PAC等)**?**
- Security Tactics（安全性战术），抵抗攻击(resisting attacks)，检测攻击(detecting attacks)，从攻击中恢复(recovering from attacks)
- Testability Tactics（可测试性战术），提供输入捕获输出(providing input & capturing output)，内部监控(internal monitoring)
- Availability Tactics（可用性战术），错误检测(fault detection)、错误恢复(fault recovery)、错误预防（错误阻止，fault prevention）
- Modifiability Tactics（可修改性战术），局部修改(Localize Modifications)，防止连锁反应(Prevent Ripple Effects)，推迟绑定时间(Defer Binding Time)
- Performance Tactics（性能战术），控制资源需求(Resource Demand)，资源管理(Resource Management)，资源仲裁(Resource Arbitration)

###设计操作（Design Operators）

设计操作是创建一个体系结构设计的重要设计工具。包括以下5个操作，

- Decomposition（分解）
- Replication（复制，冗余）
- compression（压缩）
- abstraction（抽象）
- resource sharing（资源共享）

**？没细看**

###质量属性驱动的设计(ADD, Attribute-driven design)

ADD是一步一步地系统地生成初步的体系结构设计的方法。

ADD的结果：全部的结构决策、内部连接和协调机制、应用模式和策略制定各部分的机制、显式达到质量属性的要求、不能详细到接口！

ADD输入：质量属性需求、功能需求、约束。

ADD步骤：
1. 确定足够的需求信息
2. 选择系统的一部分分解
3. 优先部分需求以及标识架构驱动
4. 选择满足与所选择的系统分解向关联的那部分系统的架构驱动的设计概念：模式(patterns)、风格(styles)、策略(tactics)
5. 实例化(instantiated)架构元素，分配功能性需求
6. 归并(merge)设计完成
7. 分配剩下的功能性需求
8. 定义戒口给实例化元素
9. 检查和提炼需求，使他们能约束实例化元素
10. 对于系统的下一个分解部分，重复步骤2到9

###架构评估

- SAAM: Scenario-based Architecture Analysis Method
- ATAM: Architecture Trade-off Analysis Method

这里主要介绍 ATAM（框架权衡分析法）。

...

####效用树

...


