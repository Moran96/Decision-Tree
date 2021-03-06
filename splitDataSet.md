前期思考(待修正):
* 对于一个无序数据集,每个样本都有若干特征.选择哪一个特征来进行分类才能得到最优结果?
* "最优"是一个抽象的概念,那么机器学习中的最优应该通过什么形式表现出来?即能替代最优的参数是什么?
* ~~香农熵~~
* ~~解决方案:对于每一个特征,分别计算信息熵,最后进行比较.~~
* 熵值体现的是"无序程度";分类算法的目的就是将无序的数据变得有序.~~所以最终结果取熵值最小的划分方式.~~
---
```python
>>> importlib.reload(trees)
<module 'trees' from '/Users/a/Desktop/WorkSpace/Decision-Tree/trees.py'>
>>> data,lab = trees.create_data_set()
>>> trees.choose_best_split(data)
0
```
运行示例代码过程中,注意到作者并非是以比较香农熵来评判划分数据集的方式.香农熵只是作为中间变量参与数学运算.最终决定性参数为信息增益(Information Gain).

>遍历当前特征中的所有唯一属性值,对每个特征划分一次数据集,然后计算数据集的新熵值,并非对......
>

输出结果为0,即:
```python
row= 0 value= 0 	 new_entropy= 0.0 	 info_gain= 1.3709505944546687
row= 0 value= 1 	 new_entropy= 0.9509775004326936 	 info_gain= 0.41997309402197514
row= 1 value= 0 	 new_entropy= 0.0 	 info_gain= 1.3709505944546687
row= 1 value= 1 	 new_entropy= 1.2000000000000002 	 info_gain= 0.17095059445466854
```
---
对于一个包含n个训练样本,i种ground_truth的数据集:

<a href="https://www.codecogs.com/eqnedit.php?latex=l(x)=-log_2&space;p(x_i)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?l(x)=-log_2&space;p(x_i)" title="l(x)=-log_2 p(x_i)" /></a>

<a href="https://www.codecogs.com/eqnedit.php?latex=H(dataSet)=\sum_{i=1}^n&space;l(x_i)p(x_i)=-\sum_{i=1}^n&space;p(x_i)&space;log_2&space;p(x_i)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?H(dataSet)=\sum_{i=1}^n&space;l(x_i)p(x_i)=-\sum_{i=1}^n&space;p(x_i)&space;log_2&space;p(x_i)" title="H(dataSet)=\sum_{i=1}^n l(x_i)p(x_i)=-\sum_{i=1}^n p(x_i) log_2 p(x_i)" /></a>

依据dataSet内某一给定特征的某一value划分数据集,得到对应新数据集newSet.

<a href="https://www.codecogs.com/eqnedit.php?latex=h(newSet)=p(newSet)H(newSet)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?h(newSet)=p(newSet)H(newSet)" title="h(newSet)=p(newSet)H(newSet)" /></a>

<a href="https://www.codecogs.com/eqnedit.php?latex=Information&space;Gain&space;=&space;H(dataSet)&space;-&space;h(newSet)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?Information&space;Gain&space;=&space;H(dataSet)&space;-&space;h(newSet)" title="Information Gain = H(dataSet) - h(newSet)" /></a>

---
