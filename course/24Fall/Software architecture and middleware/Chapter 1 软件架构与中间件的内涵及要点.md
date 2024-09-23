# 1.1 软件架构概述

## 什么是软件架构 (Software Architecture, SA)

软件架构的基本内容包括：

- **构件**：各种基本的软件构造模块 (函数、对象、模式等)；
- **连接件**：将它们组合起来形成完整的软件系统；
- **物理分布**
- **约束**
- **性能**

### 软件架构的定义 (1)

> defined by D. Garlan and M. Shaw

- 结构问题包括：
	- 构件化设计 organization of the system as a composition of components
	- 全局控制结构 global control structures
	- 通讯协议 protocols for communication
	- 异步处理 synchronization
	- 数据存取 data access
	- 设计元素的功能分配 assignment of functionality to design elements
	- 设计元素组合 composition of design elements
	- 物理部署 physical distribution
	- 伸缩性与性能 scaling and performance
	- 演化 dimensions of evolution
	- 替代方案的选择 selection of alternatives

$$
SA=\{components, connectors, constrains\}
$$

### 软件架构的定义（2）

> IEEE 2000
> - IEEE Recommended Practice for Architectural Description for Software-Intensive Systems

$$
Architecture=\{component, connector, environment, principle\}
$$

> the fundamental organization of a system embodied in its components, their relationships to each other, and to the environment, and the principles guiding its design and evolution
> 架构是以构件、构件之间的关系、构件与环境之间的关系以及指导系统设计与演化的原理为内容的某一系统的基本组织结构

### 软件架构的定义（3）

$$
SA=\{elements, form, rational\}
$$

软件架构是由一组具有一定形式的元素 (elements) 构成：

- 这组元素分成 3 类：处理元素 (processing elements)、数据元素 (data elements) 和连接元素 (connecting elements)；
- 处理元素负责对数据进行加工，数据元素是被加工的信息，连接元素把架构的不同部分组合连接起来.
**软件架构形式**(form) 是由**专有属性**(properties) 和**关系**(relationship) 组成
- 专有属性用于限制软件架构元素的选择
- 关系用于限制软件架构元素组合的拓扑结构
在多个架构方案中选择合适的架构方案往往基于一组**准则**(rational)。——<mark style="background: #FF5582A6;">TODO: 什么是准则？</mark>

### 归纳：软件架构的定义

**软件架构 (SA)：**

- 提供了一个结构、行为和属性的高级抽象
- 从一个较高的层次来考虑组成系统的构件、构件之间的连接，以及由构件与构件交互形成的拓扑结构
- 这些要素应该满足一定的限制，遵循一定的设计规则，能够在一定的环境下进行演化
- 反映系统开发中具有重要影响的设计决策，便于各种人员的交流，反映多种关注，据此开发的系统能完成系统既定的功能和性能需求

$$
\begin{align}
\begin{aligned}
架构 &= 构件 + 连接件 + 拓扑结构 + 约束 + 质量 \\ 
Architecture &= Components + Connectors + Topology + Constraints + Performance
\end{aligned}
\end{align}
$$

### 程序规模与软件架构

随着软件系统规模越来越大、越来越复杂

- 用户需求 (功能性) 越来越复杂，变化越来越频繁；
- 用户对软件质量 (非功能性) 的要求也越来越高；
- 如何将成百上千个功能组合起来，同时满足用户质量需求，变得越来越困难。

此时，整个系统的全局结构和设计显得越来越重要。

- 很多质量需求主要体现在架构中而不是功能模块内部的实现中

#### 结论

结论：*对于大规模的复杂软件系统来说，对***系统全局结构的设计***比起对算法的选择和数据结构的设计明显重要得多*。

### 架构师——负责大型复杂软件系统的系统架构设计

## 软件架构的目标与作用

### 软件架构的目标

- 软件架构关注的是：
	- 如何将复杂的软件系统划分为 " 模块 "
	- 如何规范 " 模块 " 的构成
	- 如何将这些 " 模块 " 组织为完整的系统
	- 以及保证系统的质量要求
- 主要目标：
	- 建立一个一致的系统及其视图集，并表达为最终用户和软件设计者需要的结构形式，支持用户和设计者之间的交流与理解。
- 分为两方面：
	- *外向目标*：建立满足最终用户要求的系统需求；
	- *内向目标*：建立满足系统设计者需要以及易于系统实现、维护和扩展的系统构件构成

### 软件架构的作用

- **交流的手段**：
	- It is a vehicle for communication among stakeholders（在软件设计者、最终用户之间方便的交流）
- **可传递的、可复用的模型**：
	- It is a reusable, transferable abstraction of a system（可重复利用的、可转移的系统抽象)
		- can be applied to other systems exhibiting similar requirements (用到其它的项目)
		- can promote large-scale reuse and software product lines (提高大规模重复利用率)
