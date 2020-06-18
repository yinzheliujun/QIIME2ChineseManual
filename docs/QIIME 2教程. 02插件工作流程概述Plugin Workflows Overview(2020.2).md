[TOC]

# 前情提要

- [Nature Biotechnology：QIIME 2可重复、交互和扩展的微生物组数据分析平台](https://mp.weixin.qq.com/s/-_FHxF1XUBNF4qMV1HLPkg)
- [1简介和安装Introduction&Install](https://mp.weixin.qq.com/s/vlc2uIaWnPSMhPBeQtPR4w)

# QIIME 2插件工作流程概述

**Overview of QIIME 2 Plugin Workflows**

英文原文见：https://docs.qiime2.org/2020.2/tutorials/overview/

正文共：9858 字 9 图 1 视频

预计阅读时间： 25 分钟，视频时长 18 分钟

更新时间：2020年4月6日

**本节即是对QIIME 2工作流程的概述，也是对扩增子分析过程的高度概括和总结，建议仔细阅读，新人和老司机会有不同的体验，但都会收获满满。**


> 注：在阅读此文前您应先了解Qiime2的[专业术语](https://docs.qiime2.org/2020.2/glossary/)，请点击此链接开始阅读。👺

> 注：本节是QIIME 2用户新手的指南，特别适用于那些不熟悉微生物组研究的用户。 对于已经精通微生物组分析的有经验用户可跳过本节，直接阅读下一节[《老司机上路指南》](https://docs.qiime2.org/2020.2/tutorials/qiime2-for-experienced-microbiome-researchers/)。

欢迎您加入QIIME 2大家庭👋。本节内容将帮助你了解 QIIME 2的主要插件和可用的功能，并指导你深入学习相关的教程。换言之，本节没有回答你如何使用QIIME 2的问题，但可以指明你正确的方向。把本节当成一张藏宝图：将QIIME 2的每个功能作为你通往荣耀的垫脚石，下方的流程图将会告诉你所有的宝藏埋在哪里。🗺️

请记住，条条小路通山顶，但在山顶时我们都凝视着同一个月亮。🌕


## **QIIME 2用户文档. 2插件工作流程概述**

https://v.qq.com/x/page/q0913bywmop.html

视频有广告，清晰度不够高吗？**在微信订阅号“meta-genome”后台回复“qiime2”获得1080p视频和测试数据下载链接**。

## 让我们定位：流程图

**Let’s get oriented: flowcharts**

在我们提及插件或功能之前，对于分析扩增子数据，我们需要讨论标准QIIME 2的工作流程（**workflow**）这一概念。在我们看概述之前，我们必须先看一下打开藏宝图的钥匙长什么样：

![image](http://bailab.genetics.ac.cn/markdown/qiime2/fig/2019.7.2.01.png)

每种类型的数据（如：对象Artifacts和可视化Visualizations）和功能action （如：方法methods、可视化工具visualizers和流程pipelines）用不同颜色的节点（即方框）代表。连接节点的边分为实线（代表需要的输入或输出文件）和虚线（代表可选的输入文件）。如果没明白什么意思，可以回头读一下第一节中的"核心概念"。

在下文的流程图中，具体意义如下:

- 命令/动作(Actions)采用插件或动作的名称来命名。想使用这些命令，可以打开终端，在命令行中输入`qiime`，再配合各种功能，如`qiime demux emp-single`。
- 流程(Pipelines)是一种特殊的动作，即一条命令运行多个单独的命令（译者注：可以理解为一连串的命令集）。为了简洁，在一些流程图中，流程被标记为箱体————封装多个在内部运行的动作。🌯
- 对象/数据(Artifacts)采用[语义类型](https://docs.qiime2.org/2020.2/semantic-types/)的名称来命名。别担心，除非你需要将你的文件导入并转换成这种格式，否则你不需要记往这些长的名字。译者注：语义类型这个词不好理解？没关系，你可以简单地这么理解：语义类型=专业术语，或者直接理解为“概念”。
- 可视化(Visualizations)有各种名称，一些代表数据的意义，一些用表达的意义来命名...🍙

## 给新人划重点

**Useful points for beginners**

进一步学习前的知识重点：

1. 下面的指南并非面面俱到，它只涵盖大多数QIIME 2“核心”插件中的一些主要操作。还有许多其他操作和插件需要你自己去发现和探索。如果你想了解更多，可以在终端中使用`qiime --help`功能，它可以列出全部插件。比如你想看`dada2`的功能，可以键入这个指令`qiime dada2 --help`。如想查看拆分功能中的地球微生物组标准单端序列拆分的帮助，打`qiime demux emp-single --help`。现在你学会查看每个插件和功能的方法了吗？😊
2. 下方的流程图设计为了尽量简洁，因此省略了许多的输入文件(特别是可选的输入和元数据)、输出文件(如统计摘要和次要输出文件)和其它可能的命令参数。还省略了许多附加命令（例如用于显示统计摘要或操作特征表的命令🎻）。现在你已经学会了查阅帮助文档，可以查看并学习每个插件命令的具体功能和参数(提示：如果有插件的命令在这里没有提到，它可能是用于检查那个插件其它命令的输出文件的)。
3. [元数据(metadata，样本信息，如分组信息等)](https://docs.qiime2.org/2020.2/tutorials/metadata/)是QIIME 2中的核心概念。我们在[后面有一节](https://docs.qiime2.org/2020.2/tutorials/metadata/)专门对它进行专门讲解和讨论。仔细品读，可以行稳致远！📚
4. 对象(Artifacts `.qza`)和可视化(Visualizations `.qzv`)文件都是标准的压缩文档，包括数据文件、分析过程可追溯的文件。可以使用`unzip`解压对象和可视化文件后查看内容。更好的方法是使用`qiime tools export`命令导出文件，后面的[导出数据](https://docs.qiime2.org/2020.2/tutorials/exporting/)会有详细讲解。想要进一步了解这两类文件格式，可阅读数据是如何存储一文：https://dev.qiime2.org/latest/storing-data/。🤓
5. 在QIIME 2中进行分析数据没有唯一的方法。大多数的插件和功能都是独立的软件或现存的方法。QIIME只是起到胶水的作用，将它们整合在一起，然后奇迹就发生了。通往山顶的路不只一条。⛰️
6. 不要忘记引用每个插件或功能的原文献！如果你不确定应如何引用它们，可以使用`--citations`参数查看，比如在在Terminal中输入`qiime dada2 --citations`就能显示出DADA2插件的引用信息。或者，你可以把对象和可视化文件拖入这个网页[https://view.qiime2.org/]([https://view.qiime2.org/)来显示相关信息。本功能自2018.4及以后版本中才有，这里面有产生你所需要文件的全部参考文献，方便吧！😎💃💃💃

## QIIME 2分析流程概述

**Conceptual overview of QIIME 2**

现在我们阅读完了词汇表和金钥（上一段），让我们全面了解一下扩增子测序数据的分析流程：

![image](http://bailab.genetics.ac.cn/markdown/qiime2/fig/2019.7.2.02ch.png)

==黄色框代表操作方法==，绿色块代表文件或数据。

![image](http://bailab.genetics.ac.cn/markdown/qiime2/fig/2019.7.2.02.png)

本概述中的边和节点并不表示具体的操作或数据类型，而是表示概念类别，例如，我们在实验中可能拥有的数据基本类型或分析目标。下面将更详细地讨论所有这些步骤和术语。

所有数据都必须[导入](https://docs.qiime2.org/2020.2/tutorials/importing/)为QIIME 2对象，以便由QIIME 2操作使用（除了一些元数据）。不同的用户可以在不同的阶段进入该工作流程。大多数人都有某些类型的原始序列（例如，FASTQ或FASTA）数据，这些数据应该按照适当的[序列导入方案](https://docs.qiime2.org/2020.2/tutorials/importing/#importing-seqs)导入。其他用户可以从拆分为单样本的序列数据开始，或者从合作者给他们的[特征表](https://docs.qiime2.org/2020.2/tutorials/importing/#importing-feature-tables)开始。后面章节中的导入教程专题会详细介绍用户最常见需要导入到QIIME 2中的的数据类型。

现在我们已经了解到— — 实际上可以在几乎任何节点上进入这个工作流程，接下来让我们浏览各个部分的具体功能和应用。

1. 所有的宏基因组/扩增子测序的分析的起点是原始序列数据。原始数据多数为fastq格式，其包含有DNA序列数据和每个碱基的质量值。
2. 我们必须进行混池的[样本拆分（demultiplex）](https://docs.qiime2.org/2020.2/tutorials/overview/#demultiplexing)，以便确定每条序列来自于哪个样本。
3. 然后进行**序列去噪（denoised）以获得扩增子序列变异（amplicon sequence variants, ASVs），或聚类为可操作分类单元（operational taxonomic units, OTUs）**，这样做[目的有二个](https://www.nature.com/articles/s41579-018-0029-9)：⑴降低测序错误；⑵序列去冗余。
 
4. **特征表和代表性序列是去噪获得的关键结果**，是下游分析的核心数据。一个特征表简单说就是一张Excel表，行名为ASV或OTU名称，列名为样本名。译者注：特征（feature）是对ASV/OTU等的统称。
5. **我们可以基于特征表做很多事，常用分析包括**：
    1. [序列的物种分类](https://docs.qiime2.org/2020.2/tutorials/overview/#taxonomy)。比如，这里面有什么物种？
    2. [Alpha(α)和Beta(β)多样性分析](https://docs.qiime2.org/2020.2/tutorials/overview/#diversity)，即分别描述样本内或样本间的多样性。比如我们可以了解样本间有多少物种是一样的，即相似性如何？
    3.  许多的多样性分析依赖于个体特征的进化相似性。如果你测序的是系统发育的标记基因，如16S rRNA基因，你可以采用多序列比对方式评估特征间的[系统发育关系](https://docs.qiime2.org/2020.2/tutorials/overview/#alignment)。
    4.  不同实验组间特征的差异丰度分析，确定哪些OTUs或ASVs显著的多或少。

这只是一个开始，在Qiime 2里还有众多的[统计方法和绘图方法](https://docs.qiime2.org/2020.2/tutorials/overview/#fun)触手可及。世界是你的，就让我们一探究竟吧（The world is your oyster. Let’s dive in）。🏊

> 警告
> 
> 哇！别着急！我们将开始使用一些严肃的技术术语🤓。你是否仔细研读了前面讲到过的[**语义类型**](https://docs.qiime2.org/2020.2/semantic-types/)和[**核心概念**](https://docs.qiime2.org/2020.2/concepts/)？没有的话，请赶快返回第一章阅读，否则你再往下看会一头雾水的。⚡⚡

## 样本拆分

**Demultiplexing**

可以想象一下，我们收到一堆FASTQ数据，刚从测序仪下机还热乎的（新出锅的包子很诱人，新下机的数据你也一定有马上分析的冲动吧！）。大多数二代测序仪器有能力在单个通道（lane）／同一批次（run）中测序数百甚至数千个样本。我们通过多通道混用（multiplexing）的方法来提高检测速度，即多个样本混在一个文库中测序。既然这些来自不同样本的个读段（read）混合在一个“池”中，我们是如何知道每来个read来自哪个样本呢？这通常采用在每个序列的一端或双端附加唯一的条形码`barcode`（即索引`index`或标签`tag`）序列来实现区分read来源。检测这些条形码序列并将reads分类到所属的样本来源的过程就是“样本拆分”，或者叫“序列分拣”。这个过程非常类似于快递的分拣。

想要开始样本拆分了吗？你或者为你的样品建库和测序的人应该知道哪个条形码属于哪个样品。如果你不知道，可以和你的实验室伙伴或测序中心谈谈。一般在元数据文件（sample metadata）中应包含此条形码信息，以便进行下游分析。

QIIME 2样本拆分过程见下面的流程图（现在暂时忽略此流程图的右侧）：

![image](http://bailab.genetics.ac.cn/markdown/qiime2/fig/2019.7.2.03.png)

这个流程图描述了QIIME 2样本拆分的可能步骤，原始数据类型不同，步骤会有差异。通常情况下，在`q2-demux`或`q2-cutadapt`的拆分方法只有一个适用于您的数据，但这就能满足你的需求了。

阅读有关样本拆分的更多信息，并使用人体各部位微生物组教程（针对单端数据）和沙漠土壤教程（针对双端数据）对其进行拆分实战。这些教程包括地球微生物组计划(EMP)格式数据（如导入文档中所述）。你的测序数据中有条形码和引物吗？请参阅cutadapt教程以了解如何在`q2-cutadapt`中使用`demux`方法。有多重标签、混合方向测序或其他不寻常的格式吗？这些处理非标准实验方案的处理不在标准流程中，努力祈祷🙏，然后查看QIIME 2论坛，看看是否有人找到解决办法(这些非标准的建库拆分方法一部分可以使用QIIME 1实现拆分和方向调整，但我强烈建议谁挖坑测序的让谁处理好了，他们奇怪的方案肯定有自己对应的个性化工具，别浪费自己的宝贵时间为别人奇怪的想法买单)。

双端测序结果在分析中某个合适的时间点，需要将其合并。如果您按照[沙漠土壤菌群分析教程](https://docs.qiime2.org/2020.2/tutorials/atacama-soils/#atacama-demux)，您将看到在使用`q2-dada2`去噪期间自动进行了双端合并。但是，如果希望使用`q2-debur`或`OTU聚类`方法（下文有更详细描述），则需要先使用`q2-vsearch`进行双端合并，就像上方工作流程图所示那样。要了解有关双端序列合并的更多信息，在后面我们会有`read-join`的[专题教程](https://docs.qiime2.org/2020.2/tutorials/read-joining/)。👯

你现在是否有点被搞晕了呢？不用绝望，重新回顾一下本节“分析流程概述”你会更加理解其思路。对大多数新用户来说，数据导入和原始序列样本拆分是最头痛的部分😤。但是一旦你掌握了诀窍，就很容易了。🍰

## 去噪和聚类

**Denoising and clustering**

祝贺你走得这么远！去噪和聚类步骤比导入和样本拆分更容易！ 🎉😬🎉

这些步骤的名称有丰富的内涵：

1. 我们对序列进行去噪，以便去除和/或校正噪音序列。🔊
2. 我们将序列去冗余，以减少多余重复的序列，让文件变得更小，降低计算机内存需求。不要担心，软件会记录每个序列的重复次数，这种重复次数就是read counts。🕵
3. 我们对序列进行聚类，即将相似的序列归一为单个序列，一般相似性的阈值定位97%。这个过程，也称为挑选OTU（OTU picking）。挑选OTU在Qiime第1个版本时曾经是一个常用的分析步骤，用于去重并同时进行去噪。但是这种去噪仅捕获随机的测序和PCR错误。目前强烈建议大家使用去噪的方法。译者注：与时俱进是科学精神的重要内涵之一，当由于你没有跟进近几年的新方法和进展，而使用了过时的方法导致了不合理的结论才是时代的悲哀。

### 去噪

**Denoising**

让我们从去噪开始，它在上图[样本拆分和去噪工作流程](https://docs.qiime2.org/2020.2/tutorials/overview/#derep-denoise)的右边描述。

目前在QIIME 2中可用的去噪方法包括[`DADA2`](https://pubmed.ncbi.nlm.nih.gov/27214047/)和[`Deblur`](https://msystems.asm.org/content/2/2/e00191-16)。您可以通过阅读每个方法的文章来深入了解这些方法。DADA2的实例应用于[人体各部位微生物组分析教程](https://docs.qiime2.org/2020.2/tutorials/moving-pictures/)，[粪菌移植教程（用于单端数据）](https://docs.qiime2.org/2020.2/tutorials/fmt/)以及[阿塔卡马沙漠土壤教程（用于双端测序数据）](https://docs.qiime2.org/2020.2/tutorials/atacama-soils/)。Deblur的示例在人体各部位微生物组教程（针对单端数据）和[`双端序列合并`教程（针对双端数据）](https://docs.qiime2.org/2020.2/tutorials/read-joining/)。注意，`deblur`（以及`vsearch`的`dereplicate-seqences`）分析之前必须进行[数据质量过滤](https://www.nature.com/articles/nmeth.2276)，但这个步骤对于`dada2`来说是不必要的。**`Deblur`和`DADA2`都包含内部嵌合体检查方法和丰度过滤，因此按照这些方法不需要额外的过滤**。 🦁🐐🐍

简而言之，这些方法滤除有噪声的序列，校正不确定序列中的错误（如在DADA2的分析中），去除嵌合序列，去除单体(singletons，出现频率仅有一次的序列)，合并去噪后的双端序列（在DADA2的分析中），然后对这些序列进行去冗余。

由去噪方法产生的特征有许多名称，通常是“序列变异”（sequence variant, SV）、“扩增子SV”（ASV）、“实际SV(actual SV)”、“精确SV(exact SV)”……我相信在本教程中我们已经将这些称为**ASV**，让我们保持术语的一致性。📏

### 聚类

**Clustering**

接下来我们将讨论聚类方法。去冗余(最简单的聚类方法，有效地产生100％相似度的OTU，即在数据集中观察到的所有唯一序列)也在[样本拆分和去噪工作流程](https://docs.qiime2.org/2020.2/tutorials/overview/#derep-denoise)中描述，是QIIME 2中所有其他聚类方法的起点，如下图所示：

![image](http://bailab.genetics.ac.cn/markdown/qiime2/fig/2019.7.2.04.png)

`q2-vsearch`实现了[三种不同的OTU聚类策略](http://qiime.org/tutorials/otu_picking.html)：无参(*de novo*)、有参(**closed reference**)和有无参结合(open reference)。所有步骤之前都应该进行[质量控制](https://www.nature.com/articles/nmeth.2276)，然后进行[嵌合体过滤](https://docs.qiime2.org/2020.2/tutorials/chimera/)和有侵略性的OTU丰度过滤（危险的三重奏，又称Bokulich方法，**可以极大的降低假阳性，但可能造成一定程度的假阴性——分析中很多找到最优解，通常只是经验+尝试选择较优解**）。 🙈🙉🙊

OTU聚类教程演示了几种`q2-vsearch`聚类方法的使用。别忘了阅读嵌合体过滤教程！

通过聚类方法产生的特征被称为操作分类单元（OTU），它是次优的世界语、不精确的垃圾。 🚮

> 译者注：在过去十年里，OTU的广泛使用为研究扩增子测序数据提供了简单快速的分析方式，带来了微生物组学文章的大爆发。但同时因其聚类的偏好性，序列可变性等缺点，使得不同研究无法可比较、可重复的问题十分严重，故被称为“次优的、不精确的垃圾世界语——使用广泛但并不通用”。

### 特征表

**The Feature Table**

所有去噪和聚类方法/工作流程的最终产品是`特征表[频率Frequency](特征表feature table)`对象和`特征数据[序列Sequence]`(代表序列representative sequences)对象。这是扩增子分析工作流程中最重要的两个对象，用于许多下游分析，如下面所讨论的。实际上，特征表对于任何QIIME 2分析都是至关重要的，作为每个样本的所有观察的`中心记录`。如此重要的对象值得拥有强大的插件`q2-feature-table`。我们不会在这里详细讨论这个插件的所有操作（有些在下面提到），但是它可以在特征表上执行许多有用的操作，所以要熟悉它的文档格式！😴

我重复一遍：**特征表是QIIME 2中分析的核心。几乎所有的分析步骤(除在样本拆分和去噪/聚类外)都以某种方式涉及特征表**。注意！ 😳

> 注：想要查看哪个序列与特征ID相关？使用`qiime metadata tabulate`命令，使用`特征数据FeatureData[序列Sequence]`对象作为输出。

祝贺你！🎉您已经完成了数据的导入、样本拆分和去噪/聚类，这些对于大多数用户来说都是最复杂和困难的步骤（如果仅仅是因为有那么多方法可以做到这一点！）如果你能走这么远，剩下的就很容易了。现在开始接下来愉快的旅程。

## 物种分类和分类学分析

**Taxonomy classification and taxonomic analyses**

对于许多湿实验研究人员的目的是鉴定样品中存在的微生物。例如，我的样品中有哪些属或种？这个病人的样本中有人类病原体吗？[我的酒里有什么微生物在游泳？](https://www.pnas.org/content/111/1/E139)🍷🤑

我们可以通过要查询的序列（即我们的特征，无论是ASV还是OTU）与具有已知分类信息的参考序列数据库进行比较来获得物种注释。仅仅找到最接近的比对结果并不一定是最好的，因为其他相同或接近的序列可能具有不同的分类注释。因此，我们使用基于比对、k-mer频率等物种分类器来确定最接近的分类学关联，并具有一定程度的置信度或一致区域（如果不能确定地预测物种名称，那么这可能不是同一物种！）。那些对QIIME 2中的物种分类学有更多兴趣的人可以阅读，2018年5月发表在Microbiome上的文章(https://doi.org/10.1186/s40168-018-0470-z)，够你读到天黑(until the cows come home)。🐄🐄🐄

让我们看一下物种分类工作流的样子：

![image](http://bailab.genetics.ac.cn/markdown/qiime2/fig/2019.7.2.05.png)

`q2-feature-classifier`包括三种不同的分类方法。`classify-consensus-blast`和`classify-consensus-vsearch`都是基于比对的方法，可以在N个最好的比对结果中找一致最高的用于分类。这些方法直接参考数据库`FeatureData[Taxonomy]`和`FeatureData[Sequence]`文件，不需要预先训练。

基于机器学习的分类方法是通过`classify-sklearn`实现的。理论上讲， [scikit-learn](https://scikit-learn.org/stable/)中的任何分类方法均可应用于物种分类。用于物种分类的软件或插件叫“分类器”，这些分类器因为采用了机器学习原理，在正式用于你的数据分类前必须训练这些分类器，以便让软件“学会”哪些特征可以最好地区分每个分类组。这个训练过程是在进行正式分类前额外需要的步骤。训练出来的分类器是具有“物种数据库和标记基因”特异性的。分类器一旦训练成功，只要你测序引物等测序条件没有改变，它就可以多次使用而不需要重新训练！==译者注1：训练分类器需要用到特定的物种分类数据库（比如Greengenes database）和你自己测序时的引物序列，训练步骤是：先用引物定位Greengenes中的参考序列，然后截取出这些参考序列（截取出的参考序列长度和你测序获得的序列长度类似），然后把这些序列与物种分类名称匹配，这样就获得了“分类器”。所以分类器具有“物种数据库和标记基因”特异性。== 译者注2：scikit-learn是一个著名的Python语言机器学习网站，里面有很多机器学习的代码。

大多数用户并不需要按照该教程执行训练步骤，因为可爱的QIIME 2开发人员提供了几个[预先训练的分类器](https://docs.qiime2.org/2020.2/data-resources/)供大家使用。🎅🎁🎅🎁🎅🎁

**哪种方法最好**？[它们都很好](https://microbiomejournal.biomedcentral.com/articles/10.1186/s40168-018-0470-z)，否则我们就不麻烦把它们呈现给用户了。😎 但是，一般来说，使用朴素贝叶斯(Naive Bayes)分类器的`classify-sklearn`可以稍微优于我们基于16S rRNA基因和真菌ITS序列分类的几个标准测试的其他方法。然而，对于一些用户来说，这可能更加困难和令人沮丧，因为它需要额外的训练步骤。这个训练步骤可能需要大量的内存，对于某些无法使用预先训练分类器的用户来说，这将成为一个障碍。一些用户还喜欢基于比对的方法，因为这种操作模式更加透明并且参数更易于操作 (参见后面会讲到的数据资源章节，以了解这些参数的描述以及不同应用的推荐设置)。

**特征分类过程可能会比较慢**。这完全取决于你序列的数量和参考序列的数量。与进行分类相比，OTU聚类的序列可能需要更长的时间（因为序列通常更多）。如果担心运行时间太长，在分类之前从序列文件中筛选排除低丰度的特征，并可以使用较小的参考数据库。实际上，在“正常大小”的测序实验中（无论这意味着什么😜），我们需要消耗几分钟（几百个特征）到几个小时（几十万个特征）之间来完成分类。如果您希望在看到精确的时间数字，请查看我们的分类器运行时间性能评估和测试的结果。🏃⏱️

**特征分类可以是内存密集型的**。通常最小需要4GB的RAM，最大可达32GB+的内存。这完全取决于参考序列的大小、长度和特征序列的数量……

使用`classify-sklearning`的示例在[特征分类器教程](https://docs.qiime2.org/2020.2/tutorials/feature-classifier/)和[人体各部微生物组教程](https://docs.qiime2.org/2020.2/tutorials/moving-pictures/#moving-pics-taxonomy)中出现。分类的流程图使其他分类器方法更加清晰。

所有分类器生成一个`FeatureData[Taxonomy]`对象，其中包含每个查询序列的物种分类信息。

> 提示： 想要查看哪个序列和分类学与特征ID相关？使用`qiime metadata tabulate`命令，使用`特征数据FeatureData[序列Sequence]`和`FeatureData[Taxonomy]`对象作为输出。

### 序列分类注释

**Now that we have classified our sequences**

物种分类是打开新世界成为可能 🌎

我们现在拥有了特征数据物种注释 `FeatureData[Taxonomy]` 对象:

1. **按分类层次相同的分类单元进行合并**，这用到`taxa collapse`。这将共享相同分类的所有特征合并为单个特征。该分类单元名称成为新特征表中的特征ID。这个特征表可以与原始表相同的方式使用。一些用户可能对这类表特别感兴趣，例如，可以进行基于不同分类层级的多样性分析，但大家都对这些分类群的差异丰度分析更感兴趣。比较使用分类群作为特征的差异丰度分析，与使用ASV或OTU作为特征的差异丰度分析都可以为各种分析提供诊断和信息。 🌂
2. **绘制物种组成**，方便查看每个样本中各种分类群的丰度。查看物种丰度条形图和特征表热图了解更多细节。📊
3. **过滤特征表和代表序列**（`FeatureData[Sequence]`对象）以删除某些分类学组。这对于**去除已知的污染物或非目标基团是有用的，例如，宿主DNA，包括线粒体或叶绿体序列**。对于**集中于特定组以进行更深入的分析，也是有用的**。有关更多细节和示例，请参阅[过滤教程](https://docs.qiime2.org/2020.2/tutorials/filtering/)。🌿🐀

### 多序列比对和进化树构建

**Sequence alignment and phylogeny building**

通常多样性分析依赖于个体特征之间的系统发育相似性。如果你正在进行系统发育标记基因测序（例如，16S rRNA基因），你可以多序列对齐(align)这些序列来评估每个特征之间的系统发育关系。然后这个系统发育树可以被其他下游分析使用，例如UniFrac距离分析。

用于对齐序列和产生系统发育的不同方法展示在下面的流程图中。有关多序列比对/系统发育构建的详细描述，请参阅[q2-phylogeny](https://forum.qiime2.org/t/q2-phylogeny-community-tutorial/4455)和[q2-fragment-insertion](https://library.qiime2.org/plugins/q2-fragment-insertion/16/)教程。 🌳

![image](http://bailab.genetics.ac.cn/markdown/qiime2/fig/2019.7.2.06.png)

现在我们拥有了`有根系统发育树Phylogeny[Rooted]`对象，请注意在接下来的分析中哪些地方用到它 👀

## 多样性分析

**Diversity analysis**

在微生物学实验中，研究人员经常对以下事情感到困惑：

- 我的样本中有多少不同的物种/OTUs/ASVs？
- 每个样本存在多少系统发育多样性？
- 单个样本和样本组有多相似/不同？
- 哪些因素（仅举几个例子，如pH、海拔、血压、身体部位或宿主物种）与微生物组成和多样性的差异相关呢？

还有更多。这些问题可以通过α和β多样性分析来回答。Alpha多样性测量单个样本中的多样性水平。β多样性测量样本之间的多样性或差异程度。然后我们可以使用统计检验来说明样本组之间的α多样性是否不同（例如，指出哪些组具有更多/更少的物种丰富度）以及组之间的β多样性是否显著差异（例如，确定一个组中的样本比另一个组中的样本更相似），通过这些结果来证明这些组中的成员正在形成一个特定的微生物组成。

QIIME 2中不同类型的多样性分析在[人体各部微生物组教程](https://docs.qiime2.org/2020.2/tutorials/moving-pictures/#moving-pics-diversity)和[粪菌移植教程](https://docs.qiime2.org/2020.2/tutorials/fmt/#fmt-diversity)中进行演示，这里将演示用于生成多样性对象的全套分析（并非全部：注意，其他插件可以在这些对象上进一步分析，本指南中也将进一步说明）：

![image](http://bailab.genetics.ac.cn/markdown/qiime2/fig/2019.7.2.07.png)

`q2-diversity`插件包含[许多有用的功能](https://docs.qiime2.org/2020.2/plugins/available/diversity/)！了解他们可以干什么很重要。正如您在流程图中看到的，`diversity core-metrics*`流程（`core-metrics` 和 `core-metrics-phylogenetic`）包含许多不同的核心多样性命令，并且在这个过程中产生可用于下游分析的重要对象。它们是：

- 样本数据-α多样性`SampleData[AlphaDiversity]`对象，其中包含特征表中每个样本的α多样性估计。这是α多样性分析的核心对象。
- 距离矩阵`DistanceMatrix`对象，包含特征表中每对样本之间的成对距离/差异。这是β多样性分析的核心对象。
- 主坐标结果`PCoAResults`对象，包含每个距离/不同度量的主坐标排序结果。主坐标分析是一种降维技术，有助于在二维或三维空间中进行样本相似度或差异的可视化比较。

这些是与多样性相关的主要对象。记住它们的名字和保存位置！我们将在各种下游分析中，或在流程图中所示的`q2-diversity`的各种操作中用到这些数据。这些功能大部分操作会在人体各部位微生物组教程中演示，所以请继续加油学习更多姿势吧！☔

> 注意，在QIIME 2中有许多不同的[α和β多样性度量方法](https://forum.qiime2.org/t/alpha-and-beta-diversity-explanations-and-commands/2282)。要了解更多，并找出你应该引用谁的论文，请点击前面的链接跳转网页。感谢斯蒂芬妮的辛苦总结整理！ 😁🙏😁🙏😁🙏

## 玩转特征表

**Fun with feature tables**

此时，你有一个特征表、物种分类结果、α多样性和β多样性结果。哦，Word天哪，这些结果我居然都分析分析出来啦！ 🤓

如上所述，物种和多样性分析是大多数QIIME 2用户需要执行的基本分析类型。然而，这仅仅是分析的开始，还有很多更高级的分析等待我们去挖掘和探索。🖐️⌨️

![image](http://bailab.genetics.ac.cn/markdown/qiime2/fig/2019.7.2.08.png)

我们这里只是给出一个简要的概述，因为每种分析都有自己详细的教程来指导我们：

- **分析纵向数据**：[`q2-longitudinal`](https://docs.qiime2.org/2020.2/tutorials/longitudinal/)是一个用于执行纵向时间序列实验的统计分析插件，也就是说，样本是随着时间重复地从单个患者/受试者/站点收集的。这包括对α和β多样性的纵向研究，以及一些非常棒的交互式图形。📈🍝
- **预测未来（或过去）** 🔮：[`q2-sample-classifier`](https://docs.qiime2.org/2020.2/tutorials/sample-classifier/)是用于特征数据机器学习🤖 分析的插件。支持分类和回归模型。这允许您执行以下操作：
    - 根据特征数据预测样本元数据。例如，我们能否使用粪便样本预测癌症易感性？或者根据发酵前葡萄的微生物组成预测葡萄酒质量？🍇
    - 识别和预测不同样本的特征。🚀
    - 量化微生物组发育阶段。例如，跟踪婴儿肠道中正常的微生物组发育受持续营养不良、抗生素、饮食和分娩方式的影响。👶
    - 预测异常值和标签错误的样本。👹（详者注：这在大规模研究中尤为重要，排除错误才可能找到真相）
- **丰度差异分析**用于确定在不同样本组中哪些特征显著更多或更少。QIIME 2目前支持几种不同的差异丰度统计检验方法，包括[ANCOM](https://docs.qiime2.org/2020.2/tutorials/moving-pictures/#ancom)（`q2-composition`中的一个功能）和[`q2-gneiss`](https://docs.qiime2.org/2020.2/tutorials/gneiss/) 👾👾👾
- **数据评估和质量控制**：[`q2-quality-control`](https://docs.qiime2.org/2020.2/tutorials/quality-control/)是数据评估和质量控制的插件。它包括以下功能：
    - 测试不同生物信息学或分子方法的准确性，或批次(run-to-run)的变异。常用于研究组成已知的样本，如人工合成群体(mock communities，模拟群体，即人为按一定比例混合多种微生物的合成群体)，可以研究观察值和预期组成、序列等之间的相似性，来评估实验、分析方法对结果的影响等。以及更多有创造力的实验和应用...🐢
    - 基于对参考数据库或包含特定DNA短片段(例如，引物序列)比对，进行序列的过滤。这对于去除特定生物组成序列、非目标DNA或其他无意义序列非常有效。🙃

本节只是一个简单的Qiime 2概述！Qiime 2正在持续开发中，因此请继续关注未来发布版本中的更多插件📻，并关注继续扩展Qiime 2中可用的第三方插件。👀

现在开始享受分析的愉悦之旅吧！💃


## 译者简介

**刘永鑫**，博士。2008年毕业于东北农大微生物学，2014年于中科院遗传发育所获生物信息学博士，2016年遗传学博士后出站留所工作，任宏基因组学实验室工程师。目前主要研究方向为宏基因组数据分析和植物微生物组，QIIME 2项目参与人。目前在***Science、Nature Biotechnology、Current Opinion in Microbiology***等杂志发表论文二十余篇。2017年7月创办“宏基因组”公众号，目前分享宏基因组、扩增子原创文章500余篇，代表博文有[《扩增子图表解读、分析流程和统计绘图三部曲(21篇)》](https://mp.weixin.qq.com/s/u7PQn2ilsgmA6Ayu-oP1tw)、[《Nature综述：手把手教你分析菌群数据(1.8万字)》](https://mp.weixin.qq.com/s/F8Anj9djawaFEUQKkdE1lg)、[《QIIME2中文教程(22篇)》](https://mp.weixin.qq.com/s/UFLNaJtFPH-eyd1bLRiPTQ)等，关注人数8万+，累计阅读1200万+。

## Reference

https://docs.qiime2.org/2020.2/tutorials/overview/#taxonomy-classification-and-taxonomic-analyses

Evan Bolyen*, Jai Ram Rideout*, Matthew R. Dillon*, Nicholas A. Bokulich*, Christian C. Abnet, Gabriel A. Al-Ghalith, Harriet Alexander, Eric J. Alm, Manimozhiyan Arumugam, Francesco Asnicar, Yang Bai, Jordan E. Bisanz, Kyle Bittinger, Asker Brejnrod, Colin J. Brislawn, C. Titus Brown, Benjamin J. Callahan, Andrés Mauricio Caraballo-Rodríguez, John Chase, Emily K. Cope, Ricardo Da Silva, Christian Diener, Pieter C. Dorrestein, Gavin M. Douglas, Daniel M. Durall, Claire Duvallet, Christian F. Edwardson, Madeleine Ernst, Mehrbod Estaki, Jennifer Fouquier, Julia M. Gauglitz, Sean M. Gibbons, Deanna L. Gibson, Antonio Gonzalez, Kestrel Gorlick, Jiarong Guo, Benjamin Hillmann, Susan Holmes, Hannes Holste, Curtis Huttenhower, Gavin A. Huttley, Stefan Janssen, Alan K. Jarmusch, Lingjing Jiang, Benjamin D. Kaehler, Kyo Bin Kang, Christopher R. Keefe, Paul Keim, Scott T. Kelley, Dan Knights, Irina Koester, Tomasz Kosciolek, Jorden Kreps, Morgan G. I. Langille, Joslynn Lee, Ruth Ley, **Yong-Xin Liu**, Erikka Loftfield, Catherine Lozupone, Massoud Maher, Clarisse Marotz, Bryan D. Martin, Daniel McDonald, Lauren J. McIver, Alexey V. Melnik, Jessica L. Metcalf, Sydney C. Morgan, Jamie T. Morton, Ahmad Turan Naimey, Jose A. Navas-Molina, Louis Felix Nothias, Stephanie B. Orchanian, Talima Pearson, Samuel L. Peoples, Daniel Petras, Mary Lai Preuss, Elmar Pruesse, Lasse Buur Rasmussen, Adam Rivers, Michael S. Robeson, Patrick Rosenthal, Nicola Segata, Michael Shaffer, Arron Shiffer, Rashmi Sinha, Se Jin Song, John R. Spear, Austin D. Swafford, Luke R. Thompson, Pedro J. Torres, Pauline Trinh, Anupriya Tripathi, Peter J. Turnbaugh, Sabah Ul-Hasan, Justin J. J. van der Hooft, Fernando Vargas, Yoshiki Vázquez-Baeza, Emily Vogtmann, Max von Hippel, William Walters, Yunhu Wan, Mingxun Wang, Jonathan Warren, Kyle C. Weber, Charles H. D. Williamson, Amy D. Willis, Zhenjiang Zech Xu, Jesse R. Zaneveld, Yilong Zhang, Qiyun Zhu, Rob Knight & J. Gregory Caporaso#. Reproducible, interactive, scalable and extensible microbiome data science using QIIME 2. ***Nature Biotechnology***. 2019, 37: 852-857. doi:[10.1038/s41587-019-0209-9](https://doi.org/10.1038/s41587-019-0209-9)

## 猜你喜欢

- 10000+: [菌群分析](https://mp.weixin.qq.com/s/F8Anj9djawaFEUQKkdE1lg)  
[宝宝与猫狗](http://mp.weixin.qq.com/s/K3y3an-EaX8iaytmxdzHqA) [提DNA发Nature](http://mp.weixin.qq.com/s/lO5uiMjixJ6aYTjPX-IyaQ) [实验分析谁对结果影响大](http://mp.weixin.qq.com/s/cL_IAoPFfmelKMPMgltrfA)  [Cell微生物专刊](https://mp.weixin.qq.com/s/fN0gpD3bZJDXSp8x4ck-3Q) [肠道指挥大脑](https://mp.weixin.qq.com/s/pZO20VGl3Tf_OtFIbZ-zWw)
- 系列教程：[微生物组入门](http://mp.weixin.qq.com/s/sQyl5EctXFB95Oxg8YIasg) [Biostar](http://mp.weixin.qq.com/s/JL-n2nD6YL8vwuRtTVmQlQ) [微生物组](http://mp.weixin.qq.com/s/li7SdZVaCEyFQF8h6MMh2A)  [宏基因组](http://mp.weixin.qq.com/s/bcyvhFrNr6niqD13rQfZeg) 
- 专业技能：[生信宝典](http://mp.weixin.qq.com/s/2b3_8Vvv7McqCkEfUszW3A) [学术图表](http://mp.weixin.qq.com/s/SCT4oso_vI0UNIJZTaG95g) [高分文章](http://mp.weixin.qq.com/s/kD-x7K4hI5KMgGXikyLt0Q) [不可或缺的人](http://mp.weixin.qq.com/s/1nf7vwyvC3oemkTq_pu87A) 
- 一文读懂：[宏基因组](http://mp.weixin.qq.com/s/Vsm6BJgqsSvxEenIBrGVLw) [寄生虫益处](https://mp.weixin.qq.com/s/hX0K9TOLPnrZ6f8lUoSYag) [进化树](https://mp.weixin.qq.com/s/GV8rU3FZdc8Y-x931k_yrQ)
- 必备技能：[提问](http://mp.weixin.qq.com/s/xCif04bqZB14Z4OvesK0SQ) [搜索](http://mp.weixin.qq.com/s/wn2bqIPgT5UD-GP1qzkJFA)  [Endnote](http://mp.weixin.qq.com/s/SPblPs5ByPdb2C400kIK3w)
- 文献阅读 [热心肠](http://mp.weixin.qq.com/s/1uBeAQ0utxuzTTtfUx_UXA) [SemanticScholar](https://mp.weixin.qq.com/s/gaQiUrRqLpfTXzjyfbua6A) [Geenmedical](https://mp.weixin.qq.com/s/hc8g64aHN7qv8YhVfrsuvQ)
- 扩增子分析：[图表解读](http://mp.weixin.qq.com/s/oiVHO2S1JgYrKXPDU6fH2g) [分析流程](http://mp.weixin.qq.com/s/KrYyy3jjzAL0rQzVfV6h4A) [统计绘图](http://mp.weixin.qq.com/s/6tNePiaDsPPzEBZjiCXIRg) 
- [16S功能预测](http://mp.weixin.qq.com/s/sztbvfdf9wa-3HJXc_m8TQ)   [PICRUSt](https://mp.weixin.qq.com/s/LWtiwBbUCAadMZPaKKDMag)  [FAPROTAX](http://mp.weixin.qq.com/s/J8EwJD_PTDhqRaD7kXlK1A)  [Bugbase](https://mp.weixin.qq.com/s/1WdysPZWo0H6NSYiNpcMUQ) [Tax4Fun](http://mp.weixin.qq.com/s/dzsh44ue93xnAs7gTde7wg)
- 在线工具：[16S预测培养基](http://mp.weixin.qq.com/s/YIrDqNvDX0XMazCGxhH1Lg) [生信绘图](http://mp.weixin.qq.com/s/O0QAQyfxnrXlFLw268B7lg)
- 科研经验：[云笔记](http://mp.weixin.qq.com/s/OnwhWlq3cTycf-W1rxgV7g)  [云协作](http://mp.weixin.qq.com/s/W5By9mZ5PI57_xFfZ_JXiw) [公众号](http://mp.weixin.qq.com/s/hd0sdBDAMqMJsXQs0pIjUg)
- 编程模板: [Shell](http://mp.weixin.qq.com/s/YevGR79NnBAF-xtrqL8gAA)  [R](http://mp.weixin.qq.com/s/OQiE882jM6pVwqTiIjyZ1Q) [Perl](http://mp.weixin.qq.com/s/u2ZmTo-z6cbN-L6KVLYNwg) 
- 生物科普: [肠道细菌](http://mp.weixin.qq.com/s/3T768LA6MWujF4yuzK4MKQ) [人体上的生命](http://mp.weixin.qq.com/s/_DUI6tOYTEq0Wu7K7iRTxw) [生命大跃进](http://mp.weixin.qq.com/s/O_0Il0G_v_aSwkUH_noZVA)  [细胞暗战](http://mp.weixin.qq.com/s/M35ebWAelDIK5Iqib06JzA) [人体奥秘](https://mp.weixin.qq.com/s/xlCdN8il1hcutkYK-42fAQ)  


## 写在后面

为鼓励读者交流、快速解决科研困难，我们建立了“宏基因组”专业讨论群，目前己有国内外5000+ 一线科研人员加入。参与讨论，获得专业解答，欢迎分享此文至朋友圈，并扫码加主编好友带你入群，务必备注“姓名-单位-研究方向-职称/年级”。技术问题寻求帮助，首先阅读[《如何优雅的提问》](http://mp.weixin.qq.com/s/H9gkepap0hy3NNskOkO44w)学习解决问题思路，仍末解决群内讨论，问题不私聊，帮助同行。
![image](http://bailab.genetics.ac.cn/markdown/life/yongxinliu.jpg)

学习扩增子、宏基因组科研思路和分析实战，关注“宏基因组”
![image](http://bailab.genetics.ac.cn/markdown/life/metagenome.jpg)

![image](http://bailab.genetics.ac.cn/markdown/train/1809/201807.jpg)

点击阅读原文，跳转最新文章目录阅读
https://mp.weixin.qq.com/s/5jQspEvH5_4Xmart22gjMA