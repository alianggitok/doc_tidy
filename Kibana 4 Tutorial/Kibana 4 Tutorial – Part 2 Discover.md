#Kibana 4 Tutorial – Part 2: Discover
#Kibana 4 指南 —— 第二章：Discover

*——Anna Roes* in *2015-2-7*

这一章将讲解 discover 页面的使用。我们假定你已经完成了上一章节的相关步骤。

*Discover* 主显示区以表格的形式将文档中，你所指定索引的所有数据呈现出来（在你使用 Kibana 4 vagrant machine 时没有看到任何东西？接看下去）。

[![](https://www.timroes.de/wp-content/uploads/2015/02/discover-unfiltered-300x169.png)](https://www.timroes.de/wp-content/uploads/2015/02/discover-unfiltered.png)

##修改索引
要修改索引得看数据表单，你可以点击靠近窗体右侧的齿轮图标来修改。如果使用的是样本数据，这里只有 twitter 索引，所以这里你不能修改任何东西。

##选择时间
对于所有的基于时间的数据（就像我们的 twitter 数据），你可以选择时间范围（time span）来做分析，它就在当前视图靠近窗体的右上角。有多种你感兴趣的方式来得到档案：用 *Quick* 选卡来快速选择一个像 *today*、*Last 1 hour* 之类的时间范围，或者利用 *relative* 和 *absolute* 选卡来指定你要关注时间范围。

**注意**：如果你用样本数据，在默认情况下有可能看不到任何东西。这是因为样本数据是在2015年2月7日12点前收集的。你得选择一个有数据的时间范围。

在选择了含有数据的时间段后，你将会在视图上部看到一个依时间分布的时间柱状图。你可以通过在图标上做范围选择来放大特定的时间范围，也可以通过点击浏览器的回退按钮再次缩小时间范围（是的，要是 Kibana 3 的用户，就傻掉了）。

你选择的时间将会应用到其他你访问的视图上（dashboards、visualize等等）并且所有的视图都有在页面右侧让你去改变这个时间的可能。

你同样有可能在这里去设置一个刷新频率。这将允许你对 dashboard 做自动刷新，比如每分钟（刷新一次）。这在你用 Kibana 来监视底层数据时可能是很有用的。

##字段
在页面左侧，你有一个孙在于档案中的字段列表（不同的数据类型对应着不同的图标）。如果你将鼠标移到一个字段上，就可能通过点击 *add* 按钮将该字段的一个包含内容的列添加到表格里。一旦你添加第一个字段，在列表中的整个档案的输出就会消失。无论你有没有添加字段到表格列，你都可以通过点击脱字符号来展开一行。如果不想在表格中列出字段内容你还可以在左侧字段列表上方的 *Selected Fields* 中移除字段。

下面这张截图显示了只让“用户名”、“账户名”及用户的 tweeted 显示在表格中的 discover 页：

[![](https://www.timroes.de/wp-content/uploads/2015/02/discover-columns-300x169.png)](https://www.timroes.de/wp-content/uploads/2015/02/discover-columns.png)

如果你的数据有大量字段，你还可以使用左侧 *Fields* 列表标题上的齿轮小图标来过滤字段（比如是否已被分析、是否已被索引、他们的类型或者只搜索字段名）。

##保存和读取
如果要存储你的字段列表（还有我们马上就要写的查询语句），你可以点按上面搜索框边上 *Save Search* 图标并指定一个名字。

你可以在任何时候点击 *Load Saved Search* 图标来调取任何已保存的搜索。如果你有大量的已保存的搜索，过滤框可以帮你进行查找。

要重新建一个新视图，可以点按 *New Search* 按钮。不要忘记用之前提到的保存按钮随时保存你的视图，否则它们是不会被 Kibana 留存下来的。因为当你在不同的选卡间（dashboard、discover等）来回切换时，这点很容易被忘记，而当重新回来时，Kibana 只会自动展示你最后选定字段的表格。

**Save、load、new 按钮在 *Dashboards*、*visualizations* 里有着相同的功能和注意事项**

##为档案做过滤
你可以在左侧字段列表中点击任意字段来展开它，该字段的常见值就会显示出来。用 - 和 + 图标来快速的添加一个过滤器，+ 图标用来显示含有那个值的档案，- 图表则用来排除含有那个值的档案。

如果你用那种方式添加过滤器，会在上面搜索条下显示有一个条目。每一个过滤器都会以标签的形式显示，你可以临时禁用或者完全的移除它们。

过滤器还可以通过展开右侧表格中的行的内容，点击过滤器按钮来操作。注意档案中可能包含无法用来做过滤的非索引字段，在这些字段上你无法找到任何过滤按钮。

##搜索档案
为在列表中显示出来的档案做搜索和过滤，你可以使用页面顶部的大搜索框。这个搜索框接受特定语法的查询字符。

如果你想在任一字段里搜索内容，只需要输入想要搜索的内容。在搜索框里输入 *traffic* 并敲击回车键就会为你显示出包含 *traffic* 词语的 tweets。再起个案例，添加字段 *lang* 到表格列中。如果你在搜索框里输入词语 *en* 那么显示出的表格里，*lang* 字段内容中一定有 *en*，但是同时在 text 字段中许多西班牙文的 tweets 也含有这个单词。如果你输入像这样的词语，Kibana 将搜索所有字段，而不只是在当前表格显示的列里做搜索。

[![](https://www.timroes.de/wp-content/uploads/2015/02/discover-search-en-300x169.png)](https://www.timroes.de/wp-content/uploads/2015/02/discover-search-en.png)

搜索语言同样允许如下一些更细粒度的搜索：

<table>
	<tbody>
		<tr>
			<th>lang:en</th>
			<td>to just search inside a field named “lang”</td>
		</tr>
		<tr>
			<th>lang:e?</th>
			<td>wildcard expressions</td>
		</tr>
		<tr>
			<th>lang:(en OR es)</th>
			<td>OR queries on fields</td>
		</tr>
		<tr>
			<th>user.listed_count:[0 TO 10]</th>
			<td>range search on numeric fields</td>
		</tr>
		<tr>
			<th>lang:/e[ns]/</th>
			<td>regular expression search (very slow, only do this if really necessary!)</td>
		</tr>
	</tbody>
</table>

完整的搜索语言文档可以在 [elasticsearch 文档](http://www.elasticsearch.org/guide/en/elasticsearch/reference/current/query-dsl-query-string-query.html#query-string-syntax)里找到。

就如选中的字段一样，如果你保存搜索，输入的查询语句也会被保留下来。

##下一步是？
你现在能够以一个表格的形式看到你的数据并对其做搜索和过滤。这在查询具体的档案和它们的内容时是很常用的。而 Kibana 真正强大的部分会在接下来的章节（[Visualize](https://www.timroes.de/2015/02/07/kibana-4-tutorial-part-3-visualize/)）里呈现，我们将展示如何为那些数据创建可视化图表。
