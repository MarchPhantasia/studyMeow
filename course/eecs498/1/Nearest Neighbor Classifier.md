# Nearest Neighbor Classifier 的一些解释

请先看下面这段代码
``` python
import numpy as np

class NearestNeighbor:
    def __init__(self):
        pass

    def train(self, x, y):
        """
        Train the classifier. X is NxD where each row is an example.
        Y is a 1-dimensional array of size N.
        The nearest neighbor classifier simply remembers all the training data.
        """
        self.xtr = x
        self.ytr = y

    def predict(self, X):
        """
        Predict the label for each example in X. X is NxD where each row is an example.
        """
        num_test = X.shape[0]
        # Initialize an array to hold the predictions
        Ypred = np.zeros(num_test, dtype=self.ytr.dtype)
        
        # Loop over all test examples
        for i in range(num_test):
            # Compute the L1 distance between the i-th test sample and all training samples
            distances = np.sum(np.abs(self.xtr - X[i, :]), axis=1)
            
            # Find the index of the smallest distance
            min_index = np.argmin(distances)
            
            # Predict the label of the nearest example
            Ypred[i] = self.ytr[min_index]

        return Ypred

# 示例使用
if __name__ == "__main__":
    # 训练数据（例如 2D 特征）
    X_train = np.array([[1, 2], [2, 3], [3, 4], [6, 7], [7, 8], [8, 9]])
    y_train = np.array([0, 0, 0, 1, 1, 1])

    # 测试数据
    X_test = np.array([[5, 5], [1, 1]])

    # 最近邻分类器
    nn = NearestNeighbor()
    nn.train(X_train, y_train)
    predictions = nn.predict(X_test)
    
    print("Predictions:", predictions)

```
首先要说明数据集的形式是什么样的，从`X_train`中可以看出，每一行是一个样本，每一列是一个特征。`y_train`是对应的标签。矩阵的每一行都是一个样本，而矩阵中的每一列都是这个样本对应的特征，不存在**第一列不是特征的这个情况**

关注其中的 `predict` 方法。这个方法的输入是一个测试集，输出是测试集中每个样本的预测标签。对于测试集中的每个样本，该方法计算它与训练集中所有样本的 L1 距离，然后找到距离最近的训练样本的标签作为预测标签。

L1 距离的计算方法是：对于测试集中的每个样本，计算它与训练集中所有样本的特征差的绝对值之和，然后找到和最小的训练样本的标签作为预测标签。

