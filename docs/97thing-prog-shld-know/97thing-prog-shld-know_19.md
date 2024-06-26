# 方便性不是一个-ility

# 方便性不是一个-ility

已经有很多关于设计良好 API 的重要性和挑战的讨论。第一次就做对很困难，而后来改变更加困难。有点像养育孩子。大多数有经验的程序员已经学会了一个好的 API 遵循一致的抽象水平，表现出一致性和对称性，并形成了表达性语言的词汇。然而，了解指导原则并不会自动转化为适当的行为。吃甜食对你不好。

我不想站在高处说教，我想挑选一个特定的 API 设计“策略”，一个我一再遇到的：方便性的论点。它通常以以下一种“洞察”开始：

+   我不希望其他类必须进行两次单独调用来完成这件事。

+   如果这个方法几乎和这个方法一样，为什么我要再写一个方法呢？我只是加一个简单的开关。

+   看，这很简单：如果第二个字符串参数以“.txt”结尾，那么该方法会自动假定第一个参数是文件名，所以我真的不需要两个方法。

虽然初衷良好，但这样的论点往往会降低使用 API 的代码可读性。像这样的方法调用

```
parser.processNodes(text, false); 
```

没有知道实现或至少查阅文档，这是毫无意义的。这个方法很可能是为了实现者的方便而设计的，而不是为了调用者的方便——“我不希望调用者必须进行两次单独调用”被译为“我不想编写两个单独的方法”。方便性本身并没有什么 fundamentally 错误，如果它旨在成为对繁琐、笨拙或尴尬的解药的话。然而，如果我们再仔细考虑一下，这些症状的解药是效率、一致性和优雅，而不一定是方便性。API 应该隐藏底层复杂性，因此我们可以合理地期望良好的 API 设计需要一些努力。一个单一的大方法肯定比一个深思熟虑的一系列操作更方便编写，但使用起来会更容易吗？

将 API 比作一种语言的隐喻可以指导我们在这些情况下做出更好的设计决策。一个 API 应该提供一种表达丰富的语言，这给了上层足够的词汇来提出和回答有用的问题。这并不意味着它应该为每个可能值得提问的问题提供一个方法或动词。一个多样化的词汇可以让我们表达意义上的微妙之处。例如，我们更喜欢说 run 而不是 walk(true)，尽管它可以被看作是本质上相同的操作，只是以不同的速度执行而已。一个一致而深思熟虑的 API 词汇使得上一层的代码表达丰富且易于理解。更重要的是，一个可组合的词汇允许其他程序员以你可能没有预料到的方式使用 API —— 这对于 API 的用户来说确实是一个巨大的便利！下次当你想把一些东西捆绑到一个 API 方法中时，记住英语没有一个词对应`整理房间、安静做家庭作业`，尽管对于这样一个经常被请求的操作来说，这似乎真的非常方便。

作者：[Gregor Hohpe](http://programmer.97things.oreilly.com/wiki/index.php/Gregor_Hohpe)
