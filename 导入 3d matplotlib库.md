```python
from mpl_toolkits.mplot3d import Axes3D
# 图形显示方式，默认为嵌入显示。
# %matplotlib inline
# 弹出框显示。
%matplotlib qt

# 分别提取两个特征的最小值与最大值。
max1, max2 = np.max(X_partial, axis=0)
min1, min2 = np.min(X_partial, axis=0)
# 在区间取值区间内，均匀选取若干个点。
x1 = np.linspace(min1, max1, 30)
x2 = np.linspace(min2, max2, 30)
# 生成网状结果，用来绘制三维立体图。
# 参数x1与x2是一维数组（向量）,将x1沿着行进行扩展，扩展的行数与x2元素的个数相同。
# 将x2沿着列进行扩展，扩展的列数与x1元素的个数相同。返回x1与x2扩展之后的数据X1与X2（扩展之后
# 的数组是二维的）。
# 这样扩展的目的是，依次对位获取X1与X2（扩展之后的数组）中的每个元素，
# 就能够构成x1与x2（扩展之前的数组）的任意组合。
X1, X2 = np.meshgrid(x1, x2)
# 返回figure对象。figure对象是我们绘图的底层对象，相当于画布。
fig = plt.figure()
# Axes3D在figure对象上进行绘制。
ax = Axes3D(fig)
fig.add_axes(ax)
# 绘制真实的样本散点图。
ax.scatter(X_partial[:, 0], X_partial[:, 1], y, color="b")
ax.set_xlabel("TV投放额度")
ax.set_ylabel("Radio投放额度")
ax.set_zlabel("销售额")
# 绘制预测的平面。
# rstride：行上的增量。增量越大，网格越宽。
# cstride：列上的增量。
# cmap：颜色图。
# alpha：透明度。1 完全不透明，0完全透明。
surf=ax.plot_surface(X1,X2,lr2.predict(np.array([X1.ravel(),X2.ravel()]).T).reshape(X1.shape),rstride=5, cstride=5, cmap="rainbow", alpha=0.5)
# 显示颜色条。
fig.colorbar(surf)
plt.show()
```