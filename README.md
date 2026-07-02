# 论文知识图谱观测台

本仓库用于整理一个论文知识图谱项目的公开演示版本。项目围绕大规模论文元数据构建 Neo4j 图谱，包含实体清洗、关系建模、增量更新、抽样可视化，以及一个轻量的 GraphRAG-style 检索原型。

在线页面：https://zxccvv114514.github.io/paper-kg-showcase/

![论文知识图谱首页预览](preview-desktop.png)

![GraphRAG 检索原型预览](preview-graphrag.png)

## 项目概览

项目将多源论文元数据整理为以论文为中心的知识图谱。构建流程包括字段抽取、实体归一化、稳定 ID 生成、节点与关系建模、Neo4j CSV/Cypher 导出、本地图数据库验证，以及公开抽样子图的静态 Web 浏览。

当前公开页面只包含抽样数据，用于说明图谱结构和基本交互方式。完整图谱、原始数据、本地数据库文件和非公开材料不包含在仓库中。

## 当前规模

- **107,200** 个论文节点
- **154,144** 个作者实体
- **103,366** 个关键词实体
- **约 1.90M** 条核心关系
- 覆盖 INTERSPEECH、NeurIPS、AAAI、CVPR、ACL、EMNLP、ICML、ICLR 等会议来源
- 支持抽样图谱的搜索、筛选、缩放、节点详情和邻接关系查看

## 构建流程

```text
原始论文元数据
        |
        v
字段抽取与清洗
        |
        v
稳定 ID 生成与实体去重
        |
        v
图谱 Schema 建模
        |
        v
Neo4j CSV / Cypher 导出
        |
        v
本地 Neo4j 验证 + 抽样 Web 页面
```

## 图谱结构

核心节点类型：

- `Paper`
- `Author`
- `Venue`
- `Year`
- `Keyword`
- `Subject`

核心关系类型：

- `(:Paper)-[:AUTHORED_BY {author_order}]->(:Author)`
- `(:Paper)-[:PUBLISHED_IN]->(:Venue)`
- `(:Paper)-[:PUBLISHED_YEAR]->(:Year)`
- `(:Paper)-[:HAS_KEYWORD]->(:Keyword)`
- `(:Paper)-[:HAS_SUBJECT]->(:Subject)`

项目中还保留了 DBLP XML 引用边抽取与诊断流程，后续可以继续接入 OpenAlex、Semantic Scholar、Crossref 或 OpenCitations 等来源补充引用关系。

## 页面功能

- 全屏 Canvas 图谱浏览
- 按会议筛选
- 按节点类型筛选
- 论文、作者、关键词搜索
- 点击节点查看详情
- 查看节点邻接关系
- GraphRAG-style 检索原型：输入研究问题，返回候选论文和图谱证据路径
- 适配桌面端与移动端浏览

## GraphRAG-style 检索原型

页面中的 GraphRAG Lab 是一个轻量原型，主要用于验证论文图谱能否支持更自然的文献检索流程。它不调用外部 LLM、embedding API 或后端服务，而是在浏览器端基于抽样图谱完成以下步骤：

- 基于论文标题、摘要、会议、年份、作者和关键词做文本召回；
- 用 token overlap 作为静态页面中的语义近似基线；
- 利用 `HAS_KEYWORD`、`AUTHORED_BY`、`PUBLISHED_IN`、`PUBLISHED_YEAR` 等关系做图邻域增强；
- 返回候选论文，并给出关键词、作者、会议等证据路径。

这个原型的定位是验证接口和流程。若接入完整 Neo4j 图谱，可以继续替换为真实向量检索、Cypher 邻域扩展、引用边检索和带证据的答案生成。

## 如何测试 Demo

打开在线页面后，可以按下面的顺序测试：

1. 在首页图谱中拖拽、滚轮缩放，确认图谱节点和连边可以交互。
2. 在右上角搜索框输入 `language`、`audio`、`bias` 等关键词，观察图谱是否筛选并保留相关邻接节点。
3. 修改会议筛选，例如选择 `ACL`、`AAAI`、`INTERSPEECH`，查看图谱节点数量变化。
4. 勾选或取消节点类型，例如只保留论文、作者或关键词，检查图谱结构变化。
5. 点击图谱中的节点，查看右侧详情面板和邻接关系按钮。
6. 进入 `GraphRAG` 区域，点击 `LLM 对齐`、`语音 / 音频`、`偏见与推理` 三个示例问题，查看返回论文、分数和证据路径是否变化。
7. 在 GraphRAG Lab 中切换 `关键词匹配`、`语义近似`、`图增强检索` 三种模式，对比返回结果。

如果页面能正常显示图谱、筛选后节点数量会变化、GraphRAG Lab 能返回候选论文和证据路径，就说明公开 Demo 的主要功能是正常的。

## 本地预览

```powershell
cd paper_kg_showcase
python -m http.server 8848 --bind 127.0.0.1
```

然后打开：

```text
http://127.0.0.1:8848/
```

## 仓库内容

```text
paper_kg_showcase/
  index.html                  # 静态交互页面
  assets/graph_data.js         # 公开抽样图谱数据
  README.md                    # 项目说明
  REPRODUCTION_PLAN.md          # GraphRAG-style 检索原型说明
  DEMO_SCRIPT.md               # 演示视频脚本草稿
  DEPLOY_GITHUB_PAGES.md       # GitHub Pages 部署记录
```

## 公开边界

本仓库不包含：

- 原始大规模元数据文件
- 本地 Neo4j 数据库文件
- 数据库连接信息、密钥或本地路径
- 非公开研究材料

仓库仅保留抽样数据、静态页面和项目说明，方便查看项目结构和交互效果。
