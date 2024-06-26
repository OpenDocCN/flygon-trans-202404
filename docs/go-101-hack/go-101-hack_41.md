# 无需关闭每个通道

# 无需关闭每个通道

* * *

在使用完通道后，你不需要关闭它，它可以被垃圾收集器自动回收。以下引用来自[Go 程序设计语言](http://www.gopl.io/)：

> 你无需在使用完每个通道后都关闭它。只有当有必要告诉接收 goroutine 所有数据都已发送时才需要关闭通道。垃圾收集器确定为不可达的通道将会回收其资源，无论它是否已关闭。（不要将此与打开文件的关闭操作混淆。在使用完每个文件后调用 Close 方法是很重要的。）

参考：

[是否可以保持通道开放？](http://stackoverflow.com/questions/8593645/is-it-ok-to-leave-a-channel-open);

[Go 程序设计语言](http://www.gopl.io/)。
