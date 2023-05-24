`df['columns'].str.split(expand=True)` 是 Pandas 中字符串操作方法的一个参数选项，用于将拆分后的结果展开为多个列。

默认情况下，`df['columns'].str.split()` 返回一个包含拆分后字符串的列表的 Series，每个元素是一个列表。但是，通过设置 `expand=True` 参数，可以将拆分后的结果展开为多个列，并返回一个包含这些列的 DataFrame。

以下是一个示例，展示了如何使用 `expand=True` 参数：

```python
import pandas as pd

# 创建示例数据
data = {'Name': ['John Smith', 'Jane Doe', 'Mike Johnson'],
        'Age': [25, 30, 35],
        'Location': ['New York', 'London', 'Paris']}
df = pd.DataFrame(data)

# 对 Name 列进行拆分并展开为多个列
df[['First Name', 'Last Name']] = df['Name'].str.split(expand=True)

print(df)
```

在这个示例中，我们在拆分 Name 列后，通过设置 `expand=True` 将拆分结果展开为多个列 First Name 和 Last Name。

输出的结果如下：

```
           Name  Age  Location First Name Last Name
0   John Smith   25  New York       John     Smith
1     Jane Doe   30    London       Jane       Doe
2  Mike Johnson  35     Paris       Mike   Johnson
```

可以看到，拆分后的结果被展开为两列 First Name 和 Last Name，并添加到了原始 DataFrame 中。