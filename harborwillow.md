# Olive Atlas

Olive Atlas 是一个面向技术文档工作者与知识库维护者的结构化外链汇总与资源导航工具。它定位于解决分散在多个仓库、多个文档中的外部参考链接难以统一管理、版本追踪和上下文追溯的问题。项目通过一组预定义的 Markdown 清单文件（atlas manifests），将零散的技术文章、规格说明、社区讨论和镜像站点等资源，组织为可机器读取、可人工审阅的索引体系。

本项目适合需要长期维护技术选型记录、外部依赖说明或学习路径指引的团队或个人。Olive Atlas 本身不渲染页面，也不提供搜索界面，它专注于提供一套严谨的、基于 Git 工作流的资源清单管理范式，使外部链接能够像代码一样接受变更审查、版本标记和问题关联。

## 功能概览

- **清单驱动索引**：每个清单文件（如 islandfield.md）是一个按类别组织的 Markdown 列表，记录资源标题、URL、简短描述和录入原因，便于人工编辑和脚本解析。
- **双向上下文追溯**：通过清单文件的提交历史和 Git 注释，可追溯每条外链的添加时间、修改记录和关联议题，解决“为什么添加这个链接”的溯源问题。
- **分类标签体系**：内置推荐的技术领域标签（如 #frontend, #devops, #protocol），支持按标签进行快速 grep 过滤或生成子索引。
- **状态标记管理**：支持为每条链接标记状态（如 stable, deprecated, review），方便定期清理失效或过时资源。
- **轻量级校验工具**：附带一个简单的 Shell 脚本，可批量检查清单中所有 URL 的可访问性（HTTP 状态码），并生成报告。
- **Markdown 原生兼容**：所有清单文件使用标准 Markdown 语法，可在 GitHub、GitLab 等平台直接预览，无需额外解析工具。
- **扩展元数据支持**：清单条目可附加可选的 YAML Frontmatter 或 HTML 注释，用于记录优先级、维护人、到期提醒等自定义信息。

## 应用场景

- **技术选型参考索引**：团队在评估多个中间件或数据库时，将官方文档、性能对比文章、社区案例等链接统一收录，形成选型依据的时间线记录。
- **微服务依赖关系归档**：在大型微服务架构中，将每个服务所依赖的外部库、API 网关、配置中心等文档链接，按服务模块分别整理，便于新人理解系统全貌。
- **学习路径资源集合**：教育机构或技术社区维护特定方向（如 Rust 入门、Kubernetes 运维）的推荐阅读清单，按难度或主题组织，并持续更新。
- **离线文档镜像导航**：对于内网开发环境，将官方文档的离线镜像站地址、内部翻译版本链接进行统一登记，解决外网访问受限问题。

## 快速开始

以下步骤将获取项目仓库并运行基础校验工具。

```bash
# 1. 克隆仓库
git clone https://github.com/zerxonhy/olive.git
cd olive

# 2. 安装依赖（校验工具依赖 curl 和 parallel）
# 检查系统是否已安装 curl 和 GNU parallel
command -v curl >/dev/null 2>&1 || { echo "需要安装 curl"; exit 1; }
command -v parallel >/dev/null 2>&1 || { echo "建议安装 GNU parallel 以加速校验"; }

# 3. 运行校验脚本，检查所有清单文件中的 URL 可达性
chmod +x scripts/check-urls.sh
./scripts/check-urls.sh ./**/*.md
```

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Git | 2.20 及以上 | 用于克隆仓库和查看文件历史 |
| Bash | 4.0 及以上 | 运行辅助脚本的 Shell 环境 |
| curl | 7.60 及以上 | 校验脚本依赖其进行 HTTP 请求 |
| GNU parallel | 可选，建议 2018 以上版本 | 加速并发 URL 检查，若未安装则脚本回退为串行 |
| Markdown 预览器 | 任意支持 GitHub Flavored Markdown 的查看器 | 用于本地预览清单内容，如 VS Code 插件或 Typora |
| grep | 3.0 及以上 | 用于标签过滤和状态查询的辅助命令 |

## 文档导航

| 层面 | 目录/文件 | 回答的问题 |
|---|---|---|
| 索引定义 | `/manifests/` 目录下的所有 `.md` 文件 | 各类外部资源按什么分类？每个清单包含哪些具体链接？ |
| 操作指南 | `/docs/usage.md` | 如何添加新清单？如何更新链接状态？如何生成校验报告？ |
| 规范说明 | `/docs/spec.md` | 清单文件内部的 Markdown 格式有何要求？元数据如何标注？ |
| 维护流程 | `/docs/maintenance.md` | 链接失效时的处理流程是什么？周期审查如何执行？ |

## 资源列表

本项目的核心资源清单文件位于 `main` 分支的根目录下，直接包含技术参考链接的原始数据。以下清单文件由项目维护，收录了当前批次（第 26/107 批）的外部资源条目。

