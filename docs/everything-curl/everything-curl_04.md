# 源代码

# 源代码

当然，源代码是这个项目的实际引擎部分。毕竟，这是一个软件项目。

curl 和 libcurl 是用 C 语言编写的。

## 托管和下载

你始终可以在 [官方 curl 网站](https://curl.haxx.se/) 找到最新的 curl 和 libcurl 发布的源代码。从那里你也可以找到托管副本的替代镜像，还提供了校验和数字签名，以帮助你验证当你下载这些文件时，它们是否与 curl 团队最初上传到你本地系统的内容一样。

如果你更愿意直接使用我们的源代码仓库中的 curl 源代码，你可以在 [curl 的 github 仓库](https://github.com/curl/curl/) 中找到所有细节。

## 克隆代码

```
git clone https://github.com/curl/curl.git 
```

这将在你本地系统的一个目录中下载并解压最新的 curl 代码。

# 代码布局

## 代码布局

curl 源代码树既不大也不复杂。记住的一个关键点也许是 libcurl 是库，而该库是 curl 命令行工具的最大组成部分。

### 根目录

我们尽量保持源树根目录中文件的数量最少。如果你检查一个发布存档，你会看到与存储在 git 仓库中的内容略有不同，因为几个文件是由发布脚本生成的。

一些较为显著的包括：

+   `buildconf`: 用于从 git 仓库中的源代码构建 curl 时构建 configure 和更多内容。

+   `buildconf.bat`: buildconf 的 Windows 版本。在从 git 检出完整源代码后运行此命令。

+   `CHANGES`: 在发布时生成并放入发布存档中。它包含源代码仓库中最新的 1000 个更改。

+   `configure`: 在类 Unix 系统上生成的脚本，在构建 curl 时用于生成设置。

+   `COPYING`: 描述你使用代码的规则的许可证。

+   `GIT-INFO`: 仅在 git 中存在，包含有关从 git 检出代码后如何构建 curl 的信息。

+   `maketgz`: 用于生成发布存档和每日快照的脚本

+   `README`: curl 和 libcurl 的简短摘要。

+   `RELEASE-NOTES`: 包含最新发布的更改；当在 git 中找到时，它包含自上一次发布以来即将在即将发布的版本中结束的更改。

### lib

这个目录包含 libcurl 的完整源代码。它是所有平台的相同源代码——超过一百个 C 源文件和几个更多的私有头文件。构建应用程序时使用的头文件不存储在此目录中；请参阅 include/curl。

根据你的构建中启用了哪些功能以及你的平台提供了哪些功能，一些源文件或源文件的部分可能包含在你特定构建中未使用的代码。

### lib/vtls

在 libcurl 中的 VTLS 子部分是所有 TLS 后端的家园，libcurl 可以构建以支持。"虚拟" TLS 内部 API 是 libcurl 中使用的一个常见 API，用于访问 TLS 和加密函数，而不需要主代码确切地知道使用的是哪个 TLS 库。这允许构建 libcurl 的人从各种各样的 TLS 库中进行选择以构建。

我们还在网站上维护了一个[SSL 比较表](https://curl.haxx.se/docs/ssl-compared.html)以帮助用户。

+   OpenSSL：（目前为止）最流行的 TLS 库。

+   BoringSSL：由 Google 维护的 OpenSSL 分支。它会使 libcurl 由于库中缺少某些功能而禁用一些功能。

+   LibreSSL：由 OpenBSD 团队维护的 OpenSSL 分支。

+   NSS：一款完整的 TLS 库，可能最为人所知的是被 Firefox 网页浏览器使用。这是 Fedora 和 Redhat 系统上 curl 的默认 TLS 后端。

+   GnuTLS：默认由 Debian 打包的 curl 使用的一款完整的 TLS 库。

+   mbedTLS：（以前称为 PolarSSL）是一个更专注于嵌入式市场的 TLS 库。

+   [WolfSSL](https://wiki.example.org/wolfssl)：（前身为 cyaSSL）是一个更专注于嵌入式市场的 TLS 库。

+   axTLS：一个专注于需要小的占用空间的微小的 TLS 库。

+   SChannel：Windows 上的本地 TLS 库。

+   SecureTransport：Mac OS X 上的本地 TLS 库。

+   GSKit：OS/400 上的本地 TLS 库。

### src

此目录保存 curl 命令行工具的源代码。它是在运行该工具的所有平台上相同的源代码。

命令行工具所做的大部分工作都是将给定的命令行选项转换为相应的 libcurl 选项或选项集，然后确保正确地将它们发出以根据用户的愿望驱动网络传输。

此代码使用 libcurl 就像任何其他应用程序一样。

### include/curl

这里是为使用 libcurl 的应用程序提供的公共头文件。其中一些是在配置或发布时生成的，因此它们在 git 存储库中看起来与在发布存档中看起来不同。

使用现代 libcurl，应用程序在其 C 源代码中所需包含的只有 `#include <curl/curl.h>`

### 文档

主要的文档位置。此目录中的文本文件通常是纯文本文件。我们已经开始逐渐转向 Markdown 格式，因此一些（但希望数量逐渐增加的）文件使用 .md 扩展名表示。

这些文件中的大多数也会在 curl 网站上自动转换为友好的 Web 格式/外观。

+   `BINDINGS`：列出所有已知的 libcurl 语言绑定及其位置

+   `BUGS`：如何报告错误以及在哪里报告

+   `CODE_OF_CONDUCT.md`：我们期望人们在这个项目中的行为方式

+   `CONTRIBUTE`：在贡献到项目时要考虑的事项

+   `curl.1`：curl 命令行工具的 man 手册，以 nroff 格式

+   `curl-config.1`：curl-config man 手册，以 nroff 格式

+   `FAQ`：关于各种与 curl 相关的主题的常见问题

+   `FEATURES`: curl 功能的不完整列表

+   `HISTORY`: 描述项目如何开始并随着年份的推移而发展

+   `HTTP2.md`: 如何使用 curl 和 libcurl 进行 HTTP/2

+   `HTTP-COOKIES`: curl 如何支持和处理 HTTP cookies

+   `index.html`: 作为文档索引页面的基本 HTML 页面

+   `INSTALL`: 如何从源代码构建和安装 curl 和 libcurl

+   `INSTALL.cmake`: 如何使用 CMake 构建 curl 和 libcurl

+   `INSTALL.devcpp`: 如何使用 devcpp 构建 curl 和 libcurl

+   `INTERNALS`: curl 和 libcurl 内部结构的详细信息

+   `KNOWN_BUGS`: 已知的错误和问题

+   `LICENSE-MIXING`: 描述如何结合不同的第三方模块及其各自的许可证

+   `MAIL-ETIQUETTE`: 这是如何在我们的邮件列表上进行沟通的方式

+   `MANUAL`: 一个类似教程的指南，介绍如何使用 curl

+   `mk-ca-bundle.1`: mk-ca-bundle 工具的 man 页面，采用 nroff 格式

+   `README.cmake`: CMake 特定细节

+   `README.netware`: Netware 特定细节

+   `README.win32`: win32 特定细节

+   `RELEASE-PROCEDURE`: 如何发布 curl 和 libcurl

+   `RESOURCES`: 进一步阅读关于 curl 的内容的资源

+   `ROADMAP.md`: 我们未来想要开展的工作

+   `SECURITY`: 我们如何处理安全漏洞

+   `SSLCERTS`: TLS 证书处理文档

+   `SSL-PROBLEMS`: 常见 SSL 问题及其原因

+   `THANKS`: 感谢这一大量友好人士的名单，curl 今天存在！

+   `TheArtOfHttpScripting`: 使用 curl 进行 HTTP 脚本编写的教程

+   `TODO`: 我们或您可以着手实施的事项

+   `VERSIONS`: libcurl 版本编号的工作原理

### 文档/libsurl

所有 libcurl 函数都有自己的 man 页面，以独立的带有.3 扩展名的文件形式存在，采用 nroff 格式，位于此目录中。还有一些其他文件如下所述。

+   `ABI`

+   `index.html`

+   `libcurl.3`

+   `libcurl-easy.3`

+   `libcurl-errors.3`

+   `libcurl.m4`

+   `libcurl-multi.3`

+   `libcurl-share.3`

+   `libcurl-thread.3`

+   `libcurl-tutorial.3`

+   `symbols-in-versions`

### 文档/libsurl/opts

此目录包含三种不同 libcurl 函数的各个选项的 man 页面。

`curl_easy_setopt()`选项以`CURLOPT_`开头，`curl_multi_setopt()`选项以`CURLMOPT_`开头，`curl_easy_getinfo()`选项以`CURLINFO_`开头。

### 文档/示例

包含约 100 个独立示例，旨在帮助读者了解如何使用 libcurl。

另请参阅本书的 libcurl 示例部分。

### 脚本

便捷脚本。

+   `contributors.sh`: 从给定的哈希/标签中提取 git 存储库中的所有贡献者。其目的是为 RELEASE-NOTES 文件生成列表，并允许手动添加的名称即使在更新时也保留在其中。该脚本使用'THANKS-filter`文件重写一些名称。

+   `contrithanks.sh`：从给定的哈希/标签中提取 git 存储库中的贡献者，过滤掉所有已在`THANKS`中提到的名称，然后将`THANKS`输出到 stdout，并将新贡献者的列表附加到末尾；它旨在让`THANKS`文档更容易更新。该脚本使用`THANKS-filter`文件重写某些名称。

+   `log2changes.pl`：为发布生成`CHANGES`文件，由发布脚本使用。它只是转换 git log 输出。

+   `zsh.pl`：辅助脚本，为 zsh shell 的用户提供 curl 命令行完成。

# 处理构建选项

## 处理不同的构建选项

curl 和 libcurl 源代码已经精心编写，可以在几乎所有现有的计算机平台上构建和运行。这只能通过辛勤工作和遵循一些准则（当然还有大量测试）来完成。

一个黄金法则是始终添加检查特定特性的#ifdef，然后在用户的计算机设置中编译程序之前，设置脚本（configure 或 CMake 或硬编码）检查是否存在这些特性。此外，由于代码编写方式的这种方式，一些特性甚至可以显式关闭，即使它们存在于系统中并且*可能*被使用。例如，当用户想要构建具有较小占用空间或禁用某些协议支持的库的版本时等。

该项目有时会在整个源文件周围使用#ifdef 保护，例如，当为特定操作系统提供单个文件或者也许是为一个不总是存在的特定特性提供文件时。这样做是为了使所有平台都能始终构建所有文件——这大大简化了构建脚本和 makefile。一个完全#ifdefed 的文件几乎不会增加任何构建时间。

我们提供函数和宏，使代码看起来和工作起来都是相同的，不论当前特性如何，而不是在代码中到处添加#ifdef。其中一些对于缺乏这些特性的构建来说是空宏。

TLS 处理和名称解析都是使用内部 API 处理的，该 API 隐藏了特定实现和第三方软件库的选择。这样，大部分内部工作都是相同的，不论 libcurl 被告知使用哪个 TLS 库或名称解析系统。

# 代码风格

## 风格和代码要求

具有共同风格的源代码比在不同位置使用不同风格的代码更容易阅读。它有助于使代码感觉像一个连续的代码库。易于阅读是代码的一个非常重要的属性，当新东西被添加时，它有助于使代码更容易审查，并且当开发人员试图弄清楚为什么事情出错时，它有助于调试代码。统一的风格比满足个人品味更重要。

我们的 C 代码有一些样式规则。其中大部分都由 lib/checksrc.pl 脚本验证和维护。可以通过 `make checksrc` 命令调用，甚至在使用 `./configure --enable-debug` 后构建时默认由构建系统调用。

对于任何人来说，遵循指南通常不是问题，因为您只需复制源代码中已使用的样式，并且在我们的规则集中没有特别异常的规则。

我们也努力编写在所有主要平台上都没有警告的代码，通常在尽可能多的平台上。显然会导致警告的代码不会被原样接受。

您不被允许违反的一些规则是：

### 缩进

我们仅使用空格进行缩进，永远不使用制表符。我们为每个新的开放花括号使用两个空格。

### 注释

由于我们编写的是 C89 代码，// 是不被允许的。它们直到 C99 标准才被引入。我们只使用 /* 和 */ 进行注释：

```
/* this is a comment */ 
```

### 长行

curl 中的源代码不得超过 80 列。即使在现代非常大且高分辨率的屏幕时代，仍有两个原因要保持这一点：

1.  较窄的列比非常宽的列更容易阅读。报纸几十年甚至几个世纪来都使用栏目有其原因。

1.  较窄的列允许开发人员更容易地在不同窗口中并排查看多个代码片段。我经常在同一个屏幕上有两三个源代码窗口，以及多个终端和调试窗口。

### 开放的花括号位于同一行

在 if/while/do/for 表达式中，我们将开放的花括号与关键字放在同一行，然后我们将闭合的花括号设置在与初始关键字相同缩进级别的位置。就像这样：

```
if(age < 40) {
  /* clearly a youngster */
} 
```

### else 在下一行

当使用花括号为条件表达式添加 `else` 子句时，我们将其添加在闭合花括号的后一行。就像这样：

```
if(age < 40) {
  /* clearly a youngster */
}
else {
  /* probably intelligent */
} 
```

### 括号前不加空格

当使用 if/while/do/for 写表达式时，关键字与开放括号之间不应有空格。就像这样：

```
while(1) {
  /* loop forever */
} 
```

# 贡献

## 贡献

贡献意味着帮助。

当您向项目贡献任何内容时——代码、文档、错误修复、建议或者只是良好的建议——我们假设您是在有许可的情况下这样做的，并且您提供给我们的内容不会违反任何合同或法律。如果您没有许可，请不要向我们贡献。

对于 curl 这样的项目，贡献可能是许多不同的事情。虽然源代码是构建产品所需的东西，但我们还依赖于良好的文档、测试（包括测试代码和测试基础设施）、网络内容、用户支持等。

将您的更改或建议发送给团队，通过共同努力，我们可以解决问题，改进功能，澄清文档，添加功能或使您提供帮助的任何其他事情落在正确的位置。我们将确保改进的代码和文档被正确合并到源树中，其他类型的贡献也会得到适当的接受。

将您的贡献发送到邮件列表，提交问题或提交拉取请求。

### 建议

想法容易，实现难。是的，我们确实赞赏好主意和建议该做什么以及如何做，但是如果您也自愿参与将想法转化为现实，那么想法实际变为真实功能的机会就会大大增加。

我们已经在`TODO`文档中收集了想法，我们通常了解流行网络协议的当前趋势，因此通常不需要提醒我们这些。

### 应添加的内容

向 curl 或 libcurl 添加任何内容的最佳方法当然是首先将想法和建议带给 curl 项目团队成员，然后与他们讨论该想法是否适合包含，以及如何最好地实现——并且以最佳方式将其合并到源代码存储库中，假设这是您想要的。

该项目通常批准改进对当前协议的支持的功能，特别是流行客户端或浏览器具有但 curl 仍然缺少的功能。

当然，您也可以向项目添加非代码内容，例如文档、图形或网站内容，但一般规则同样适用。

如果您正在修复您或其他人报告的问题，我们将非常高兴收到您的修复，并尽快将其合并！

### 无需添加的内容

没有任何好的规则来说明您不能添加哪些功能或我们永远不会接受的内容，但我想提一些您应该避免以减少摩擦并更快成功的事情：

+   不要先编写一个巨大的补丁，然后将其发送到列表进行讨论。请始终从列表上讨论开始，并尽早发送您的初始审查请求，以获取有关设计和方法的反馈。这样可以避免您浪费时间沿着最终可能需要重写的道路前进！

+   在代码中引入新事物时，您需要遵循已经存在的风格和架构。当您向普通的传输代码路径添加代码时，例如，它必须以非阻塞的方式异步工作。我们不会接受引入阻塞行为的新代码——我们已经有太多这样的代码了，而我们尚未设法删除其中的许多。

+   快速的小技巧或有可能无法在您不运行的平台上或您不了解的架构上运行的肮脏解决方案。我们不关心您是否赶时间或它是否对您有效。我们不接受高风险的代码或难以阅读或理解的代码。

+   打破构建的代码。当然，我们接受有时必须向某些区域添加代码，使新功能可能依赖于特定的第三方库或特定操作系统等，但我们绝不能以牺牲所有其他系统为代价。我们不会破坏构建，并确保所有测试都能成功运行。

## git

我们首选的源代码控制工具是[git](https://git-scm.com/)。

尽管 git 有时不是最容易学习和掌握的工具，但对于一个普通的开发者和贡献者所需了解的所有基本步骤都非常直接，学习起来也不需要太多时间或精力。

本书将不会帮助您学习 git。在当今这个时代，所有的软件开发人员都应该学会 git。

您可以在我们的 GitHub 页面上使用 Web 浏览器浏览 curl git 树：[`github.com/curl/curl`](https://github.com/curl/curl)。

要从 git 中检出 curl 源代码，您可以像这样克隆它：

```
git clone https://github.com/curl/curl.git 
```

### 拉取请求

一种非常流行和便捷的方式是通过在 GitHub 上进行所谓的拉取请求，对您自己的更改进行贡献并将它们带回项目中。

首先，您可以在 GitHub 网站上创建自己的源码树版本，称为 fork。这样，您就可以获得您自己的 curl git 树的版本，您可以将其克隆到本地副本。

您编辑自己的本地副本，提交更改，将它们推送到 GitHub 上的 git 仓库，然后在 GitHub 网站上，您可以选择基于您对原始 curl 仓库的本地仓库克隆所做的更改来创建一个拉取请求。

我们建议您在专门的单独分支中执行用于拉取请求的工作，而不是在主分支中执行，这样可以更轻松地更新拉取请求，例如在审查之后，或者如果您意识到这是一条死路并决定将其丢弃。

### 为邮件列表制作一个补丁

即使您选择不发起拉取请求，而更喜欢发送补丁到 curl-library 邮件列表的老式和可信赖的方法，也最好在本地 git 分支中工作并在那里提交您的更改。

分支使得在需要更改时轻松编辑和重新基础，并且使得在上游更新时轻松同步到主分支变得容易。

一旦您的提交足够好，可以发送到邮件列表，您只需使用 `git format-patch` 创建补丁并发送它们。更高级的用户甚至直接使用 `git send-email` 并让 git 自己发送电子邮件！

### git 提交风格

当您向 git 提交补丁时，您会为其提供一个描述所做更改的提交消息。我们在项目中有一定的风格，我们要求您使用：

```
[area]: [short line describing the main effect]

[separate the above single line from the rest with an empty line]

[full description, no wider than 72 columns that describes as much as
possible as to why this change is made, and possibly what things
it fixes and everything else that is related]

[Bug: link to source of the report or more related discussion]
[Reported-by: John Doe—credit the reporter]
[whatever-else-by: credit all helpers, finders, doers] 
```

不要忘记在您提交他人的工作时使用 `git commit --author="Jane Doe <jane@example.com>"`，并确保在提交之前在 git 中正确设置了您自己的用户和电子邮件！

作者和 *-by: 行，当然，是为了确保我们在项目中给予适当的认可。我们不希望在没有清楚标明来源的情况下使用他人的工作。正确给予认可是至关重要的！

### 谁来决定什么内容进入？

首先，对于并不明显的一点是，并非所有人都可以将提交合并到实际的官方 git 仓库中。让我们称他们为核心团队。

每个人都可以派生出自己的 curl 代码库，可以向其中提交和推送更改，并将其在线托管并构建自己的 curl 版本等等，但是要想将更改纳入*官方*代码库，必须由信任的人推送。

核心团队是一小部分 curl 开发人员，他们已经在这个项目中工作了几年，并且已经证明他们是熟练的开发人员，完全理解我们在这个项目中所做的价值观和开发风格。他们是 开发团队 部分中列出的一些人。

你可以随时将讨论带到邮件列表，并说明你认为你的更改应该被接受的动机，或者甚至反对其他正在被接受的更改等等。

丹尼尔仍然是项目负责人，虽然很少需要，但他在辩论中拥有最终决定权，这些辩论似乎无法偏向任何一方或未能达成某种共识。

# 漏洞报告

## 漏洞报告

所有已知的和公开的 curl 或 libcurl 相关的漏洞都列在 [curl 网站的安全页面](https://curl.haxx.se/docs/security.html) 上。

安全漏洞不应该输入到项目的公开错误跟踪器中，除非已经配置好了必要的配置，以限制只有报告者和项目的安全团队才能访问该问题。

### 漏洞处理

处理新安全漏洞的典型流程如下。

在此过程结束前，不应该公开任何有关漏洞的信息。这意味着，例如，不应该创建 bug 跟踪器条目来跟踪该问题，因为这会使问题公开，并且不应该在项目的任何公开邮件列表上讨论该问题。此外，如果在公开公告之前进行了提交，则与任何提交相关的消息都不应提及提交的安全性质。

+   发现问题的人，即报告者，私下向`curl-security@haxx.se`报告漏洞。这是一个邮件别名，可以联系到几个被选择和信任的人。

+   与 curl 或 libcurl 中未公开的安全漏洞的报告或管理无关的消息将被忽略，并且不需要进一步的操作。

+   安全团队的一名成员会发送电子邮件给原始报告者，以确认报告。

+   安全团队调查报告，要么拒绝，要么接受。

+   如果报告被拒绝，团队会写信给报告者解释原因。

+   如果报告被接受，团队会写信给报告者，让他/她知道报告被接受，并且他们正在解决问题。

+   安全团队讨论问题，制定修复方案，考虑问题的影响并建议发布时间表。这次讨论应尽可能涉及报告者。

+   信息发布应尽快进行，并且通常与包含修复的即将发布的版本同步。如果报告者或其他人认为下一个计划的发布时间太遥远，则应考虑出于安全原因考虑提前发布。

+   撰写有关问题的安全咨询草案，解释问题是什么，其影响，影响的版本，任何解决方案或解决方法以及修复发布的时间，确保适当地表彰所有贡献者。

+   从[distros@openwall](http://oss-security.openwall.org/wiki/mailing-lists/distros)请求 CVE 编号时，同时通知并准备他们即将公开的安全漏洞公告——附上咨询草案以供参考。请注意，“distros”不会接受长于 19 天的禁令。

+   使用 CVE 编号更新“安全咨询”。

+   安全团队在私有分支中提交修复。提交消息理想情况下应包含 CVE 编号。通常也会将此修复分发给“distros”邮件列表，以便他们在公开公告之前使用修复。

+   在下一个发布日，私有分支合并到主分支并推送。一旦推送，信息就对公众可见，实际发布应立即跟进。

+   项目团队创建包含修复的发布版本。

+   项目团队以与我们通常宣布发布的方式向全世界公布发布和漏洞信息——它会发送到 curl-announce、curl-library 和 curl-users 邮件列表。

+   网站上的安全页面应提及新的漏洞。

### curl-security@haxx.se

谁在这个名单上？您必须符合一些标准，然后我们可能会邀请您加入名单，或者您可以要求加入。这真的不是很正式。我们基本上只要求您在 curl 项目中有长期存在，并且您已经表现出对项目及其工作方式的理解。您必须已经在这里待了一段时间，而且您不应该计划在不久的将来消失。

我们不会公开列出参与者的名单，主要是因为随着时间的推移，名单往往会有所变化，而且某处的名单只会增加过时的风险。

# 网站

## 网站源代码

大部分 curl 网站也可以在公共 git 存储库中找到，尽管与源代码存储库分开，因为它通常对同一群人不感兴趣，我们可以维护一个不同的具有推送权限等人员名单。

网站 git 存储库可在此 URL 上找到：[`github.com/curl/curl-www`](https://github.com/curl/curl-www)，您可以像这样克隆网页代码的副本：

```
git clone https://github.com/curl/curl-www.git 
```

### 构建网站

这个网站是一个老式的定制设置，主要是从一组源文件构建静态 HTML 文件。这些源文件经过了一种基本上是增强版 C 预处理器（[fcpp](https://daniel.haxx.se/projects/fcpp/)）和一组 Perl 脚本的预处理。man 手册通过 [roffit](https://daniel.haxx.se/projects/roffit/) 转换为 HTML。确保 fcpp、perl、roffit、make 和 curl 都在你的 $PATH 中。

一旦你第一次克隆了 git 仓库，就调用一次 `sh bootstrap.sh` 来获取一个符号链接和一些初始的本地文件设置，然后你可以在源根目录中调用 `make` 来本地构建网站。

请注意，这并不意味着你成为了完整的网站镜像，因为一些脚本和文件只在实际的真实网站上可用，但应该足够让你在本地查看大多数 HTML 页面。