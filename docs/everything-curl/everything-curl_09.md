# 构建和安装

# 构建和安装

该项目的源代码以一种允许在几乎任何操作系统和平台上编译和构建的方式编写，尽可能少地限制和要求。

如果您有32位（或更大）的CPU架构，如果您有一个符合C89标准的编译器，并且您大致有一个支持POSIX套接字API的系统，那么您很可能可以为您的目标系统构建curl和libcurl。

对于最流行的平台，curl项目已经准备好并准备好了构建系统，以允许您轻松地自行构建。

也有友好的个人和组织会打包curl和libcurl的二进制包，并提供下载。下面将探讨不同的选项。

## 最新版本？

查看curl网站[https://curl.haxx.se](https://curl.haxx.se)，您可以看到该项目发布的最新curl和libcurl版本。那是您可以获取的最新源代码包。

当您选择预先构建和打包版本以供您选择的操作系统或分发版本时，您可能不会总是找到最新版本，但您可能必须要么满足于某人为您的环境打包的最新版本，要么需要自己从源代码构建。

curl项目还在此URL提供了关于最新版本的稍微更加机器可读的信息：`https://curl.haxx.se/info`。

## 从git上获取！

当然，当从源代码构建时，您也可以选择构建最新的版本，该版本存在于[git存储库](https://github.com/curl/curl)中。但这可能会更加脆弱，并且可能需要更多的注意细节。

# 安装预编译的二进制文件

## 安装预编译的二进制文件

有许多友好的个人和组织会打包curl和libcurl的二进制包，并提供下载。

许多操作系统提供了一个“软件包存储库”，其中包含了可供您安装的软件包。您还可以从[curl下载页面](https://curl.haxx.se/download.html)跟随链接到流行操作系统的纯二进制包。

## 从您的软件包存储库安装

curl和libcurl已经存在很长时间了，大多数Linux发行版、BSD版本和其他*nix版本都有包存储库，允许您安装curl包。

最常见的描述如下。

### apt

`apt`是在Debian Linux和Ubuntu Linux发行版及其派生版本上安装预编译软件包的工具。

要安装curl命令行工具，通常只需执行

```
apt install curl 
```

…然后确保安装了依赖项，通常还会单独安装libcurl作为一个单独的包。

如果您想要针对libcurl构建应用程序，则需要安装一个开发包以获取包含头文件和一些额外文档等内容。然后您可以选择您喜欢的带有TLS后端的libcurl：

```
apt install libcurl4-openssl-dev 
```

或者

```
apt install libcurl4-nss-dev 
```

或者

```
apt install libcurl4-gnutls-dev 
```

### yum

对于 Redhat Linux 和 CentOS Linux 的衍生系统，你可以使用 `yum` 来安装软件包。使用以下命令来安装命令行工具：

```
yum install curl 
```

你可以使用以下命令来安装 libcurl 开发包（包括头文件和一些文档等）：

```
yum install curl-devel 
```

(Redhat 系列的 Linux 系统通常使用 NSS 作为 TLS 后端来构建 curl。)

### nix

[Nix](https://nixos.org/nix/) 是 NixOS 发行版默认的包管理器，但它也可以在任何 Linux 发行版上使用。

为了安装命令行工具：

```
nix-env -i curl 
```

### homebrew

[Homebrew](https://brew.sh/) 是一个 OSX 的软件包管理器。它不是默认安装的，但是可以很容易地安装。

要安装命令行工具：

```
brew install curl 
```

### cygwin

待定

## Windows 的二进制包

待定

# 从源代码构建

# 从源代码构建

curl 项目创建的源代码可以构建出两个产品 curl 和 libcurl。从源代码转换为二进制文件通常被称为 "构建"。你需要从源代码构建 curl 和 libcurl。

curl 项目根本不提供任何已构建的二进制文件，它只提供源代码。可以在 curl 网站的下载页面找到的二进制文件以及从互联网上其他地方安装的二进制文件都是由其他友好的人和组织构建并提供给世界的。

源代码包含大量包含 C 代码的文件。一般来说，相同的文件集用于构建 curl 支持的所有平台和计算机架构的二进制文件。curl 可以在大量不同的平台上构建和运行。如果你自己使用的是一种罕见的操作系统，那么从源代码构建 curl 可能是获得 curl 的最简单或者唯一的方法。

使 curl 易于构建是 curl 项目的首要任务，尽管我们并不总是成功！

## git vs 压缩包

当创建发布的压缩包时，会生成一些文件并将它们包含在最终的发布文件中。这些生成的文件在 git 存储库中不存在，因为它们是生成的，不需要将它们存储在 git 中。

所以，如果你想要从 git 构建 curl，你需要在构建之前自己生成一些文件。在 Linux 和 Unix 系统上，通过运行 `./buildconf` 来执行这个操作，而在 Windows 上，你需要运行 `buildconf.bat`。

## 在 Linux 和类 Unix 系统上

在 Linux 和其他类 Unix 系统上，构建 curl 有两种明显不同的方式。一种是使用 configure 脚本，另一种是使用 CMake 方法。

有两种不同的构建环境来满足人们不同的意见和喜好。基于 configure 的构建可能是更成熟、更完整的构建系统，并且可能被认为是默认的构建系统。

### Autotools

"Autotools" 是一组不同的工具，它们一起用来生成 `configure` 脚本。用户想要构建 curl 时会运行 configure 脚本，它会做很多事情：

+   它会检查你系统中是否存在的功能和函数

+   它提供了命令行选项，因此作为构建者，您可以决定在构建中启用和禁用什么。功能和协议等可以切换打开/关闭。甚至可以切换编译器警告级别等。

+   它提供了命令行选项，让构建者指向各种第三方依赖项的特定安装路径，以便curl可以构建以使用它们。

+   指定生成的安装应该放置在哪个文件路径上，当最终进行构建并调用“make install”时

在最基本的用法中，只需在源代码目录中运行`./configure`即可。当脚本完成时，它会输出一个摘要，列出它检测到/启用的选项以及仍然禁用的功能，其中一些可能是因为它未能检测到必要的第三方依赖项的存在而禁用的，这些依赖项是这些功能正常工作所必需的。

然后你调用`make`来构建整个项目，使用`make install`来安装curl、libcurl及其相关组件。`make install`需要你在系统中拥有正确的权限来创建和写入安装目录中的文件，否则会出现一些错误。

### 交叉编译

交叉编译意味着您在一个架构上构建源代码，但输出是为在不同架构上运行而创建的。例如，您可以在Linux机器上构建源代码，但输出却能在Windows机器上运行。

要使交叉编译生效，您需要为您要构建的特定目标系统设置专用的编译器和构建系统。如何获取和安装该系统不在本书的范围之内。

一旦你有了交叉编译器，你可以指示configure在构建curl时使用该编译器，而不是使用“本地”编译器，这样最终结果就可以移植并在其他机器上使用。

### CMake

待定

### 静态链接

待定

## 在Windows上

待定

### make

待定

### CMake

待定

### 其他编译器

待定

## 在其他系统上

待定

## 将curl移植到不受支持的系统

待定

## 选择TLS后端

基于configure的构建允许用户在构建时从各种不同的TLS库中进行选择。您可以通过使用正确的命令行选项来选择它们。

默认的OpenSSL配置检查也将检测并使用BoringSSL或libressl。

+   GnuTLS：`--without-ssl --with-gnutls`。

+   Cyassl：`--without-ssl --with-cyassl`

+   NSS：`--without-ssl --with-nss`

+   PolarSSL：`--without-ssl --with-polarssl`

+   mbedTLS：`--without-ssl --with-mbedtls`

+   axTLS：`--without-ssl --with-axtls`

+   schannel：`--without-ssl --with-winssl`

+   安全传输：`--with-winssl --with-darwinssl`

# 依赖项

# 依赖项

制作优秀软件的关键是在其他优秀软件的基础上构建。通过使用许多其他人使用的库，我们减少了重复造轮子的次数，我们得到的软件更可靠，因为有更多的人使用相同的代码。

curl提供的许多功能都需要构建以使用一个或多个外部库。然后它们是curl的依赖项。它们都不是*必需*的，但大多数用户都希望至少使用其中一些。

## **zlib**

[http://zlib.net/](http://zlib.net/)

如果使用zlib构建，curl可以自动解压通过HTTP传输的数据。通过传输压缩数据，可以使用更少的带宽。

## **c-ares**

[https://c-ares.haxx.se/](https://c-ares.haxx.se/)

curl可以使用c-ares构建以执行异步名称解析。启用异步名称解析的另一种方法是使用线程化名称解析后端构建curl，然后为每个名称解析创建一个单独的辅助线程。 c-ares在同一个线程中完成所有操作。

## **libssh2**

[https://libssh2.org/](https://libssh2.org/)

当curl使用libssh2构建时，它会启用对SCP和SFTP协议的支持。

## **nghttp2**

[https://nghttp2.org/](https://nghttp2.org/)

这是一个用于处理HTTP/2帧的库，是curl支持HTTP版本2所必需的先决条件。

## **openldap**

[https://www.openldap.org/](https://www.openldap.org/)

这个库是一个选项，允许curl支持LDAP和LDAPS URL方案。在Windows上，您还可以选择构建curl以使用winssl库。

## **librtmp**

[https://rtmpdump.mplayerhq.hu/](https://rtmpdump.mplayerhq.hu/)

要使curl支持RTMP URL方案，您必须使用来自RTMPDump项目的librtmp库构建curl。

## **libmetalink**

[https://launchpad.net/libmetalink](https://launchpad.net/libmetalink)

使用libmetalink构建curl以支持[metalink](http://www.metalinker.org/)格式，该格式允许curl从多个位置下载相同的文件。它包括校验和等内容。请参阅curl的[--metalink](https://curl.haxx.se/docs/manpage.html#--metalink)选项。

## **libpsl**

[https://rockdaboot.github.io/libpsl/](https://rockdaboot.github.io/libpsl/)

当您构建支持libpsl的curl时，cookie解析器将了解公共后缀列表，从而适当地处理此类cookie。

## **libidn2**

[https://www.gnu.org/software/libidn/libidn2/manual/libidn2.html](https://www.gnu.org/software/libidn/libidn2/manual/libidn2.html)

curl借助libidn2库处理国际化域名（IDN）。

## TLS库

有许多不同的TLS库可供选择，因此它们在[单独的部分](building-tls.html)中进行了介绍。

# TLS库

# 构建以使用TLS库

要使curl支持基于TLS的协议（如HTTPS，FTPS，SMTPS，POP3S，IMAPS等），您需要使用第三方TLS库构建，因为curl本身不实现TLS协议。

curl被设计用于与大量TLS库一起工作：

+   **BoringSSL**

+   GSkit（仅限OS/400）

+   **GnuTLS**

+   **NSS**

+   **OpenSSL**

+   Secure Transport（本地macOS）

+   **WolfSSL**

+   **axTLS**

+   **libressl**

+   **mbedTLS**

+   Schannel（本地Windows）

当您构建curl和libcurl以使用这些库之一时，重要的是您在构建机器上安装了库及其包含头文件。

## 配置

下面，您将学习如何告诉configure使用不同的库。请注意，对于除OpenSSL及其同类外的所有库，您必须通过使用`--without-ssl`来*禁用*对OpenSSL的检查。

### OpenSSL，BoringSSL，libressl

```
./configure 
```

默认情况下，configure将在默认路径中检测到OpenSSL。您可以选择将configure指向自定义安装路径前缀，以便它找到openssl：

```
./configure --with-ssl=/home/user/installed/openssl 
```

备选项[BoringSSL](building-boringssl.html)和libressl看起来相似，因此configure将以与OpenSSL相同的方式检测它们，但它将使用一些额外的措施来确定它使用的特定风格。

### GnuTLS

```
./configure --with-gnutls --without-ssl 
```

默认情况下，configure将在默认路径中检测到GnuTLS。您可以选择将configure指向自定义安装路径前缀，以便它找到gnutls：

```
./configure --with-gnutls=/home/user/installed/gnutls --without-ssl 
```

### NSS

```
./configure --with-nss --without-ssl 
```

默认情况下，configure将在默认路径中检测到NSS。您可以选择将configure指向自定义安装路径前缀，以便它找到nss：

```
./configure --with-nss=/home/user/installed/nss --without-ssl 
```

### WolfSSL

```
./configure --with-cyassl --without-ssl 
```

（cyassl是该库的以前名称）默认情况下，configure将在默认路径中检测到WolfSSL。您可以选择将configure指向自定义安装路径前缀，以便它找到WolfSSL：

```
./configure --with-cyassl=/home/user/installed/nss --without-ssl 
```

### axTLS

```
./configure --with-axtls --without-ssl 
```

默认情况下，configure将在默认路径中检测到axTLS。您可以选择将configure指向自定义安装路径前缀，以便它找到axTLS：

```
./configure --with-axtls=/home/user/installed/axtls --without-ssl 
```

### mbedTLS

```
./configure --with-mbedtls --without-ssl 
```

默认情况下，configure将在默认路径中检测到mbedTLS。您可以选择将configure指向自定义安装路径前缀，以便它找到mbedTLS：

```
./configure --with-mbedtls=/home/user/installed/mbedtls --without-ssl 
```

### Secure Transport

```
./configure --with-darwinssl --without-ssl 
```

（DarwinSSL是Secure Transport的另一个名称）默认情况下，configure将在默认路径中检测到Secure Transport。您可以选择将configure指向自定义安装路径前缀，以便它找到DarwinSSL：

```
./configure --with-darwinssl=/home/user/installed/darwinssl --without-ssl 
```

### Schannel

```
./configure --with-winssl --without-ssl 
```

（WinSSL是Schannel的另一个名称）默认情况下，configure将在默认路径中检测到Schannel。您可以选择将configure指向自定义安装路径前缀，以便它找到WinSSL：

```
./configure --with-winssl=/home/user/installed/winssl --without-ssl 
```

# BoringSSL

# 使用boringssl构建curl

## 构建boringssl

$HOME/src是我在这个示例中放置代码的地方。您可以选择任何地方。

```
$ cd $HOME/src
$ git clone https://boringssl.googlesource.com/boringssl
$ cd boringssl
$ mkdir build
$ cd build
$ cmake ..
$ make 
```

## 设置构建树以被curl的configure检测到

在boringssl源代码树根目录下，请确保存在`lib`和`include`目录。`lib`目录应包含两个库（我将它们设置为了构建目录中的符号链接）。`include`目录已经默认存在。像这样创建和填充`lib`（命令在源代码树根目录中执行，而不是在`build/`子目录中）。

```
$ mkdir lib
$ cd lib
$ ln -s ../build/ssl/libssl.a
$ ln -s ../build/crypoto/libcrypto.a 
```

## 配置curl

`LIBS=-lpthread ./configure --with-ssl=$HOME/src/boringssl`（其中我指出了boringssl树的根目录）

验证配置结束时，是否显示检测到将使用BoringSSL。

## 构建curl

在curl源代码树中运行`make`。

现在，您可以像平常一样使用`make install`等命令来安装curl。