### 清单文件索引

<code>https://github.com/zerxonhy/olive/blob/main/islandfield.md</code>

<code>https://github.com/zerxonhy/olive/blob/main/jadeatlas.md</code>

<code>https://github.com/zerxonhy/olive/blob/main/jademaple.md</code>

<code>https://github.com/zerxonhy/olive/blob/main/jadenebula.md</code>

<code>https://github.com/zerxonhy/olive/blob/main/lanternforest.md</code>

<code>https://github.com/zerxonhy/olive/blob/main/lanternpixel.md</code>

上述清单文件均遵循项目规范，每个文件对应一个独立的技术领域或主题类别。使用者可直接通过浏览器访问上述 GitHub 链接查看原始清单内容，也可通过 Git 命令本地检出并解析。

## 项目结构

```
olive/
├── manifests/                         # 核心清单目录，存放所有 .md 资源索引
│   ├── islandfield.md                 # 后端服务与中间件相关资源
│   ├── jadeatlas.md                   # 前端工程化与UI框架资源
│   ├── jademaple.md                   # 数据存储与数据库技术资源
│   ├── jadenebula.md                  # 云原生与容器化生态资源
│   ├── lanternforest.md               # 网络协议与安全技术资源
│   └── lanternpixel.md                # 多媒体处理与图形学资源
├── scripts/                           # 辅助工具脚本
│   ├── check-urls.sh                  # 批量检查清单中URL状态
│   └── generate-report.sh             # 根据校验结果生成CSV报告
├── docs/                              # 项目文档
│   ├── usage.md                       # 详细使用指南
│   ├── spec.md                        # 清单文件格式规范
│   └── maintenance.md                 # 维护周期与流程说明
├── templates/                         # 新清单文件模板
│   └── manifest-template.md           # 包含必填字段和示例条目
├── tests/                             # 单元测试与校验规则测试
│   ├── test_url_parser.sh             # 测试URL解析逻辑
│   └── fixtures/                      # 测试用的样本清单文件
├── .github/                           # GitHub 社区配置
│   ├── ISSUE_TEMPLATE/                # 问题与建议模板
│   └── PULL_REQUEST_TEMPLATE.md       # PR 描述模板
├── .gitignore                         # Git忽略规则
└── README.md                          # 项目入口说明文档（本文件）
```

## 贡献指南

1.  **克隆仓库并创建特性分支**：从 `main` 分支创建新的分支，分支名请简要描述修改内容，例如 `feat/add-new-list` 或 `fix/broken-link`。
2.  **编辑或新增清单文件**：严格按照 `/docs/spec.md` 中定义的格式编辑 `.md` 清单文件。添加新链接时，请确保提供完整的 URL、标题以及简短的上文描述。若新增分类，需同步更新根目录的索引说明。
3.  **运行本地校验**：在提交前，于仓库根目录执行 `./scripts/check-urls.sh`，确保所有新增或修改的链接均可达（返回 HTTP 2xx 或 3xx）。若链接无法访问，请在清单中标记状态或添加注释说明。
4.  **提交变更并发起拉取请求**：提交信息应清晰描述变更内容和原因。发起 PR 后，请填写 PR 模板中的检查项，并等待维护者审阅。维护者将关注链接的长期有效性及分类合理性。
5.  **定期审阅已合并清单**：项目维护者每月会运行校验脚本并创建议题，列出状态异常的链接。届时请相关贡献者及时响应并更新。

## 常见问题

**Q：清单文件中的链接出现 404 或超时，应该如何处理？**

A：首先确认链接是否因网络环境（如内网限制）导致不可达。若公开网络下确实失效，请打开一个议题，说明失效链接所在文件及行号。同时，建议查找替代链接或归档该条目，并在清单中将其状态标记为 `deprecated`，附带截至日期。

**Q：是否可以添加非技术类或商业产品的链接？**

A：原则上项目以技术参考和开源生态为主。若商业产品提供详尽的技术文档或开源 SDK 的 GitHub 地址，则允许收录。但纯粹的营销页面、注册引导页或需要付费订阅才能查看内容的核心页面，不予收录。收录前请参考 `/docs/spec.md` 中的“收录准则”。

**Q：如何为清单中的链接添加自定义标签或备注，方便后续检索？**

A：项目推荐在清单条目末尾使用 HTML 注释格式添加元信息，例如 `<!-- tag: database, priority: high -->`。您也可以直接在条目描述中用自然语言标注，例如 `[PostgreSQL Docs](url) - 官方文档，重点参考第 5 章事务隔离`。标签检索可使用 `grep -r "tag: database" manifests/` 实现。

## 许可证

MIT

> 外链数量: 6 | 生成时间: 2026-07-21 04:26:20
