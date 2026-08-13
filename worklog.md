8.3
- 下载了2016-2019media cloud上所有包含退役运动员关键词的报道。发现很多下载内容不准确&完全不相关hhh。在jupyter notebook上试图filter出真正正文包括关键词「退役运动员」的报道。
- 排除使用[CFPS China Family Panel Study数据库](https://cfpsdata.pku.edu.cn/#/home)（没有询问是否上体校/职业是否是运动员这一项）来分析退役运动员经济状况/出身等问题。

/// hhh有点绝望甚至想彻底换题目mer

-
8.4
- 排除使用人口普查数据（没有能否确定职业是运动员的项目）
- 通过get_textbody_tags.ipynb提取出了每个新闻媒体网站上对应正文的tag @media_textbody_tags.csv
- 2016-2019根据关键词“退役运动员”筛选出2488条；来自可搜索媒体的共2340条，真正包含“退役运动员”的新闻2条。
    - | title | publish_date | media_name | url | contains_keyword |
|---|---|---|---|---|
| 广东中山：2020年全市将有超303个足球场 | 2018-07-03 | chinanews.com | http://www.chinanews.com/sh/2018/07-03/8555102... | 1 |
| "体操皇后"霍尔金娜：在"有限"里造出个"无限"来 | 2018-07-09 | people.com.cn | http://sports.people.com.cn/n1/2018/0709/c2215... | 1 |
- 结论：media cloud不行？ + 新闻找不出什么东西


-
8.5 周三
- 和librarian开会，需要明确research方向才能找数据集。估计需要自己多方取材自己搭建数据库。
- 今天：和claude聊聊决定具体方向


A。

//////// 重新定位研究问题："公共话语如何建构运动员" --> 把媒体的极端化变成数据本身,不是干扰。
- 什么情况下运动员会被报道：
- in what tone
- frequency across years
- 次要：可对比国外媒体VS中国媒体对中国运动员的呈现。！
- 次次要：对比中国媒体如何呈现中国运动员 VS 海外运动员。

//////// "报道要么正面要么负面"的直觉 ---> 通过数据证明！
- 计算情感分布的双峰性(bimodality)。如果你能证明报道情感呈U型/双峰分布(两端多、中间少),这本身就是一个可发表的实证发现——你用数据证明了"极化呈现"的存在,而不是断言。可以用 bimodality coefficient 或 dip test 来检验。分析极化是否结构化:是不是金牌项目偏正面(励志)、冷门项目偏负面(困境)?是不是某类成绩层级更容易被极端叙事?一旦极化能被这些变量预测,你的论文就从"描述极化"升级到"解释极化的生成机制"。
//// （有余力可考虑）小型微博数据库对特定热点话题进行大众讨论VS官方报道的比较


方法；
    推荐的方法论:计算文本分析 + 人工编码验证的混合设计

    以你的基础,最能体现水平也最扎实的是混合流程:

    1. 数据采集
    从新闻数据库(如慧科、中国知网的报纸库、或直接爬主流媒体)抓取一个明确时间段(建议10–15年,足够看趋势)、含"退役运动员""退役+运动员姓名"等关键词的报道。社交媒体可作为补充但先聚焦新闻媒体,因为它更规范、去重和作者归属更清晰。给每篇报道打上元数据:日期、媒体、涉及项目、运动员性别、成绩层级。

    2. 框架的操作化——这是全文成败关键
    框架不能拍脑袋定。规范做法是先归纳后演绎:随机抽读100–150篇,用扎根方式提炼出实际存在的框架类型(常见的会是:励志逆袭、生存困境、体制批判、政策成就、中性叙事等),写成带定义和判例的编码手册。

    3. 大规模分类
    你有编程基础,这里有两条路:

    监督学习:人工标注一个训练集(比如800–1500篇),微调一个中文预训练模型(如 BERT-wwm、RoBERTa-wwm-ext)做框架多分类。这是目前的主流做法,准确率和可信度都高。
    LLM 辅助标注:用大模型按你的编码手册对每篇做零样本/少样本分类,再人工抽检校准。省标注成本,但需在方法部分论证可靠性。

    无论哪条,都要保留一个人工双编码的验证子集,报告 Krippendorff's α 或 Cohen's κ,证明你的分类可信。这是审稿人/答辩老师一定会看的点。

    4. 统计分析

    描述:各框架的总体比例、按项目、按年份的分布。
    关系检验:框架类型(分类因变量)对项目类型、时间、性别、成绩层级做多项逻辑回归(multinomial logistic regression),看哪些因素显著预测"困境框架"vs"励志框架"。
    时间趋势:框架比例的时间序列,或以某标志性事件为断点做中断时间序列(interrupted time series),检验事件是否改变了报道倾向。



B. 
选e.g.全运会的50名不用届、不用项目、不同地区的运动员抽样，用媒体搜索他们的名字，获取退役后的处境。


-
8.6周四 + 8.7周五

排除B：
- 条件：如果拿到确切运动员名单之后搜不出有用信息。
- 方式：随便找一个全运会有成绩的运动员，在media cloud搜关于ta的报道。e.g. 第十一届全运会（2009）跳水男子1米跳板金牌王峰
- 结论：排除！通过媒体搜不出来个体运动员的退役处境。


8.8 + 8.10 数据库work

❌ **WiseNews (Wisers / 慧科)**
- no subscription by Dartmouth.

❌ **Nexis Uni / LexisNexis**
- does not contain chinese-language source.

❌ **NewsBank Access World News Research Collection**
- //// (not robust explanation?) limited Chinese language sources compared to the other two.

✅ **CNKI China Core Newspapers Full-text Database(中国重要报纸全文数据库)**
https://search.library.dartmouth.edu/view/action/uresolver.do?operation=resolveService&package_service_id=20911662920005706&institutionId=5706&customerId=5705&VE=true
- "collected and continuously updated more than 726 kinds of important party newspapers, industry newspapers and comprehensive newspapers at all levels published since 2000."

✅ **People's Daily 人民日报**
- official voice of the CCP and gov. since June 1946.
https://data.people.com.cn/rmrb/20220325/1?code=2


✅ **Factiva(Dow Jones)** https://app-dowjones-com.dartmouth.idm.oclc.org/factiva/home?redirect_from=gl
- 425 major chinese media sources. 

//////
    **一个关键提醒(跨库可比性)**:框架分析要求你的语料在时间、媒体类型、检索逻辑上尽量一致。不同库对同一媒体的收录起止时间、去重逻辑差别很大,混用多个库会引入难以控制的异质性。建议**尽量以单一主力库构建核心语料**,其他库只用于补漏或验证,并在方法部分说明清楚检索式、时间范围和库的选择理由——这是框架分析类论文常被审稿人追问的地方。

    **关于社交媒体**:微博没有对应的西方学术数据库,若你要纳入微博做补充,通常得走 API 或第三方舆情工具,数据获取和伦理审查(IRB)都要另行规划。
- DONE. work to choose database. - how to justify my decision.
    - check what sources the datbase has. -> e.g. China Daily. => what the database represents in terms of data.
- check also text scrapability for the databases?
- Systematic Review Method. for going through all possible literature. https://researchguides.dartmouth.edu/sys-reviews
https://guides.mclibrary.duke.edu/sysreview/definition
- construct keywords - search terms + search strings. -> and be consistent for every database.



------
        你能做到的是——用制度诊断框架,论证执行落差的结构性/制度性成因,并用文本重复度提供落差存在的间接证据。这是有真实分析深度的、独立研究者力所能及的、两周可完成的贡献。

        你做不到的是——证明具体的因果链(比如"正是因为没有 X 部门,所以某年某地安置失败"),或给出全国实际安置率这类执行数据。这些要留给未来有访谈和内部数据的研究。你在局限部分诚实地标出这条边界,反而是成熟的表现。你没法证明落差"如何在每个个案中发生",但你完全可以有力地论证落差"为什么在制度上必然容易发生"。对一个想推动政策改善的研究者来说, 后者其实更有用——因为它直接指向该改哪些制度要件。

pivot
- 问题：政策执行上，为什么对运动员的保障措施推行不利。
- 对比军人的待遇和安置政策，因为有特别多共同点。


对比具体政策文件的用语：是否具体。是否强硬。是否真的想把事情办成。


Proof：fixing problems
    对历年政策文件做一个"重复度/新增度"的文本追踪。 —— 把 2010 年至今的运动员政策文件按时间排列,逐年编码每份文件提出的具体措施,标注哪些是新增的、哪些是重复前几年的。如果你能用数据显示:十几年间政策文本高度重复、实质性新增措施极少、且反复出现的都是同样几个未解决的维度(就业、教育、伤残保障)——这个"重复率"本身就是执行落差的间接量化证据:一个被有效执行的政策不需要年年重申。这一步用得上你的文本分析能力,也让"象征性政策"这个论点从断言变成有数据支撑的发现。


8.11 周二

vague idea: policy is there, but implementation is not. 

Background Readings.

Q: 举国体制、retirement policy 如何运作

Q: how are retired athletes treated @now.
- 大部分如果想继续学业需要高考吗///

Q: GOV problem
- Li Mengzi 
    - poor communication between departments
    - no longer fair b/c market-改革 & focus on performance. compared to planned economy.

Q:

arguing that education is important:
- 【after the glory】- "human capital" theory. p/633 Schultz
    - becker - educaton === more productivity b/c more ability




/// implementation studies structure ??