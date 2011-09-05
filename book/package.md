---
layout: book
title: 软件包管理 
---
Package Management

If we spend any time in the Linux community, we hear many opinions as to which of the
many Linux distributions is &quot;best.&quot; Often, these discussions get really silly, focusing on
such things as the prettiness of the desktop background (some people won't use Ubuntu
because its default color scheme is brown!) and other trivial matters.

如果我们花些时间在Linux社区里，就会听到许多意见，在众多Linux发行版中哪个是最好的。 通常，
这些讨论真是很愚蠢，集中于这些事情上，比方说最漂亮的桌面背景（一些人不会使用Ubuntu，因为它
默认的主题颜色是棕色！）和其它琐碎的东西。

The most important determinant of distribution quality is the packaging system and the
vitality of the distribution's support community. As we spend more time with Linux, we
see that its software landscape is extremely dynamic. Things are constantly changing.
Most of the top-tier Linux distributions release new versions every six months and many
individual program updates every day. To keep up with this blizzard of software, we
need good tools for package management.

Linux发行版本质量最重要的决定因素是软件包管理系统和其支持社区的持久性。随着我们
花更多的时间在Linux上，我们会发现它的软件园地是非常动态的。软件不断变化。大多数一线
Linux发行版每隔六个月发布一个新版本，并且许多独立的程序每天都会更新。为了能和这些
如暴风雪一般多的软件保持联系，我们需要一些好工具来进行软件包管理。

Package management is a method of installing and maintaining software on the system.
Today, most people can satisfy all of their software needs by installing packages from
their Linux distributor. This contrasts with the early days of Linux, when one had to
download and compile source code in order to install software. Not that there is anything
wrong with compiling source code; in fact, having access to source code is the great
wonder of Linux. It gives us (and everybody else) the ability to examine and improve the
system. It's just that having a pre-compiled package is faster and easier to deal with.
In this chapter, we will look at some of the command line tools used for package
management. While all of the major distributions provide powerful and sophisticated
graphical programs for maintaining the system, it is important to learn about the
command line programs, too. They can perform many tasks that are difficult (or
impossible) to do with their graphical counterparts.

软件包管理是指系统中一种安装和维护软件的方法。今天，通过从Linux发行版中安装的软件包，
已能满足许多人所有需要的软件。这不同于早期的Linux，人们需要下载和编辑源码来安装软件。
编辑源码没有任何问题，事实上，拥有对源码的访问权限是Linux的伟大奇迹。它赋予我们（
其它每个人）才干来检测和提高系统性能。只是若有一个预先编译好的软件包处理起来要相对
容易快速些。这章中，我们将查看一些用于包管理的命令行工具。虽然所有主流Linux发行版都
提供了强大且精致的图形管理程序来维护系统，但是学习命令行程序也非常重要。因为它们
可以完成许多让图形化管理程序处理起来困难（或者不可能）的任务。

Packaging Systems

### 打包系统

Different distributions use different packaging systems and as a general rule, a package
intended for one distribution is not compatible with another distribution. Most
distributions fall into one of two camps of packaging technologies: the Debian “.deb”
camp and the Red Hat “.rpm” camp. There are some important exceptions such as
Gentoo, Slackware, and Foresight, but most others use one of these two basic systems.

不同的Linux发行版使用不同的打包系统，一般而言，大多数发行版分别属于两大包管理技术阵营：
Debian的&quot;.deb&quot;，和红帽的&quot;.rpm&quot;。也有一些重要的例外，比方说Gentoo，
Slackware，和Foresight，但大多数会使用这两个基本系统中的一个。

<p>
<table class="multi" cellpadding="10" border="1" width="%100">
<caption class="cap">Table 15-1: Major Packaging System Families</caption>
<tr>
<th class="title">Packaging System </th>
<th class="title">Distributions (Partial Listing)</th>
</tr>
<tr>
<td valign="top" width="25%">Debian Style (.deb) </td>
<td valign="top">Debian, Ubuntu, Xandros, Linspire</td>
</tr>
<tr>
<td valign="top">Red Hat Style (.rpm) </td>
<td valign="top">Fedora, CentOS, Red Hat Enterprise Linux, OpenSUSE,
Mandriva, PCLinuxOS</td>
</tr>
</table>
</p>

How A Package System Works

### 软件包管理系统是怎样工作的

The method of software distribution found in the proprietary software industry usually
entails buying a piece of installation media such as an &quot;install disk&quot; and then running an
&quot;installation wizard&quot; to install a new application on the system.

