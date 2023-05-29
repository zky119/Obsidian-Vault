TF-IDF（Term Frequency-Inverse Document Frequency）是一种用于评估词语在文本中重要程度的统计方法。其公式如下：

TF（词频）表示词语在文本中出现的频率，计算方式为该词语在文本中出现的次数除以文本中所有词语的总数。

$$
\text{TF}(t, d) = \frac{\text{词语 t 在文本 d 中出现的次数}}{\text{文本 d 中所有词语的总数}}
$$

IDF（逆文档频率）表示词语的普遍重要程度，计算方式为总文档数除以包含该词语的文档数的对数。

$$
\text{IDF}(t, D) = \log \left( \frac{\text{总文档数}}{\text{包含词语 t 的文档数} + 1} \right)
$$

TF-IDF 是将 TF 和 IDF 相乘得到的结果，用于衡量一个词语在文本中的重要程度。

$$
\text{TF-IDF}(t, d, D) = \text{TF}(t, d) \times \text{IDF}(t, D)
$$

其中，$t$ 表示词语，$d$ 表示文本，$D$ 表示文本集合。

通过计算 TF-IDF，可以得到每个词语在不同文本中的重要程度，重要程度越高，说明该词语在该文本中越关键。TF-IDF 在文本挖掘、信息检索和文本分类等任务中被广泛应用。