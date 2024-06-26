CSE 331 软件设计与实现

# 类和方法规范

内容：

+   介绍

+   抽象值和抽象状态

    +   数学抽象值

    +   规范字段

    +   派生字段

+   方法规范

    +   前置条件

    +   后置条件

    +   使用规范字段进行规范

    +   使用派生规范字段进行规范

+   子类和重写方法

* * *

## 介绍

本手册描述了如何记录类和方法的规范。本文侧重于实际问题。

本文以`Line`类为例。我们的示例中不提供字段或方法体。本文涵盖了*指定*类和方法的行为（它们应该做什么），而不是它们的*实现*（它们实际上做什么以及如何做到）。

抽象函数和表示不变量介绍了如何记录类的实现。

```
/**
 * This class represents the mathematical concept of a line segment.
 *
 * Specification fields:
 *  @specfield start-point : point // The starting point of the line
 *  @specfield end-point   : point // The ending point of the line
 *
 * Derived specification fields:
 *  @derivedfield length : real // length = sqrt((start-point.x - end-point.x)² + (start-point.y - end-point.y)²)
 *                              // The length of the line
 *
 * Abstract Invariant:
 *  A line's start-point must be different from its end-point.
 */
public class Line {

  ... // Fields not shown.

 /**
  * @requires p != null && ! p.equals(start-point)
  * @modifies this
  * @effects Sets end-point to p
  */
  public void setEndPoint(Point p) {
    ...
  }

  ...

}

```

因为这里讨论的几个概念是相互关联的，让我们在深入细节之前先列出一些定义的简要列表。

*抽象值*

类的实例应该代表什么。例如，`Line`的每个实例代表某条线段。

*抽象状态*

定义抽象值的信息。例如，每个抽象线都有一个起点和一个终点。

*规范字段*

描述类的抽象状态的组件。例如，`Line`的抽象状态由规范字段`start-point`和`end-point`组成。

*派生规范字段*

可以从规范字段派生但有用的信息。例如，`Line`具有派生字段`length`，描述线段的长度。

*抽象不变量*

必须在类的所有实例的抽象状态上保持真实的条件。例如，`Line`要求没有实例具有相同的起点和终点。抽象不变量是以抽象状态为基础表达的。请注意，这与描述具体表示属性的表示不变量（RI）不同。如果存在抽象不变量，则它仅指定对抽象值的约束。

*方法规范*

以抽象状态的术语描述方法的行为。例如，`Line`的`setEndPoint`方法更新`end-point`规范字段。

上述概念包含在类的外部规范（在 Javadoc 中）。它们帮助客户端文档化如何使用该类。

本文档的其余部分组织如下。首先，它解释了如何使用抽象状态、规范字段和派生字段来记录类抽象地代表的内容。然后，它解释了如何根据抽象状态来指定方法行为。

## 抽象值和抽象状态

对象的抽象值是客户端在推理对象时使用的信息。例如，一条线段是根据起点和终点定义的。这并*不*一定意味着对象的具体表示具有两个点字段。那只是一种表示，但还有其他表示，比如起点、角度和长度。抽象值通常比实现的细节级别低，因为这有助于客户端只关注对他们重要的内容。例如，某些字符串表示的客户端只需要知道字符串是字符序列，而不需要知道该序列是用数组、链表、两者的组合还是完全不同的方式实现的。*序列*的概念比表示序列的特定方式更抽象。

### 数学抽象值

对于一些 ADT，抽象值由数学中常见且软件开发人员熟悉的概念和符号描述得很好。例如：

+   一个*整数集*

+   一个*字符序列*（即，一个字符串）

+   一对实数（或三元组，或一般的*元组*）

如果您正在指定这样一个类，那么您很幸运。您可以使用传统符号来指定类的抽象值和方法。这样的符号包括：

+   *集合推导式*：**{ x | P(x) }**表示满足属性*P*的所有元素*x*的集合。更一般地，**{ f(x) | P(x) }**表示对所有满足属性*P*的*x*的表达式*f(x)*的值的集合。例如，**{ x * x | x > 10 }**表示所有平方根大于 10 的数字的集合。

+   *集合并*：**x ∪ y**表示两个集合*x*和*y*的并集。（当不会与加法混淆时，也可以写成**x + y**。）

+   *集合成员*：**a ∈ x**或**a in x**测试*a*是否是集合*x*的元素。

+   *序列构造*：**[a, b, c]**表示三个元素的序列。

+   *序列连接*：**x : y**表示两个序列*x*和*y*的连接。（当不会与加法或并集混淆时，也可以写成**x + y**。）

+   *序列索引*：**x[i]**表示序列*x*的第*i*个元素。

+   *集合或序列大小*：**|x|**表示集合或序列*x*中的元素数量。

+   *元组构造*：**<a, b, c>**是三个元素的元组。这也可以写成**(a, b, c)**。与序列不同，元组是固定长度的，所以我们通常不考虑将它们连接起来。

