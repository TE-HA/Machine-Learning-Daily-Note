# RNN

循环神经网络处理==时间序列==数据

![image.png](https://i.loli.net/2020/05/11/k7y5uzsxwhFaTbZ.png)

瞬时状态下的输入包括==之前输入的数据==和==当前的数据==。

![image.png](https://i.loli.net/2020/05/11/TMP7uJxGwXEvW4B.png)

RNN最大的问题是当处理很长的时候会造成信息冗余。

## LSTM

C:控制参数，控制什么样的信息会被保留什么样的会被遗忘。

门：是一种让信息选择式通过的方法，Sigmoid神经网络层和一乘法操作。

![image.png](https://i.loli.net/2020/05/11/baQBTn1cwJxR3rL.png)

自然语言处理：词向量（词嵌入模型）

