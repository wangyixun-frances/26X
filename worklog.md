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
- 今天：和claude聊聊决定具体方向，create sample of athletes to follow up?


