
```python
from sklearn.neighbors import KNeighborsRegressor
np.random.seed(0)
# 在[0, 5)的范围内，随机生成若干x点。
x = 5 * np.random.random(20)
X = x[:, np.newaxis]
y = np.sin(x) + np.random.normal(0, 0.01, size=len(x))
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3,
random_state=0)
plt.figure(figsize=(12, 5))
for i, weights in enumerate(['uniform', 'distance']):
    plt.subplot(1, 2, i + 1)
    knn = KNeighborsRegressor(n_neighbors=3, weights=weights)
    knn.fit(X_train, y_train)
    plt.scatter(X_train, y_train, c="b", marker="o", label="训练集")
    plt.scatter(X_test, y_test, c="g", marker="D", label="测试集")
    t = np.linspace(0, 5, 500).reshape(-1, 1)
    plt.plot(t, knn.predict(t), c="r", label="拟合曲线")
    plt.legend()
    plt.title(f"KNN回归预测：weights={weights}")
    plt.xlabel("x")
    plt.ylabel("y")
```
![[Pasted image 20230525150358.png]]