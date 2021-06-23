---
title: 集成学习（Ensemble Learning）
date: 2019-11-15 17:38:56
tags: [Note, Machine Learning]
categories: Note
---

[参见Tommy Huang Blog]([https://medium.com/@chih.sheng.huang821/%E6%A9%9F%E5%99%A8%E5%AD%B8%E7%BF%92-ensemble-learning%E4%B9%8Bbagging-boosting%E5%92%8Cadaboost-af031229ebc3](https://medium.com/@chih.sheng.huang821/機器學習-ensemble-learning之bagging-boosting和adaboost-af031229ebc3))

## 集成学习的概念

Ensemble Learning基本條件是:每個分類器之間應該要有差異，每個分類器準確率需大於0.5。
如果用的分類器沒有差異，那只是用很多個一樣的分類器來分類，結果合成起來是沒有差異的。如果分類器的精度p<0.5，隨著ensemble規模的增加，分類準確率不斷下降；如果精度大於p>0.5，那麼最終分類準確率可以趨向於1。

## Bagging

随机取样/training set ——>bootstrap——>training subsets——>weak classifier——>majority vote

>bootstrap：從訓練資料中隨機抽取(取出後放回，n<N)樣本訓練多個分類器(要多少個分類器自己設定)，每個分類器的權重一致最後用投票方式(Majority vote)得到最終結果

Bagging的優點在於原始訓練樣本中有噪聲資料(不好的資料)，透過Bagging抽樣就有機會不讓有噪聲資料被訓練到，所以可以降低模型的不穩定性。

## Boosting

>將很多個弱的分類器(weak classifier)進行合成變成一個強分類器(Strong classifier)，和Bagging不同的是分類器之間是有關聯性的，是透過將舊分類器的錯誤資料權重提高，然後再訓練新的分類器，這樣新的分類器就會學習到錯誤分類資料(misclassified data)的特性，進而提升分類結果。

對於Boosting來說，有兩個關鍵，一是在如何改變訓練資料的權重；二是如何將多個弱分類器組合成一個強分類器。而且存在一個重大的缺陷：該分類算法要求預先知道弱分類器識別準確率的下限。

## AdaBoost

>是一種改進的Boosting分類算法。方式是提高被前幾個分類器線性組合的分類錯誤樣本的權重，這樣做可以讓每次訓練新的分類器的時後都聚焦在容易分類錯誤的訓練樣本上。每個弱分類器使用加權投票機制取代平均投票機制，只的準確率較大的弱分類器有較大的權重，反之，準確率低的弱分類器權重較低。

##Bagging與Boosting的區別之處

#### **訓練樣本:**

**Bagging**: 每一次的訓練集是隨機抽取(每個樣本權重一致)，抽出可放回，以獨立同分布選取的訓練樣本子集訓練弱分類器。

**Boosting**: 每一次的訓練集不變，訓練集之間的選擇不是獨立的，每一是選擇的訓練集都是依賴上一次學習得結果，根據錯誤率(給予訓練樣本不同的權重)取樣。

#### **分類器:**

**Bagging**: 每個分類器的權重相等。

**Boosting**: 每個弱分類器都有相應的權重，對於分類誤差小的分類器會有更大的權重。

#### **每個分類器的取得:**

**Bagging**: 每個分類器可以並行生成。

**Boosting**: 每個弱分類器只能依賴上一次的分類器順序生成。（串行）

## 随机森林

**下面是随机森林的构造过程：**

>​      1.假如有N个样本，则有放回的随机选择N个样本(每次随机选择一个样本，然后返回继续选择)。这选择好了的N个样本用来训练一个决策树，作为决策树根节点处的样本。
>
>　　2. 当每个样本有M个属性时，在决策树的每个节点需要分裂时，随机从这M个属性中选取出m个属性，满足条件m << M。然后从这m个属性中采用某种策略（比如说信息增益）来选择1个属性作为该节点的分裂属性。
>
>　　3. 决策树形成过程中每个节点都要按照步骤2来分裂（很容易理解，如果下一次该节点选出来的那一个属性是刚刚其父节点分裂时用过的属性，则该节点已经达到了叶子节点，无须继续分裂了）。一直到不能够再分裂为止。注意整个决策树形成过程中没有进行剪枝。
>
>　　4. 按照步骤1~3建立大量的决策树，这样就构成了随机森林了。