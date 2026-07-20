# Olive Resource Atlas

Olive Resource Atlas 是一个面向技术研究、知识工程与信息检索场景的轻量化外链资源归集与结构化导航系统。该项目定位于为开发者、技术文档撰写者、研究助理以及信息架构师提供一套可本地部署、可扩展、可版本化的外链管理框架，用于将分散于网络各处的技术文档、规范定义、项目笔记与参考实现按照明确的主题维度进行组织、标注和回溯。

Olive Resource Atlas 并不试图成为另一个搜索引擎或社交书签工具，而是聚焦于“结构化外链集合的长期可维护性”。它通过约定优于配置的目录规则、轻量级元数据标记方案以及基于纯文本的存储格式，使得用户能够在不依赖复杂数据库或云服务的前提下，对大量参考链接进行分主题、分层级、带注释的管理。该项目尤其适合需要频繁处理外部技术资料、维护内部知识库或构建项目文档体系的团队与个人。

## 功能概览

- **多层级外链目录树**：支持按主题、项目、时间或任意自定义维度创建多层嵌套的外链分类结构，每个分类可附带独立的描述说明。

- **富文本注释与摘要**：每条外链记录支持存储标题、简短摘要、关键标签以及阅读优先级标记，便于快速筛选与回顾。

- **自动生成文档导航表**：基于目录结构自动生成 Markdown 格式的导航表格，直接嵌入项目 README 或 Wiki 页面，降低维护成本。

- **外链状态标记**：内置链接可达性检查辅助字段，可手动标记“有效”、“失效”、“需复审”等状态，便于定期清理与更新。

- **标签聚合与快速过滤**：支持为每条外链分配多个标签，并提供按标签聚合统计的能力，帮助用户从不同维度切入查看资源分布。

- **多实例支持**：允许同一套框架下管理多个独立的外链集合（例如“项目 A 参考”、“周报素材”、“面试题库”等），互不干扰且可并行维护。

- **纯文本可版本化存储**：所有资源数据均以 Markdown 和 YAML Frontmatter 形式保存，可直接纳入 Git 版本控制，完整保留变更历史与协作记录。

## 应用场景

- **技术选型与调研归档**：团队在评估多个中间件或框架时，可将官方文档、性能测试报告、社区评测文章等链接按评估维度分类存放，附带对比摘要，便于后续复盘与决策追溯。

- **项目文档外链附录**：开源项目维护者可将外部参考标准、API 规范、相关论文或姊妹项目的链接统一整理至 `references` 目录下，与项目主文档保持同步更新，提升文档完整度。

- **个人知识体系构建**：研究人员或高级工程师可将日常阅读的技术博客、会议演讲视频、在线课程等资源按照自身知识结构（如“分布式系统”、“编译器原理”、“数据库实现”）组织成可检索、可注释的本地资料库，减少信息碎片化。

- **团队周报素材汇总**：技术负责人可要求团队成员将每周阅读的有价值外链提交至共享仓库，由专人归并至 Atlas 系统中，形成团队集体积累的技术雷达，降低信息孤岛风险。

## 快速开始

以下步骤将指导您在本地环境完成 Olive Resource Atlas 的克隆、依赖安装与首次运行。

```bash
# 1. 克隆项目仓库至本地
git clone https://github.com/zerxonhy/olive.git
cd olive

# 2. 安装所需 Python 依赖（建议使用虚拟环境）
python -m venv venv
source venv/bin/activate  # Windows 请使用 venv\Scripts\activate
pip install -r requirements.txt

# 3. 执行初始化脚本，生成示例目录结构与配置文件
python scripts/init_atlas.py --name my_atlas

# 4. 启动本地预览服务（默认监听 8000 端口）
python scripts/serve.py --port 8000

# 5. 打开浏览器访问 http://localhost:8000 查看生成的导航页面
```

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Python | 3.9 或更高 | 核心脚本运行环境，用于生成导航页、检查链接格式及执行自动化任务 |
| Git | 2.25 或更高 | 用于克隆仓库以及利用版本控制管理外链数据的变更历史 |
| pip | 21.0 或更高 | Python 包管理工具，用于安装 requirements.txt 中列出的依赖库 |
| Markdown 解析库 | markdown>=3.4.0 | 用于将外链注释中的 Markdown 文本渲染为 HTML 预览内容 |
| PyYAML | 6.0 或更高 | 用于解析每条外链记录头部的 YAML 格式元数据信息 |
| 现代 Web 浏览器 | 不限 | 用于查看生成的静态导航页面，推荐 Chrome/Firefox/Edge 最新稳定版 |

## 文档导航

| 层面 | 目录/文件 | 回答的问题 |
|---|---|---|
| 用户手册 | `docs/usage/atlas_structure.md` | 如何设计外链目录结构？每条外链记录应包含哪些字段？ |
| 配置参考 | `docs/config/settings_schema.md` | 支持哪些全局配置项？如何自定义标签别名或状态枚举值？ |
| 脚本命令 | `docs/commands/cli_reference.md` | 提供哪些命令行工具？如何批量导入、导出或校验外链？ |
| 范例集合 | `examples/tech_radar/` | 一个完整的外链集合长什么样？如何从零开始构建一个实际主题的 Atlas？ |

## 资源列表

### 核心参考文档（项目内）

<code>https://github.com/zerxonhy/olive/blob/main/jademaple.md</code>

<code>https://github.com/zerxonhy/olive/blob/main/jadenebula.md</code>

<code>https://github.com/zerxonhy/olive/blob/main/lanternforest.md</code>

