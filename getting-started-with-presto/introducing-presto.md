# 1. Presto 介绍

想必你阅读此书时，已经听说过 Presto 了。或许你只是随便看看第一章节，以便知道应该深入阅读何处。在这个介绍性的章节，我们讨论下你可能已经遇到过的关于数据大规模增长的问题，以及数据之后被忽略的价值。Presto 是数据工作的关键推动者，同时已经被证明是 SQL 界的成功案例。

了解 Presto 的设计和功能能够让你获得更好的见解，而不仅仅是现在已知的。 你可以更快地获得这些知识，并获得过去由于成本过高、时间太长而无法获得的信息。 除此之外，你将使用更少的资源，花费更少的预算，可以学到更多。

## 大数据的问题

每个人都在从设备指标，用户行为追踪，商业交易，地理位置信息，软件和系统测试过程等等环节中获取越来越多的信息。对数据的理解和洞察可以为一个公司抢占成功的先机。

同时，各种各样的存储系统也越来越多：关系型数据库、非关系型数据库、文档型数据库、K-V型数据库、对象存储系统，等等。它们中的很多系统在当今的技术中都是有必要的，只使用一种存储技术已然不太可能。如 图1-1，处理这些系统是足够让人畏惧的。

![&#x56FE; 1-1](../.gitbook/assets/figure-1-1.-big-data-can-be-overwhelming.png)

另外，我们并不能够用统一的标准工具访问这些不同的系统。不同的语言和分析工具各种各样。同时，你的数据分析师可能了解一门语言，那就是 SQL。无数的工具依靠 SQL 来进行分析、报表展示和进行其他商业智能的工作。

数据被分布在各处，其中有些对于数据的查询甚至不能满足分析师的要求。另外有一些系统，和现代的云架构不同，它们把数据集中存储，无法进行横向扩展。没有了这些能力，数据的应用场景进一步变小。

传统的大规模数据仓库处理方案已经被证明成本非常高。更常见的是，这种实现方案经常被诟病：慢。

现在有一种系统，提供了解决这些问题的好机会。

## 让 Presto 来解救吧

Presto 是解决以上问题的高手，同时它能够提供各种高级特性：联合查询不同的系统；并行查询；集群水平扩展；等等。图1-2是 Presto 的 logo。

![&#x56FE;1-2](../.gitbook/assets/figure-1-2-presto-logo.png)

Presto 是一个开源的分布式 SQL 查询引擎。它是从零开始设计和编写的，可针对各种大小（从千兆字节到PB大小）的不同数据源高效地查询数据。 Presto 打破了使用昂贵的商业解决方案进行快速分析或使用需要大量硬件的缓慢“免费”解决方案之间的错误选择。

### 为了性能和扩展而设计

Presto 旨在通过使用分布式执行来有效查询大量数据的工具。如果要查询的数据量为 TB 甚至是 PB，则可能会使用如 Apache Hive 之类的工具，这些工具可与 Hadoop 及其 Hadoop 分布式文件系统（HDFS）交互。 Presto 旨在替代这些工具，以更有效地查询该数据。

期望 SQL 响应时间能达到毫秒、秒和分钟的分析师应该使用Presto。 Presto 支持 SQL，通常用于数据仓库的分析工作中。这些工作性质通常被归类为在线分析处理（OLAP）。

即使 Presto 理解并可以有效执行 SQL，Presto 也不是数据库，因为它不包括自己的数据存储系统。它并不是要成为可替代 Microsoft SQL Server，Oracle，MySQL 或 PostgreSQL 的通用关系数据库。此外，Presto 并非旨在进行在线交易处理（OLTP）。对于为数据仓库或分析而设计和优化的其他数据库，例如 Teradata，Netezza，Vertica 和Amazon Redshift，也是如此。

Presto 利用众所周知的技术和新颖的技术来进行分布式查询处理。这些技术包括：内存中并行处理，集群中跨节点的流水线执行，使所有 CPU 核心保持繁忙的多线程执行模型，有效的扁平化内存数据结构以最大程度地减少 Java 垃圾回收以及 Java 字节码生成。这些复杂的 Presto 内部细节的详细描述超出了本书的范围。对于 Presto 用户而言，这些技术可以更快地洞察数据，而成本非常小。

### SQL 查一切

Presto 最初旨在查询 HDFS 中的数据，它可以非常有效地完成此任务。 但这不是终点。 相反，Presto 是一种查询引擎，可以查询对象存储，关系数据库管理系统（RDBMS），NoSQL 数据库和其他系统中的数据，如图1-3所示。

Presto 会查询数据所处的位置，并且不需要将数据迁移到集中的位置。 因此，Presto 允许查询 HDFS 和其他分布式对象存储系统中的数据。 它允许查询 RDBMS 和其他数据源。这样，它可以真正查询任何位置的数据，因此可以替代传统、昂贵且繁重的提取，转换和加载（ETL）过程。因此，Presto 显然不仅仅是另一个 SQL-on-Hadoop 解决方案。

![&#x56FE; 1-3](../.gitbook/assets/figure-1-3-sql-support-for-a-variety-of-data-sources-with-presto.png)

对象存储系统包括 Amazon Web Services（AWS）简单存储服务（S3），Microsoft Azure Blob 存储，Google Cloud Storage 和与 S3 兼容的存储，例如 MinIO 和 Ceph。 Presto 可以查询传统的 RDBMS，例如 Microsoft SQL Server，PostgreSQL，MySQL，Oracle，Teradata和 Amazon Redshift。Presto 还可以查询 NoSQL 系统，例如 Apache Cassandra，Apache Kafka，MongoDB 或 Elasticsearch。 Presto 几乎可以查询任何内容，并且实际上是一个 SQL-on-Anything 系统。

对于用户而言，这意味着突然之间，他们不再需要依赖特定的查询语言或工具来与这些特定系统中的数据进行交互。 他们可以简单地利用Presto 及其现有的 SQL 技能，以及易于理解的分析，仪表板和报表工具。 这些工具建立在使用 SQL 的基础之上。 用户甚至可以使用 Presto进行跨系统的 SQL 查询。

### 计算存储分离

Presto 不是带有存储功能的数据库； 相反，它只是查询数据所在的位置。 使用 Presto 时，存储和计算是分离的，可以独立扩展。 Presto 代表计算层，而基础数据源代表存储层。

这样，Presto 可以根据对访问此数据的分析需求来扩展和缩减其计算资源以进行查询处理。 无需移动数据，无需为当前查询的确切需求配置计算和存储，也无需根据不断变化的查询需求定期进行更改。

Presto 可以通过动态扩展计算集群来扩展查询能力，并且可以直接查询数据在数据源中的位置。 此特性使用户可以极大地优化硬件资源需求，从而降低成本。

## Presto 使用场景

Presto 的灵活性和强大功能使用户可以自己决定使用 Presto 的程度。 对于特定的问题，只能从一个小的用途开始。 大多数 Presto 用户都是这样开始的。

一旦用户习惯了这些优点和功能，就会发现新情况。消息四处传播，很快您就会发现 Presto 可以访问各种数据源，可以满足无数的需求。

在下一节中，我们将讨论其中一些用例。 请记住，您可以扩展使用范围以涵盖所有内容。 另一方面，用 Presto 解决一个特定问题也很好。 只是准备好喜欢 Presto 并最终增加其使用量即可。

### SQL 分析场景

RDBMS 和 SQL 的使用已经存在了很长时间，并且被证明是非常有用的。 没有他们，任何组织都无法运作。 实际上，大多数公司都在运行多个系统。 大型商业数据库，例如 Oracle 数据库或 IBM DB2，可能正在支持您的企业。像 MariaDB 或 PostgreSQL 这样的开源系统可以用于其他解决方案和一些内部应用程序。

作为消费者和分析师，您可能会遇到许多问题：

* 有时甚至不知道在哪里可以使用数据，只有公司的知识或多年内部工作经验可以帮助您找到正确的数据。
* 查询各种源数据库要求您使用不同的连接，以及运行不同的 SQL 方言。 它们足够相似，看起来一样，但是它们的行为却足以引起混乱和需要学习各种细节。
* 如果不使用数据仓库，则无法在查询中合并来自不同系统的数据。

Presto 解决上诉所有问题。你可以在一个系统中处理这些数据。你可以使用 SQL、标准函数、各种操作符。

### 数据仓库和源系统场景

当组织发现需要更好地理解和分析其众多 RDBMS 中的数据时，数据仓库系统的创建和维护便开始发挥作用。 然后，从各种系统中选择数据将经历复杂的 ETL 流程，并且通常通过长时间运行的批处理作业，最终将其存储在受到严格控制的大型数据仓库中。

尽管这在很多情况下对您有很大帮助，但作为数据分析师，您现在遇到了新问题：

* 在所有数据库系统之外，又有了一个新的数据库
* 今天需要的数据并不在数据仓库中，另外把它们放到数据仓库中需要耗费特别大的精力

Presto 允许您像添加任何其他关系数据库一样将任何数据仓库数据库添加为数据源。

如果您想更深入地研究数据仓库查询，则可以在同一系统中直接进行。 您可以在同一位置访问数据仓库和源数据库系统，甚至可以编写将它们组合在一起的查询。 Presto 允许您查询同一系统中的任何数据库，数据仓库，源数据库以及任何其他数据库。

### SQL 访问一切的特性

只使用 RDBMS 的日子已经一去不复返了。现在，数据已存储在针对相关用例进行了优化的许多不同的系统中。基于对象的存储，K-V 存储，文档数据库，图形数据库，事件流系统以及其他所谓的 NoSQL 系统都具有独特的功能和优势。

您的组织中至少有一些系统正在使用，这些系统中的数据对于理解和改善您的业务至关重要。

当然，所有这些系统还要求您使用不同的工具和技术来查询和使用数据。

至少，这是一项具有巨大学习曲线的复杂任务。但是，更有可能的是，您最终只能“刮擦“数据的表面，而并没有真正获得全面的了解。您缺乏查询数据的好方法。很难找到或者根本不存在用于更详细地可视化和分析的工具。

另一方面，Presto 允许您将所有这些系统作为数据源连接。它使用标准的美国国家标准学会（ANSI）SQL ，使用 SQL 的所有工具都可以通过它进行查询，如图1-4所示。

![&#x56FE; 1-4](../.gitbook/assets/figure-1-4-one-sql-access-point-for-many-use-cases-to-all-data-sources.png)

有了 Presto，理解不同系统的数据第一次变得容易了。

### 联邦查询

暴露 Presto 中的所有数据孤岛是了解数据的一大步。您可以使用 SQL 和标准工具来查询它们。 但是，通常，解决问题需要您进入数据孤岛，从中拉出各个方面，然后以本地方式组合它们。

Presto 允许您使用联合查询来做到这一点。 联合查询是一种 SQL 查询，它在同一条语句中引用和使用完全不同的系统中的不同数据库和架构。 您可以同时查询 Presto 中的所有数据源，并且在同一查询中使用相同的 SQL。

您可以定义对象存储中的用户跟踪信息与 RDBMS 中的客户数据之间的关系。如果键值存储区包含更多相关信息，则也可以将其挂接到查询中。

将联合查询与 Presto 结合使用可以使您获得原本无法了解的信息。

### 虚拟的数据仓库语义层

数据仓库系统不仅为用户带来了巨大收益的同时，给组织带来了负担：

* 运行和维护数据仓库是一个庞大而昂贵的项目
* 需要专门的团队运行和管理数据仓库以及相关的 ETL 流程
* 将数据放入仓库需要用户突破繁文缛节，通常会花费太多时间

另一方面，Presto 可用作虚拟数据仓库。它可以通过使用一种工具和标准 SQL 来定义您的语义层。在 Presto 中将所有数据库配置为数据源后，即可查询它们。Presto 提供了查询数据库中存储的必要计算能力。使用 SQL 以及受支持的函数和运算符，Presto 可以直接从源提供所需的数据。在将数据用于分析之前，无需复制，移动或转换数据。

借助对所有连接的数据源的标准 SQL 支持，您可以创建所需的语义层，以更简单的方式从工具和最终用户层进行查询。并且该层可以包含所有基础数​​据源，无需迁移任何数据。 Presto 可以在源和存储级别查询数据。

使用 Presto 作为这种“动态数据仓库”，组织可以利用附加功能来增强其现有数据仓库，甚至完全避免建立和维护仓库。

### 数据湖查询引擎

术语“数据湖”通常用于大型 HDFS 或类似的分布式对象存储系统，将各种数据转储到其中，而无需考虑如何访问它。Presto 将其解锁，成为有用的数据仓库。实际上，Presto 诞生于 Facebook，是一种处理超大型 Hadoop 数据仓库的工具。它比 Hive 和其他工具所能提供的功能更强大。这将在“用于分布式存储数据源的 Hive 连接器”中进行讨论。

现在，现代数据湖经常使用云服务商或其他开源项目提供的 HDFS 以外的其他对象存储系统。 Presto 能够对它们中的任何一个使用 Hive 连接器，因此可以在您的数据湖上（无论其位于何处，只要在存储数据）进行基于 SQL 的分析。

### SQL 转换和 ETL

借助对 RDBMS 和其他数据存储系统的支持，Presto 可用于移动数据。 SQL 和可用的丰富 SQL 函数集使您可以查询数据，对其进行转换，然后将其写入同一数据源或任何其他数据源。

实际上，这意味着您可以将数据从对象存储系统或键值存储中复制并复制到 RDBMS 中，并将其用于以后的分析。当然，您也可以转换和汇总数据以获得新的信息。

另一方面，从运营的 RDBMS 或事件流系统（如 Kafka）中获取数据并将其移入数据湖以减轻 RDBMS 中的查询负担也是很常见的。ETL流程（现在通常也称为数据准备）可以成为该流程中重要的部分，以改善数据并创建更适合查询和分析的数据模型。

在这种情况下，Presto 是整个数据管理解决方案的关键部分。

### 更快的响应，更好的认知

提出复杂的问题并使用海量数据集总是会遇到限制。复制数据并将其加载到数据仓库并进行分析可能最终太昂贵了。这些需要太多的计算能力才能完全运行它们，否则要花很多天才能得到答案。

Presto 避免了设计中的数据复制。并行处理和繁重的优化工作通常会改善 Presto 分析的性能。

如果过去耗时三天的查询现在可以在 15 分钟内运行，那么是值得的。 从结果中获得的知识为您提供了优势，并具有运行更多查询的能力。

Presto 的这些更快的处理时间可实现更好的分析和结果。

### 大数据，机器学习，人工智能

Presto 向支持 SQL 的平台提供越来越多的数据，并将查询扩展到海量数据集这一事实，使其成为处理大数据的主要工具。现在，这通常包括统计分析、机器学习和人工智能系统。借助对 R 和其他工具的支持，Presto 在这些用例中肯定可以发挥作用。

### 其他使用场景

在前面的部分中，我们提供了 Presto 用例的高级概述。新的用例和组合后续经常出现。

在第 13 章中，您可以了解有关一些知名公司和组织使用 Presto 的详细信息。我们将在本书结尾处提供这些信息，因此您可以通过阅读以下章节来首先获得理解手头数据所需的知识。

## Presto 相关资源

### 官网

![&#x56FE; 1-5](../.gitbook/assets/figure-1-5-home-page-of-presto-website-and-prestosql.io.png)

### 文档

[https://prestosql.io/docs](https://prestosql.io/docs)

### 社区沟通

[https://prestosql.slack.com/](https://prestosql.slack.com/)

### 源代码、许可证、版本管理

[https://github.com/prestosql/presto](https://github.com/prestosql/presto)

### 贡献代码

略

### 本书原版仓库

[https://github.com/prestosql/presto-the-definitive-guide](https://github.com/prestosql/presto-the-definitive-guide)

### Iris 数据集

在本书的后续部分中，您将遇到有关 Iris 花和 Iris 数据集的示例查询和用例。Iris 是著名的数据集，通常在数据科学分类示例中使用。

数据集包含一个简单的表，该表包含150个记录和列，其中包含萼片长度，萼片宽度，花瓣长度，花瓣宽度和种类的值。

数据集体积小巧，用户可以轻松地测试和运行查询并执行各种分析。这使得数据集适合学习，包括与 Presto 一起使用。您可以在 Wikipedia 页面上找到有关该数据集的更多信息。

我们的图书存储库包含目录 iris-data-set，其中包含以逗号分隔值（CSV）格式的数据，以及用于创建表格并将其插入的 SQL 文件。阅读完第2章和“ Presto命令行界面”后，可以轻松遵循以下说明。

您可以通过以下方式使用数据集：首先将 etc/catalog/memory.properties 文件复制到 Presto 安装所在的位置，然后重新启动 Presto 。

现在，您可以使用 Presto CLI 将数据集放入内存目录的默认架构中的Iris 表中：

```text
$ presto -f iris-data-set/iris-data-set.sql
USE
CREATE TABLE
INSERT: 150 rows
```

确认数据可查：

```text
$ presto --execute 'SELECT * FROM memory.default.iris;'
"5.1","3.5","1.4","0.2","setosa"
"4.9","3.0","1.4","0.2","setosa"
"4.7","3.2","1.3","0.2","setosa"
...
```

### Flight 数据集

类似于 Iris 数据集，Flight 数据集将在本书的后面使用，例如查询和用法。 该数据集比 Iris 数据集复杂一点，它由航空公司，机场和其他信息表以及有关特定航班的交易数据组成。这使得数据集适用于使用更复杂查询以及联合查询（在联合查询中不同的表位于不同的数据源中）。

数据是从美国联邦航空管理局（FAA）收集并整理用于分析的。 Flights 表架构非常大，表1-1中显示了可用列的子集。

| flightdate | airlineid | origin | dest | arrtime | deptime |
| :--- | :--- | :--- | :--- | :--- | :--- |


数据集中的每一行代表在美国机场的航班起飞或降落。

图书存储库（请参阅“图书存储库”）包含一个单独的文件夹，即 Flight 数据集。它包含有关如何将数据导入不同数据库系统的说明，以便您可以将它们连接到 Presto 并运行示例查询。

## Presto 简史

在 2008 年，Facebook 开源了 Hive，后来成为 Apache Hive。 Hive 在Facebook 内被广泛使用，以针对其超大型 Apache Hadoop 集群上的 HDFS 中的数据运行分析。

Facebook 的数据分析师使用 Hive 在其大型数据仓库上运行交互式查询。在 Presto 出现在 Facebook 之前，所有数据分析都依赖于 Hive，它不适用于 Facebook 规模的交互式查询。 2012年，其 Hive 数据仓库的大小为 250PB，每天需要处理来自数百名用户发出的数万条查询。 Hive 开始在 Facebook 内达到其极限，并且没有提供查询 Facebook 内其他数据源的功能。

于是 Presto 被开始设计，可以在 Facebook 的数据规模上运行快速查询。 Presto 并未创建新的系统来将数据移至其中，而是被设计为通过可插拔连接器系统从存储位置读取数据。 Hive 连接器是为 Presto 开发的首批连接器之一。请参阅“用于分布式存储数据源的 Hive 连接器”。该连接器直接查询存储在 Hive 数据仓库中的数据。

2012 年，四名 Facebook 工程师开始进行 Presto 开发，以解决 Facebook 分析的性能，可伸缩性和可扩展性需求。从一开始，目的就是将 Presto 构建为一个开源项目。 2013 年初，Presto 的初始版本在 Facebook 上正式投入生产。到 2013 年秋季，Presto 由 Facebook 正式开源。看到 Facebook 的成功，其他大型网络公司开始采用 Presto，包括 Netflix，LinkedIn，Treasure Data 等。许多公司继续关注。

2015 年，Teradata 宣布了 20 名 Presto 开发工程师的重大承诺，重点是增加安全增强和生态系统工具集成等企业功能。 2015 年下半年，Amazon 将 Presto 添加到了其 AWS Elastic MapReduce（EMR）产品中。 2016 年，亚马逊宣布推出 Athena，其中 Presto 作为主要基础作品。 2017 年，Starburst 创立了，该公司致力于推动 Presto 在世界各地的成功。

2018 年底，Presto 的原始创建者离开 Facebook 并成立了 Presto 软件基金会，以确保该项目保持协作和独立。从那时起，该项目的创新和发展进一步加速。

如今，Presto 社区蓬勃发展并蓬勃发展，许多知名公司继续广泛使用Presto。该项目由来自世界各地许多公司（包括阿里巴巴集团，亚马逊，Appian，Gett，Google，Facebook，Hulu，Line，LinkedIn，Lyft，Motorola，Qubole，Red Hat，Salesforce， Starburst，Twitter，Uber，Varada，沃尔玛 和 Zoho。

## 总结

在本章中，我们向您介绍了 Presto。 您了解了有关其某些功能的更多信息，我们一起探讨了可能的用例。

在第 2 章中，您将启动并运行 Presto，连接数据源，并了解如何查询数据。