您并不一定要使用这种语法。其中一些比其他更标准：集合推导语法在几乎所有数学中都是标准的，但序列连接并没有特别标准化。您可能会发现将序列连接写为像**concat(x, y)**这样的函数更清晰。真正重要的是清晰和没有歧义，所以如果您对读者是否能理解您有任何疑问，只需定义它：“...其中**concat(x,y)**是两个序列**x**和**y**的连接。”

### 规范字段

通常，抽象值不仅仅是简单的数值或集合等数学对象。在这些情况下，将抽象值视为具有字段的对象更有用。例如，一条线有一个*起点*和一个*终点*；一个邮寄地址有一个*号码*、*街道*、*城市*和*邮政编码*；一个 URL 有一个*协议*、*主机名*和*资源名*。

从数学上讲，这与一个*元组*是相同的；它只是一个元组，其部分对于人类来说具有有用的名称，而不仅仅是没有名称的某种顺序的部分。因此，即使我们可以使用元组，将抽象状态分解为具有命名部分的部分，其中每个部分都是*规范字段*，这样做更方便，更可读。（规范字段通常被称为*抽象字段*，因为它们是抽象值的字段，而不是*表示值*的字段。不幸的是，在 Java 中，*抽象*有另一个含义，因此我们将避免那种可能令人困惑的术语。）

规范字段通常（但并非总是）对应于抽象数据类型上的观察者或获取器。由于抽象值的结构对于您的类的客户端是感兴趣的，规范字段应该在类概述中列出。在 CSE 331 中，我们有一个 Javadoc 约定来描述它们：`@specfield *name* : *type* // *description*`。这里有一个例子：

```
/**
 * Represents an appointment for a meeting.
 * @specfield date : Date         // The time
 * @specfield room : integer      // The room number of the meeting's location
 * @specfield with : Set<Person>  // Whom the appointment is with
 */
 class Meeting {

```

按照惯例，在规范字段中，像*序列*或*集合*这样的小写类型指的是数学实体。大写类型指的是其他 ADT（类或接口）。在有选择的情况下，最好将数学实体作为规范字段的类型；例如，最好使用序列而不是 List。这样更加优雅，减少了规范与特定 Java 类型之间的耦合。

规范字段的存在并不意味着类的接口或实现方面的任何事情。虽然规范字段通常对应于观察者方法，但并不总是如此。（观察者方法是指计算值而不执行任何副作用的方法。所有的 getter 方法都是观察者，但并非所有的观察者都是 getter。）接口可能不提供任何查询规范字段状态的观察者，因此类的客户端可能无法访问存储在规范字段中的信息。（一个示例是栈实现可能有一个用于存储栈元素的规范字段，但客户端可能只能推入和弹出而无法获取栈的完整状态。）同样，实现可能实际上没有规范字段类型的具体字段：该信息可以从多个具体字段计算出，或者根本无法获取。重点是规范字段有助于以提供的抽象的术语给出方法规范。

### 衍生字段

衍生字段是可以从规范字段中推导出的信息，给出一个名称是有用的。例如，考虑这个类：

```
/**
 * Represents a square.
 * @specfield length : int // The length of the square's sides
 * @derivedfield area : int // area = length²\. The area of the square
 *
 * Abstract Invariant:
 *  length > 0
 */
class Square {...}

```

衍生字段`area`可以通过对`length`规范字段进行平方来得到。衍生字段的文档应说明它是如何从规范字段衍生出来的。

衍生字段的目的是帮助编写方法规范、抽象函数和表示不变式：写和理解`area`比写和理解`length²`更容易。它们是一种简写，可以使类和方法的规范更容易理解。因为衍生字段完全是根据规范字段（或其他衍生字段）定义的，方法规范不需要说明方法对衍生字段的影响。例如：

```
/**
 * Represents a square.
 * @specfield length : int // The length of the square's sides
 * @derivedfield area : int // area = length²\. The area of the square
 *
 * Abstract Invariant:
 *  length > 0
 */
class Square {

  /** The length of the square's sides. */
  int size;

  // Abstraction Function:
  //  AF(r) = a square, s, with s.length = r.size.
  //
  // Representation Invariant:
  //  size > 0

  /** Creates a new Square with length = len.
   * @requires len > 0
   * @effects a new Square s with s.length = len
   */
  public Square(int len) {
    if (len <= 0) throw new IllegalArgumentException(len + " < 0");
    this.size = len;
  }

  /** Returns the difference in area between this and s.
   * @return this.area - s.area
   */
  public int differenceInArea(Square s) {
    return (this.size*this.size) - (s.size*s.size);
  }

  /** Sets this.length to len.
   * @requires len > 0
   * @effects sets this.length to len
   */
   public void setLength(int len) {
     if (len <= 0) throw new IllegalArgumentException(len + " < 0");
     size = len;
   }
}

```

注意`differenceInArea`方法规范如何使用衍生字段`area`，以便更容易解释它返回的内容。

永远不需要方法规范指示它对衍生规范字段的影响，因为类文档已根据规范字段定义了衍生规范字段。由于`area`是一个衍生字段，构造函数不需要说明新构造的`Square`的`area`是多少。同样，`setLength`的方法规范不需要说明它对`area`的影响。