<code>https://github.com/zerxonhy/olive/blob/main/lanternpixel.md</code>

<code>https://github.com/zerxonhy/olive/blob/main/maplecosmic.md</code>

<code>https://github.com/zerxonhy/olive/blob/main/mapleharbor.md</code>

上述资源链接为 Olive Resource Atlas 项目内部维护的示例外链数据文件，分别对应不同的主题分类与注释模板。用户可参考这些文件的格式与内容结构，替换为自己的外链清单。每个文件均采用统一的 YAML + Markdown 混合格式，包含标题、标签、状态、摘要及正文备注区域。

## 项目结构

```
olive/
├── atlas/                                 # 外链数据根目录，可包含多个子集合
│   ├── default/                           # 默认外链集合
│   │   ├── _meta.yaml                     # 该集合的全局配置（标签别名、默认状态）
│   │   ├── distributed_systems/           # 分布式系统主题目录
│   │   │   ├── consensus/                 # 共识算法子专题
│   │   │   │   ├── raft_explained.md      # 单条外链记录，含 YAML 头
│   │   │   │   └── paxos_notes.md         # 另一条记录
│   │   │   └── messaging/                 # 消息队列子专题
│   │   │       └── kafka_review.md
│   │   ├── database_engineering/          # 数据库工程主题目录
│   │   │   ├── storage_engines/
│   │   │   └── query_optimizers/
│   │   └── programming_languages/         # 编程语言主题目录
│   │       ├── rust/
│   │       └── ocaml/
│   └── research_weekly/                   # 另一个独立的外链集合（周报素材）
│       ├── _meta.yaml
│       └── 2026/
│           ├── week_29.md
│           └── week_30.md
├── scripts/                               # 辅助脚本目录
│   ├── init_atlas.py                      # 初始化新集合的脚本
│   ├── serve.py                           # 本地静态预览服务
│   ├── validate_links.py                  # 校验外链 URL 格式与可达性（手动触发）
│   └── generate_toc.py                    # 根据目录结构自动生成导航表格
├── docs/                                  # 用户文档与设计说明
│   ├── usage/
│   │   ├── atlas_structure.md
│   │   └── metadata_spec.md
│   ├── config/
│   │   └── settings_schema.md
│   ├── commands/
│   │   └── cli_reference.md
│   └── design/
│       └── rationale.md                   # 设计决策与取舍说明
├── examples/                              # 完整示例集合，供新用户参考
│   └── tech_radar/
│       ├── _meta.yaml
│       ├── frontend/
│       └── backend/
├── tests/                                 # 单元测试与集成测试
│   ├── test_parser.py
│   └── test_generator.py
├── requirements.txt                       # Python 依赖清单
├── README.md                              # 项目主文档（本文件）
└── LICENSE                                # MIT 许可证文本
```

## 贡献指南

1.  Fork 本仓库至您的个人账户下，并克隆到本地开发环境中。请确保您已安装上述依赖表格中列出的所有必需组件。

2.  在 `atlas/` 目录下新增或修改外链记录文件时，请严格遵守 `docs/usage/metadata_spec.md` 中定义的 YAML 字段规范，并保持每条记录包含 `title`、`tags`、`status` 三个核心字段。新增主题目录时，需同步更新该集合根目录下的 `_meta.yaml` 文件。

3.  提交变更前，请在本地运行 `python scripts/validate_links.py --atlas_path atlas/default` 执行格式与必填字段校验，确保不会破坏现有导航生成流程。若新增了脚本或文档，请同步更新 `docs/commands/cli_reference.md` 或对应的使用手册。

4.  通过 Pull Request 提交您的贡献，并在 PR 描述中清晰说明本次变更的范围（例如“新增分布式存储专题外链 12 条”或“修复导航表格生成脚本中的路径拼接问题”）。项目维护者会在 3 个工作日内进行审查与合并。

5.  若您希望长期参与维护，可联系项目核心成员申请成为 Collaborator，以便直接管理 `atlas/` 下的数据目录，但仍建议重大变更通过 PR 流程进行集体评审。

## 常见问题

**问：Olive Resource Atlas 是否必须使用 Python 环境？能否仅用纯静态方式管理外链？**

答：Python 环境主要用于运行初始化、校验、导航页生成等自动化辅助脚本，这些脚本并非系统运行时的强制依赖。您完全可以手工创建目录结构并编写 Markdown 文件，仅将 Python 工具视为可选增强手段。不过，使用脚本可大幅降低维护成本并减少人为格式错误，因此强烈建议初次使用时至少执行一次初始化流程。

**问：如何将现有的浏览器书签或 Pocket 收藏批量导入到 Atlas 中？**

答：项目目前未内置直接导入浏览器书签 HTML 或 Pocket 导出文件的功能，但您可借助 `scripts/` 目录下的 `import_from_csv.py` 示例脚本（需自行根据实际导出格式调整字段映射）将 CSV 格式的数据转换为符合 Atlas 记录规范的多条 `.md` 文件。未来版本将考虑提供更通用的导入适配层。

**问：外链记录中的“状态”字段有哪些可选值？如何自定义？**

答：默认状态枚举包括 `active`（有效）、`deprecated`（已废弃）、`broken`（链接失效）、`review`（待复审）。您可以通过修改每个集合根目录下的 `_meta.yaml` 文件中的 `status_enum` 列表来增加或重命名状态值，但需注意保持所有记录文件中的状态值与该列表严格一致，否则校验脚本会报错。

## 许可证

MIT

> 外链数量: 6 | 生成时间: 2026-07-21 04:26:58
