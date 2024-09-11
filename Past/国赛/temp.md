

## 问题一的模型建立与求解

### 决策变量及其二元化

设 $a_{i,j,k}^{t,s}$ 为在未来第 $t$ 年（$t \in \{0, 1, \ldots, T\}$），类型为 $i$ ($i \in \{1, \ldots, I\}$) 的第 $j$ ($j \in \{1, \ldots, J_{i}\}$) 个地块上，在第 $s$ ($s \in \{1, \ldots, S\}$) 季次种植作物 $k$ ($k \in \{1, 2, \ldots, K\}$) 的面积（单位：亩），其中：

- $T = 7$ 为未来总年数。记 $t=1$ 为 2024 年，以此类推，$t=7$ 为 2030 年。
- $I = 6$ 为地块类型总数（如平旱地、梯田、山坡地等，共 6 种）。
- $J_{i}$：类型为 $i$ 的地块总数。
- $S=2$：一年中的季次数量。记 $s=1,2$ 分别为第一季和第二季。
- $K$：作物总数。

特别地，根据假设，$t=0$ 时，$a_{i,j,k}^{0,s}$ 为 2023 年的已知数据。

考虑到**耕种作业和田间管理的便利性**，我们对不同耕地类型作以下假设：

- 对于露天耕地，即：平旱地、梯田、山坡地和水浇地，某一季只能种植一种作物。
- 对于人工大棚，即：普通大棚和智慧大棚，可以进行二分地块进行种植，让二分后的子耕地，某一季只能种植一种作物

接下来，我们创新地对决策变量进行**二元化**。具体地，设 $x_{i,j,k}^{t,s} \in \{0,1\}$ 为在未来第 $t$ 年（$t \in \{0, 1, \ldots, T\}$），类型为 $i$ ($i \in \{1, \ldots, I\}$) 的第 $j$ ($j \in \{1, \ldots, J_{i}\}$) 个地块上，在第 $s$ ($s \in \{1, \ldots, S\}$) 季次是否种植作物 $k$ ($k \in \{1, 2, \ldots, K\}$)，公式表示为：

$$
\begin{align}
x_{i,j,k}^{t,s} = \begin{cases}
1, & \text{如果在第 } i \text{ 类地块的第 } j \text{ 第 } t \text{ 年} \text{第 } s \text{ 季种植作物 } k \\
0, & \text{否则}
\end{cases}
\end{align}
$$

通过决策变量二元化，我们不再直接关注种植的面积，而是通过该变量和地块面积 $A_{i,j}$ 的乘积来决定实际种植面积：

$$
\begin{align}
a_{i,j,k}^{t,s} &= x_{i,j,k}^{t,s} \cdot A_{i,j}
\end{align}
$$

其中，$A_{i,j}$ 是类型 $i$ 的第 $j$ 块地的总面积（亩）。

将决策变量二元化的优势主要体现在以下几个方面：

1. 简化决策结构，使得问题的核心转移到是否种植某种作物的决策上，而非具体面积
2. 便于处理以下约束条件：
    1. 总面积约束
    2. 轮作约束
3. 便于优化求解

对于约束条件简化这一优势，会在后文详细介绍。

### 朴素目标函数

对于问题 1 的两种情况，**朴素**的目标是最大化 2024-2030 年间（即 $t = 1$ 到 $t = 7$）的总利润。但目标函数都需要根据不同的滞销处理方式进行调整。

针对情况 1（滞销部分浪费），目标函数为：

$$
\max \sum_{t=1}^{T} \sum_{i=1}^{I} \sum_{j=1}^{J_i} \sum_{s=1}^{S} \sum_{k=1}^{K} \Bigl( P_k^{t,s} \cdot \min \Bigl( a_{i,j,k}^{t,s} \cdot Y_{i,k}^{t,s}, V_{i,k}^{t,s} \Bigr) - C_{i,k}^{t,s} \cdot a_{i,j,k}^{t,s} \Bigr)
$$

针对情况 2（超出部分按 50% 折扣价出售），目标函数为：