在专有软件产业中找到的软件发布方法通常需要买一张安装媒介，比方说&quot;安装盘&quot;，然后运行
&quot;安装向导&quot;，来在系统中安装新的应用程序。

Linux doesn't work that way. Virtually all software for a Linux system will be found on
the Internet. Most of it will be provided by the distribution vendor in the form of
package files and the rest will be available in source code form that can be installed
manually. We'll talk a little about how to install software by compiling source code in a
later chapter.

Linux不是这样。Linux系统中几乎所有的软件都可以在互联网上找到。其中大多数软件由发行商以
包文件的形式提供，剩下的则以源码形式存在，可以手动安装。在后面章节里，我们将会谈谈怎样
通过编译源码来安装软件。

Package Files

### 包文件

The basic unit of software in a packaging system is the package file. A package file is a
compressed collection of files that comprise the software package. A package may
consist of numerous programs and data files that support the programs. In addition to the
files to be installed, the package file also includes metadata about the package, such as a
text description of the package and its contents. Additionally, many packages contain
pre- and post-installation scripts that perform configuration tasks before and after the
package installation.

在包管理系统中软件的基本单元是包文件。包文件是一个构成软件包的文件压缩集合。一个软件包
可能由大量程序以及支持这些程序的数据文件组成。除了安装文件之外，软件包文件也包括
关于这个包的元数据，如软件包及其内容的文本说明。另外，许多软件包还包括预安装和安装后脚本，
这些脚本用来在软件安装之前和之后执行配置任务。

Package files are created by a person known as a package maintainer, often (but not
always) an employee of the distribution vendor. The package maintainer gets the
software in source code form from the upstream provider (the author of the program),
compiles it, and creates the package metadata and any necessary installation scripts.
Often, the package maintainer will apply modifications to the original source code to
improve the program's integration with the other parts of the Linux distribution.

软件包文件是由软件包维护者创建的，他通常是（但不总是）一名软件发行商的雇员。软件维护者
从上游提供商（程序作者）那里得到软件源码，然后编辑源码，创建软件包元数据以及所需要的
安装脚本。通常，软件包维护者要把所做的修改应用到最初的源码当中，来提高此软件与Linux
发行版其它部分的融合性。

Repositories

### 资源库

While some software projects choose to perform their own packaging and distribution,
most packages today are created by the distribution vendors and interested third parties.
Packages are made available to the users of a distribution in central repositories that may
contain many thousands of packages, each specially built and maintained for the
distribution.

虽然某些软件项目选择执行他们自己的打包和发布策略，但是现在大多数软件包是由发行商和感兴趣
的第三方创建的。系统发行版的用户可以在一个中心资源库中得到这些软件包，这个资源库可能
包含了成千上万个软件包，每一个软件包都是专门为这个系统发行版建立和维护的。

A distribution may maintain several different repositories for different stages of the
software development life cycle. For example, there will usually be a “testing”
repository that contains packages that have just been built and are intended for use by
brave souls who are looking for bugs before they are released for general distribution. A
distribution will often have a “development” repository where work-in-progress packages
destined for inclusion in the distribution's next major release are kept.

因软件开发生命周期不同阶段的需要，一个系统发行版可能维护着几个不同的资源库。例如，通常会
有一个&quot;测试&quot;资源库，其中包含刚刚建立的软件包，它们想要勇敢的用户来使用，
在这些软件包正式发布之前，让用户查找错误。系统发行版经常会有一个&quot;开发&quot;资源库，
这个资源库中保存着注定要包含到下一个主要版本中的半成品软件包。

A distribution may also have related third-party repositories. These are often needed to
supply software that, for legal reasons such as patents or DRM anti-circumvention issues,
cannot be included with the distribution. Perhaps the best known case is that of
encrypted DVD support, which is not legal in the United States. The third-party
repositories operate in countries where software patents and anti-circumvention laws do
not apply. These repositories are usually wholly independent of the distribution they
support and to use them, one must know about them and manually include them in the
configuration files for the package management system.

一个系统发行版可能也会拥有相关第三方的资源库。这些资源库需要支持一些因法律原因，
比如说专利或者是DRM反规避问题，而不能被包含到发行版中的软件。可能最著名的案例就是
那个加密的DVD支持，在美国这是不合法的。第三方资源库在这些软件专利和反规避法案不
生效的国家中起作用。这些资源库通常完全地独立于它们所支持的资源库，要想使用它们，
你必须了解它们，手动地把它们包含到软件包管理系统的配置文件中。

Dependencies

### 依赖性

