## requirements traceability

需求追溯的参考模型 (年代久远，似乎奠定了当前的需求追溯的参考模型的基本架构)[https://ieeexplore.ieee.org/document/895989][https://ieeexplore.ieee.org/document/895989]

## Towards a generic framework for requirements traceability management for SysML language

这篇文章的前四章节关注了需求追溯的建模过程，也就是框架的确定过程。第五部分开始通过具体的 reqo 进行系统的描述，但是追溯算法仍然是一个通用的过程，我们可以自行拟定一个系统，在这个系统上应用这个框架。[https://ieeexplore.ieee.org/abstract/document/7805044/references#references][https://ieeexplore.ieee.org/abstract/document/7805044/references#references]

- 系统工程中使用 sysml 进行模型的追溯。
- 提出一个框架，用在需求管理追溯的过程中。
- 文章中使用了一个温度控制系统进行描述，在我们的工作当中需要拟定一个航空工程领域的模拟系统。
- 从元模型进行特化, 来对具体的系统进行针对性的追溯设计。
- 介绍了一些追溯的算法（可以在技术报告中进行描述），根据生成算法自动生成**跟踪模型**，并且跟踪模型符合定义的跟踪元模型。
- 参考了下面的文章，可以使用下面文中描述的航空工程系统，来描述一个需求追溯过程的具体案例。
- 最终根据这个案例应当有一个需求可追溯模型。在 magicdraw 中，体现为需求的追溯矩阵。
![image.png](https://raw.githubusercontent.com/MarchPhantasia/pic/main/hexoblog/20241203132653.png)

### 疑问🤔

- 需求追溯的架构在不同研究中并非完全一致，多篇文章中分别都提出了自己的想法，是否要以类似 magicdraw 的需求追溯原理为准，如果是的话还需要进行相关的资料搜集。不太清楚 magicDraw 中的需求追溯原理具体指的是什么，如果是说它的需求矩阵是通过哪些参数进行构造出来的话，可以看这一个部分的参考。[https://docs.nomagic.com/display/MD190/Dependency+Matrix][https://docs.nomagic.com/display/MD190/Dependency+Matrix]

## Using a Model Based Systems Engineering Approach for Aerospace System Requirements Management

- 关注系统工程在航空工程中的应用。
- 定义系统中的利益相关者。
- 文章里提到了原有的基于文件的方法，然后也提到了当前的 MBSE 方法，这里做了简单的 sysml 介绍。
- 以 FDS（fuel distribution system 飞行器的燃料分配系统）为例，首先是对利益相关者部分的定义。
![image.png](https://raw.githubusercontent.com/MarchPhantasia/pic/main/hexoblog/20241203131822.png)
- 在此分析后分别使用了 SysML 的活动图、时序图、用例图、BDD 等，描述了 FDS 的生命周期、FDS 的操作行为、FDL 中参与的子系统及其用例，每个子系统定义为一个 Block，绘制在 BDD 图中。
- 当然也可以对子系统的用例进行细化，每个子系统单独绘制 SysML 用例图。
- 阅读这篇文章的目的是，采用一个航空工程领域的示例，关联上需求追溯的分析（前文是在元模型的基础上的分析）。


## prompt 
我正在进行一份技术报告的书写，其中的内容是有关系统工程领域中的需求可追溯问题，我关注的是如何从自然语言溯源到系统工程中定义的 SysML 模型，这两篇论文中的部分思想对我有很强的借鉴意义，因为对于一个 SysML 模型，我们可以导出它的 clean xmi code 形式，而这份 code 内定义了完整的 SysML 模型，于是在通过 RAG、LLM 等方法（我们并不使用 NLP、知识图谱），我们就可以完成自然语言到具体的 SysML 模型的追溯，并且请你注意，我们完成的是追溯的过程，而非论文中可能提到的通过自然语言生成 sysml 模型的代码表示，我们仅仅是通过自然语言进行追溯到已有系统工程项目中定义的 sysml 模型。例如：如果我们通过 magicdraw 完成了一整个系统的定义，那么我们应当可以通过自然语言的描述，来获得与这份自然语言描述相关的 sysml 模块。那么首先请你为我整理一份详细的关键技术介绍。请你对每一项技术的作用进行叙述。