$$
\begin{align}
\max \sum_{t=1}^{T} \sum_{i=1}^{I} \sum_{j=1}^{J_i} \sum_{s=1}^{S} \sum_{k=1}^{K} \Bigl( & P_{k}^{t,s} \cdot \min \Bigl( a_{i,j,k}^{t,s} \cdot Y_{i,k}^{t,s}, V_{i,k}^{t,s} \Bigr) \\
+ 0.5 \cdot & P_{k}^{t,s} \cdot \max \Bigl( 0, a_{i,j,k}^{t,s} \cdot Y_{i,k}^{t,s} - V_{i,k}^{t,s} \Bigr)
- C_{i,k}^{t,s} \cdot a_{i,j,k}^{t,s} \Bigr)
\end{align}
$$

其中：

- $a_{i,j,k}^{t,s}$：类型为 $i$ 的第 $j$ 个地块上，在第 $t$ 年第 $s$ 季次种植作物 $k$ 的面积（亩）。
- $P_k^{t,s}$：作物 $k$ 在第 $t$ 年第 $s$ 季次的销售单价（元/斤）。
- $Y_{i,k}^{t,s}$：作物 $k$ 在第 $t$ 年第 $s$ 季次中，于类型为 $i$ 的地块上种植的亩产量（斤/亩）。
- $V_{i,k}^{t,s}$：作物 $k$ 在第 $t$ 年第 $s$ 季次中，于类型为 $i$ 的地块上的预计销售量（斤）。
- $C_{i,k}^{t,s}$：作物 $k$ 在第 $t$ 年第 $s$ 季次中，于类型为 $i$ 的地块上的种植成本（元/亩）。

特别地，根据假设，2023 年统计的数据中，预计销售量可根据以下公式计算得到：

$$
V_{i,k}^{0, s} = Y_{i,k}^{0, s} \cdot \sum_{j=0}^{J_{i}}  a_{i,j,k}^{0,s}
$$

对于情况 1，当某种作物的产量超过预期销售量时，超过的部分无法销售，导致 **收益为 0**。因此，作物的 **有效产量** 不能超过其预期销售量。后续，我们可以通过引入约束条件来处理这一情况。进而，目标函数调整为：

$$
\max \sum_{t=1}^{T} \sum_{i=1}^{I} \sum_{j=1}^{J_i} \sum_{s=1}^{S} \sum_{k=1}^{K} \Bigl( P_k^{t,s} \cdot a_{i,j,k}^{t,s} \cdot Y_{i,k}^{t,s} - C_{i,k}^{t,s} \cdot a_{i,j,k}^{t,s} \Bigr)
$$

同时，问题进而转化为**混合整数线性规划**问题。然而，对于情况 2，目标函数中的非线性难以去除，因而，问题仍然是**混合整数非线性规划**问题。

### 约束条件

本节将结合题意，详细分析问题 1 两种情形的约束条件，同时对比决策变量二元化操作对约束条件的简化作用。

#### 总面积约束

每块地在每个季次上的种植面积不能超过其可用面积：

$$
\sum_{k=1}^{K} a_{i,j,k}^{t,s} \leq A_{i,j}, \quad \forall i, \forall j, \forall t, \forall s
$$

其中：$A_{i,j}$ 是类型 $i$ 的第 $j$ 块地的总面积（亩）。

由于我们使用布尔变量 $x_{i,j,k}^{t,s}$ 进行简化，因而该约束一定满足。

#### 作物类型约束

根据地块类型和季次的不同，某些作物只能在特定地块类型和季次上种植：

$$
a_{i,j,k}^{t,s} = 0, \quad \text{若作物} \, k \, \text{不适合种植在类型为} \, i \, \text{的地块或第} \, s \, \text{季次}
$$

决策变量二元化后，约束条件更改为：

$$
x_{i,j,k}^{t,s} = 0, \quad \text{若作物} \, k \, \text{不适合种植在类型为} \, i \, \text{的地块或第} \, s \, \text{季次}
$$

#### 轮作约束

根据题意，轮作约束包含三个方面：

1. 连续两年同一地块的轮作约束
2. 同一年份不同季次同一地块的轮作约束
3. 任意三年同一地块豆类作物的轮作约束

