---
categories: [Tools, Search]
tags: [tool, search]
math: false
mermaid: false
render_with_liquid: false
img_path: 
pin: 
---

# search command

## Google 高级搜索指令：
1. 相关网站搜索 
    related:
2. 网站反向链接查找(来自其它网站进入链接)
    link:
3. 
## 常用搜索技巧（官方）

| 搜索指令 | 功能 | 示例 |
| --- | --- | --- |
| @ | 搜索社交媒体 | @twitter |
| $ | 搜索特定价格 | camera $400 |
| # | 搜索 # 标签 | #throwbackthursday |
| \- | 从搜索结果中排除特定字词 | 马云语录 -女人 |
| "" | 搜索完全匹配的结果 | "tallest building" |
| .. | 在某个数字范围内执行搜索 | camera $50..$100 |
| OR（大写） | 组合搜索 | marathon OR race |
| site: | 搜索特定网站 | site:chongbuluo.com |
| related: | 搜索相关网站 | related:time.com |
| info: | 获取网站详情 | info:giffox.com |
| cache: | 查看网站的 Google 缓存版本 | cache:google.com |

## 常用搜索技巧（补充）

以下补充搜索技巧非出自官方的简明文档，但仍旧为官方承认且截止目前实测仍旧有效，故作补充。

| 搜索指令  |                功能                |              示例               |
| -------- | --------------------------------- | ------------------------------ |
| \|       | 效用等同于 OR  apple               | apple\|google, apple OR google |
| \*       | 泛搜索，表征未知部分，只适用于英文   | \* is the mother of success    |
| 《》      | 只查询图书、影视作品，只适用于中文   | 《钢铁是怎样炼成的》             |
| def:     | 查询关键词的定义                    | def:diversity / google def:    |
| inurl    | 查找在URL地址里有搜索关键词的页面    | inurl:download                 |
| intitle  | 查找在网页标题里有搜索关键词的页面   | intitle:                       |
| filetype | 查找特定文件格式的结果              | 机器学习 filetype:csv           |
| link:    | 查看网站的反向链接                  | link:chongbuluo.com            |
| AROUND   | 搜索包含给定单词之间最大分隔数的网页 | 华为 AROUND(5) 必然             |

注意：如果你在使用 Google 搜索时，将界面语言选择为简体中文，这时使用 `def:` 则会出现一些意外状况，即第一条结果并非显示关键词的定义。比如 `def:download`。所以更通用的做法推荐使用 `关键词 def` 的形式。