```python
def con2cat_analysis(df, feature, target="Churn"):
    """对连续变量（特征）与类别变量（目标值）实现相关性分析。
    分析包括如下内容：
    1 按照目标变量分组，在每个分组上，根据连续变量的分布绘制箱线图。
    2 使用Kruskal-Wallis H检验，判断差异是否显著。

    Parameters
    ----------
    df : DataFrame
        DataFrame数据，至少要包含feature与target两个列。
    feature : str
        特征变量的名称（连续类型）。
    target : str default="Churn"。
        目标变量的名称（类别变量）。
    """
    sns.boxplot(x=target, y=feature, data=df)
    # 根据类别变量（target）进行分组。
    g = data.groupby(target)[feature]
    group_data = []
    g.apply(lambda s: group_data.append(s.values))
    # Kruskal-Wallis H-test，用来检验各个分组的中位数是否相等。
    # 原假设：每个分组的中位数相等。
    # 备择假设：至少存在两个分组的中位数不等。
    # print(group_data)
    print(stats.kruskal(*group_data))
```

![[Pasted image 20230522214448.png]]