接下来，我们将分别具体阐述轮作约束。

为防止连续两年在同一地块上种植相同作物，轮作约束条件为：

$$
\begin{align}
&a_{i,j,k}^{t-1,2} \cdot a_{i,j,k}^{t} = 0, \quad \forall i, \forall j, \forall k \ \text{为非单季作物},\ \forall t \\
&a_{i,j,k}^{t-1,1} \cdot a_{i,j,k}^{t} = 0, \quad \forall i, \forall j, \forall k \ \text{为单季作物},\ \forall t
\end{align}
$$

同一年不同季次同一地块上不能种植相同作物：

$$
a_{i,j,k}^{t-1,1} \cdot a_{i,j,k}^{t-1,2} = 0, \quad \forall i, \forall j, \forall k \ \text{为非单季作物},\ \forall t
$$

此外，从 2023 年开始，要求每块地在三年内至少种植一次豆类作物：

$$
\sum_{t=t_{1}}^{t_{1}+2} \sum_{s=1}^{S} \sum_{k \in \text{豆类} } a_{i,j,k}^{t,s} \geq 1, \quad \forall i, \forall j,\forall t_{1}
$$

如果直接使用种植面积来构造约束条件，将涉及**非线性乘积约束**，增加模型了复杂性和求解难度。通过决策变量二元化后，轮作约束条件修正为：

$$
\begin{align}
x_{i,j,k}^{t} + x_{i,j,k}^{t-1,2} \leq &1, \quad \forall i, \forall j, \forall k \ \text{为非单季作物} \\
\\
x_{i,j,k}^{t} + x_{i,j,k}^{t-1,1} \leq &1, \quad \forall i, \forall j, \forall k \ \text{为单季作物} \\
\\
x_{i,j,k}^{t} + x_{i,j,k}^{t} \leq &1, \quad \forall i, \forall j, \forall k \ \text{为非单季作物} \\
\sum_{t=t_{1}}^{t_{1}+2} \sum_{s=1}^{S} \sum_{k \in \text{豆类}} x_{i,j,k}^{r,s} \geq &1, \quad \forall i, \forall j, \forall t_{1} \\
\end{align}
$$

#### 田间管理约束

考虑到耕种作业和田间管理的便利性，在前文我们已经对耕地类型做了假设，具体形式化为：

$$
\sum_{k=1}^{K} x_{i,j,k}^{t,s} \leq 1, \quad \forall i, \forall j, \forall s
$$

### 逐年决策目标函数的优化

前文所述的朴素目标函数是直接最大化 7 年总利润，是一种 **全局最优解** 的求解方式，其有显著的优缺点：

1. 优点
    1. **全局优化**：这种方法可以充分考虑每一年之间的相互影响，尤其是像 **作物轮作** 这样的长周期约束。如果某些作物在某年收益较低，模型可能会为更长远的收益做出牺牲，以最大化未来几年的总收益。
    2. **长期规划**：它能够确保从战略角度规划种植安排，比如提前安排豆类作物的种植以提高后续几年的产量。
2. 缺点
    1. **复杂性高**：这种方法需要考虑所有 7 年的数据和所有可能的决策组合，计算复杂度较高，模型规模非常大，求解可能变得非常困难。
    2. **灵活性差**：在实际操作中，如果外部因素发生变化（如气候变化或市场价格波动），整个模型的最优性可能会受到影响，难以及时调整。

我们创新地使用**逐年决策模型**，采用**贪心策略**，每年只关注当年的收益，而不考虑未来的收益影响，即：每一步都寻求当前阶段的最优解。其也有显著的优缺点：

1. 优点
    1. **计算简便**：逐年优化只需要考虑当年的数据和决策，因此模型的规模大幅缩减，计算复杂度相对较低，求解更加高效。
    2. **应对不确定性**：由于每年都在重新优化，所以如果遇到不确定性（如市场需求或气候变化），这种方法可以迅速适应，并且根据新数据调整决策。
    3. **操作灵活**：这种方法能够每年根据实际情况动态调整，而不受前几年长期决策的过多限制。
