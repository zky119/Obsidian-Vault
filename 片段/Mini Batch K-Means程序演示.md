# 生成数据集

```python
import time
from sklearn.cluster import MiniBatchKMeans
from sklearn.metrics.pairwise import pairwise_distances_argmin
from sklearn.datasets import make_blobs
centers = [[1, 1], [-1, -1], [1, -1]]
# 生成用于聚类的数据。
# n_samples：样本数量。
# n_features：特征数量。
# centers：聚类中心。
# cluster_std：簇的标准差。可以统一指定，也可以为每个簇指定不同的标准差。
# random_state：随机种子，用来生成样本数据。
X, y = make_blobs(
    n_samples=3000,
    n_features=2,
    centers=centers,
    cluster_std=0.7,
    random_state=0
    )
colors = np.array(["red", "green", "blue"])
plt.scatter(X[:, 0], X[:, 1], c=colors[y], marker=".")
```
![[Pasted image 20230610170128.png]]

# 计算聚类时间与效果

```python
# 定义函数，用于计算模型训练时间。
def elapsed_time(model, data):
    start = time.time()
    model.fit(data)
    end = time.time()
    return end - start
    
n_clusters = len(centers)

kmeans = KMeans(
    init="k-means++",
    n_clusters=n_clusters,
    n_init=10
    )
# batch_size：小批量的样本数。
mbk = MiniBatchKMeans(
    init="k-means++",
    n_clusters=n_clusters,
    batch_size=128,
    n_init=10
    )
kmeans_time = elapsed_time(kmeans, X)
mbk_time = elapsed_time(mbk, X)
# 这里样本数量较小，无法体现Mini Batch K-Means的性能优势，如果在数十万的样本规模上，
# Mini Batch K-Means的消耗时间会小于K-Means。大家可自行尝试。
print("K-Means消耗时间：", kmeans_time)
print("Mini Batch K-Means消耗时间：", mbk_time)
print("K-Means SSE：", kmeans.inertia_ )
print("Mini Batch K-Means SSE：", mbk.inertia_ )
print("K-Means的质心：", kmeans.cluster_centers_)
print("Mini Batch K-Means的质心：", mbk.cluster_centers_)
```

```python
# K-Means消耗时间： 0.6133561134338379
# Mini Batch K-Means消耗时间： 0.7168104648590088 
# K-Means SSE： 2470.58484882684 
# Mini Batch K-Means SSE： 2481.795725429417 
# K-Means的质心： [[ 0.96786467 1.0173955 ] [-1.07262225 -1.00554224] [ 1.07510478 -1.06937206]] 
# Mini Batch K-Means的质心： [[ 1.08757595 -1.12057593] [ 1.0016192 0.96138633] [-1.14789466 -1.03896078]]
```

# 绘制聚类效果

```python
plt.figure(figsize=(12, 5))
model = [kmeans, mbk]
for index, m in enumerate(model, start=1):
    plt.subplot(1, 2, index)
    plt.scatter(X[:, 0], X[:, 1], c=colors[m.labels_], marker=".")
    plt.scatter(m.cluster_centers_[:, 0], m.cluster_centers_[:, 1],marker="o", s=150, c="orange")
```
![[Pasted image 20230610192953.png]]

# 标签统一

```python
import pandas as pd
plt.figure(figsize=(12, 5))
model = [kmeans, mbk]
# 定义列表，用于保存两个模型预测的结果。
y_hat_list = []
for index, m in enumerate(model, start=1):
    plt.subplot(1, 2, index)
    y_hat = m.predict(X)
    if m == mbk:
        # 计算从MiniBatchKMeans质心到KMeans质心的映射，目的是在可视化的时候，
        # 相同的簇可以使用相同的颜色绘制。
        # pairwise_distances_argmin(X, Y) 对于数组X中的每条记录x，计算Y中与x距离最近的元素y，返回y的索引构成的数组。
        map_ = pairwise_distances_argmin(mbk.cluster_centers_,kmeans.cluster_centers_)
        print(map_)
        # 生成从mbk到kmeans质心的映射。
        map_ = dict(enumerate(map_))
        # 将y_hat转换成Series类型，方面调用map函数进行映射。
        y_hat = pd.Series(y_hat).map(map_).values
    # 将预测结果加入到列表中。
    y_hat_list.append(y_hat)
    plt.scatter(X[:, 0], X[:, 1], c=colors[y_hat], marker=".")
    plt.scatter(m.cluster_centers_[:, 0], m.cluster_centers_[:, 1],marker="o", s=150, c="orange")
```
![[Pasted image 20230610193141.png]]

# 两种聚类算法的差异对比

```python
same = y_hat_list[0] == y_hat_list[1]
diff = y_hat_list[0] != y_hat_list[1]
plt.scatter(X[same, 0], X[same, 1], c="g", marker=".", label="预测相同样本")
plt.scatter(X[diff, 0], X[diff, 1], c="r", marker=".", label="预测不同样本")
plt.legend()
print("预测相同样本数量：", X[same].shape[0])
print("预测不同样本数量：", X[diff].shape[0])
```
![[Pasted image 20230610194328.png]]