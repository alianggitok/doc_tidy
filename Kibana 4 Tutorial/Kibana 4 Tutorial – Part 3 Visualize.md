#Kibana 4 指南 —— 第三章：Visualize

*——Anna Roes* in *2015-2-7*

原文链接：[Kibana 4 Tutorial – Part 3: Visualize](https://www.timroes.de/2015/02/07/kibana-4-tutorial-part-3-visualize/)

这部分是 Kibana 4 指南的第三章节。我们假设你已经至少完成了[第一章（介绍）](https://www.timroes.de/2015/02/07/kibana-4-tutorial-part-1-introduction/)所讲的步骤。

可视化图表（visualizations）是 Kibana 4 的心脏。它们通常以不同的形式来聚合与形象化你的数据。为了理解可视化图表，我们得先看下 elasticsearch 的聚合（elasticsearch aggregations），因为它们是基础。

如果你对 elasticsearch 的聚合已经熟门熟路，那么可以跳过接下来的段落。

##聚合（Aggregations）
我们数据的聚合并不是靠 Kibana 完成，而是放在 elasticsearch下进行的。我们可以区分出两种聚合：bucket 和 metric。为从 Kibana 4 获得一个可控的图表，理解这些聚合如何工作的会是个要点，所以不要对接下来的段落感到气馁。

###Bucket aggregations
由所有文档都被一个 bucket aggregation 放到数个 bucket 中，每个都包含一个已被索引的文档的子集。

