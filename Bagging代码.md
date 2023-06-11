# 分类示例
```python
from sklearn.datasets import make_classification
from sklearn.tree import DecisionTreeClassifier
from sklearn.ensemble import BaggingClassifier
from sklearn.model_selection import train_test_split
# flip_y：类别随机分配的比例。值越大，则噪声越大，分类难度越大。
X, y = make_classification(
    n_samples=1000,
    n_features=20,
    n_informative=15,
    n_classes=3,
    random_state=0,
    flip_y=0.2
    )

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3,random_state=0)
# 定义一颗不限生长的决策树（强学习器）。
tree = DecisionTreeClassifier()
tree.fit(X_train, y_train)
print("决策树正确率：")
print(tree.score(X_train, y_train))
print(tree.score(X_test, y_test))
print("bagging正确率：")
# estimator：指定基本评估器。即bagging算法所组合的评估器。
# n_estimators：基本评估器的数量。有多少个评估器，就会进行多少次随机采样，产生多少个原始数据集的子集。
# max_samples：每次随机采样的样本数量。该参数可以是int类型或float类型。如果是int类型，则指定采样的样本数量。
# 如果是float类型，则指定采样占原始数据集的比例。
# max_features：训练每个评估器的特征数量。可以是int类型或float类型。
# bootstrap：指定是否进行放回抽样。默认为True。
# bootstrap_features：指定对特征是否进行重复抽取。默认为False。
bag = BaggingClassifier(
    estimator=tree,
    bootstrap=True,
    bootstrap_features=True,
    max_features=0.7,
    max_samples=0.7,
    n_estimators=100
    )
bag.fit(X_train, y_train)
print(bag.score(X_train, y_train))
print(bag.score(X_test, y_test))
```

# 回归示例
```python
from sklearn.datasets import make_regression
from sklearn.linear_model import LinearRegression
from sklearn.ensemble import BaggingRegressor
# 生成回归样本数据
X, y = make_regression(
    n_samples=1000,
    n_features=10,
    n_informative=1,
    noise=30,
    random_state=12,
    bias=2
    )

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3,random_state=199)
lr = LinearRegression()
lr.fit(X_train, y_train)
print("线性回归 R^2值：")
print(lr.score(X_train, y_train))
print(lr.score(X_test, y_test))
bag = BaggingRegressor(estimator=lr, n_estimators=100, max_samples=0.9,max_features=0.9)
bag.fit(X_train, y_train)
print("bagging R^2值：")
print(bag.score(X_train, y_train))
print(bag.score(X_test, y_test))
```