[地图](data_mining_map.htm) > [数据科学](data_mining.htm) > [预测未来](predicting_the_future.htm) > [建模](modeling.htm) > [分类](classification.htm) > OneR

# OneR

OneR，即"One Rule"，是一种简单但准确的分类算法，它为数据中的每个预测变量生成一条规则，然后选择总误差最小的规则作为其"一条规则"。为了为一个预测变量创建一条规则，我们针对每个预测变量与目标变量构建一个频率表。已经证明，OneR生成的规则准确度仅略低于最先进的分类算法，同时生成的规则易于人类解释。**OneR算法**对于每个预测变量，

对于该预测变量的每个值，制定以下规则；

统计目标（类别）的每个值出现的频率

找到最频繁的类别

制定规则将该类别分配给该预测变量的这个值

计算每个预测变量规则的总误差

选择总误差最小的预测变量。  *例子:*使用相关频率表基于OneR算法找到总误差最小的最佳预测变量。

![](../Images/b0cf1a9c371a0cca05f2c73fce68495b.jpg)![](../Images/37407197f3975ab4ff911595c1d334bd.jpg)

最佳预测变量是：

![](../Images/f0f61199580e9b362807f954c53b30c3.jpg)

**预测变量贡献**

简单地说，从频率表中计算的总误差是每个预测变量贡献度的度量。低总误差意味着对模型的可预测性有更高的贡献。

**模型评估**

以下混淆矩阵显示了显著的预测能力。OneR不生成分数或概率，这意味着评估图表（增益、提升、K-S和ROC）不适用。

| 混淆矩阵 | **打高尔夫** |   |
| --- | --- | --- |
| 是 | 否 |
| **OneR** | 是 | 7 | 2 | *[正预测值](model_evaluation_c.htm)* | 0.78 |
| No | 2 | 3 | *[负预测值](model_evaluation_c.htm)* | 0.60 |
|   | *[灵敏度](model_evaluation_c.htm)* | *[特异性](model_evaluation_c.htm)* | **[准确率](model_evaluation_c.htm)** = 0.71 |
| 0.78 | 0.60 |
| [练习](oner_exercise.htm) | [![](../Images/a890baab528b0ca069f7f2599c0c5e39.jpg)](datasets/OneR.txt) | ![](../Images/dc9f5f2d562c6ce8cb7def0d0596abff.jpg) [OneR互动](flash/OneR.html) |

![发明！](../Images/04c11d11a10b9a2348a1ab8beb8ecdd8.jpg)尝试通过使用[ANOVA](categorical_numerical.htm)和[Chi²检验](categorical_categorical.htm)来发明一个新的OneR算法。
