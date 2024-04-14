# 可空变量

在Java和Scala中，类型为\(T\)的变量要么包含对正确类型对象的引用，要么包含特殊值 null。如果值为null，则意味着该变量当前不引用任何对象。

程序员使用 null 作为特殊标记，例如表示发生错误，或者无法找到某些请求的信息。当随后的代码不检查这种特殊情况时，会出现问题，因为对具有值 null 的变量调用任何操作都将失败。由于变量不引用任何对象，因此无法调用任何方法！结果是NullPointerException，这是一个常常难以找到的错误。

Kotlin通过不允许Int、String等类型的变量为null来帮助我们避免这个问题。如果尝试将变量设置为null，编译器会报错：

```
>>> val s: String = null
error: null can not be a value of a non-null type kotlin.String

```

有时，确实希望允许null，要么因为想使用null来指示特殊情况或错误，要么因为调用一些使用 null 的Java函数。在这种情况下，需要通过在类型后面放置问号来指示变量是可空的：

```
>>> var s: String? = null
>>> println(s)
null
>>> s = "Hello World"
>>> println(s)
Hello World
>>> s = null
>>> println(s)
null
>>> s = "I'm nullable"
>>> println(s)
I'm nullable

```

由于s的类型是String?，它允许具有值 null。

然而，每当我们想调用对象 s 的String方法时，我们必须小心：如果 s == null，则调用方法会失败。因此，Kotlin禁止在不先检查null的情况下调用可空变量的方法：

```
>>> s.length
error: only safe (?.) or non-null asserted (!!.) calls are allowed on a nullable receiver of type kotlin.String?

```

我们可以手动测试是否为null：

```
>>> fun printlen(s: String?) {
...   if (s == null)
...     println("Null string")
...   else
...     println(s.length)
... }
>>> printlen("Hello")
5
>>> printlen(null)
Null string

```

请注意编译器认识到在else部分 s 的值不可能为null，因此调用 s.length 是可以的。

Kotlin提供了一些很好的快捷方式来更轻松地处理可空变量。首先，我们可以使用 ?. 运算符。如果对象存在，则调用方法，否则不调用方法，结果为null：

```
>>> s
I'm nullable
>>> s?.length
12
>>> s = null
>>> s?.length
null

```

如果我们不喜欢返回null作为值，可以使用"Elvis operator" ?:. 如果左侧不为null，则返回左侧，否则返回右侧。现在我们可以将上面的函数printlen重写如下：

```
>>> fun printlen(s: String?) {
...   println(s?.length ?: "Null string")
... }
>>> printlen("Hello world")
11
>>> printlen(null)
Null string

```

最后，有时你有一个类型为String?的变量，但你知道（因为文档或者因为是你仔细分析过的自己的代码）该变量永远不会为null。在这种情况下，你可以向编译器保证一切正常：

```
>>> val s: String? = "Hello World"
>>> val t: String = s
error: type mismatch: inferred type is kotlin.String? but kotlin.String was expected
>>> val t : String = s!!

```

第一个赋值失败，因为s的类型为String?，因此可能为null，因此不允许将其赋值给t（类型为String）。在第二个赋值中，我使用 !! 运算符向编译器保证一切正��。

!! 运算符也可以用于在你确信变量不为null时调用方法：

```
>>> s.length
error: only safe (?.) or non-null asserted (!!.) calls are allowed on a nullable receiver of type kotlin.String?
>>> s!!.length
11

```

如果你的承诺是错误的，而实际上s为null，那么在这一点上将会发生异常：

```
>>> var s: String? = null
>>> s!!.length
kotlin.KotlinNullPointerException

```

一个返回可空类型的标准Kotlin函数的例子是 readLine()：它返回String?，即输入字符串，或者当输入结束时为null（例如因为你正在从文件重定向输入）。

下面的简短脚本展示了这一点（[reverse.kts](https://github.com/otfried/cs109-kotlin/raw/master/tutorial/11-null/reverse.kts)）：

```
fun reverser() {
  var line: String? = readLine()
  while (line != null) {
    println(line.reversed())
    line = readLine()
  }
}

println("Enter lines to be reversed:")
reverser()

```

如果我们在从脚本文件本身重定向输入的情况下运行脚本，它会在最后一行正确地停止：

```
$ kts reverse.kts < reverse.kts 
Enter lines to be reversed:
{ )(resrever nuf
)(eniLdaer = ?gnirtS :enil rav  
{ )llun =! enil( elihw  
))(desrever.enil(nltnirp    
)(eniLdaer = enil    
}  
}

)":desrever eb ot senil retnE"(nltnirp
)(resrever

```
