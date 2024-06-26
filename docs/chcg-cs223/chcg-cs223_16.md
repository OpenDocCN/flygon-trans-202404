# 摊销分析的几句话

请参阅 Okasaki 教科书第 5.1 节，了解两种摊销分析方法的概要，即银行家方法和物理学家方法。在这里，我们将就以前的[`FastQueue`](https://www.classes.cs.uchicago.edu/archive/2015/winter/22300-1/public-code/Queues/FastQueue.elm)实现的会计做一些额外的说明。

请记住，当评估函数的运行时间时，我们通常使用符号常量而不是具体单位（例如秒），以便从执行环境的低级，偶然和可变特性中抽象出来。而且因为大 O 分析进一步抽象了函数的特定常量，因此符号常量（例如*k*）经常被特定的小常量（例如*1*）所取代。

一旦对这种推理感到舒适，我们通常可以直接说像是"**enqueue**的摊销成本为*2*"和"**dequeue**的摊销成本为*1*"。与此同时，让我们额外花费精力明确计算操作的实际（符号）成本，然后再将其降低到它们的渐近特性。

为避免与教科书中代表学分的符号*c*混淆，在这里我们将使用元变量*k*来表示常量的范围。让以下常量代表在包含*m*个元素的`back`列表中`Queue`上各种操作的实际成本：

+   *k[1]*是**enqueue**的成本；

+   *k[2]*是**peek**的成本；

+   当**List.reverse**未被调用时，*k[3]*是**dequeue**的成本（廉价情况）；而

+   *k[4]m + k[5] = m + k[6]*是**dequeue**的成本，当**List.reverse**被调用时（昂贵的情况）。请注意，该实际成本与`back`列表的大小成线性关系。

我们现在使用这些符号常量重新审视教科书中的摊销分析，而不是具体的成本，例如*1*和*2*。

使用银行家方法（*a[i] = t[i] + c[i] - c[i]*）：

+   **enqueue**：*k[1] + 1 - 0 = k[1] + 1*

+   **peek**：*k[2] + 0 - 0 = k[2]*

+   **dequeue**（廉价的）：*k[3] + 0 - 0 = k[3]*

+   **dequeue**（昂贵的）：*(m + k[6]) + 0 - m = k[6]*

因此，所有操作都以*O(1)*的摊销时间运行。

使用物理学家方法（*a[i] = t[i] + Φ(d[i]) - Φ(d[i]-1*)：

+   **enqueue**：*k[1] + (m+1) - m = k[1] + 1*

+   **peek**：*k[2] + m - m = k[2]*

+   **dequeue**（廉价的）：*k[3] + m - m = k[3]*

+   **dequeue**（昂贵的）：*(m + k[6]) + 0 - m = k[6]*

因此，所有操作都以*O(1)*的摊销时间运行。

## 阅读

#### 需要

+   Okasaki，第 5.1 节和第 5.6 节
