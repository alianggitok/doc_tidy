#Kibana 4 指南 —— 第三章：Visualize

*——Anna Roes* in *2015-2-7*

原文链接：[Kibana 4 Tutorial – Part 3: Visualize](https://www.timroes.de/2015/02/07/kibana-4-tutorial-part-3-visualize/)

这部分是 Kibana 4 指南的第三章节。我们假设你已经至少完成了[第一章（介绍）](https://www.timroes.de/2015/02/07/kibana-4-tutorial-part-1-introduction/)所讲的步骤。

可视化图表（visualizations）是 Kibana 4 的心脏。它们通常以不同的形式来聚合与形象化你的数据。为了理解可视化图表，我们得先看下 elasticsearch 的聚合（elasticsearch aggregations），因为它们是基础。

如果你对 elasticsearch 的聚合已经熟门熟路，那么可以跳过接下来的段落。

##聚合（Aggregations）
我们数据的聚合并不是靠 Kibana 完成，而是放在 elasticsearch下进行的。我们可以区分出两种聚合：bucket 和 metric。为从 Kibana 4 获得一个可控的图表，理解这些聚合如何工作的会是个要点，所以不要对接下来的段落感到气馁。

###Bucket Aggregations
所有文档都被一个 bucket aggregation 放到数个 bucket 中，每个都包含一个已被索引的文档的子集。bucket 可以根据一个特定的字段的值、一个自定义过滤或者其他参数挑选出一个特定的文档。当前，Kibana 4 支持 7个 bucket aggregation，这会在接下来的段落里做说明。为说明每一个聚合，twitter 数据样本已经为每个聚合给出了对应的案例。稍后在这个指南里我们将看到一些完整的案例。

####Date Histogram（时间直方图）
直方图聚合要求一个日期类型字段和一个时间间隔。 It will then put all the documents into one bucket, whose value of the specified date field lies within the same interval.

*举例来说*：你可以用 created_at 字段创建一个每分钟刷新一次的所有留言的时间直方图。在这个例子中，将会是每分钟一个 bucket 并且每个 bucket 都会保留下那一分钟里写下的留言。

除了像 minutes、hourly、daily 等常用的时间间隔值，还有个特别的值 *auto*。当你选择这个时间间隔时，实际的时间会由 Kibana 依据你对这图表绘制规模的大小来给出，所以一个适当数量的 bucket 会被创建（不至于因太多而弄脏图表，也不会因太少而让图表变得没有价值）。

####Histogram（直方图）
一个和 Date Histogram 相似的直方图，除了你能在每个数字字段里都用它

####Range

####Terms

####Filters

####Significant Terms

####Geohash

###Metric Aggregations
在你数据上运行一个 bucket 聚合之后，你会得到其文档上的数个 bucket。现在指定一个 metric 聚合来为每个 bucket 计算一个值。Metric 聚合将会运行于每个 bucekt 及每个 bucket 的一个值上。

在 visualizations 上，bucket 聚合通常会得出图表的“初级维度”（比如在饼图里每个 bucket 就是一个扇形；在柱状图里每个 bucket 会得到一个“柱”）。由 metric 聚合计算出的值就会作为“二级维度”来显示（比如在整个饼图里会有个百分比数；在柱状图的纵轴上有“柱”的实际高度）。

由于 metric 聚合通常是有意义的，当他们运行在 bucket 上时，metric 聚合的案例将会像个样本一样总是包含一个 bucket 聚合。但你还得在其他 bucket 聚合上用 metric 聚合……一个 bucket 挨着一个 bucket。

####计数（Count）

####平均值、求和（Average/Sum）



