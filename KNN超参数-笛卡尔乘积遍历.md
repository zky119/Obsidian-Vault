
```python
from itertools import product

weights = ['uniform', 'distance']
ks = [2, 15]
plt.figure(figsize=(12, 10))
# 计算weights与ks的笛卡尔积组合。这样就可以使用单层循环取代嵌套循环，
# 增加代码可读性与可理解性。
for i, (w, k) in enumerate(product(weights, ks), start=1):
    plt.subplot(2, 2, i)
    plt.title(f"K值：{k} 权重：{w}")
    knn = KNeighborsClassifier(n_neighbors=k, weights=w)
    # 这里只看决策边界，不考虑模型预测效果，因此使用所有数据训练。
    knn.fit(X, y)
    plot_decision_boundary(knn, X, y)
```