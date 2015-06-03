#Kibana 4 指南 —— 第三章：Visualize

*——Anna Roes* in *2015-2-7*

原文链接：[Kibana 4 Tutorial – Part 3: Visualize](https://www.timroes.de/2015/02/07/kibana-4-tutorial-part-3-visualize/)

这部分是 Kibana 4 指南的第三章节。我们假设你已经至少完成了[第一章（介绍）](https://www.timroes.de/2015/02/07/kibana-4-tutorial-part-1-introduction/)所讲的步骤。

可视化图表（visualizations）是 Kibana 4 的心脏。它们通常以不同的形式来聚合与形象化你的数据。为了理解可视化图表，我们得先看下 elasticsearch 的聚合（elasticsearch aggregations），因为它们是基础。

如果你对 elasticsearch 的聚合已经熟门熟路，那么可以跳过接下来的段落。

##聚合（Aggregations）
我们数据的聚合并不是靠 Kibana 完成，而是放在 elasticsearch下进行的。我们可以区分出两种聚合：bucket 和 metric。为从 Kibana 4 获得一个可控的图表，理解这些聚合如何工作的会是个要点，所以不要对接下来的段落感到气馁。

###Bucket aggregations
所有文档都被一个 bucket aggregation 放到数个 bucket 中，每个都包含一个已被索引的文档的子集。bucket 可以根据一个特定的字段的值、一个自定义过滤或者其他参数挑选出一个特定的文档。当前，Kibana 4 支持 7个 bucket aggregation，这会在接下来的段落里做说明。为说明每一个聚合，twitter 数据样本已经为每个聚合给出了对应的案例。稍后在这个指南里我们将看到一些完整的案例。

####Date Histogram（直方图）
直方图聚合要求一个日期类型字段和一个时间间隔。


