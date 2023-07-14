```python
a = tf.constant(4.0)
b = tf.constant(1.0)
c = a + b
print(a.graph, '\n', b.graph)
default_g = tf.get_default_graph()
print(default_g)
with tf.Session() as sess:
    d = sess.run(c)
    # print(sess.graph)
    print(d)
    # 这句 👇👇👇👇👇👇👇👇👇👇👇👇👇👇👇👇
    tf.summary.FileWriter('./temp/summary', graph=sess.graph)
    
'''
- 然后打开anaconda prompt
- cd /d cd /d D:\Step2\7-12
- tensorboard --logdir="./temp/summary"
- http://localhost:6006/
'''
```