当我们使用抽象函数将具体实现与抽象值相关联时，我们只需要根据规范字段描述抽象，然后衍生字段将根据规范字段而来。

请注意，可以将`area`作为规范字段而不是派生字段。这将使程序员免除记录如何从规范字段派生`area`的责任。但是，在这种情况下，构造函数和`setLength`将需要指定它们对`area`的影响。

假设你有一个派生规范字段`f`。在实现中可以有一个具体字段存储`f`的值，或者有一个计算`f`值的方法，或者没有这样的字段或方法。这是一个对规范的客户端无关的实现细节。

## 方法规范

方法规范描述了方法的行为，涉及其前提条件和后置条件。请注意，方法规范只能引用规范字段、方法参数和全局变量（也称为公共静态字段），而不能引用实现的具体字段。

### 前提条件

前提条件是方法调用时必须为真的属性。调用者有责任保证这些属性成立。如果前提条件不成立，方法可以以任何方式行为，包括崩溃程序、继续以不正确的结果进行、通知用户问题或从问题中优雅地恢复。调用者应始终假定方法不会检查前提条件。但是，对于一个实现来说，检查其前提条件（如果检查可以高效地执行）并在不满足时抛出异常是一个好的做法，尽管不是必需的。

前提条件在方法规范中由“**requires**”子句指示。如果方法规范中省略了“requires”子句，则假定该方法没有任何前提条件。

**requires**（默认：无约束）

方法调用者必须满足的前提条件

### 后置条件

后置条件是方法保证在方法退出时将成立的属性。但是，如果前提条件在方法调用时不成立，则其他任何事情都不相关，方法可以以任何方式行为。特别是，如果前提条件在方法进入时不成立，则后置条件在方法退出时不需要成立。

后置条件可以写成一个复杂的逻辑公式，但将其分解为逻辑上不同的部分更为方便。CSE 331 使用“return”、“effects”、“throws”和“modifies”。（在下面的描述中，“default”表示如果该子句在方法规范中被省略，则假定什么。）

**return**（默认：对返回内容没有约束）

方法返回的值（如果有）

**throws**（默认：无，这意味着从不抛出异常）

可能引发的异常及其条件。规范不应对前提条件不满足时的行为做出保证。

**修改**（默认：无，表示没有副作用）

可能由过程修改的值的变量：除非在影响子句中另有说明，否则不能保证会被修改。如果对象`x`具有规范字段`f`、`g`和`h`，那么“`修改 x`”表示`x.f`、`x.g`和`x.h`的任何组合可能被修改。“`修改 x.g, x.h`”将更为严格。通常，程序员更感兴趣的是未在修改子句中列出的数量，因为这些数量保证不会被方法更改。

**影响**（默认：true，表示对修改列表中列出的引用可能产生“任何影响”）

方法的副作用，例如更改当前对象的状态、参数或全局变量中保存的对象：如果规范字段在修改子句中列出但不在影响子句中，则它可以取得此类对象的抽象不变式允许的任何值。修改和影响之间的区别在于修改列出可能发生变化的所有内容，而影响指示发生了什么变化。

### 使用规范字段进行规范

规范字段对于编写 ADT 操作的规范非常有用。以下是`Line`类方法的规范：

```
/**
 * @requires l.start-point is equal to this.end-point && l != null
 * @return a line segment that is equal to this + l; that is, l appended to this
 */
public Line add(Line l) {...}

```

规范可以引用规范字段（例如`start-point`和`end-point`），但不能引用表示字段。表示字段取决于特定的实现，因此我们不希望在规范中公开它们，因为可以以许多不同的方式实现规范。

### 使用派生规范字段进行规范

当您为操作编写规范时，可能会发现使用*派生*规范字段很有用。派生规范字段只是可以用其他规范字段来表示的规范字段。换句话说，它是一种简写。您可以在方法规范中自由使用派生规范字段（并且简化这些规范是派生规范字段的目的）：

```
/**
 * @return true is this.length > l.length
 */
public boolean longer(Line l) {...}

```

## 子类和重写方法

子类通常具有比其超类更强的规范，并且通常具有比其超类更大的抽象状态。当规范和抽象状态与父类相同（例如，抽象类的实现）时，就不需要在子类中重复它们。但是，包含一段简短的说明，指示应该使用超类文档会很有帮助。该说明有助于读者区分规范是否相同，或者作者只是没有记录该类。

当规格不同时，你有两个选择。第一个选择是在子类中重复完整的父类文档。优点是所有内容都在一个地方，这可能提高理解。第二个选择是增补现有规格 -- 例如，在一些新的规格字段和对它们的约束。无论你选择哪种方式，一定要清楚地指明你的方法。

对于覆盖另一个方法的方法，相似的规则适用。如果规格相同，将 Javadoc 留空是可以接受的。（生成的 HTML 将使用被覆盖方法的 Javadoc 文档，但对于阅读源代码的人来说，一个正常的 Java 注释是一个很好的提示。）否则，通常最好提供完整的规格。如果仅增补被覆盖方法的规格，请确保在文档中引用它。
