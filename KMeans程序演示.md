1，生成（50,2）的数据，并可视化
```python
import numpy as np
import matplotlib.pyplot as plt
plt.rcParams["font.family"] = "SimHei"
plt.rcParams["axes.unicode_minus"] = False
np.random.seed(1)
# 生成样本数据
X = np.random.randint(70, 100, size=(50, 2))
plt.scatter(X[:, 0], X[:, 1])
plt.xlabel("语文")
plt.ylabel("数学")
```

2，执行KMeans，输出结果
```python
from sklearn.cluster import KMeans
# n_clusters：簇的数量。
kmeans = KMeans(n_clusters=4, n_init="auto")
kmeans.fit(X)
# 获取聚类后的质心。
print("质心：", kmeans.cluster_centers_)
# 获取每个样本所属的簇。标签的数值对应所属簇的索引。
print("标签：", kmeans.labels_)
# 获取SSE（簇惯性）。
print("SSE：", kmeans.inertia_)
# 获取迭代次数。
print("迭代次数：", kmeans.n_iter_)
# 聚类的分值，分值越大，效果越好。直接取SSE的相反数。
print("分值：", kmeans.score(X))
```

3，进行预测
```python
unknown = np.array([[76, 99], [94, 80]])
y_hat = kmeans.predict(unknown)
print(y_hat)
# kmeans.predict([[76,99],[94,80]])
# kmeans.predict([[76,99],[94,80]]).tolist()
```

4，结果呈现
```python
def plot_cluster(model, train, test=None):
    color = np.array(["r", "g", "b", "orange"])
    cc = model.cluster_centers_
    label = model.labels_
    plt.scatter(cc[:, 0], cc[:, 1], marker="+", s=150, c=color)
    plt.scatter(train[:, 0], train[:, 1], c=color[label])
    if test is not None:
        y_hat = model.predict(test)
    plt.scatter(test[:, 0], test[:, 1], marker="*", s=150,c=color[y_hat])
    plt.xlabel("语文")
    plt.ylabel("数学")
    plt.title(f"SSE：{model.inertia_:.2f} 迭代次数：{model.n_iter_}")
plot_cluster(kmeans, X, unknown)
```
![[Pasted image 20230609223739.png]]

