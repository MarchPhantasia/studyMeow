- 这是一篇访谈类的文章，主要是对访谈内容的处理和分析。
- 重点在于第四节*RESULT AND ANALYSIS*

# 文章标题的含义

文章标题 "An Empirically Grounded Path Forward for Scenario-Based Testing of Autonomous Driving Systems" 可以翻译为中文为：" 基于实证的自动驾驶系统场景测试路径展望 "。这个翻译传达了原标题中的 "Empirically Grounded"（基于实证）和 "Path Forward"（路径展望）这两个核心概念，同时也保留了 "Scenario-Based Testing"（场景测试）和 "Autonomous Driving Systems"（自动驾驶系统）的技术焦点。

- 本文中的软件测试主要指的是**场景化的自动驾驶测试**，能**够模拟更多自动驾驶场景**。

> 虽然自动驾驶系统（ADS）有望提高道路安全和未来移动性，但必须进行全面测试以验证其安全性和功能。此类测试包括**模拟测试、试验场测试和道路测试**，以涵盖各种驾驶场景

> 现有的工业研究主要集中在**情景识别方法**和**工具链**上 [34]，而忽略了几个实际观点，如**选择、实施和评估这些方法**，以**验证**工业中真实的 ADS。此外，2）由于**技术的竞争和保密**问题，**工业界在自动驾驶领域的合作受到阻碍** [37]。因此，在现阶段，相关行业实践的可及性和探索也受到限制。

# 1.Introduction

## 作者的目标

- 探索当前自动驾驶 ADS 的行业现状和相关挑战
- 给出一条 ADS 的发展道路，用来提高研究相关性。并通过**基于场景的测试方法**促进 ADS 的工业测试。

## 作者提出的三个问题

和作者的目标相对应：

- RQ1：当前与自动驾驶系统基于场景的测试相关的行业实践是什么？（第四部分）
- RQ2：自动驾驶系统的场景化测试面临哪些挑战？（第四部分）
- RQ3：工业界和学术界如何共同推进基于场景的自动驾驶系统测试？（第五部分，合作共赢之类的话）

## 作者的工作

### 先前的工作

- 采访了瑞典 7 家自动驾驶公司的 13 位测试专家，关注**关键场景识别**的实践，他们涵盖了 ADS 测试的多个方面。

### 现在的工作

- 不关注关键场景识别，关注 **ADS 场景测试的通用实践**（如何更一般的对 ADS 进行场景测试）和实际应用
- 挖掘之前研究中没有深度讨论的一般性实践
- 剔除关键场景的讨论

### 本篇论文的工作

这段内容概述了论文的研究发现、挑战识别以及针对自动驾驶系统（ADS）场景测试提出的建议，并总结了论文的主要贡献和结构。以下是对这部分内容的详细解读：

1. **研究结果分类**：
   - **行业实践分类**：作者的研究揭示了在 ADS 场景测试中的多种行业实践，这些实践被归纳为几个方面，包括：
     - **测试原则**：指不同公司在测试过程中的基本理念和方法，例如采用的测试流程和方法论。
     - **测试场景选择和识别**：包括如何确定哪些场景应该被用作测试，如何生成和筛选这些场景。
     - **测试分析与展示**：如何对测试结果进行分析，如何展示测试的有效性和覆盖率。
     - **相关行业标准**：在 ADS 场景测试中使用的行业标准，帮助规范测试过程。
     - **工具和平台**：进行**场景测试**时所使用的工具和平台，如仿真环境和数据分析工具。

2. **ADS 测试当前的主要问题（挑战）**：
   - 作者在研究中识别出了一些主要挑战，包括：
     - **概念和标准的不足**：缺乏统一的测试概念和标准，使得各公司在测试场景的选择和验证上存在差异。
     - **流程和工具的不足**：缺乏完善的流程和工具来支持场景的识别、选择和验证，影响了测试的效率和效果。

3. **提出的建议**：
   - **整合现有方法**：建议行业和学术界结合多种现有方法来优化 ADS 的测试过程，这包括知识驱动、数据驱动和搜索驱动的场景识别方法。
   - **加强合作**：鼓励行业和学术界与不同利益相关者进行合作，以分享知识和资源，共同提升 ADS 的测试能力。
   - **持续学习和改进**：强调行业需要在技术快速发展的背景下，持续学习和改进测试方法和工具，以适应新的挑战和需求。
   - **倡导开放性实践**：作者建议行业采纳更开放的实践，包括数据、工具和流程的共享，从而在测试领域内推动更广泛的协作和进步。

