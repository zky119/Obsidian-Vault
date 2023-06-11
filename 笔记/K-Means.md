# <font  color="#A7BBEA"  size="7">1，算法步骤</font>

K-Mean算法，即K均值算法，是最常见的一种<font  color="#f47983"  size="5">聚类算法</font>。顾名思义，该算法会将数据集分为K个簇， 每个簇使用簇内所有样本的均值来表示，我们将<font  color="#f47983"  size="5">该均值称为“质心”</font>。具体步骤如下：
1. 从样本中选择K个点作为初始质心。 
2. 计算每个样本到各个质心的距离，将样本划分到距离最近的质心所对应的簇中。 
3. 计算每个簇内所有样本的均值，并使用该均值更新簇的质心。 
4. 重复步骤2与3，直到达到以下条件之一结束： 
	1. 质心的位置变化小于指定的阈值。 
	2. 达到最大迭代次数。

# <font  color="#A7BBEA"  size="7">2，优化目标</font>

- KMeans算法的<font  color="#f47983"  size="5">目标就是选择合适的质心</font>，使得在每个簇内，<font  color="#f47983"  size="5">样本距离质心的距离尽可能的小</font>。这样就可以保证簇内样本具有较高的相似性。
- 我们可以使用最小化簇内误差平方和（within-cluster sum-ofsquares ）来作为优化算法的量化目标（目标函数），<font  color="#f47983"  size="5">簇内误差平方和也称为簇惯性（inertia）</font>。

$$SSE=\sum_{i=1}^k\sum_{j=1}^{m_i}(||x_j-\mu_i||^2)$$
- $k$：簇的数量。
- $m_i$： 第 $i$ 个簇含有的样本数量。
-  $\mu_i$： 第 $i$ 个簇的质心。
- $||x_j-\mu_i||^2$ ： 第 $i$ 个簇中，每个样本 $x_j$ 与质心 $\mu_i$ 的距离。

                              [[计算SSE中的两点距离]]
![[Pasted image 20230609165037.png]]

- 当计算SSE（Sum of Squared Errors）时，公式 $||x_j - \mu_i||$ 表示数据点 $x_j$与簇中心点 $\mu_i$ 之间的<font  color="#f47983"  size="5">欧氏距离</font>·。
- 欧氏距离的计算公式为：$$ ||x_j - \mu_i|| = \sqrt{\sum_{d=1}^{D}(x_{j,d} - \mu_{i,d})^2} $$
	- $D$ 表示数据点的维度（特征数），
	- $x_{j,d}$表示数据点 $x_j$在第 $d$个特征上的取值，
	- $\mu_{i,d}$表示簇中心点 $\mu_i$ 在第 $d$ 个特征上的取值。


# <font  color="#A7BBEA"  size="7">3，算法优点与缺点</font>

- KMeans优点如下： 
	- 易于理解和实现，使其成为聚类任务的常用选择。 
	- 计算效率高，可以处理高维的大型数据集。 
	-  广泛应用于不同领域。 同时，
- KMeans算法也具有一定的缺点，如下： 
	- 需要事先指定 $k$ 值，如果 $k$ 值选择不当，聚类效果可能不佳。 
	- 聚类结果受初始质心的影响，可能会收敛到局部最小值。
	- 适用于凸形的数据分布，对于[[条形或不规则形状的数据]]，效果较差。

# <font  color="#A7BBEA"  size="7">4，程序演示</font>

- [[KMeans的默认值]]
- [[KMeans程序演示]]
- [[初始质心的影响]]

# <font  color="#A7BBEA"  size="7">5，K-Means++</font>

- [[KMeans++算法步骤]]
	- K-Means++只是K-Means算法的简单扩展，并非是一种全新的算法实现，因此，K-Means++也称 为Vanilla K-Means++。
	- 虽然K-Means++在选择初始质心时，会比K-Means<font  color="#f47983"  size="5">多出一些额外的计算</font>，<font  color="#f47983"  size="5">但</font>通常K-Means++的<font  color="#f47983"  size="5">收敛速度会更快</font>，因此，其<font  color="#f47983"  size="5">性能会优于K-Means</font>

# <font  color="#A7BBEA"  size="7">6，Mini Batch K-Means</font>

## 算法步骤
1. 随机部分数据，使用KMeans获得质心
2. 再从数据集中随机部分数据，分配给质心
3. 根据该批次数据更新质心
4. 重复2,3，直至质心变化小于指定阈值(<font  color="#f47983"  size="5">tol</font>)或者到达最大迭代次数(<font  color="#f47983"  size="5">max_iter</font>)

## [[Mini Batch K-Means程序演示]]
- [[计算一组点与另一组点之间的最近邻索引]]


# <font  color="#A7BBEA"  size="7">7，确定合适的K值</font>

- [[肘部法则]]
- [[轮廓系数]]