2. 缺点：
    1. **局部最优解**：逐年优化容易陷入局部最优解，而忽略了长远的全局收益。比如，在某一年中追求最大利润可能会影响后续几年的作物轮作或豆类作物种植要求。
    2. **无法提前规划**：由于只考虑当年的收益，无法提前为后续几年的决策做出合理安排，可能导致长期收益不理想。

在实际决策中，需要考虑市场需求或气候变化等风险因素，适时调整。由于风险因素过多，几乎不存在全局最优的情况。因此，逐年决策较全局优化更为合理。最后，我们给出两种情况的逐年决策目标函数。

针对情况 1（滞销部分浪费），逐年决策目标函数为：

$$
\begin{align}
&\max \sum_{i=1}^{I} \sum_{j=1}^{J_i} \sum_{s=1}^{S} \sum_{k=1}^{K} \Bigl( P_k^{t,s} \cdot \min \Bigl( a_{i,j,k}^{t,s} \cdot Y_{i,k}^{t,s}, V_{i,k}^{t,s} \Bigr) - C_{i,k}^{t,s} \cdot a_{i,j,k}^{t,s} \Bigr) \\
\\
&\text{s.t.} \quad
\left\{
\begin{aligned}
&\quad x_{i,j,k}^{t,s} \in \{0,1\}, \quad \forall i, \forall j, \forall k, \forall s \\
\\
&\quad \sum_{k=1}^{K} x_{i,j,k}^{t,s} \leq 1, \quad \forall i, \forall j, \forall s \\
\\
&\quad x_{i,j,k}^{t,s} = 0, \quad \text{若作物} \, k \, \text{不适合种植在类型为} \, i \, \text{的地块或第} \, s \, \text{季次} \\
\\
&\quad x_{i,j,k}^{t} + x_{i,j,k}^{t-1,2} \leq 1, \quad \forall i, \forall j, \forall k \ \text{为非单季作物}\\
\\
&\quad x_{i,j,k}^{t} + x_{i,j,k}^{t-1,1} \leq 1, \quad \forall i, \forall j, \forall k \ \text{为单季作物}\\
\\
&\quad x_{i,j,k}^{t} + x_{i,j,k}^{t} \leq 1, \quad \forall i, \forall j, \forall k \ \text{为非单季作物} \\
\\
&\quad a_{i,j,k}^{t,s} \cdot Y_{i,k}^{t,s} \leq V_{i,k}^{t,s}, \quad \forall i, \forall j, \forall k, \forall s \\
\\
&\quad \sum_{r=t-2}^{t} \sum_{s=1}^{S} \sum_{k \in \text{豆类}} x_{i,j,k}^{r,s} \geq 1, \quad \forall i, \forall j \\
\end{aligned}
\right.
\end{align}
$$

针对情况 2（超出部分按 50% 折扣价出售），逐年决策目标函数为：

$$
\begin{align}
&\begin{aligned}
\max \sum_{i=1}^{I} \sum_{j=1}^{J_i} \sum_{s=1}^{S} \sum_{k=1}^{K} \Bigl( & P_{k}^{t,s} \cdot \min \Bigl( a_{i,j,k}^{t,s} \cdot Y_{i,k}^{t,s}, V_{i,k}^{t,s} \Bigr) \\
+ 0.5 \cdot & P_{k}^{t,s} \cdot \max \Bigl( 0, a_{i,j,k}^{t,s} \cdot Y_{i,k}^{t,s} - V_{i,k}^{t,s} \Bigr)
- C_{i,k}^{t,s} \cdot a_{i,j,k}^{t,s} \Bigr)
\end{aligned} \\
\\
&\text{s.t.} \quad
\left\{
\begin{aligned}
&\quad x_{i,j,k}^{t,s} \in \{0,1\}, \quad \forall i, \forall j, \forall k, \forall s \\
\\
&\quad \sum_{k=1}^{K} x_{i,j,k}^{t,s} \leq 1, \quad \forall i, \forall j, \forall s \\
\\
&\quad x_{i,j,k}^{t,s} = 0, \quad \text{若作物} \, k \, \text{不适合种植在类型为} \, i \, \text{的地块或第} \, s \, \text{季次} \\
\\
&\quad x_{i,j,k}^{t} + x_{i,j,k}^{t-1,2} \leq 1, \quad \forall i, \forall j, \forall k \ \text{为非单季作物} \\
\\
&\quad x_{i,j,k}^{t} + x_{i,j,k}^{t-1,1} \leq 1, \quad \forall i, \forall j, \forall k \ \text{为单季作物} \\
\\
&\quad x_{i,j,k}^{t} + x_{i,j,k}^{t} \leq 1, \quad \forall i, \forall j, \forall k \ \text{为非单季作物} \\
\\
&\quad \sum_{r=t-2}^{t} \sum_{s=1}^{S} \sum_{k \in \text{豆类}} x_{i,j,k}^{r,s} \geq 1, \quad \forall i, \forall j \\
\end{aligned}
\right.
\end{align}
$$

其中：

- $a_{i,j,k}^{t,s} = x_{i,j,k}^{t,s} \cdot A_{i,j}, \quad \forall i, \forall j, \forall k, \forall s$
- $V_{i,k}^{t,s} = Y_{i,k}^{t,s} \cdot \sum_{j=0}^{J_{i}}  a_{i,j,k}^{t,s}$

### 模型求解与结果分析

## 问题二的模型建立与求解

### 随机变量建立

根据题意，各作物预期销售量变化如下：

$$
V_{i,k}^{t,s} = \begin{cases}
V_{i,k}^{t-1,s} \cdot (1+\varepsilon_{V}^{k}), \quad & k \ \text{为小麦或玉米} \\
V_{i,k}^{0,s} \cdot (1+\varepsilon_{V}^{k}), \quad  &\text{其他情况}\\
\end{cases}
$$

其中，

$$
\varepsilon_{V}^{k} \sim \begin{cases}
\text{Unif}(0.05, 0.10), \quad & k \ \text{为小麦或玉米}  \\
\text{Unif}(-0.05, 0.05), \quad  &\text{其他情况} \\
\end{cases}
$$

农作物的亩产量变化如下：

$$
Y_{i,k}^{t,s} = Y_{i,k}^{0,s} \cdot (1+\varepsilon_{Y})
$$

其中，$\varepsilon_{Y} \sim \text{Unif}(-0.10, 0.10)$

因受市场条件影响，农作物的种植成本变化如下：

$$
C_{i,k}^{t,s} = C_{i,k}^{t-1,s} \cdot (1+\varepsilon_{C})
$$

其中，$\varepsilon_{C} \sim \text{Deter}(0.5)$，$\text{Deter}$ 为退化分布。

各作物销售单价变化如下：

$$
P_{k}^{t,s} = P_{k}^{t-1,s} \cdot (1+\varepsilon_{P}^{k})
$$

其中，

$$
\varepsilon_{P}^{k} \sim \begin{cases}
\text{Deter}(0), \quad & k \ \text{为粮食类作物}  \\
\text{Deter}(0.05), \quad & k \ \text{为蔬菜类作物}  \\
\text{Unif}(-0.05, -0.01), \quad & k \ \text{为除羊肚菌外的食用菌}  \\
\text{Deter}(-0.05), \quad & k \ \text{为羊肚菌}  \\
\end{cases}
$$

### 动态调整定价

市场中，商品的价格通常会受到供需关系的影响。超出预期销售量的部分，如果供大于求，则价格往往会下降。我们可以引入一个动态的折扣系数，根据超出量的比例进行定价。

$P_k^{t,s}$ 为该作物的基准价格，$\alpha\bigl(V_{i,k}^{t,s} \bigr)$ 为一个折扣系数函数，定义为：

$$
\alpha\bigl(V_{i,k}^{t,s}\bigr) = 1 - \beta \cdot \frac{\max \Bigl( 0, a_{i,j,k}^{t,s} \cdot Y_{i,k}^{t,s} - V_{i,k}^{t,s} \Bigr)}{V_{i,k}^{t,s}}
$$

其中，$\beta$ 是一个调整参数，控制折扣的敏感度，$V_{i,k}^{t,s}$ 是基准销售量。超出部分的定价为：$\alpha\bigl(V_{i,k}^{t,s} \bigr) \cdot P_{k}^{t,s}$

这种策略下，超出的部分如果很少，则折扣较小；而如果超出量大，则折扣会显著增加，甚至接近零（即基本无法销售）。

### 鲁棒优化模型求解

在该问题中，我们要处理农作物未来的销售量、产量、种植成本和价格的不确定性，并在最不利的情况下（即 " 最差情况下 "）制定稳健的种植策略。通过鲁棒优化，我们可以确保决策在不确定性条件下的稳定性。

鲁棒优化的主要动机是为了应对不确定性。在现实世界中，很多决策问题都涉及到不确定性因素，比如市场需求波动、气候变化、成本波动等。这些不确定性会直接影响决策的结果，而传统的优化方法通常假设未来是确定的，因此在面对不确定性时可能会表现出较差的鲁棒性。

鲁棒优化的主要优势在于它能够提供一个在不确定性下稳健的决策方案。具体来说：

- **考虑最坏情况**：鲁棒优化关注的是在最坏情况下的表现，而不仅仅是期望值。这意味着在面临不确定性时，决策方案能够保持一定的收益，避免出现极端的低收益或损失。
- **风险规避**：通过考虑不确定性范围内的最坏情况，鲁棒优化能够帮助决策者规避风险，尤其是在对未来不确定性较大或无法准确预测的情况下。
- **稳健性强**：鲁棒优化方案通常在面对不同的实际情况时表现出更高的稳健性，即使实际情况与预期不同，仍然能够获得较为理想的结果。

相较于问题 1，约束条件没有变动，整体优化模型形式化如下：

$$
\begin{align}
&\begin{aligned}
\max \mathbb{E} \Biggl[ \sum_{i=1}^{I} \sum_{j=1}^{J_i} \sum_{s=1}^{S} \sum_{k=1}^{K} \Bigl( & P_{k}^{t,s} \cdot \min \Bigl( a_{i,j,k}^{t,s} \cdot Y_{i,k}^{t,s}, V_{i,k}^{t,s} \Bigr)  \\ 
+ \alpha\bigl( V_{i,k}^{t,s} \bigr) \cdot & P_{k}^{t,s} \cdot \max \Bigl( 0, a_{i,j,k}^{t,s} \cdot Y_{i,k}^{t,s} - V_{i,k}^{t,s} \Bigr)
- C_{i,k}^{t,s} \cdot a_{i,j,k}^{t,s} \Bigr) \Biggr]
\end{aligned} \\
\\
&\text{s.t.} \quad
\left\{
\begin{aligned}
&\quad x_{i,j,k}^{t,s} \in \{0,1\}, \quad \forall i, \forall j, \forall k, \forall s \\
\\
&\quad \sum_{k=1}^{K} x_{i,j,k}^{t,s} \leq 1, \quad \forall i, \forall j, \forall s \\
\\
&\quad x_{i,j,k}^{t,s} = 0, \quad \text{若作物} \, k \, \text{不适合种植在类型为} \, i \, \text{的地块或第} \, s \, \text{季次} \\
\\
&\quad x_{i,j,k}^{t} + x_{i,j,k}^{t-1,2} \leq 1, \quad \forall i, \forall j, \forall k \ \text{为非单季作物} \\
\\
&\quad x_{i,j,k}^{t} + x_{i,j,k}^{t-1,1} \leq 1, \quad \forall i, \forall j, \forall k \ \text{为单季作物} \\
\\
&\quad x_{i,j,k}^{t} + x_{i,j,k}^{t} \leq 1, \quad \forall i, \forall j, \forall k \ \text{为非单季作物} \\
\\
&\quad \sum_{r=t-2}^{t} \sum_{s=1}^{S} \sum_{k \in \text{豆类}} x_{i,j,k}^{r,s} \geq 1, \quad \forall i, \forall j \\
\end{aligned}
\right.
\end{align}
$$
```