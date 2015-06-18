# 简介
<!-- toc -->


## 简介
本文档将对Apache Tomcat中的一些概念以及Tomcat容器内部一些术语进行简要的阐述和解释。系统管理员、开发人员等在需要帮助时欢迎随时翻阅。


## 术语
在阅读本文的过程中，您将会遇到一系列的术语。其中一部分是Tomcat所特有的，另一部分则是定义在[Servlet和JSP规范][1]中。
* __Context__ - 简而言之，一个Context就是一个Web应用
* __Term2__ - 就是这样
* __Term3__ - 就是这样！

```
PS： Term2和Term3是官方文档在卖萌...
```


## 文件及目录结构
许多文档中都会有多次提到__$CATALINA_HOME__，这个指的是Tomcat的安装跟路径。当文中说`您可以在$CATALINA_HOME/README.txt文件中找到相关信息`时，我们的指的就是Tomcat的安装跟路径下的README.txt文件。根据需要，我们还可以通过配置__$CATALINA_BASE__的方式来为Tomcat配置多个实例。如果仅是单实例的话，__$CATALINA_BASE__和__$CATALINA_HOME__的值是一样的。

以下是Tomcat中比较重要的一些路径：

* __/bin__ - 该路径下存放startup, shutdown等脚本。后缀为.sh的文件（针对Unix系统）和后缀为.bat的文件（针对Windows系统）在功能上其实是一致的。鉴于Win32的命令行缺少某些功能，所以针对Windows的脚本文件会稍多一些。
* __/conf__ - 该路径下存放配置文件和相关的DTD文件。该路径下最重要的文件是server.xml，它是容器的主要配置文件。
* __/logs__ - 默认情况下用于存放日志文件
* __/webapps__ - 存放您的Web应用。


## 配置Tomcat
这一章节主要是您熟悉在配置Tomcat容器时需要知道的基本信息。所有的配置文件都在容器启动时被加载，这也就意味着对配置文件的任何修改需要重启容器才能生效。


## 去哪儿寻求帮助

尽管我们已竭尽全力的把这些文档描述的尽量清楚并且容易理解，但可能还是会有疏漏。以下是一些可以寻求帮助的网站及邮件列表以备不时之需。

需要注意的是，其中所提到的问题及解决方案可能会因Tomcat的大版本不同而有所差异。当你在网络上查找资料时，有些文档可能与Tomcat 8并无关系，所描述的可能只是老版本中的一些问题。

* 最新文档 - 其中的大多数文档都会有些潜在的困扰点。确保您已完整阅读了相关的文档，这将会为您省去很多麻烦和时间。以免出现在网上逛了一大圈才发现答案其实早就摆在你眼前的窘境。
* [Tomcat FAQ][2]
* [Tomcat WIKI][3]
* [jGuru][4]的Tomcat FAQ
* Tomcat邮件列表归档 - 很多站点都对Tomcat的邮件列表进行了归档。鉴于很多链接都已过时，查阅遇阻可以对其搜索之。
* [订阅][5]Tomcat用户邮件列表。如果你在其中发起的问题没有人答复你，那么很有可能是因为你的问题在之前的交流中已经被回答过了或者是已经在其他的FAQ中有了解答。尽管网页开发方面的问题经常会有人问和解答，但在此最好还是只讨论雨Tomcat相关的问题。
* [订阅][6]Tomcat开发者邮件列表。在这个列表中，人们一般讨论Tomcat开发相关的问题。Tomcat配置亦或是开发及应用运行相关的问题最好还是在Tomcat用户邮件列表中讨论。

此外，如果您有什么需要在文档中阐述的内容想要让我们知道的话，欢迎在Tomcat开发者邮件列表中发言。


[1]:http://wiki.apache.org/tomcat/Specifications
[2]:http://wiki.apache.org/tomcat/FAQ
[3]:http://wiki.apache.org/tomcat/
[4]:http://www.jguru.com/faq/java-tools/tomcat
[5]:http://tomcat.apache.org/lists.html
[6]:http://tomcat.apache.org/lists.html