4. **论文的主要贡献**：
   - **贡献 1：行业实践和挑战的探索**：论文从实践的角度深入探讨了 ADS 场景测试的行业现状和面临的挑战，提供了对这一领域的深刻理解。
   - **贡献 2：改善测试方法的建议**：论文提出了一些改善现有 ADS 测试方法的建议，为未来行业的发展提供了参考和指导。

5. **论文的组织结构**：
   - **第二部分**：简要回顾了 ADS 测试及其场景测试的相关研究文献。
   - **第三部分**：描述了研究的背景和方法，包括研究设计、数据收集和分析过程。
   - **第四部分**：展示了研究结果和分析，包括行业的实践现状和识别出的挑战。
   - **第五部分**：讨论了研究的见解和对 ADS 场景测试的建议，以及研究的有效性。
   - **第六部分**：总结了研究的主要发现和对未来研究的展望。

总的来说，这段内容总结了论文的核心发现，即自动驾驶场景测试的行业实践和挑战，并提出了具体的改进建议，希望通过这些建议推动 ADS 测试方法的进步。作者还详细介绍了论文的结构，帮助读者理解研究的整体脉络。

# 2.Related Work 相关工作

这部分看起来不太重要

## ADS Testing

- 对过去研究的分析，主要关注基于场景的测试。
- 作者的研究则从实际操作角度入手，基于对自动驾驶领域从业者的访谈，分析了这些场景测试方法在实际应用中的表现和挑战，并提出了具体的改进建议。
- 作者强调了其研究的独特性和差异点。与其他多为学术研究的工作不同，作者的研究聚焦于探索 ADS 场景测试的工业实践，为学术界和工业界提供了一些实际应用中的见解。
- 作者的研究从访谈材料中提炼出具体的行业实践和挑战，这使其研究更加贴近实际应用，并为未来的研究提供了参考基础和实际案例。

# 3.CONTEXT AND METHODOLOGY 背景和方法

## 背景

