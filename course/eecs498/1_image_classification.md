# Image Classification

## Nearest Neighbor Classifier

我们遇到的第一个问题就是这个算法的原理其实很简单，但是还是要对他的具体代码实现有一个大概的了解。先贴一个关于此算法的介绍

- [Hobbitqia关于此算法的笔记](https://note.hobbitqia.cc/DL/lec01/#data-driven-approach)

这是一个关于算法具体代码实现中的问题的一些解答。

- [Nearest Neighbor Classifier](./Nearest%20Neighbor%20Classifier.md)

但其实这个算法效果并不好，其实没有实质上的训练，理论上的 test 的时间会更长，达到了 `O(n)` 的时间复杂度。

这个算法实际上是一个 `KNN` 在 `K=1` 的情况下的特例，所以我们可以把这个算法看作是 `KNN` 的一个特例。

从上面的算法可以引出 `KNN` 的概念，可以增加使用邻居的数量来抹除一些 noise。

## 关于如何 Setting Hyperparameters

- **超参数**：我们需要在学习中做出的选择，不一定能从数据中学习，而是直接设置。
  - idea_1: Choose the hyperparameters that work best on whole data. 这显然是不可取的，当 K=1 时，这个算法的效果总是 perfect，肯定有问题
  - idea_2: Split the data into two parts: training and test. 这个方法仍然有问题，我们每次都通过 test 数据集来选择超参数，那么如果在一个 wild 数据集上表现如何？我们不得而知。
  - idea_3: Split the data into three parts: training, validation and test. 这个方法是最好的，我们可以通过 validation 数据集来选择超参数，然后在 test 数据集上测试。test 数据集只在最后最后的唯一一次使用来判断我们的算法的效果。
- **交叉验证**：这是最好的方法，最出名的应该是**五折交叉验证**，我们把数据分成五份，每次取其中的一份作为 validation 数据集，剩下的作为 training 数据集，然后重复五次，最后取平均值。这样可以避免数据集的不平衡问题。在五折交叉验证后取得好的超参数再最后到验证集上做测试。**但这个方法存在一定的弊端**，因为成本很高，大型的数据集会因此消耗巨量的时间。
