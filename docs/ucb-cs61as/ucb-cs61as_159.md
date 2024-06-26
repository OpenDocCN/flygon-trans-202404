# 编程考虑

## 编程考虑

即使使用了串行器，编写成功处理并发的程序也并不容易。事实上，今天广泛使用的所有操作系统在这个领域都存在错误；例如，Unix 系统预计每个月或两个月会因并发错误而崩溃。

为了使讨论具体化，让我们考虑一个为全球数千名同时用户提供服务的航空公司预订系统。以下是可能出错的事情：

+   **错误的结果。** 最糟糕的问题是同一个座位被两个不同的人预订。就像给 x 加 1 的情况一样，预订系统必须首先找到一个空座位，然后将该座位标记为已占用。读取然后修改数据库的这个顺序必须受到保护。

+   **低效率。** 确保正确结果的一个非常简单的方法是使用单个串行器保护整个预订数据库，以便一次只有一个人可以发出请求。但这是一个不可接受的解决方案；成千上万的人正在等待预订座位，大多数人并非为同一航班。

+   **死锁。** 假设有人想去一个没有直达航班的城市。我们必须确保在同一天可以预订到 A 航班的座位和连接航班 B 的座位，然后再承诺任何预订。这可能意味着我们需要同时使用两个串行器，一个用于每个航班。假设我们说类似于

    (serializer-A (serializer-B (lambda () ...))))

与此同时，还有人说

```
(serializer-B (serializer-A (lambda () ...)))) 
```

时间可能会安排得当，我们得到串行器 A，另一个人得到串行器 B，然后我们每个人都被困在等待对方（永远！）。

+   **不公平。** 这并非在每种情况下都是问题，但有时您希望避免解决死锁问题的解决方案总是优先考虑某个进程。如果高优先级进程贪婪，低优先级进程可能永远无法轮到共享数据。

## 并发程序的正确行为

根据您正在编写的特定程序，正确行为的定义可能有所不同。通常情况下，如果并发程序产生与进程按某种顺序顺序运行时相同的结果，则说该并发程序显示正确行为。这一要求有两个重要方面。

首先，它不要求进程实际按顺序运行，而只要求产生与它们按顺序运行时相同的结果。

其次，由于我们只要求结果与某个顺序的结果相同，所以并发程序可能会产生多个可能的“正确”结果。
