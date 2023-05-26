一，KNN介绍
- KNN算法实现分类与回归任务。
- KNN（K-Nearest Neighbor），即 近邻算法。 近邻就是 个最近的邻居
	- 当需要预测一个未知样本 的时候，就由与该样本最接近的 个邻居来决定。
	- KNN既可以用于<font  color="#A7BBEA"  size="5">分类问题</font>，也可以用于<font  color="#A7BBEA"  size="5">回归问题</font>。
		- 当进行<font  color="#A7BBEA"  size="5">分类</font>预测时，使用 个邻居中，<font  color="FFA488"  size="6">类别数量最多（或加权最多）者</font>，作为预测结果。
		- 当进行<font  color="#A7BBEA"  size="5">回归</font>预测时，使用 个邻居的<font  color="FFA488"  size="6">均值</font>（或加权均值），作为预测结果。

二，算法超参数 

1，K值
- 当 `K` 值<font  color="#A7BBEA"  size="5">较小</font>时，模型会依赖于附近的邻居样本，具有<font  color="FFA488"  size="6">较好敏感性</font>，但是<font  color="FFA488"  size="6">稳定性会较弱</font>，容易导致过拟合。
- 当 `K` 值<font  color="#A7BBEA"  size="5">较大</font>时，<font  color="FFA488"  size="6">稳定性增加</font>，但是<font  color="FFA488"  size="6">敏感性会减弱</font>，容易导致欠拟合。
	- 稳定性：会不会受 异常样本 干扰，容错能力
```
问：如果K和样本数量一样会怎么样
答：会预测为样本类别多的那类，完全不准

问：如果K特别小会不会好
答：不会，容错率太低，如果距离噪声很近，就会预测为噪声
```

2，距离度量方式
- 欧几里得距离
	- 两个点在空间中的直线距离
	- $$d(x, y) = \sqrt{{(x_2 - x_1)^2 + (y_2 - y_1)^2}}$$
- 曼哈顿距离
	-  也称为城市街区距离或L1距离，是两个点在坐标轴上的绝对值差的和
	- $$d(x, y) = |x_2 - x_1| + |y_2 - y_1|$$
- <font  color="FFA488"  size="6">闵可夫斯基距离</font>
	- 闵可夫斯基距离（Minkowski Distance）是一种通用的距离度量方法，可以视为欧几里得距离和曼哈顿距离的一般化形式。它可以根据参数p的不同取值，包含这两种距离作为特例
	- $$d(x, y) = \left(\sum_{i=1}^{n} |x_i - y_i|^p\right)^{\frac{1}{p}}$$
	- 可知：当p为1时，距离就是曼哈顿距离，当p为2时，距离就是欧几里得距离（欧氏距离）。

3，权重计算
- 统一权重：所有样本的权重相同。
- 距离加权权重：样本的权重与待预测样本的距离成反比。
	- 距离的倒数，然后规范化，使其 相加 为 1

4，算法步骤
1. 确定算法超参数。
	1. 确定近邻的数量K 。
	2. 确定距离度量方式。
	3. 确定权重计算方式。
	4. 其他超参数。
2. 从训练集中选择离待预测样本A最近的K个样本。
3. 根据这 K个样本预测A 。
	1. 对于分类，使用 K个样本的类别（或加权类别）预测 A。
	2. 对于回归，使用 K个样本目标值（y）的均值（或加权均值）预测 A。
```
问：给定待预测样本A，如果在训练集中，存在两个（或更多）不同的邻居N1与N2（N1与N2的标签不 同），二者距离A的距离相等，假设K的值为1，则此时选择哪个邻居较为合理？

答： 根据N1与N2在训练集中出现的先后顺序选择。

问：K=2呢

答：根据N1与N2在训练集中出现的先后顺序选择
	sklearn会预测为标签值小的哪个
```

```
问：通过网格交叉验证，可以帮助我们完成调参工作，因此，即使我们不太了解超参数的含义，也可以顺利 完成调参任务。这种说法正确吗？

答：根据超参数本身的含义来选择，比如range（10）
```

三，使用KNN实现分类

1，建模预测

```python
from sklearn.neighbors import KNeighborsClassifier

# n_neighbors：邻居的数量。
# weights：权重计算方式。可选值为uniform与distance。 
	# uniform：所有样本统一权重。 
	# distance：样本权重与距离成反比。 

knn = KNeighborsClassifier(n_neighbors=3, weights="uniform") 

knn.fit(X_train, y_train) 

# y_hat = knn.predict(X_test) 

# print(classification_report(y_test, y_hat))
```

2，[[KNN超参数-笛卡尔乘积遍历]] + [[KNN画图]]

```python
from itertools import product
weights = ['uniform', 'distance']
ks = [2, 15]

for i, (w, k) in enumerate(product(weights, ks), start=1):
	knn = KNeighborsClassifier(n_neighbors=k, weights=w)
    # 这里只看决策边界，不考虑模型预测效果，因此使用所有数据训练。
    knn.fit(X, y)
```
![[Pasted image 20230525144458.png]]
- 图一大概 （5,2.5）位置还是绿色区域是因为：K值是2，确定是哪个的时候会选择先出现的那个标签，[0,1,2]会选在前面的

3，[[超参数调整]]
- 导入`from sklearn.model_selection import GridSearchCV`
- 写grid
- fit

四，[[使用KNN回归预测]]

```python
from sklearn.neighbors import KNeighborsRegressor

knn = KNeighborsRegressor(n_neighbors=3, weights=weights)

knn.fit(X_train, y_train)
```
![[Pasted image 20230525150358.png]]

- 图一平直是因为：等权重
- 图二是曲线是因为：距离权重，随着距离的变化而变化