用于将分类变量（字符串或整数形式）转换为整数编码。它将每个不同的类别映射到一个唯一的整数值，从而使分类变量可以在机器学习模型中使用。

以下是一个示例代码，演示如何使用`LabelEncoder`进行标签编码：

```python
from sklearn.preprocessing import LabelEncoder

# 创建LabelEncoder对象
label_encoder = LabelEncoder()

# 示例数据
labels = ['apple', 'banana', 'apple', 'orange', 'banana']

# 对标签进行编码
encoded_labels = label_encoder.fit_transform(labels)

# 输出编码后的标签
print(encoded_labels)
```

运行上述代码，输出结果为 `[0 1 0 2 1]`。这表示 `'apple'` 被编码为 `0`，`'banana'` 被编码为 `1`，`'orange'` 被编码为 `2`。

在实际使用中，您可以将`LabelEncoder`应用于特征变量（如示例中的标签），也可以将其应用于目标变量。对于目标变量，通常建议使用`LabelEncoder`进行编码，但在一些情况下，可能需要使用`OneHotEncoder`等其他编码方式。

请注意，`LabelEncoder`只能处理单列的分类变量。如果您有多个分类特征需要进行编码，可以使用`OneHotEncoder`或`OrdinalEncoder`等工具。`OneHotEncoder`将每个类别编码为一个二进制向量，而`OrdinalEncoder`将每个类别编码为一个整数或一个有序的整数。根据您的数据和模型需求，选择适当的编码方式是很重要的。