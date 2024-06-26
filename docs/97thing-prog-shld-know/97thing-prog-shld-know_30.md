# 不要重复自己

# 不要重复自己

在所有编程原则中，不要重复自己（DRY）可能是最基本的之一。这一原则由安迪·亨特和戴夫·托马斯在《实用程序员》中提出，并贯穿许多其他著名的软件开发最佳实践和设计模式。学会识别重复，并通过适当的实践和适当的抽象消除它的开发人员，可以比那些不断在应用程序中引入不必要重复的人产生更干净的代码。

## 重复是浪费

每行代码进入应用程序都必须维护，并且是未来错误的潜在来源。重复无谓地膨胀了代码库，导致更多的错误机会，并给系统增加了意外的复杂性。重复添加到系统中的膨胀也使得与系统一起工作的开发人员更难完全理解整个系统，或者确保在一个位置进行的更改不需要在复制他们正在处理的逻辑的其他位置也进行。DRY 要求“系统中的每一条知识必须有一个单一、明确、权威的表示”。

## 过程中的重复需要自动化

软件开发中许多过程是重复的，容易自动化。DRY 原则在这些情境中同样适用，也适用于应用程序的源代码。手动测试是缓慢、容易出错且难以重复的，因此应尽可能使用自动化测试套件。如果可能的话，应该经常运行构建过程，最好是每次检入都运行一次。无论何处存在痛苦的手动过程可以自动化，都应该自动化和标准化。目标是确保只有一种完成任务的方式，并且尽可能无痛。

## 逻辑中的重复需要抽象

逻辑中的重复可以采取许多形式。复制粘贴的 if-then 或 switch-case 逻辑是最容易检测和纠正的。许多设计模式的显式目标是减少或消除应用程序中逻辑的重复。如果一个对象通常需要在使用之前发生几件事情，这可以通过抽象工厂或工厂方法来实现。如果一个对象在行为上有许多可能的变化，这些行为可以使用策略模式注入，而不是使用大量的 if-then 结构。事实上，设计模式的制定本身就是为了减少解决常见问题所需的重复努力，并讨论这些解决方案。此外，DRY 也可以应用于结构，如数据库模式，导致规范化。

## 原则问题

其他软件原则也与 DRY 有关。Once and Only Once 原则，仅适用于代码的功能行为，可以被视为 DRY 的一个子集。开闭原则指出“软件实体应该对扩展开放，但对修改关闭”，只有在遵循 DRY 原则时才能实际运作。同样，众所周知的单一责任原则要求一个类只有“一个变化的理由”，依赖于 DRY。

当遵循结构、逻辑、过程和功能方面的原则时，DRY 原则为软件开发人员提供了基本指导，并有助于创建更简单、更易维护、更高质量的应用程序。虽然有些情况下重复可能是必要的，以满足性能或其他要求（例如，在数据库中进行数据去规范化），但应仅在直接解决实际问题而非想象问题的情况下使用。

作者：[史蒂夫·史密斯](http://programmer.97things.oreilly.com/wiki/index.php/Steve_Smith)
