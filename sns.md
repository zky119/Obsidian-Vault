# pairplot 多个变量之间的散点图和变量分布
```python
sns.pairplot(data, vars=["car_ID", "enginesize", "price"])
```
![[Pasted image 20230701144811.png]]

```python
# kind：取值为scatter（默认）与reg。 
# scatter：绘制散点图。 
# reg：除了散点图外，同时绘制回归线与置信区间。 
sns.pairplot(data, vars=["car_ID", "enginesize", "price"], kind="reg")
```
![[Pasted image 20230701145029.png]]


# 热力图
```python
sns.heatmap(data.corr(numeric_only=True), cmap=plt.cm.RdYlGn, annot=True, fmt=".2f")
```

# 柱状图
```python
ax = sns.barplot(y=s.index, x=s.values)
```
