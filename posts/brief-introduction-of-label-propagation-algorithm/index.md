<!-- 
.. title: Brief Introduction of Label Propagation Algorithm
.. slug: brief-introduction-of-label-propagation-algorithm
.. date: 2017-07-16 23:46:04 UTC+08:00
.. tags: mathjax
.. category: 
.. link: 
.. description: 
.. type: text
-->

As I said before, I'm working on a text classification project. I use `doc2vec` to convert text into vectors, then I use LPA to classify the vectors.

LPA is a simple, effective semi-supervised algotithm. It can use the density of unlabeled data to find a hyperplane to split the data.

Here are the main stop of the algorithm:

0. Let $ (x_1,y1)...(x_l,y_l)$ be labeled data, $Y_L = \{y_1...y_l\} $ are the class labels. Let $(x_{l+1},y_{l+u})$ be unlabeled data where $Y_U = \{y_{l+1}...y_{l+u}\}$ are unobserved, useally $l \ll u$. Let $X=\{x_1...x_{l+u}\}$ where $x_i\in R^D$. The problem is to estimate $Y_U$ for $X$ and $Y_L$.
1. Calculate the similarity of the data points. The most simple metric is Euclidean distance. Use a parameter $\sigma$ to cotrol the weights.

$$w_{ij}= exp(-\frac{d^2_{ij}}{\sigma^2})=exp(-\frac{\sum^D_{d=1}{(x^d_i-x^d_j})^2}{\sigma^2})$$

Larger weight allow labels to travel through easier.

2. Define a $(l+u)*(l+u)$ probabilistic transition matrix $T$.

$$T_{ij}=P(j \rightarrow i)=\frac{w_{ij}}{\sum^{l+u}_{k=2}w_{kj}}$$

$T_{ij}$ is the probability to jump from node $j$ to $i$. If there are $C$ classes, we can define a $(l+u)*C$ label matrix $Y$, to represent the probability of a label belong to class $c$. The initialiation of unlabeled data points is not important.

3. Propagate $Y \leftarrow TY$
4. Row-normalize Y.
5. Reset labeled data's Y. Repeat 3 until Y converges.

In short, let the nearest label has larger weight, then calculate each label's new label, reset labeled data's label, repeat.

![label spreading](/images/label_spreading.png)

Ref:

1. [Learning from Labeled and Unlabeled Data with Label Propagation](http://mlg.eng.cam.ac.uk/zoubin/papers/CMU-CALD-02-107.pdf)

2. [标签传播算法（Label Propagation）及Python实现](<http://blog.csdn.net/zouxy09/article/details/49105265>)
