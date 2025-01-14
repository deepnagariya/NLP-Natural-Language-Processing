# Topic Modeling


Topic modelling is an unsupervised machine learning method that **helps us discover hidden semantic structures in a paper**, that allows us to learn topic representations of papers in a corpus. The model can be applied to any kinds of labels on documents, such as tags on posts on the website.

> Ещё можно называть мягкой би-кластеризацией

- [Topic Modeling](https://paperswithcode.com/task/topic-models) on Papers with Code
- [Topic Modeling](https://stackoverflow.com/questions/tagged/topic-modeling) on StackOverflow


## Models

- **Unsupervised**
	- Latent Dirichlet Allocation (LDA)
	- Expectation–maximization algorithm (EM Algorithm)
	- Probabilistic latent semantic analysis (PLSA)
	- LDA2Vec
	- Sentence-BERT (SBERT)
- **Sepervised or semi-supervised**
	- Guided Latent Dirichlet Allocation (Guided LDA)
	- Anchored CorEx: Hierarchical Topic Modeling with Minimal Domain Knowledge (CorEx)


> Dataset for this task:
  > - [A Million News Headlines](https://www.kaggle.com/therohk/million-headlines) - News headlines published over a period of 18 Years 
  
## Useful Articles 

- [Topic Modeling with LSA, PLSA, LDA & Lda2Vec](https://medium.com/nanonets/topic-modeling-with-lsa-psla-lda-and-lda2vec-555ff65b0b05)
- [Topic Modeling with Gensim (Python)](https://www.machinelearningplus.com/nlp/topic-modeling-gensim-python/#18dominanttopicineachsentence)
- [Topic Modeling in Python](https://ourcodingclub.github.io/tutorials/topic-modelling-python/)
- [Topic modeling visualization – How to present the results of LDA models?](https://www.machinelearningplus.com/nlp/topic-modeling-visualization-how-to-present-results-lda-models/)


______________________________________________________________

- классификация и категоризация документов
- тематическая сегментация документов
- атоматическое аннотирование документов
- автоматическая суммаризация коллекций

## Предварительная обработка и очистка текстов

- удаление форматирования и переносов
- удаление обрывочной и нетекстовой информации
- исправление опечаток
- сливание коротких текстов
- Формирование словаря:
	- Лемматизация
	- Стемминг
	- Выделение терминов (term extraction)
	- Удаление stopwords и слишком редких слов (реже 10 раз)
	- Использовать биграммы

### Базовые предположения

- Порядок слов в документе не важен (bag of words)
- Каждая пара **_(d, w)_** связана с некторой темой **_t ∈ T_** 
- Гипотеза условной независимости (cлова в документах генерируются темой, а не документом): **_p(w | t, d) = p(w | t)_**
- Иногда вводят предположение о разрежености:
	- Документ относится к небольшому числу тем
	- Тема состоит из небольшого числа терминов 
- Документ **_d_** -- это смесь распределений **_p(w | t)_** с весами **_p(t | d)_**

<img src="https://github.com/ElizaLo/NLP-Natural-Language-Processing/blob/master/img/formula_1.png" width="681" height="376">

### Постанвка задачи

**Дано:**
- **_W_** - словарь терминов (слов или словосочетаний)
- **_D_** - коллекция текстовых документов **_d ⊂ W_**
- **_n <sub>dw</sub>_** - сколько раз термин (слово) **_w_** встретится в документе **_d_**
- **_n <sub>d</sub>_** - длина документа **_d_**

**Найти:**
Параметры вероятностной тематической модели (формула полной вероятности):

<img src="https://github.com/ElizaLo/NLP-Natural-Language-Processing/blob/master/img/formula_2.png" width="280" height="72">

Условные распределения:
- **_φ<sub>w t</sub> = p(w | t)_** - вероятности терминов **_w_** в каждой теме **_t_**
- **_Θ<sub>t d</sub> = p(t | d)_** - вероятности тем **_t_** в каждом документе **_d_**

<img src="https://github.com/ElizaLo/NLP-Natural-Language-Processing/blob/master/img/formula_3.png" width="581" height="488">
<img src="https://github.com/ElizaLo/NLP-Natural-Language-Processing/blob/master/img/formula_4.png" width="501" height="231">

**Стохастическая матрица - столбцы дискретные вероятностные распределения**
- В **_Φ_** неотрицательные нормарованные значения, сумма по каждому столбцу = 1, столбец - дискретное распределение вероятностей

<img src="https://github.com/ElizaLo/NLP-Natural-Language-Processing/blob/master/img/formula_5.png" width="600" height="473">

### Не одно решение

<img src="https://github.com/ElizaLo/NLP-Natural-Language-Processing/blob/master/img/formula_6.png" width="594" height="171">

**Решение: Использование регуляризаторов**

<img src="https://github.com/ElizaLo/NLP-Natural-Language-Processing/blob/master/img/formula_7.png" width="594" height="469">

<img src="https://github.com/ElizaLo/NLP-Natural-Language-Processing/blob/master/img/formula_8.png" width="590" height="500">
<img src="https://github.com/ElizaLo/NLP-Natural-Language-Processing/blob/master/img/formula_9.png" width="482" height="156">

<img src="https://github.com/ElizaLo/NLP-Natural-Language-Processing/blob/master/img/formula_16.png" width="597" height="460">


##  Latent Dirichlet Allocation (LDA)

- **Generative model**

### Articles

- [Topic Modelling in Python with NLTK and Gensim](https://towardsdatascience.com/topic-modelling-in-python-with-nltk-and-gensim-4ef03213cd21)
- [Topic Modeling and Latent Dirichlet Allocation (LDA) in Python](https://towardsdatascience.com/topic-modeling-and-latent-dirichlet-allocation-in-python-9bf156893c24)
- [Topic Modelling in Python with NLTK and Gensim](https://towardsdatascience.com/topic-modelling-in-python-with-nltk-and-gensim-4ef03213cd21)
- [Using LDA Topic Models as a Classification Model Input](https://towardsdatascience.com/unsupervised-nlp-topic-models-as-a-supervised-learning-input-cf8ee9e5cf28)

### The Process

- We pick the number of topics ahead of time even if we’re not sure what the topics are.
- Each document is represented as a distribution over topics.
- Each topic is represented as a distribution over words.

<img src="https://github.com/ElizaLo/NLP-Natural-Language-Processing/blob/master/img/formula_10.png" width="598" height="337">
<img src="https://github.com/ElizaLo/NLP-Natural-Language-Processing/blob/master/img/formula_11.png" width="601" height="428">
<img src="https://github.com/ElizaLo/NLP-Natural-Language-Processing/blob/master/img/formula_12.png" width="577" height="291">

### Two important parameters of the algorithm are:

- **Topic concentration / Beta**
- **Document concentration / Alpha**

For the symmetric distribution, a high alpha-value means that each document is likely to contain a mixture of most of the topics, and not any single topic specifically. A low alpha value puts less such constraints on documents and means that it is more likely that a document may contain mixture of just a few, or even only one, of the topics. Likewise, a high beta-value means that each topic is likely to contain a mixture of most of the words, and not any word specifically, while a low value means that a topic may contain a mixture of just a few of the words.

If, on the other hand, the distribution is asymmetric, a high alpha-value means that a specific topic distribution (depending on the base measure) is more likely for each document. Similarly, high beta-values means each topic is more likely to contain a specific word mix defined by the base measure.

In practice, a high alpha-value will lead to documents being more similar in terms of what topics they contain. A high beta-value will similarly lead to topics being more similar in terms of what words they contain.



### Code examples

- [LDA_news_headlines](https://github.com/susanli2016/NLP-with-Python/blob/master/LDA_news_headlines.ipynb)


<img src="https://github.com/ElizaLo/NLP-Natural-Language-Processing/blob/master/img/formula_15.png" width="606" height="502">


# Semi-Supervised Topic Modeling

## Guided Latent Dirichlet Allocation (LDA)

`GuidedLDA` OR `SeededLDA` implements latent Dirichlet allocation (LDA) using collapsed Gibbs sampling. `GuidedLDA` can be guided by setting some seed words per topic. Which will make the topics converge in that direction.

- [Incorporating Lexical Priors into Topic Models](https://www.aclweb.org/anthology/E12-1021.pdf) Paper
- [GuidedLDA’s documentation](https://guidedlda.readthedocs.io/en/latest/)
- [GuidedLDA](https://github.com/vi3k6i5/guidedlda) GitHub repository
- [How we Changed Unsupervised LDA to Semi-Supervised GuidedLDA](https://www.freecodecamp.org/news/how-we-changed-unsupervised-lda-to-semi-supervised-guidedlda-e36a95f3a164/) Article

### Articles 

- [How did I tackle a real-world problem with GuidedLDA?](https://medium.com/analytics-vidhya/how-i-tackled-a-real-world-problem-with-guidedlda-55ee803a6f0d)
  - [Guided LDA_6topics-4-grams](https://github.com/ShahrzadH/Insight_Project_SHV/blob/master/notebook/Guided%20LDA_6topics-4-grams.ipynb) Code Exapmle
- 

### Code examples

- [Topic modelling using guided lda](https://www.kaggle.com/nvpsani/topic-modelling-using-guided-lda) Kaggle
- [guided_LDA](https://github.com/ramirezfranco/guided_LDA_example/blob/master/guided_LDA.ipynb)


### Issues

- [**Installation Error**](https://github.com/vi3k6i5/GuidedLDA/issues/26)

**Solution:**

Running on OS X 10.14 w/Python3.7. able to get past them by upgrading cython:

`pip3 install -U cython`

Removing the following 2 lines from `setup.cfg`:

`[sdist]`
```@python
pre-hook.sdist_pre_hook = guidedlda._setup_hooks.sdist_pre_hook
```

And then running the original installation instructions:

```@shell
git clone https://github.com/vi3k6i5/GuidedLDA
cd GuidedLDA
sh build_dist.sh
python setup.py sdist
pip3 install -e .
```
- **The package `GuidedLDA` doesn't installed**

**Solution:**

The package that this is built of off is LDA and it installed with no issue. I managed to copy from the GuidedLDA package: the guidedlda.py, utils.py, datasets.py and the few NYT data set items into the original LDA package, post installation.

[GuidedLDA_WorkAround](https://github.com/dex314/GuidedLDA_WorkAround)

1. Pull down the repository.

2. Install the original LDA package. 
	https://pypi.org/project/lda/
	
3. Drop the *.py files from the GuidedLDA_WorkAround repo in the lda folder under site-packages for your specific enviroment.

4. Profit...


## Anchored CorEx: Hierarchical Topic Modeling with Minimal Domain Knowledge (2017)

**Cor**relation **Ex**planation (**CorEx**) is a topic model that yields rich topics that are maximally informative about a set of documents. The advantage of using CorEx versus other topic models is that it can be easily run as an unsupervised, semi-supervised, or hierarchical topic model depending on a user's needs. For semi-supervision, CorEx allows a user to integrate their domain knowledge via **"anchor words"**. This integration is flexible and allows the user to guide the topic model in the direction of those words. This allows for creative strategies that promote topic representation, separability, and aspects. More generally, this implementation of CorEx is good for clustering any sparse binary data.

- **Paper**: Gallagher, R. J., Reing, K., Kale, D., and Ver Steeg, G. [**"Anchored Correlation Explanation: Topic Modeling with Minimal Domain Knowledge"**](https://www.transacl.org/ojs/index.php/tacl/article/view/1244). Transactions of the Association for Computational Linguistics (TACL), 2017.
- [GitHub repository](https://github.com/gregversteeg/corex_topic)
- [Example Notebook](https://github.com/gregversteeg/corex_topic/blob/master/corextopic/example/corex_topic_example.ipynb)
- [PyPI page for CorEx](https://pypi.org/project/corextopic/)
- [Anchored Correlation Explanation: Topic Modeling With Minimal Domain Knowledge (TACL) : Ryan J. Gallagher, Kyle Reing, David Kal](https://vimeo.com/276403824) at ACL Performance


### Modifications of CorEx

- [Bio CorEx: recover latent factors with Correlation Explanation (CorEx)](https://github.com/gregversteeg/bio_corex)
- [Correlation Explanation Methods](https://github.com/hrayrhar/T-CorEx)
	- Linear CorEx
	- T-CorEx
- [Latent Factor Models Based on Linear Total Correlation Explanation (CorEx)](https://github.com/gregversteeg/LinearCorex)


### Useful Articles 

- [Interactive Search using BioBERT and CorEx Topic Modeling](https://www.kaggle.com/jdparsons/biobert-corex-topic-search)


## Regulariazation

### Kullback–Leibler divergence (relative entropy)

Способ померять растояние между двумя распределениями

<img src="https://github.com/ElizaLo/NLP-Natural-Language-Processing/blob/master/img/formula_13.png" width="618" height="456">
<img src="https://github.com/ElizaLo/NLP-Natural-Language-Processing/blob/master/img/formula_14.png" width="613" height="189">

<img src="https://github.com/ElizaLo/NLP-Natural-Language-Processing/blob/master/img/formula_17.png" width="614" height="500">
<img src="https://github.com/ElizaLo/NLP-Natural-Language-Processing/blob/master/img/formula_18.png" width="602" height="552">
<img src="https://github.com/ElizaLo/NLP-Natural-Language-Processing/blob/master/img/formula_19.png" width="571" height="188">
<img src="https://github.com/ElizaLo/NLP-Natural-Language-Processing/blob/master/img/formula_20.png" width="605" height="507">
<img src="https://github.com/ElizaLo/NLP-Natural-Language-Processing/blob/master/img/formula_21.png" width="595" height="493">
<img src="https://github.com/ElizaLo/NLP-Natural-Language-Processing/blob/master/img/formula_22.png" width="610" height="329">
<img src="https://github.com/ElizaLo/NLP-Natural-Language-Processing/blob/master/img/formula_23.png" width="610" height="515">
<img src="https://github.com/ElizaLo/NLP-Natural-Language-Processing/blob/master/img/formula_24.png" width="593" height="430">
<img src="https://github.com/ElizaLo/NLP-Natural-Language-Processing/blob/master/img/formula_25.png" width="598" height="484">
