<!--
.. title: LSTM and GRU
.. slug: lstm-and-gru
.. date: 2018-04-22 23:27:45 UTC+08:00
.. tags: mathjax
.. category: 
.. link: 
.. description: 
.. type: text
-->

## LSTM

The avoid the problem of vanishing gradient and exploding gradient in vanilla RNN, LSTM was published, which can remember information for longer periods of time.

Here is the structure of LSTM:

![LSTM](/images/LSTM_LSTM.png)

The calculate procedure are:

<div>

$$
\begin{aligned}
f_t&=\sigma(W_f\cdot[h_{t-1},x_t]+b_f)\\
i_t&=\sigma(W_i\cdot[h_{t-1},x_t]+b_i)\\
o_t&=\sigma(W_o\cdot[h_{t-1},x_t]+b_o)\\
\tilde{C_t}&=tanh(W_C\cdot[h_{t-1},x_t]+b_C)\\
C_t&=f_t\ast C_{t-1}+i_t\ast \tilde{C_t}\\
h_t&=o_t \ast tanh(C_t)
\end{aligned}
$$

</div>

$f_t$,$i_t$,$o_t$ are forget gate, input gate and output gate respectively. $\tilde{C_t}$ is the new memory content. $C_t$ is cell state. $h_t$ is the output. 

Use $f_t$ and $i_t$ to update $C_t$, use $o_t$ to decide which part of hidden state should be outputted.

## GRU

![LSTM](/images/LSTM_GRU.png)

<div>

$$
\begin{aligned}
z_t&=\sigma(W_z\cdot[h_{t-1},x_t])\\
r_t&=\sigma(W_r\cdot[h_{t-1},x_t])\\
\tilde{h_t}&=tanh(W\cdot[r_t \ast h_{t-1},x_t])\\
h_t&=(1-z_t)\ast h_{t-1}+z_t \ast \tilde{h_t}
\end{aligned}
$$

</div>

$z_t$ is update gate, $r_t$ is reset gate, $\tilde{h_t}$ is candidate activation, $h_t$ is activation.

Compare with LSTM, GRU merge cell state and hidden state to one hiddent state, and use $z_t$ to decide how to update the state rather than $f_t$ and $i_t$.


Update:

Here is a good article: [Illustrated Guide to LSTM’s and GRU’s: A step by step explanation](https://medium.com/m/global-identity?redirectUrl=https%3A%2F%2Ftowardsdatascience.com%2Fillustrated-guide-to-lstms-and-gru-s-a-step-by-step-explanation-44e9eb85bf21)

Ref：

- [Understanding LSTM Networks](http://colah.github.io/posts/2015-08-Understanding-LSTMs/)
- [RNN, LSTM, GRU 公式总结](https://blog.csdn.net/zhangxb35/article/details/70060295)