- 研究团队选择了 13 位受访者，他们都是直接参与自动驾驶系统（ADS）测试的专业人士，分别来自瑞典 7 家从事自动驾驶技术的公司。这样做的目的是确保受访者的多样性，使得研究能够涵盖不同公司的实践和观点。受访者的角色多样，拥有丰富的 ADS 测试经验，从而为研究提供了全面的视角。
- 访谈的时长在 55 到 75 分钟之间，内容包括了对 CSI 研究的基本介绍、与 CSI 研究相关的预设问题，以及扩展到更广泛的 ADS 测试和场景测试的跟进讨论。通过这种方式，研究团队不仅获得了关于关键场景识别的深入讨论，还收集到了一些关于通用场景测试实践的见解。
![image.png](https://raw.githubusercontent.com/MarchPhantasia/pic/main/hexoblog/20241010094306.png)

## 方法

### 数据分析方法：主题建模

**数据分析方法：主题建模（Thematic Modeling）**：

- 研究团队遵循了 Cruzes 等人提出的主题建模指南，将转录内容进行系统化的分析和合成，整个过程分为四个步骤：
    1. **初始编码**：每位作者分别对一份访谈记录进行编码，然后共同审阅和讨论这些编码，以确保不同作者对编码的理解一致。
    2. **模型构建**：在初始编码的基础上，每位作者将这些编码归类，并组织成一个分层模型。随后，作者们将各自的模型进行审阅和合并，形成一个一致的模型框架。
    3. **进一步编码**：第一作者对剩余的访谈记录进行编码，并将这些编码整合到之前的模型中。
    4. **模型审核与完善**：所有作者共同审阅最终的模型，讨论并解决其中的分歧，最终达成一致意见，以确保模型的全面性和一致性。

# 4.RESULT AND ANALYSIS 结果分析

以下的部分名称来自第三节的访谈、公司列表。

## 4.1 Practices of Testing 实践 (RQ1)

解决问题：

- RQ1：当前与自动驾驶系统基于场景的测试相关的行业实践是什么？

### 4.1.1 Type of Testing

#### 传统测试方法

- **单元测试**：针对软件中的最小可测试单元进行验证。
- **集成测试**：测试不同模块之间的接口和交互，以确保它们能够正确协同工作。
- **系统测试**：对整个系统进行测试，检查其是否满足设计要求。
- **接口合规测试**：验证系统与外部系统或组件之间的接口是否符合标准或规范。
- **回归测试**：在引入新功能或修改代码后，确保之前功能仍然正常。
- **交付测试**：在系统发布之前进行的最终测试，确保系统在实际环境中能够稳定运行。

#### 其他测试方法（以仿真为主体）

- **硬件在环（HIL）测试**：HIL 测试是一种将真实硬件与**仿真环境**相结合的方法，用于测试系统在近似真实的物理环境下的表现。
- **软件在环（SIL）测试**：SIL 测试是一种通过**软件仿真测试系统软件**的方法，通常不需要真实的硬件。
- **场景测试 (Scenario-based Testing)**：仿真测试的主导部分，可以限制测试范围，组件化的、系统的进行完整的测试。P2 和 P8 比较强调关键场景的识别，有意的创造特定场景进行仿真。

### 4.1.2 Testing Principles

**类似于软件开发的开发流程**
- **瀑布模型**：测试按照项目里程碑在特定的时间和阶段进行。每个测试阶段都经过精确规划，通常需要数周时间才能完成。瀑布模型具有明确的阶段划分，强调测试的顺序和计划性。
- **敏捷方法**：与之前的瀑布模型有很大不同。在敏捷流程中，测试更为频繁和迭代，即每次代码变更都会触发测试流程。这个流程包括从**软件在环（SIL）测试**到**硬件在环（HIL）测试**，然后是**试验场测试（Proving Ground Testing）**，最终进行**道路测试（On-road Testing）**，即将 ADS 部署到真实车辆上进行测试。敏捷方法强调持续集成和快速反馈，以适应不断变化的开发需求。
- **迭代 V 模型**：模型处于瀑布模型和敏捷方法之间。V 模型 P5 提到他们在使用 V 模型时，采用了**迭代开发和测试**的方式，即在开发过程中多次循环执行 V 模型的测试和集成。这种方法结合了 V 模型的结构化流程和敏捷方法的灵活性。将系统拆分为不同的功能组件，每个组件单独开发和测试，然后集成为完整系统，并在每个开发层面进行测试，这是 V 模型的典型特征。

### 4.1.3 Test Scenario Selection

#### 测试场景的选择|设计

如何选择测试场景

- **操作设计域（ODD from P6、P7）**：DD 定义了自动驾驶系统所适用的操作环境，即哪些场景和情况是 ADS 应当处理的，哪些是不在其能力范围内的。因此，ODD 帮助限定了测试的范围，使得测试聚焦于系统设计所涵盖的情境。
- **多层次的方法（from P11）**：
	- 测试的必要性，任何有关项目的更改都必须通过的测试，包括一般性和关键的场景。
	- 组件相关的测试，对修改的组件进行为此组件设计的测试。
	- 基于安全和功能角度的测试，这部分的测试是拓展的
- **根据系统的具体实现选取方法 (from P9)**:
	- 对于感知系统，使用开环测试（open-loop testing，即无反馈控制的测试）
	- 对于决策系统和整个自动驾驶系统的完整栈（full stack），更倾向于使用闭环测试（closed-loop testing，即有反馈控制的测试）。
- 由**测试团队和产品负责人**共同负责的场景选择
- 每个功能团队负责其交付内容的测试

#### 当前场景选择存在的问题

- 相对依赖于人工，手动创建、执行、评估场景，需要定期进行
- 辅助驾驶系统的测试场景选择相对简单，存在标准如 EuroNCAP 评估程序）
- 自动驾驶系统的场景选择十分麻烦，尤其是对高等级的 `L4/L5` 自动驾驶。

### 4.1.4 识别测试场景（定义、创建、推导或生成测试场景）

识别出合适的测试场景，也叫做**定义、创建、推导或生成测试场景**。场景识别的目标是找到足够多且有代表性的测试情境，确保 ADS 在多种环境下的表现得到充分验证。

#### 识别测试场景的方法

**知识驱动方法（Knowledge-based Approaches）**：
- 该方法依赖于领域专家、领域特定本体论、标准、法律法规等，通过专家的知识和经验推导出测试场景。**覆盖范围有限**，难以应对所有可能的场景。因此，仅仅依赖这种方法是不够的，需要与其他方法相结合。
**数据驱动方法（Data-driven Approaches）**：
- 数据驱动方法通过利用来自不同数据源的数据来识别测试场景，例如从实际交通中收集的传感数据、交通事故报告、道路拓扑数据和天气信息等。数据驱动方法的优势在于它能够从现实数据中生成更真实的测试场景，但它也存在明显的局限性：
	- 数据收集、验证、标注和整理的**成本很高**。
	- 需要从数据中**学习并理解**哪些数据是相关的。
	- 某些人类驾驶数据（如醉酒驾驶、超速）可能对自动驾驶车辆来说并不具有相关性（P2 提到）。
	- 需要良好的可视化系统（如仿真工具）来从数据中捕捉必要的信息，并在测试中真实地再现这些场景。
**基于搜索的方法（Search-based Approaches）**：
- 这种方法通过使用算法（如外推、引导搜索等）来探索场景空间，从而生成更多的测试场景。
- 它在识别**关键场景**（critical scenarios）方面尤为有效，正如之前的 CSI 研究所报告的那样。
- 基于搜索的方法也面临一些问题，例如**如何系统地选择相关参数来组合测试场景**、**如何在仿真平台中真实地再现这些场景**、以**及如何评估这些场景的真实性和相关性**。

#### 组合使用方法

由于每种方法都有其局限性，作者指出：因此**必须结合使用这些方法**，以更有效地识别出有意义的测试场景。例如，知识驱动方法在早期提供良好的基础，数据驱动方法提供更真实的数据来源，而基于搜索的方法能够探索更多的未知场景。

#### 这段可以这么说

场景识别主要依赖于三种方法：知识驱动、数据驱动和基于搜索的方法，但它们在**覆盖范围、成本和相关性**方面各有不足。因此，通过将这些方法结合使用，可以更全面地弥补单一方法的不足，最终提高 ADS 测试的有效性。

### 4.1.5 测试结果的分析和证明（展示）

#### 多样化的指标

- **测试场景的数量和多样性**：展示在测试中执行和通过的场景数量及其多样性，以此评估系统在多种情境下的表现。
- **对象检测的准确性提升**：用于评估系统感知能力的改善情况。
- **系统性能**：例如系统在处理不同事件时的反应速度和流畅性，这些指标反映了系统对突发情况的应对能力。
- **覆盖率和完整性**

#### 指标的局限性

- 作者指出，基于里程的指标被广泛用于表示自动驾驶汽车的安全性或测试的成熟程度。**单一场景的测试不足**，仅依靠在某一简单场景（如高速公路上的跟车场景）中积累数百万公里的测试里程。
- 要在测试中覆盖所有可能的驾驶场景是几乎不现实的。因此，**作者认为**通过对未测试或未知场景的风险评估（*如何？*），来证明场景覆盖的充分性，并用此来支持系统的安全性论证。

#### 安全性的分析和证明

**如何使用测试的结果来证明 ADS 的安全性**
- 在证明系统安全性时，需要基于现有的资源和测试结果进行论证，同时也要识别测试结果与行业标准和普遍接受的标准之间的差距。
- 同时分析已测试的场景和未测试的潜在场景
- 必须整合所有可用的资源（如专家分析、收集的数据、测试里程、标准和法规）来证明并提升系统的安全性。*有点胡扯了*

#### 安全性不意味着无风险

**" 安全 " 并不意味着 100% 的无风险**
某些未测试或未知的场景可能仍然存在风险，但通过引入冗余设计（如传感器冗余）或防御性驾驶策略（如在系统无法识别物体或事件时减速或靠边停车），可以在一定程度上提高系统的安全性。

#### 总结一下

测试成熟度使用各种指标（如场景覆盖率）来演示。尽管被广泛使用，但仅凭测试里程很难证明测试的成熟度。

### 4.1.6ADS 相关的测试标准

#### 通用标准

- **SO-26262**：用于道路车辆的功能安全标准，主要用于处理或减轻由系统故障引起的风险和危害。
- **SOTIF（Safety of the Intended Functionality）**：针对自动驾驶车辆的预期功能的安全性，用于处理由功能不足（例如，感知误差）引发的风险。
- **ASAM OpenX 标准**：描述了道路交通领域的内容，包括道路基础设施、交通参与者和驾驶仿真中的场景等概念。
- **ISO-34501 至 34505**：用于自动驾驶测试场景的标准。
- **ISO TS 5083**：主要涉及自动驾驶的安全性和网络安全。

#### 特定的标准

**UNECE No.157 标准**: 用于自动车道保持系统（ALKS）的认证。

#### 标准的作用和局限

标准在自动驾驶测试中提供了重要的参考依据，是测试过程中的基础资源，但它们**仅能作为测试的起点**。标准通常用于提供基本的指导和框架，但在实际应用中，还需要根据具体的系统特性和测试需求进行扩展。例如：

- **SOTIF 的局限性**：无法涵盖所有可能的驾驶场景。标准仅提供了**需要应对的挑战和方向**，**而非具体的解决方案**
标准仅能提供一个**最低要求的基础**，并不能完全替代系统全面的测试需求。

### 4.1.7 工具和平台（不提）

#### 仿真工具的使用

**高效**: 仿真工具在 ADS 测试中被广泛使用，因为相比于在测试场地（如测试轨道）或公共道路上的测试，仿真测试在创建、执行和分析测试场景方面更为高效。真工具在测试场景的生成和运行过程中可以节省大量时间和资源。

#### 局限性

**真实世界再现的不足**：当前的仿真工具在再现真实世界场景方面存在一定不足。仿真的质量还需要进一步提升，以便更准确地模拟实际的驾驶环境。

#### 缓解局限性的方法

与不同的供应商合作，以获得**相关的工具**和**平台**进行测试。这不仅包括**仿真工具**，还涉及**数据**、**方法**和**技术支持**等资源。这样的合作有助于企业在测试过程中获得更全面的技术支持，提升测试的整体效率和效果。

### 4.1.8 ADS Testing 的改进

- **多种方法结合**：不同的方法和资源（如数据和标准）需要结合使用，以便能够识别出更多的测试场景。
- **加强利益相关者的合作**：不同的利益相关者（如工业界、学术界、供应商等）需要共同合作。通过与不同供应商的合作，获取数据、方法、技术支持以及测试工具和平台，而不是完全依靠自主开发。这种合作有助于共享资源、降低成本。
	- **工业界和学术界的合作尤为重要**：学术界的中立地位使其在推动这一生态系统方面具有优势，因为它们没有与制造商直接的利益冲突。如何利用真实世界数据以及如何筛选出相关的数据来支持系统的开发和测试，**这是学术界可以提供的重要支持**。
- **采用与 ADS 发展相适应的持续测试方法**
	- 需要更**持续和长期的测试方法**：持续的测试意味着不断学习该领域，收集新的驾驶数据，监测新出现的驾驶场景和行为，并随着技术的发展不断改进测试方法和实践
	- 可以基于收集的数据来发现罕见场景，计算场景的分布情况，并扩展测试场景目录
	- 可以根据现实世界场景的分布情况来评估场景发生的概率，并据此优化测试资源的分配。
	- **回归测试**：开发一个反馈循环，理解每次更改对系统行为、性能或相关测试场景可能造成的影响。这样的反馈循环有助于更精准地进行测试，确保系统更改不会引入新的问题。

## Challenges of Testing 挑战 ( RQ 2 )

### 概念和方法的不一致

自动驾驶测试中的概念和方法存在差异性。" 安全 " 这样的常用术语，不同公司对其理解和参考的标准也不一致。目前每个制造商都在独立进行开发，缺乏国际公认的测试方法。虽然有些国家或地区提供了交通事故和危险分析的公开数据，但这些数据未必适用于其他国家或地区。

问题在于：**如何让工业界、研究人员和监管机构等所有利益相关者共同合作，收集数据、制定验收标准，并开发一致的测试流程 。****

### 标准和法规的不足

测试 ADS 的标准和法规不够完善。自动驾驶测试面临的最大挑战并非技术层面，而是标准法规方面。当前的标准和法规虽然不成熟，但在逐步完善。例如，现有的标准（如 ISO-26262）在展示安全性测试结果方面显得过于笼统。传统的测试和评估项目（如 EuroNCAP）对于高级自动驾驶（如 SAE L4 和 L5 级别）来说，仍显不足。即使对于更有限的自动驾驶功能（如自动紧急制动系统 AEB），他们只能基于已知系统的表现来证明安全性。

主要的问题在于：**要明确所有测试要求和涉及的利益相关方、过程、场景、标准等方面仍然存在巨大挑战。**

### 技术和工具的局限性

虽然仿真工具广泛用于 ADS 测试，当前的仿真工具在真实世界场景再现方面仍有不足，仿真质量需要进一步提升。仿真测试结果向真实世界的转移仍然是一个挑战。测试过程中缺乏用于数据聚合、场景提取和评价的工具，这进一步加剧了保持最新测试标准和数据集的难度。

### 数据管理的挑战

数据驱动方法在自动驾驶测试中的应用面临数据收集、验证和管理的高成本问题。虽然数据驱动的方法能生成更真实的测试场景，但要从这些数据中学习并理解其相关性同样不易。同时，当前的机器学习系统、深度学习系统处理开放输入空间，输入数据的微小变化可能导致系统做出截然不同的决策，这也增加了测试难度。

## 5.Discussion

### RQ3 如何提升相关利益方，工业界、学术界的合作

在讨论的这部分内容中，作者提出了一种被称为**3CO 策略（Combine, Collaborate, Continuously Learn, and be Open）**的方法，用以改进自动驾驶系统（ADS）的测试，特别是针对场景测试的挑战。

### 1. **Combine（结合）**

   - **整合多种测试方法和数据来源**：不同的测试方法（如知识驱动、数据驱动、基于搜索的方法）各有优劣，作者建议将这些方法结合使用。通过这种方式，可以更全面地覆盖系统的不同部分和视角，从而识别更多的测试场景。
   - **利用多样化的资源**：包括使用现有标准、收集的驾驶数据和合成数据等。结合这些资源的目的在于更全面地分析和理解每种方法的贡献，最终在测试中实现互补，从而达到更高的覆盖率和可靠性。

### 2. **Collaborate（合作）**

   - **加强多方合作**：作者呼吁工业界、学术界、监管机构、消费者等不同利益相关者之间的合作。这种合作能够促进数据、方法和工具的共享，从而提升整体的测试能力。
   - **构建数据生态系统**：P9 和 P10 建议建立一个数据生态系统，以便更好地共享自动驾驶测试数据。通过这种合作，不同的制造商和研究机构可以减少重复劳动，共享已有的测试成果和数据集，从而加速 ADS 测试的进步。
   - **互相学习**：如 P12–13 所说，制造商可以通过合作互相学习，而不是各自独立进行相同的任务，这样可以提高效率，减少资源浪费。

### 3. **Continuously Learn（持续学习）**

   - **适应技术进步**：自动驾驶领域发展迅速，测试方法和工具需要持续改进，以应对新的挑战。作者建议行业和学术界应保持持续的学习状态，不断改进测试工具、方法和流程，以保持与技术发展的同步。
   - **扩展测试场景目录**：通过分析稀有场景、计算场景分布等方式，不断更新和扩展测试场景目录。这种持续学习和改进的过程，有助于识别新的驾驶行为和场景，从而提高 ADS 的测试覆盖率。

### 4. **Be Open（开放）**

   - **支持开放实践**：作者强调开放实践在 ADS 测试中的重要性，包括数据共享、共同开发工具，以及公开披露测试方法和结果。这不仅有助于构建透明性和信任，还能帮助整个行业更好地理解实际的挑战和测试方法。
   - **公开测试数据和结果**：如 P1 所提到的，加利福尼亚 DMV 要求自动驾驶公司公开披露所有自动驾驶失效和碰撞数据，这是一种开放数据的典型案例。类似的，作者鼓励更多企业发布他们的研究和测试结果，这样有助于学术界和工业界更好地理解实际挑战，从而缩小研究与实际应用之间的差距。
   - **共同开发和使用工具**：如 OpenScenario 和 OpenDrive 等开放框架，为测试自动驾驶系统提供了标准化的平台。通过共同使用和改进这些工具，可以提高测试效率，并让更多参与者从中受益。

## 6.总结

**总结**：论文的结论部分强调了自动驾驶系统测试的重要性及其复杂性，尤其是在场景测试方面的挑战。作者通过对行业现状的分析，提出了结合多种方法、加强合作、持续改进和开放数据的建议，以应对 ADS 测试中的困难。这些建议旨在缩小行业实践与学术研究之间的差距，并推动 ADS 测试的整体进步。尽管取得了一些进展，论文也承认当前的标准、方法和工具仍需要进一步完善，以应对未来的挑战。
