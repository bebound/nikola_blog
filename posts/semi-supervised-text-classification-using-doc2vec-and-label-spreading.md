<!--
.. title: Semi-supervised text classification using doc2vec and label spreading
.. slug: semi-supervised-text-classification-using-doc2vec-and-label-spreading
.. date: 2017-09-10 22:18:15 UTC+08:00
.. tags: mathjax
.. category: 
.. link: 
.. description: 
.. type: text
-->

Here is a simple way to classify text without much human effort and get a impressive performance.

It can be divided into two steps:

1. Get train data by using keyword classificaton
2. Generate a more accurate classification model by using doc2vec and label spreading

### Keyword-based Classification
Keyword based classification is a simple but effective method. Extracting the target keyword is a monotonous work. I use this method to automatic extract keyword candicate.


1. Find some most common words to classify the text.
2. Use this equition to calculate the score of each word appears in the text.
   $$ score(i) = \frac{count(i)}{all\_count(i)^{0.3}}$$
   which $all\_count(i)$ is the word i's wordc ount in all corpus, and $count(i)$ is the word i's word count in positive corpus.
3. Check the top words, add it to the final keyword list. Repeat this process.

Finally, we can use the keywords to classify the text and get the train data. 

### Classification by `doc2vec` and Label Spreading

Keyword-based classification sometimes produces the wrong result, as it can't using the symantic information in the text. Fortunately, Google has open sourced `word2vec`, which can be used to produce word embedding. Furthermore, sentences can also be converted to vectors by using `doc2vec`. Sentences which has closed meaning also have small vector distance.

So the problem is how to classify these vectors.

1. Using corpus to train the `doc2vec` model.
2. Using `doc2vec` model to convert sentence into vector.
3. Using label spreading algorithm to train a classify model to classify the vectors.





