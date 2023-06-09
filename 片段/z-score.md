Z-score（Z值）是一种统计量，用于<font color="#f47983">衡量一个数据点与其所在数据集的平均值之间的差异</font>。它<font color="#f47983">表示一个数据点距离平均值的标准差数目</font>。

Z-score的计算公式如下：
Z = (X - μ) / σ

其中，Z是Z-score，X是数据点的值，μ是数据集的平均值，σ是数据集的标准差。

Z-score可以告诉我们一个数据点在数据集中的位置，以及它与平均值的偏离程度。如果Z-score为正数，表示数据点高于平均值；如果Z-score为负数，表示数据点低于平均值。<font color="#f47983">绝对值越大的Z-score表示数据点与平均值的偏离程度越大</font>。

在异常值检测中，Z-score常用于判断一个数据点是否偏离正常范围。一般来说，如果Z-score的绝对值大于某个阈值（如3），则可以将该数据点视为异常值。这是因为在正态分布中，约99.7%的数据落在平均值加减3倍标准差的范围内。

需要注意的是，<font color="#f47983">Z-score的使用前提是数据服从正态分布或近似正态分布</font>。对于非正态分布的数据，使用Z-score可能会导致不准确的结果。在这种情况下，可以考虑使用其他异常值检测方法。