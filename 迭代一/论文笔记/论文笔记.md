# Sentiment Strength Detection for the Social Web论文笔记

[TOC]

## **Abstract**

大多数情绪分析设计商业，如分析**产品评论**情感。但是**they exploit indirect indicators of sentiment that can reflect genre or topic instead**。这对于分析社交文本是不可取的。

无监督学习是SSth的优点。

数据集：**MySpace, Twitter, YouTube,Digg,RunnersWorld,BBC Forums**

**结论：**

本文评估了该算法的改进版本。SentiStrength优于原来版本，不优于机器学习方法。对于social web context表现足够好，对于情感弱的文本（新闻）表现不好。

## **Introduction**

social web context只是情感分析的一小部分，但是涉及内容广泛，对社会学研究有意义。

不能使用传统情感分析方法分析social web context，因为：

1. 标注数据少。情感文本必须手动标注

2. 情感分析是领域依赖的。不同topics and communication styles需要不同的classifier。

3. 关键点：技术优化后的classifier可能会使用indirect indicators，会给出误导性结果。

   e.g.：政治话题中，`伊拉克、伊朗、巴勒斯坦和以色列`可能会成为消极词。因为它们通常出现在消极话题中。

所以我们使用direct indicators of sentiment进行情感分析。

方法：主要通过文本中存在的**已知的含情感词汇或短语的词汇**进行情感分析。

方法1：

​	情绪分类：

​	积极情绪强度；消极情绪强度。转化为分数。

方法2：

​	积极消极情绪合成单一指标。

### 研究目的：

SentiStrength作为MySpace  sentiment strength detection program的升级版，只依赖direct indicator of sentiment的Lexical Algorithms。对于social web能否有效？

## **Sentiment Analysis**

### 情绪分析任务：

- 主观性（subjective）检测

  subjective or objective

- 极性（polarity）检测

  positive or negative

- 情绪强度（sentiment strength）检测（不常用）

  predicts the **strength** of positive or negative sentiment

本节分析极性检测，三种检测方法类似。

### 常用情绪分析方法：

#### 机器学习

- 选择机器学习算法
- 提取文本特征，训练classifier

#### 种子词法

- co-occur frequency

缺点：使用indirect indicator

### *Lexical Algorithms*

已知情绪集+算法 $\to$ 预测文本情绪

#### 优点：

1. 可扩展其他信息。

   表情符号表、语义规则...

2. 词汇源丰富

3. 有各种方法改进标准源

   添加额外术语，已针对特定领域。如，“小”在便携设备中是积极词

#### SO-CAL

SO-CAL和本文的SentiStrength很相似。

##### negtive to positive 

-5 to +5

##### 词法建立

手工标注2,252 adjectives, 745 adverbs 1,142 nouns, and 903 verbs

强化情绪表达词，如would；重复字符；大写字符...

## **SentiStrength 2**

### 定义：

SentiStrength is a **lexicon-based classifier** that uses additional (nonlexical) linguistic information and rules to **detect sentiment strength** in **short informal English text**.

### 输出：

two integers:  1 to 5 for positive sentiment strength; a separate score of 1 to 5 for negative sentiment strength.

e.g.: 

1,1 不积极，不消极

3,5 适度积极，强烈消极 

### 主要特征列表

本文P166

![image-20230303105517868](C:\NJU_SE_NOTES\2023-软件工程与计算III\lab\lab1\ProcessDocumentation\迭代一\论文笔记\images\image-20230303105517868.png)

### 1$\to$2

**SentiStrength 2相对 1 扩展了什么？**

![image-20230303110048794](C:\NJU_SE_NOTES\2023-软件工程与计算III\lab\lab1\ProcessDocumentation\迭代一\论文笔记\images\image-20230303110048794.png)

## **Research Questions**

### 研究目标

- 评估SentiStrength2在各种不同的在线环境中，是否可行。
- 评估SentiStrength2与其他使用indirect terms的方法、机器学习相比，表现如何。

## **Methods and Data**

### test data set 6+1

![image-20230303141146739](C:\NJU_SE_NOTES\2023-软件工程与计算III\lab\lab1\ProcessDocumentation\迭代一\论文笔记\images\image-20230303141146739.png)

- 证明测试数据有效
  - Krippendorff’s *α*
- 标准机器学习算法(已改进)
  - support vectormachines (SVM; Sequential Minimal Optimization variant, SMO)
  - Logistic Regression (SLOG for short)
  - ADA Boost
  - SVM Regression
  - Decision Table
  - Naïve Bayes
  - J48 classification tree, and JRip rule-based classififier

### *Corpus Statistics*

数据集大小

![image-20230303143132518](C:\NJU_SE_NOTES\2023-软件工程与计算III\lab\lab1\ProcessDocumentation\迭代一\论文笔记\images\image-20230303143132518.png)

### *Overall Sentiment Distribution*

见Figures 1 and 2

![image-20230303144131924](C:\NJU_SE_NOTES\2023-软件工程与计算III\lab\lab1\ProcessDocumentation\迭代一\论文笔记\images\image-20230303144131924.png)

## **Results**

- correct：accuracy，测试集命中率
- +/- 1：accuracy，允许误差为 $\pm1$class 之后的命中率
- correl：correlation，Pearson算法计算相关度

见 Table 2

![image-20230303144421842](C:\NJU_SE_NOTES\2023-软件工程与计算III\lab\lab1\ProcessDocumentation\迭代一\论文笔记\images\image-20230303144421842.png)

## **Limitations and Discussion**

1. 数据集有限
2. 数据标注可能有误差

之后水了一堆ml的内容。

## **Conclusions**

- 监督/非监督两个版本都表现良好，在全新的social web context中，无监督SSth可以有效检测情绪。
- SSth可能不如ml

SSth的无监督版本有应用价值。



