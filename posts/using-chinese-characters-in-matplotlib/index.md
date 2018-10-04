<!--
.. title: Using Chinese characters in Matplotlib
.. slug: using-chinese-characters-in-matplotlib
.. date: 2018-10-04 21:47:37 UTC+08:00
.. tags: 
.. category: 
.. link: 
.. description: 
.. type: text
-->

After searching from Google, here is easiest solution. This should also works on other languages:

```python
import matplotlib.pyplot as plt
%matplotlib inline
%config InlineBackend.figure_format = 'retina'

import matplotlib.font_manager as fm
f = "/System/Library/Fonts/PingFang.ttc"
prop = fm.FontProperties(fname=f)

plt.title("你好",fontproperties=prop)
plt.show()
```

Output:
![LSTM](/images/matplot_chinese.png)