Programs seldom “standalone;” rather they rely on the presence of other software
components to get their work done. Common activities, such as input/output for
example, are handled by routines shared by many programs. These routines are stored in
what are called shared libraries, which provide essential services to more than one
program. If a package requires a shared resource such as a shared library, it is said to
have a dependency. Modern package management systems all provide some method of
dependency resolution to ensure that when a package is installed, all of its dependencies
are installed, too.

程序很少是&quot;孤立的&quot;，而是依赖于其它软件组件来完成它们的工作。常见活动，以
输入/输出为例，就是由共享程序例程来处理的。这些程序例程存储在共享库中，共享库不只
为一个程序提供基本服务。如果一个软件包需要共享资源，比如说共享库，据说就有一个依赖。
现代的软件包管理系统都提供了一些依赖项解析方法，以此来确保当安装软件包时，也安装了
其所有的依赖程序。

High And Low-level Package Tools

### 上层和底层软件包工具

Package management systems usually consist of two types of tools: low-level tools which
handle tasks such as installing and removing package files, and high-level tools that
perform metadata searching and dependency resolution. In this chapter, we will look at
the tools supplied with Debian-style systems (such as Ubuntu and many others) and those
used by recent Red Hat products. While all Red Hat-style distributions rely on the same
low-level program (rpm), they use different high-level tools. For our discussion, we will
cover the high-level program yum, used by Fedora, Red Hat Enterprise Linux, and
CentOS. Other Red Hat-style distributions provide high-level tools with comparable
features.

软件包管理系统通常由两种工具类型组成：底层工具用来处理这些任务，比方说安装和删除软件包文件，
和上层工具，完成元数据搜索和依赖解析。在这一章中，我们将看一下由Debian风格的系统
（比如说Ubuntu，还有许多其它系统）提供的工具，还有那些由Red
Hat产品使用的工具。虽然所有基于Red Hat风格的发行版都依赖于相同的底层程序（rpm）,
但是它们却使用不同的上层工具。我们将研究上层程序yum供我们讨论，Fedora, Red
Hat企业版，和CentOs都是使用yum。其它基于Red Hat风格的发行版提供了带有可比较特性的上层工具。

<p>
<table class="multi" cellpadding="10" border="1" width="%100">
<caption class="cap">Table15- 2: Packaging System Tools</caption>
<tr>
<th class="title">Distributions 
</th>
<th class="title">Low-Level Tools 
</th>
<th class="title">High-Level Tools
</th>
</tr>
<tr>
<td valign="top">Debian-Style 
</td>
<td valign="top">dpkg</td>
<td valign="top">apt-get, aptitude</td>
</tr>
<tr>
<td valign="top">Fedora, Red Hat
Enterprise Linux, CentOS
</td>
<td valign="top">rpm</td>
<td valign="top">yum</td>
</tr>
</table>
</p>

Common Package Management Tasks

### 常见软件包管理任务

There are many operations that can be performed with the command line package
management tools. We will look at the most common. Be aware that the low-level tools
also support creation of package files, an activity outside the scope of this book.
In the discussion below, the term &quot;package_name&quot; refers to the actual name of a
package rather than the term “package_file,” which is the name of the file that
contains the package.

通过命令行软件包管理工具可以完成许多操作。我们将会看一下最常用的工具。注意底层工具也
支持软件包文件的创建，这个话题超出了本书叙述的范围。在以下的讨论中，&quot;package\_name&quot;
这个术语是指软件包实际名称，而不是指&quot;package_file&quot;，它是包含在软件包中的文件名。

Finding A Package In A Repository

### 查找资源库中的软件包

Using the high-level tools to search repository metadata, a package can be located based
on its name or description.

使用上层工具来搜索资源库元数据，可以根据软件包的名字和说明来定位它。

<p>
<table class="multi" cellpadding="10" border="1" width="%100">
<caption class="cap">Table 15-3: Package Search Commands</caption>
<tr>
<th class="title">Style</th>
<th class="title">Command(s)</th>
</tr>
<tr>
<td valign="top">Debian</td>
<td valign="top"><p>apt-get update</p>
apt-cache search search_string</td>
</tr>
<tr>
<td valign="top">Red Hat</td>
<td valign="top">yum search search_string</td>
</tr>
</table>
</p>

Example: To search a yum repository for the emacs text editor, this command could be
used:

例如：搜索一个yum资源库来查找emacs文本编辑器，使用以下命令：

<div class="code"><pre>
<tt>yum search emacs</tt>
</pre></div>

