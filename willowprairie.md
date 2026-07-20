# Olive Link Atlas

Olive Link Atlas 是一个面向开发者、技术内容策展人与开源项目维护者的结构化外链资源归集系统。它不提供新的内容创作范式，而是解决一个长期存在于技术社区中的基础效率问题：当项目文档、技术博客、讨论帖与参考链接分散在数十个标签页与书签文件夹中时，如何以可维护、可版本控制、可团队协作的方式，将这些外部资源与项目自身的知识体系进行统一映射。

本项目的目标用户包括：维护大型技术文档站点的文档工程师、需要管理多仓库依赖与参考链接的开源项目维护者、以及希望建立个人技术知识外链数据库的研究者。Olive Link Atlas 通过将外链资源抽象为独立的 Markdown 记录文件，配合索引机制与自动化检查脚本，使得链接的增删改查可以像代码提交一样被追踪、审查与回滚，从而将外链管理纳入正规的软件开发工作流。

## 功能概览

- **基于文件的链接记录系统**：每条外链资源以独立 Markdown 文件存储于指定目录，包含元数据头（标题、分类、状态、添加日期）与正文备注，支持人类直接阅读与编辑。

- **自动化链接状态检查**：集成定时任务脚本，对记录的所有外链进行 HTTP 状态码探测，自动标记失效链接（如 404、500），并生成报告供维护者批量处理。

- **分类标签与多维度筛选**：内置分类体系（如文档、工具、社区、参考），每条链接可附加多个自定义标签，支持通过目录结构或简单 grep 命令完成多维度筛选。

- **版本控制友好**：所有记录均为纯文本 Markdown 格式，完全适配 Git 工作流。变更历史、提交说明、合并请求评审均可用于链接增删改的全过程。

- **链接关系图谱生成**：提供辅助脚本，可扫描所有记录文件中的相互引用关系，输出简单的关系列表，便于发现链接之间的关联脉络。

- **Markdown 语法严格校验**：内置校验规则，确保记录文件中的每个 URL 符合预期格式（如禁止自动补全协议、禁止大小写错误），避免因格式不一致导致的解析异常。

## 应用场景

1. **技术文档站点的外链管理**：当项目文档中引用了大量第三方库、API 参考或社区教程时，使用 Olive Link Atlas 维护一个独立的链接清单。文档中的外链统一引用清单中的标识符，当外部资源地址变更时，仅需修改清单文件，无需逐个翻阅文档页面。

2. **开源项目的资源聚合页**：在项目 README 或官网中维护一个“生态资源”板块，但苦于链接繁杂难以维护。Olive Link Atlas 可作为后台数据源，通过脚本自动生成资源列表的 Markdown 片段，直接嵌入项目文档。

3. **个人技术知识库的外链备份**：研究员或高级开发者通常积累了大量技术书签。利用本系统按主题分类存储，并定期运行链接检查脚本，及时清理失效资源，避免知识库随时间贬值。

4. **团队内部的公共链接库**：在团队仓库中建立统一的链接记录目录，所有成员在发现有用资源时按规范添加。代码审查流程同时审查链接质量，保证团队共享资源池的长期可用性。

## 快速开始

以下步骤适用于 Linux 与 macOS 环境。Windows 用户建议使用 WSL2 或 Git Bash。

```bash
# 1. 克隆项目仓库
git clone https://github.com/your-org/olive-link-atlas.git
cd olive-link-atlas

# 2. 安装依赖（Python 3.9+ 与 pip）
pip install -r requirements.txt

# 3. 初始化本地链接数据库（创建目录结构与示例记录）
python scripts/init_db.py

# 4. 运行链接状态检查（示例）
python scripts/check_links.py --source ./records --report ./reports

# 5. 生成资源列表索引（用于 README 或文档）
python scripts/build_index.py --input ./records --output ./index.md
```

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---------|---------|------|
| Python | 3.9 及以上 | 脚本运行与链接检查引擎 |
| pip | 21.0 及以上 | Python 包依赖管理 |
| Git | 2.25 及以上 | 版本控制与协作基础 |
| curl | 7.68 及以上 | 备选链接探测工具（可选） |
| make | 3.81 及以上 | 自动化任务运行器（可选） |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|-----------|
| 用户手册 | docs/user-guide.md | 如何添加、编辑、删除链接记录？如何运行检查脚本？ |
| 维护指南 | docs/maintainer-guide.md | 如何批量更新失效链接？如何合并链接变更的 Pull Request？ |
| 设计文档 | docs/design.md | 为什么选择纯文件存储？索引机制如何工作？关系图谱算法简述 |
| 贡献规范 | CONTRIBUTING.md | 提交记录的文件格式规范是什么？命名规则与标签体系如何定义？ |

