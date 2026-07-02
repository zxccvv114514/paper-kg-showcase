# Paper KG Showcase

这是一个用于保研套磁和科研项目展示的静态项目页，展示“论文知识图谱与科研知识底座构建”项目的核心结果。

项目页地址本地预览：

```powershell
cd paper_kg_showcase
python -m http.server 8848 --bind 127.0.0.1
```

浏览器访问：

```text
http://127.0.0.1:8848/
```

## 项目定位

本项目面向课题组科研文献组织与知识管理需求，独立完成从论文元数据解析、实体归一化、Neo4j 入库、动态增量更新到 Web 可视化展示的完整流程。

展示页使用抽样图谱数据，不包含原始大规模数据文件，也不依赖本地 Neo4j 服务，适合部署到 GitHub Pages。

## 预览

![Paper KG desktop preview](preview-desktop.png)

## 关键规模

- 输入论文记录：121,940
- 入库论文节点：107,200
- 作者实体：154,144
- 关键词实体：103,366
- 关系规模：约 190 万
- 覆盖来源：INTERSPEECH、NeurIPS、AAAI、CVPR、ACL、EMNLP、ICML、ICLR 等

## 核心能力

- 大规模论文元数据解析与字段清洗
- DOI、arXiv ID、DBLP key、标题归一化等多标识去重
- Paper、Author、Venue、Keyword、Subject、Year 等图谱 Schema 设计
- Neo4j CSV/Cypher 导入、约束创建与入库验收
- 新增论文 JSON/JSONL 的动态增量 MERGE 更新
- DBLP XML 引用边抽取逻辑与匹配诊断
- 轻量 Web 图谱可视化 Demo

## 目录结构

```text
paper_kg_showcase/
  index.html                 # 静态展示页和交互图谱
  assets/graph_data.js        # 抽样演示图谱数据
  README.md                   # 项目页说明
  RESUME_SNIPPET.md           # 简历可复制文案
  DEMO_SCRIPT.md              # 1 分钟录屏/面试讲稿
  DEPLOY_GITHUB_PAGES.md      # GitHub Pages 部署步骤
```

## 简历建议写法

> 论文知识图谱与科研知识底座构建｜独立完成  
> 面向课题组科研文献组织与知识管理需求，独立设计并实现论文知识图谱构建与动态更新系统；完成十万级论文数据的实体建模、关系组织、去重匹配、图数据库导入与可视化展示，形成可复现脚本、增量更新流程、验收文档与 Web Demo。

## 公开注意

如果部署到公开 GitHub 仓库，不要上传：

- 原始论文大数据文件
- 课题组未公开数据
- 账号、密码、Neo4j 连接信息
- 任何不适合公开的实验材料

当前展示页只包含抽样演示数据和项目说明，适合公开展示。
