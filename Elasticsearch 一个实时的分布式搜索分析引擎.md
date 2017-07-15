*Elasticsearch* 是一个实时的**分布式搜索分析引擎**， 它能让你以一个之前从未有过的速度和规模，去探索你的数据。 它被用作全文检索、结构化搜索、分析以及这三个功能的组合：

- Wikipedia 使用 Elasticsearch 提供带有高亮片段的全文搜索，还有 *search-as-you-type* 和 *did-you-mean* 的建议。
- *卫报* 使用 Elasticsearch 将网络社交数据结合到访客日志中，实时的给它的编辑们提供公众对于新文章的反馈。
- Stack Overflow 将地理位置查询融入全文检索中去，并且使用 *more-like-this* 接口去查找相关的问题与答案。
- GitHub 使用 Elasticsearch 对1300亿行代码进行查询。

然而 Elasticsearch 不仅仅为巨头公司服务。它也帮助了很多初创公司，像 Datadog 和 Klout， 帮助他们将想法用原型实现，并转化为可扩展的解决方案。Elasticsearch 能运行在你的笔记本电脑上，或者扩展到上百台服务器上去处理PB级数据。

**Elasticsearch 中没有一个单独的组件是全新的或者是革命性的。**全文搜索很久之前就已经可以做到了， 就像早就出现了的分析系统和分布式数据库。 革命性的成果在于将这些单独的，有用的组件融合到一个单一的、一致的、实时的应用中。它对于初学者而言有一个较低的门槛， 而当你的技能提升或需求增加时，它也始终能满足你的需求。

如果你现在打开这本书，是因为你拥有数据。除非你准备使用它 *做些什么* ，否则拥有这些数据将没有意义。

不幸的是，大部分数据库在从你的数据中提取可用知识时出乎意料的低效。 当然，你可以通过时间戳或精确值进行过滤，但是它们能够进行全文检索、处理同义词、通过相关性给文档评分么？ 它们从同样的数据中生成分析与聚合数据吗？最重要的是，它们能实时地做到上面的那些而不经过大型批处理的任务么？

这就是 Elasticsearch 脱颖而出的地方：Elasticsearch 鼓励你去探索与利用数据，而不是因为查询数据太困难，就让它们烂在数据仓库里面。

Elasticsearch 将成为你最好的朋友。

Elasticsearch 也是使用 Java 编写的，它的内部使用 Lucene 做索引与搜索，但是它的目标是使全文检索变得简单， 通过隐藏 Lucene 的复杂性，取而代之的提供一套简单一致的 RESTful API。

然而，Elasticsearch 不仅仅是 Lucene，并且也不仅仅只是一个全文搜索引擎。 它可以被下面这样准确的形容：

- 一个分布式的实时文档存储，*每个字段* 可以被索引与搜索
- 一个分布式实时分析搜索引擎
- 能胜任上百个服务节点的扩展，并支持 PB 级别的结构化或者非结构化数据

Elasticsearch 将所有的功能打包成一个单独的服务，这样你可以通过程序去访问它提供的简单的 RESTful API 服务， 不论你是使用自己喜欢的编程语言还是直接使用命令行（去充当这个客户端）。



当你解压好了归档文件之后，Elasticsearch 已经准备好运行了。

如果你是在 Windows 上面运行 Elasticseach，你应该运行 `bin\elasticsearch.bat` 而不是 `bin\elasticsearch` 。

测试 Elasticsearch 是否启动成功，可以打开另一个终端，执行以下操作：

```
curl 'http://localhost:9200/?pretty'
```

你应该得到和下面类似的响应(response)：

这就意味着你现在已经启动并运行一个 Elasticsearch 节点了，你可以用它做实验了。
单个 *节点* 可以作为一个运行中的 Elasticsearch 的实例。 而一个 集群 是一组拥有相同 `cluster.name` 的节点， 他们能一起工作并共享数据，还提供容错与可伸缩性。
(当然，一个单独的节点也可以组成一个集群) 你可以在 `elasticsearch.yml` 配置文件中 修改 `cluster.name` ，该文件会在节点启动时加载 (译者注：这个重启服务后才会生效)。
关于上面的 `cluster.name` 以及其它 [Important Configuration Changes](https://elasticsearch.cn/book/elasticsearch_definitive_guide_2.x/important-configuration-changes.html) 信息， 你可以在这本书后面提供的生产部署章节找到更多。
TIP：看到下方的 View in Sense 的例子了么？[Install the Sense console](https://elasticsearch.cn/book/elasticsearch_definitive_guide_2.x/running-elasticsearch.html#sense) 使用你自己的 Elasticsearch 集群去运行这本书中的例子， 查看会有怎样的结果。
当 Elastcisearch 在前台运行时，你可以通过按 Ctrl+C 去停止。
