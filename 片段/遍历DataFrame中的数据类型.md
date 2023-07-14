```python
number_var = []
for k, v in data.dtypes.items():
	if np.issubdtype(v, np.number):
		number_var.append(k)
print("数值类型变量个数：", len(number_var))
print(number_var)
```

