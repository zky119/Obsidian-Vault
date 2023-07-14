
### 散点图矩阵

```python
import seaborn as sns
# 生成散点图矩阵
sns.pairplot(data, vars=["car_ID", "enginesize", "price"])
```
![[Pasted image 20230512192250.png]]


### 热力图

`sns.heatmap` 是 Seaborn 库中的函数，用于绘制热力图。在给定的矩阵数据中，`sns.heatmap` 可以展示不同元素之间的关系，并使用颜色编码来表示数据的大小或相关性。

在给定的示例中，`sns.heatmap(data.corr(numeric_only=True), cmap=plt.cm.RdYlGn, annot=True, fmt=".2f")` 绘制了一个热力图，其中包含了数据集 `data` 中数值型变量之间的相关性。

具体参数的含义如下：

- `data.corr(numeric_only=True)`: 计算数据集 `data` 中数值型变量之间的相关系数矩阵。
- `cmap=plt.cm.RdYlGn`: 指定热力图的颜色映射，使用 `RdYlGn` 颜色映射方案，从红色到黄色再到绿色表示数据的大小或相关性。
- `annot=True`: 在热力图上显示数值标签。
- `fmt=".2f"`: 数值标签的格式化字符串，保留两位小数。

以下是一个完整的示例：

```python
import seaborn as sns
import matplotlib.pyplot as plt
import pandas as pd

# 创建示例数据
data = pd.DataFrame({'x1': [1, 2, 3, 4, 5],
                     'x2': [5, 4, 3, 2, 1],
                     'x3': [1, 3, 5, 2, 4]})

# 计算相关系数矩阵并绘制热力图
sns.heatmap(data.corr(numeric_only=True), cmap=plt.cm.RdYlGn, annot=True, fmt=".2f")

# 显示图形
plt.show()
```

该示例中，我们创建了一个包含三个变量 x1、x2 和 x3 的示例数据集，并使用 `sns.heatmap` 绘制了它们之间的相关性热力图。颜色的深浅表示相关性的强弱，数值标签显示了相关系数的具体数值。

### 箱线图

`sns.boxplot` 是 Seaborn 库中的函数，用于绘制箱线图。箱线图是一种用于展示数据分布和离群值的可视化方法。

通过 `sns.boxplot`，可以对数据集中的一个或多个变量进行分组，并显示每个组的数据分布情况。箱线图展示了数据的中位数、上下四分位数、最小值和最大值，并使用箱体和须线表示这些统计量。

以下是一个示例，展示了如何使用 `sns.boxplot`：

```python
import seaborn as sns
import pandas as pd

# 创建示例数据
data = pd.DataFrame({'Category': ['A', 'A', 'B', 'B', 'B', 'C', 'C'],'Value': [1, 2, 3, 4, 5, 6, 7]})

# 绘制箱线图
sns.boxplot(x='Category', y='Value', data=data)

# 显示图形
plt.show()
```

在这个示例中，我们创建了一个包含两个变量 Category 和 Value 的示例数据集。通过调用 `sns.boxplot`，我们对数据集进行了分组，将 Category 变量作为 x 轴，Value 变量作为 y 轴，绘制了箱线图。

输出的结果是一个箱线图，其中每个箱体代表一个组别，须线表示数据的分布范围。可以通过箱体的位置、长度和须线的位置来观察数据的中位数、四分位数和离群值等信息。

需要注意的是，为了使用 `sns.boxplot`，需要先安装 Seaborn 库，并导入相应的模块。

### 计数图

`sns.countplot` 是 Seaborn 库中的函数，用于绘制计数图。计数图用于显示离散变量的频数分布，即每个类别的观测数量。

通过 `sns.countplot`，可以可视化数据集中离散变量的不同类别及其对应的观测数量。它通常用于探索分类变量的分布情况，比较不同类别的频率或比例。

以下是一个示例，展示了如何使用 `sns.countplot`：

```python
import seaborn as sns
import pandas as pd

# 创建示例数据
data = pd.DataFrame({'Category': ['A', 'A', 'B', 'B', 'C', 'C', 'C']})

# 绘制计数图
sns.countplot(x='Category', data=data)

# 显示图形
plt.show()
```

在这个示例中，我们创建了一个包含一个变量 Category 的示例数据集。通过调用 `sns.countplot`，我们将 Category 变量作为 x 轴，绘制了计数图。

输出的结果是一个计数图，其中每个类别对应一个条形，高度表示该类别的观测数量。可以通过计数图来观察每个类别的频数，并比较不同类别之间的差异。

需要注意的是，为了使用 `sns.countplot`，需要先安装 Seaborn 库，并导入相应的模块。