## 资源列表

官方资源库

<code>https://github.com/zerxonhy/olive/blob/main/pixeljade.md</code>

<code>https://github.com/zerxonhy/olive/blob/main/pixelpearl.md</code>

<code>https://github.com/zerxonhy/olive/blob/main/prairiewillow.md</code>

<code>https://github.com/zerxonhy/olive/blob/main/quartzhorizon.md</code>

<code>https://github.com/zerxonhy/olive/blob/main/quartzjade.md</code>

<code>https://github.com/zerxonhy/olive/blob/main/quartznebula.md</code>

## 项目结构

```
olive-link-atlas/
├── records/                         # 链接记录主目录
│   ├── docs/                        # 文档类资源记录
│   │   ├── pixeljade.md             # 示例记录：PixelJade 文档
│   │   └── quartzhorizon.md         # 示例记录：QuartzHorizon 手册
│   ├── tools/                       # 工具类资源记录
│   │   ├── pixelpearl.md            # 示例记录：PixelPearl 工具集
│   │   └── quartzjade.md            # 示例记录：QuartzJade 框架
│   └── community/                   # 社区讨论资源记录
│       ├── prairiewillow.md         # 示例记录：PrairieWillow 论坛
│       └── quartznebula.md          # 示例记录：QuartzNebula 社区
├── scripts/                         # 辅助脚本集合
│   ├── check_links.py               # 链接状态批量检查主脚本
│   ├── init_db.py                   # 初始化本地记录目录与模板
│   ├── build_index.py               # 从记录生成 Markdown 索引
│   └── utils/                       # 公用函数库
│       ├── http_client.py           # 异步 HTTP 探测封装
│       └── parsers.py               # 记录文件元数据解析器
├── tests/                           # 单元测试与集成测试
│   ├── test_check_links.py          # 链接检查功能测试
│   └── fixtures/                    # 测试用的示例记录文件
├── reports/                         # 检查报告输出目录（自动生成）
│   ├── latest_report.json           # 最新链接状态报告
│   └── history/                     # 历史报告归档
├── docs/                            # 项目文档
│   ├── user-guide.md
│   ├── maintainer-guide.md
│   └── design.md
├── requirements.txt                 # Python 依赖清单
├── Makefile                         # 常用任务快捷命令
└── README.md                        # 项目介绍（本文件）
```

## 贡献指南

欢迎并感谢任何形式的贡献。请遵循以下步骤以确保协作流程顺畅：

1. 阅读贡献规范文档（CONTRIBUTING.md），了解记录文件的格式标准、标签分类约定以及命名规则。所有新增或修改的记录文件必须通过格式校验脚本。

2. 从 issue 列表中选择或自行提出待处理的链接变更需求。对于新增链接，需提供链接标题、原始 URL、分类标签及简要说明。对于失效链接，需确认资源是否已迁移或彻底关闭。

3. 在本地分支上进行修改，并运行链接检查脚本验证所有记录（包括未修改部分）的状态。确保本次变更不会引入批量失效链接。

4. 提交 Pull Request，在描述中清晰说明本次链接变更的类型（新增、更新、删除）及理由。至少一位项目维护者将进行评审，重点关注链接的可用性与分类准确性。

5. 合并后，CI 流水线将自动触发全量链接检查，并更新公开的索引页面。若检查发现新增失效链接，将自动回滚合并并通知提交者。

## 常见问题

**Q：本项目是否替代传统书签管理工具？**

A：不替代。Olive Link Atlas 面向的是需要版本控制、团队协作与自动化检查的场景，更适合嵌入开发工作流。日常快速访问单个链接仍可使用浏览器书签。本系统的输出（如索引文件）可与书签工具结合使用。

**Q：链接记录的 Markdown 文件格式具体是怎样的？**

A：每条记录必须包含 YAML Front Matter 用于存储元数据，格式如下：
```
---
title: 资源标题
url: 原始URL（必须与原字符串完全一致）
category: docs | tools | community
tags: [tag1, tag2]
status: active | archived
added: YYYY-MM-DD
---
正文备注内容，可包含多段说明或使用要点。
```
校验脚本会严格检查 url 字段是否与原格式一致，禁止自动补全协议或大小写转换。

**Q：如何批量处理大量失效链接？**

A：运行 `python scripts/check_links.py --source ./records --report ./reports` 生成 JSON 报告后，可使用 `--fix` 参数尝试自动更新已知迁移地址，或使用 `--mark-archived` 将全部失效链接标记为 archived 状态，便于后续人工逐一复查。建议在测试分支上先行验证。

## 许可证

MIT

> 外链数量: 6 | 生成时间: 2026-07-21 04:26:20
