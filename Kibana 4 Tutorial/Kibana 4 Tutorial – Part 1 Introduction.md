#Kibana 4 指南 —— 第一章：介绍

*——Anna Roes* in *2015-2-7*

原文链接：[Kibana 4 Tutorial – Part 1: Introduction](https://www.timroes.de/2015/02/07/kibana-4-tutorial-part-1-introduction/)

这份指南是针对的 Kibana 4.0.1 的。

Kibana 4 是 Kibana 新出的版本， 一个依托 elasticsearch 集群分析数据的网页前端界面，相比 Kibana 3 有着许多的变化。这份指南专注于讲解如何用 Kibana 4 分析你的数据。指南面向需要升级版本的 Kibana 3 用户，及从未用过 Kibana 而想要知道如何使用它的人。

这份指南不会涉及 elasticsearch（脱离Kibana） 的使用，也不会告诉你如何配置所需软件。这是一份纯粹的 Kibana 指南。

在结束指南时，你的 Kibana 4 Dashboard 看起来可能是这样的：

[![](https://www.timroes.de/wp-content/uploads/2015/02/final-dashboard-300x169.png)](https://www.timroes.de/wp-content/uploads/2015/02/final-dashboard.png)


##配置一个测试环境
如果你有运行一个 elasticsearch 并且会用到它，那么只需要再下载最新版的 [Kibana 4](http://www.elasticsearch.org/blog/kibana-4-literally/) 并安装。如果你没有运行 elasticsearch 或者不需要去用它，我们提供了一个 [kibana 4 Vagrant VM](https://github.com/timroes/kibana4-vagrant)。你可以下载它并依托样本的数据来配置你自己的 Kibana 4 实例，不会花费过多的精力。链接到 GitHub 的页面里看下使用与配置介绍吧。如果有关于 Kibana 4 vagrant machine 的问题，请提交到 GitHub 上。

###简单数据

如果你使用 Kibana 4 vagrant machine，将会得到一个样本数据，我们要使用它来贯穿整个指南。它含有两个索引（数据集）：

- **twitter**：包含一个公开的 tweets 集（~15.000），搜集于大约在2015年2月5日12：00到12：05（UTC+1）这段时间内。这是一些由事件驱动的数据，我们会在这份指南里使用它。注意这些数据：它来自实时流，意味着每条信息在录入的时候都已经发表了（was tweeted）。这也是为什么其中没有回复数或收藏总数的原因。

- **bank**：包含一个账户数据样本的列表（截取自 [elasticsearch docs](http://www.elasticsearch.org/guide/en/elasticsearch/reference/current/_exploring_your_data.html)）。这份数据不是基于事件的，意味着其中的文档或录入信息在“发生”时没有时间戳的约束。我们不会拿他来贯穿整个指南，但是你可以用它来玩玩或者做一些不需要基于事件的数据测试。

##设置你的索引（es）

如果你是第一次配置 Kibana 将被要求配置一个索引模式（index pattern）。首先要选择你是想处理像 *twitter* 这样的基于时间的事件（time-based events）数据样本还是一些在每个文档里包含时间戳的其他数据集，或者你需要用像 *bank* 数据样本这样的“静态”数据来工作。

Elasticsearch 里，在用多索引帮助搜索及允许内存优化的情况下，存储基于时间的事件（数据）是很普遍的。每天一个索引，你也就得到一个像 *twitter-2015.01.15，twitter-2015.01.26* 等等的索引命名模式。如果你像这样存储数据那么就要勾选“Use event times to create index names”项。在这个示例中，你可以用如下方式指定索引模式：*[twitter-]YYYY.MM.DD*。并且选择 hourly、daily、weekly、monthly或yerly 索引。

为了这份指南，我们需要配置包含基于时间的 twitter 事件索引，但是不要使用索引分割。所以我们勾选第一个复选框，第二个不要选，并且在 *Index name or pattern* 框内输入索引名字 twitter。当 Kibana 通过那个名字侦测到一个索引就会出现一个下拉选框，我们要在其中指定时间戳字段（事件的时间）。在这个例子里 twitter 索引的时间字段被命名为 *created_at* 并且在点击 *Create* 按钮前你的屏幕看起来应该像下面的截图那样。

[![](https://www.timroes.de/wp-content/uploads/2015/02/index-pattern-300x169.png)](https://www.timroes.de/wp-content/uploads/2015/02/index-pattern.png)

在建立索引模式后，索引视图将为你呈现一个存在于文档中的所有字段的列表并进一步显示它们的类型、是否被索引、及内容是否被进行了分析的进一步的信息。

##Kibana上的页面
在页面的顶部，Kibana 展示了一个主导航，分别链接到4个主页面：*Discover*、*Visualize*、*Dashboard* 和 *Settings*。接着我们给这些部分做简短的用途定义。它们会在指南相应的章节里做更详细的描述。我们推荐根据链接顺序地读读这些有深度章节，因为它们是互相关联的。

###Discover
这个页面将所有选定时间范围内的档案显示在一个表格中。它相当于在 Kibana 3 dashboard 下面的表格视图。如果你索引没有包含基于时间的数据，它将只会列出所有数据。

在 [Discover](https://www.timroes.de/2015/02/07/kibana-4-tutorial-part-2-discover/) 指南中阅读更多。

###Visualize
在 Kibana 4 里，可视化的东西（visualization）可以是一个图表、一张地图、一份表格或者其他数据的特殊形态。在这个页面中可以建立或者修改你的可视化视图。大部分 Kibana 中的“生产”动作发生在这里。

在 [Visualize](https://www.timroes.de/2015/02/07/kibana-4-tutorial-part-3-visualize/) 指南中阅读更多。

###Dashboard
多个可视化图表（visualizations）可被放置在一个 dashboard 中。这里的 dashboard 和 Kibana 3 的相似，不同的是可视化图表不再链接到一个特殊的 dashboard，并且一个 dashboard 不会受限于一个索引，它可以如愿的包含多个索引的多个可视化图表。更多地让 Kibana 的“消费者”（最终用户）专注在那些你所创建的漂亮的可视化图表上。

在 [Dashboard](https://www.timroes.de/2015/02/07/kibana-4-tutorial-part-4-dashboard/) 指南中阅读更多。

###Settings
这个设置页面就像它名字描述的那样能做许多事情。在这里你能改变你的配置，比如从你的 Kibana 实例中添加或删除索引之类的事。关于这一部分我们还没有编写指南，但是或许可以找到其他一些指南（来做补充）。

##接下来做什么？
你之前在 Kibana 界面中添加了 twitter 索引，所以勇往直前，到 [Discover](https://www.timroes.de/2015/02/07/kibana-4-tutorial-part-2-discover/) 指南里开始使用你的数据吧。
