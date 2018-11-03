<!--
.. title: Models and Architechtures in Word2vec
.. slug: models-and-architechtures-in-word2vec
.. date: 2018-01-05 21:57:17 UTC+08:00
.. tags: mathjax,word2vec
.. category: 
.. link: 
.. description: 
.. type: text
-->

## Models

### CBOW (Continuous Bag of Words)

Use the context to predict the probability of current word.

![cbow](/images/doc2vec_cbow.png)

1. Context words' vectors are $\upsilon_{c-n} ... \upsilon_{c+m}$ ($m$ is the window size)
2. Context vector $ \hat{\upsilon}=\frac{\upsilon_{c-m}+\upsilon_{c-m+1}+...+\upsilon_{c+m}}{2m} $
3. Score vector $z_i = u_i\hat{\upsilon}$, where $u_i$ is the output vector representation of word $\omega_i$
4. Turn scores into probabilities $\hat{y}=softmax(z)$
5. We desire probabilities $\hat{y}$ match the true probabilities $y$.

We use cross entropy $H(\hat{y},y)$ to measure the distance between these two distributions.
$$H(\hat{y},y)=-\sum_{j=1}^{\lvert V \rvert}{y_j\log(\hat{y}_j)}$$

$y$ and $\hat{y}$ is accurate, so the loss simplifies to:
$$H(\hat{y},y)=-y_j\log(\hat{y})$$

For perfect prediction, $H(\hat{y},y)=-1\log(1)=0$

According to this, we can create this loss function:

<div>

$$\begin{aligned}
minimize\ J &=-\log P(\omega_c\lvert \omega_{c-m},...,\omega_{c-1},...,\omega_{c+m}) \\
&= -\log P(u_c \lvert \hat{\upsilon}) \\
&= -\log \frac{\exp(u_c^T\hat{\upsilon})}{\sum_{j=1}^{\lvert V \rvert}\exp (u_j^T\hat{\upsilon})} \\
&= -u_c^T\hat{\upsilon}+\log \sum_{j=1}^{\lvert V \rvert}\exp (u_j^T\hat{\upsilon})
\end{aligned}$$

</div>


### Skip-Gram

Use current word to predict its context.

![cbow](/images/doc2vec_skip-gram.png)


1. We get the input word's vector $\upsilon_c$
2. Generate $2m$ score vectors, $uc_{c-m},...,u_{c-1},...,u_{c+m}$.
3. Turn scores into probabilities $\hat{y}=softmax(u)$
4. We desire probabilities $\hat{y}$ match the true probabilities $y$.

<div>

$$\begin{aligned}
minimize J &=-\log P(\omega_{c-m},...,\omega_{c-1},\omega_{c+1},...\omega_{c+m}\lvert \omega_c)\\
&=-\log \prod_{j=0,j\ne m}^{2m}P(\omega_{c-m+j}\lvert \omega_c)\\
&=-\log \prod_{j=0,j\ne m}^{2m}P(u_{c-m+j}\lvert \upsilon_c)\\
&=-\log \prod_{j=0,j\ne m}^{2m}\frac{\exp (u^T_{c-m+j}\upsilon_c)}{\sum_{k=1}^{\lvert V \rvert}{\exp (u^T_k \upsilon_c)}}\\
&=-\sum_{j=0,j\ne m}^{2m}{u^T_{c-m+j}\upsilon_c+2m\log \sum_{k=1}^{\lvert V \rvert} \exp(u^T_k \upsilon_c)}
\end{aligned}$$

</div>

## Models

Minimize $J$ is expensive, as the summation is over $\lvert V \rvert$. There are two ways to reduce the computation. Hierarchical Softmax and Negative Sampling.

### Hierarchical Softmax

Encode words into a huffman tree, then each word has a Huffman code. The probability of it's probability $P(w\lvert Context(\omega))$ can change to choose the right path from root the che leaf node, each node is a binary classification. Suppose code $0$ is a possitive label, $1$ is negative label. If the probability of a possitive classification is 
$$
\sigma(X^T_\omega \theta)=\frac{1}{1+e^{-X^T_\omega}}
$$

Then the probability of negative classification is
$$
1-\sigma(X^T_\omega \theta)
$$

![cbow](/images/doc2vec_hierarchical_softmax.png)
足球's Huffman code is $1001$, then it's probability in each node are

<div>

$$\begin{aligned}
p(d_2^\omega\lvert X_\omega,\theta^\omega_1&=1-\sigma(X^T_\omega \theta^\omega_1))\\
p(d^\omega_3\lvert X_\omega,\theta^\omega_2&=\sigma(X^T_\omega \theta^\omega_2))\\
p(d^\omega_4\lvert X_\omega,\theta^\omega_3&=\sigma(X^T_\omega \theta^\omega_3))\\
p(d^\omega_5\lvert X_\omega,\theta^\omega_4&=1-\sigma(X^T_\omega \theta^\omega_4))\\
\end{aligned}$$

</div>

where $\theta$ is prarameter in the node.

The probability of the `足球` is the production of these equation.

Generally,

<div>

$$p(\omega\lvert Context(\omega))=\prod_{j=2}^{l\omega}p(d^\omega_j\lvert X_\omega,\theta^\omega_{j-1})$$

</div>

### Negative Sampling

Choose some negitive sample, add the probability of the negative word into loss function. Maximize the positive words' probability and minimize the negitive words' probability.

Let $P(D=0 \lvert \omega,c)$ be the probability that $(\omega,c)$ did not come from the corpus data. Then the objective funtion will be

<div>

$$\theta = \text{argmax} \prod_{(\omega,c)\in D} P(D=1\lvert \omega,c,\theta) \prod_{(\omega,c)\in \tilde{D}} P(D=0\lvert \omega,c,\theta)$$

</div>

where $\theta$ is the parameters of the model($\upsilon$ and $u$).

Ref:

- [word2vec原理推导与代码分析](http://www.hankcs.com/nlp/word2vec.html)
- [CS 224D: Deep Learning for NLP Lecture Notes: Part I](http://cs224d.stanford.edu/lecture_notes/notes1.pdf)
- [word2vec 中的数学原理详解（一）目录和前言](http://blog.csdn.net/itplus/article/details/37969519)
