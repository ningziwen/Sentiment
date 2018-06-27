# 基于RNN的文本情感极性分析
## 一. 摘要
本文讨论了基于 RNN 进行文本情感极性分析的过程。
本文首先概述了 RNN 的原理，然后对餐馆评价数据集做预处理设定训练集和
测试集，在 python 环境下调用 passage 库实现 rnn 过程，最后用 scikit-
learn 库评价实验结果。
## 二. . 引言
文本的情感极性分析指的是对带有感情色彩的主观性分别进行分析、处理、
归纳和推理的过程，常见的情感极性分析方法主要有基于情感词典的方法和基
于机器学习的方法。本文采用的是基于 R N N 的机器学习方法，主要参考
Andrej Karpathy 的研究成果。
## 三. . 正文
### 1. R N N 的原理概述
R N N 所采用的思想是利用文本的序列信息。在传统神经网络中我们假设所
有的输入是相互独立的，但这种假设对于很多任务来说不够好。如果想要预测
一句话中的下一个字，最好要知道在它之前的字。R N N 被称为循环神经网络正
是因为它对于序列中每个元素都设定其输出依赖于之前的计算。理解 R N N 的
另一个方法是 R N N 有“记忆”功能，可以包含很久以前被计算的信息。R N N
理论上可以利用任意长序列信息，但是实际上有一定限制。
要处理的文本序列有几个字网络就有几层。
x t 是第 t次的输入。
s t 是第 t次的隐藏状态，由前一次的隐藏状态和此次的输入决定：s t =
𝑓(𝑉𝑥 𝑡 + 𝑋𝑡 𝑡−1 )。f是一个非线性函数例如 tanh 或 R eLU 。s −1 一般初始化为全
0。
o t 是第 t次的输出，如果想要预测下一个字那么在字典中存在o t =
𝑡𝑜𝑓𝑢𝑚𝑎𝑥(𝑊𝑡 𝑡 )。
### 2. 数据集描述
Sem Eval-2015 ABSA R estaurants R eview s - Test D ata - G old
Annotations
数据来源
http://m etashare.ilsp.gr:8080/repository/dow nload/d32aeb3e9ca011e4a35
0842b2b6a04d737ee004f7cdc428bbf1ad4bd67977d22/
2
整个数据集包含对餐厅服务、食品各方面的评价，这里简单抽取了对食品
的 positvie 和 negative 的评价分析
1095 组餐馆食物评价数据，text.txt为评价的内容，polarity.txt为情感极
性，包含 2881 个好评和 3215 个差评。
### 3. 设计步骤
1) 读入 text.txt和 polarity.txt数据
2) 设定训练集中正极性情感数目为 500 个，负极性为 100 个，其他均
为测试集。随机产生训练集和测试集。
3) 用训练集训练出循环神经网络。
4) 用训练出的模型在测试集中预测出结果。
5) 将预测结果与实际结果对比，输出精确率、召回率和 F1。
### 4. 实验结果
精确率为 0.7672，召回率为 1.0，F1 为 0.8683。
### 5. 结果评价
根据传统的准确率评价分类器存在局限性，因而定义出新的评价指标。
首先分别定义正类分类为正类、正类分类成负类、负类分类成正类、负
类分类成负类的数目分别为 TP,FN ,FP,FN 。
则精确率为P =
𝑇𝑃
𝑇𝑃+𝐹𝑃 ，表示正类样本预测正确占全部正类样本的比
值，召回率为R =
𝑇𝑃
𝑇𝑃+𝐹𝑁 ，表示针对原来样本中正类预测正确的比值，
F1 为F 1 =
2𝑇𝑃
2𝑇𝑃+𝐹𝑃+𝐹𝑁 ，是 P 和 R 的调和平均数。
根据得到的实验结果可知该分类器基本实现了对文本情感极性的分类。
## 四. . 结论
本文利用循环神经网络成功实现了文本情感极性的分类，性能较好。虽然
只是一个简单的例子，却验证了 R N N 的可靠性。因此很容易看出 R N N 在自然
语言处理领域的重要地位，经过进一步完善很可能会在科学界产生重大成就。
## 五. . 参考 文献
【1】 Karpathy A. The unreasonable effectiveness of recurrent neural networks[J]. Andrej
Karpathy blog, 2015.

【2】 Graves A. Supervised sequence labelling with recurrent neural networks[M].
Heidelberg: Springer, 2012.
3

【3】 http://www.wildml.com/2015/09/recurrent-neural-networks-tutorial-part-1-
introduction-to-rnns