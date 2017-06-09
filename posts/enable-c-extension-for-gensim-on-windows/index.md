<!-- 
.. title: Enable C Extension for gensim on Windows
.. slug: enable-c-extension-for-gensim-on-windows
.. date: 2017-06-10 03:40:32 UTC+08:00
.. tags: 
.. category: 
.. link: 
.. description: 
.. type: text
-->

For these days, I’m working on some text classificatin works, and I use `gensim`’s `doc2vec` function.

When using gensim, it shows this warning message:
```
C extension not loaded for Word2Vec, training will be slow.
```

I search this on Internet and found that gensim has rewrite some part of the code using `cython` rather than `numpy` to get better performance. A compiler is required to enable this featrue.

I tried to install mingw and add it into the path, but it's not wroking.

Finally, I tried to install [Visual C++ Build Tools](http://landinghub.visualstudio.com/visual-cpp-build-tools) and it works.

If this output a none `-1` digit, then it's fine.
```python3
from gensim.models import word2vec
print(word2vec.FAST_VERSION)
```