- **关键决策的体现**
	- It is the representation of the earliest design decisions that has the most significant influence on *system qualities*. It shows the tradeoffs (表达最早期设计层面的决策，对系统质量起到至关重要的作用。体现了那些折衷所在)
		- between performance and security（性能与安全性）
		- between maintainability and reliability（可维护性与可靠性）
		- between the cost of the current development effort and the cost of future developments in the architecture（当前开发费用和未来开发代价）

### 架构师具备的一些 Views

- 全局观 Overall View
	- 在软件开发过程中，应有一种从全局的角度对软件进行设计的 " 视图 " 而非仅仅关注底层的算法细节；
- 折衷观 Tradeoff View
	- 用户提出的各类功能与非功能需求之间存在着大量的 " 矛盾 "，无法同时 " 完美 " 的满足，必须要在彼此之间做出权衡；
- 交流观 Communication View
	- 参与软件研发的各成员需要有一个公共的 " 媒介 " 进行沟通，以应对需求的不明确、频繁变更、复杂度增加；
- 复用观 Reuse View
	- 不同的软件系统之间是否存在整体风格上的相似性，通过利用已存在的 " 软件资产 "，提高效率、降低成本；

#### 注意

**如果提高一个质量，经常会影响（提高或降低）其它质量**

# 1.2 软件中间件概述

## 什么是软件中间件

- 中间件（Middleware）是一组程序，应用于**分布式系统**各应用之中，为**系统屏蔽底层通讯**和**提供公共服务**，并保障系统的高可靠性、高可用性、高灵活性。
- **分布式应用**借助中间件在不同技术之间**共享资源**。
- 中间件位于客户机/ 服务器（C/S）的操作系统之上，管理**计算机资源**和**网络通讯**。
- 中间件是**连接**两个独立应用程序或独立系统的**软件**，即使它们具有不同的接口。
- 通过中间件，应用程序可以工作于**多平台**或 OS 环境

### 软件中间件的定位

![image.png|425](https://raw.githubusercontent.com/MarchPhantasia/pic/main/hexoblog/20240918213252.png)

### 常见的软件中间件

- 常见的邮件系统 Mail System——现在的邮件系统是什么厂家提供呢？
- Http
- RPC
- .NET
- WeChat——微信也是？
- CORBA
- Lotus Notes
- J2EE

## 软件中间件的作用

### 屏蔽异构性

异构性表现在计算机的软硬件差异，包括硬件（CPU 和指令集、硬件结构、驱动程序等），操作系统（不同 OS 的 API 和开发环境）、数据库（不同的存储和访问格式）等。长期以来，高级语言依赖于特定的编译器和 OS API 来编程，而他们是不兼容的

### 实现互操作

因为异构性，产生的结果是软件依赖于计算环境，使得各种不同软件之间在不同平台之间不能移植，或者移植困难。而且，因为网络协议和通信机制不同，这些系统不能有效相互集成

### 共性凝练和复用

软件应用领域越来越多，相同领域的应用系统之间许多基础功能和结构是有相似性的。通过中间件提供简单、一致、集成的开发和运行环境，简化分布式系统的设计、编程和管理

# 1.3 软件架构与中间件设计过程

## 软件架构设计的模型

### (Kruchten)4+1 视图模型

- **用例视图**：描述系统的典型场景与功能，主要图形包括 * ⽤例图（use case diagram）* 等。
- **逻辑视图**：描述系统的抽象概念与功能 (类、对象、接口、模式等)，主要图形包括*类图（class diagrams）*、* 协作图（Communication diagrams）* 和 * 时序图 (sequence diagrams）* 等；
- **开发视图**：描述系统中的子系统、模块、文件、资源及其之间的关系，主要图形包括*构件图（component diagrams）*、* 包图（package diagrams）* 等；
- **进程视图**：描述系统的进程及其之间的通信协作关系，主要图形包括*活动图（activity diagram）*、* 时序图（sequence diagrams）* 等；
- **物理视图**：描述系统如何被安装、部署与配置在分布式的物理环境下，主要图形包括 * 部署图（deployment diagram）* 等。

**4+1 视图模型是一种已经被标准化 (UML, RUP) 的方法，用来描述和文档化软件系统的体系结构。**

# homework

> 请根据身边的实际软件需求问题设计它的软件架构
> - 需求可以是前序课程的项目（e.g. 进销存系统）
> - 特别要求该软件系统能够基于网络提供服务
> - 请使用 UML 建模 4+1 视图，并提供文档化报告
> - 提交在作业 1，命名为 " 作业 1 - 学号 - 姓名 "
> - 截止时间：+2 周
