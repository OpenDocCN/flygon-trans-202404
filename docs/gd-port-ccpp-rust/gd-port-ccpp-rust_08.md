# 让我们从简单的开始

# 让我们从简单的开始

任何语言的通常介绍都是"Hello, World!"。一个将该消息打印到控制台的简单程序。

这是我们如何为C编写它的方式：

```
#include <stdio.h>

int main(int argc, char *argv[]) {
  printf("Hello, World!\n");
  return 0;
} 
```

C++可以以相同的方式编写，或者如果我们更喜欢的话，可以使用C++的流类：

```
#include <iostream>

using namespace std;

int main(int argc, char *argv[]) {
  cout << "Hello, World!" << endl;
  return 0;
} 
```

这里是Rust中的等效部分：

```
fn main() {
  println!("Hello, World!");
} 
```

我们可以观察到一些明显的相似之处：

+   C/C++和Rust都遵循将`main()`函数作为代码入口点的约定。注意，Rust的main函数不返回任何内容。它实际上是一个空方法。

+   有一个通用的打印语句。

+   在主要方面的一般结构，即主要部分，使用{ }和分号大部分相同。在两种语言中，一段代码被大括号括起来，分号用作语句之间的分隔符。

+   Rust看起来比C或C++更为简洁，因为它自动包含对其称为"预导入"的标准运行时的部分的引用。

`println!()`实际上是一个宏，它会扩展成写入标准输出的代码。我们知道它是一个宏，因为它以一个!字符结尾，但是你现在可以将它视为一个函数调用。我们将在后面看到Rust宏与C/C++中的宏有何不同。

## 编译我们的代码

打开命令提示符并设置您的编译器环境。

如果你使用gcc，你会像这样编译你的代码：

```
gcc hw.cpp -o hw 
```

如果你使用Microsoft Visual C++，你会这样编译：

```
cl /o hw.exe hw.cpp 
```

要在Rust中编译，你需要调用rustc编译器。

```
rustc hw.rs 
```

并运行其中一个

```
./hw (or .\hw.exe)
Hello, World! 
```

再次有相似之处：

+   有一个shell命令，用于编译代码并创建可执行文件。

+   二进制文件以相同的方式运行。

一个不太明显的相似之处是Rust与gcc-llvm和clang共享其代码生成后端。Rustc输出llvm比特码，通过LLVM编译（和优化）成机器码。这意味着生成的可执行文件在形式上与C++编译器输出的非常相似。这包括它为调试目的提供的符号信息。一个Rust可执行文件可以在gdb、lldb或Microsoft Visual Studio中进行调试，具体取决于目标平台。

```
rustc -O hw.rs 
```
