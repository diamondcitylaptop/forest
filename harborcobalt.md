# Olive Resource Catalog

Olive Resource Catalog 是一个面向开发者和技术研究人员的轻量级外链资源聚合与导航系统。该项目定位于技术文档、开源仓库、参考资料等外部链接的集中化管理与结构化展示，解决个人或团队在多个项目间分散收藏链接、难以追溯上下文、缺乏版本化记录的问题。通过将外链资源以 Markdown 文件形式托管于 Git 仓库，Olive 提供了一种低维护成本、高可移植性的资源索引方案，适用于技术博客的参考文献管理、项目文档的外部依赖说明、以及知识库的链接资产沉淀。

Olive 本身不依赖任何后端服务或数据库，完全基于静态文件与 Git 工作流。用户可以通过标准的 Git 操作对资源列表进行增删改查，并利用分支、标签、提交历史实现链接变更的可追溯审计。项目默认以 `olive` 作为根仓库名称，所有资源文件按类别或主题平铺于 `main` 分支下的指定目录中，便于快速浏览与批量导入。

## 功能概览

- **外链聚合存储**：提供统一的 Markdown 文件格式规范，用于记录每个外部资源的标题、URL、描述标签、收录日期及维护状态，支持单文件单链接或批量清单两种模式。

- **分类索引机制**：支持通过文件名前缀或目录层级对资源进行逻辑分组，例如按技术领域、优先级、来源机构等维度组织，便于后续脚本自动化处理。

- **版本化追溯能力**：基于 Git 原生能力，每次对资源文件的修改均可附带提交信息，支持通过 `git log` 和 `git diff` 查看特定链接的添加、更新或删除历史。

- **静态站点生成友好**：资源文件采用纯 Markdown 语法编写，可无缝集成到 MkDocs、VitePress、Hugo 等静态站点生成器中，一键生成带搜索功能的在线导航页。

- **链接可达性检查辅助**：项目提供可选的 Shell 脚本示例，利用 `curl` 或 `wget` 批量检测资源列表中的失效链接，并将检查结果输出为单独的报告文件。

- **多仓库关联管理**：允许在资源文件中使用相对路径或绝对 URL 引用同一组织下的其他 Git 仓库，形成跨项目的外链网络，适合微服务架构或 monorepo 场景的文档串联。

- **导入导出兼容性**：资源列表支持与浏览器书签 HTML 格式、Pinboard 导出 JSON、以及 Raindrop.io CSV 格式之间的双向转换（需配合外部转换脚本），降低迁移成本。

## 应用场景

- **技术博客外部参考文献管理**：博主在撰写系列技术文章时，可以将引用的论文、官方文档、Stack Overflow 回答等链接统一收录到 Olive 仓库中，并在文章末尾通过固定链接指向仓库中的对应条目，避免原文链接散落且无法批量更新。

- **开源项目 README 依赖说明索引**：开源项目的维护者可以使用 Olive 集中记录项目所依赖的第三方库主页、API 文档站点、社区论坛地址以及镜像下载源，代替在 README 中罗列大量裸链接，使主文档保持简洁，同时便于贡献者快速找到所有相关外部资源。

- **团队内部知识库外链沉淀**：企业技术团队可以将日常工作中频繁访问的内部 Wiki、Jira 面板、CI/CD 控制台、日志平台、监控仪表盘等地址整理为 Olive 资源列表，配合 Git 仓库权限管理实现团队共享，新成员入职时仅需克隆一份即可获得完整的工具链入口。

- **离线文档打包前置步骤**：在需要生成离线技术文档包（如用于封闭网络环境）时，可先通过 Olive 的资源列表提取所有外链，使用爬取工具将对应页面保存为本地文件，再将离线副本与 Olive 索引一同归档，确保文档的完整性和可浏览性。

- **学术研究文献参考数据库**：研究人员在撰写论文或综述时，可将引用的预印本、数据集仓库、实验代码仓库、以及相关项目主页整理为 Olive 资源清单，通过 Git 标签管理不同草稿版本所对应的参考文献集合，便于后续回溯和交叉验证。

## 快速开始

以下命令演示了从克隆仓库、安装基础依赖到运行本地预览服务的完整流程。Olive 本身为静态资源仓库，无需额外编译，但为便于本地预览，推荐安装轻量级 Markdown 渲染工具。

```bash
# 步骤 1: 克隆仓库到本地
git clone https://github.com/zerxonhy/olive.git
cd olive

# 步骤 2: 安装推荐的 Markdown 预览工具（以 Node.js 的 live-server 为例）
npm install -g live-server

# 步骤 3: 启动本地预览服务，默认监听端口 8080
live-server --port=8080 --entry-file=README.md
```

若不需要本地预览，可以直接使用任意 Markdown 编辑器打开仓库中的 `*.md` 文件进行查看或编辑。对于批量链接检查，可以执行项目根目录下提供的示例脚本：

```bash
# 检查所有资源文件中的链接可达性（需要安装 curl）
bash scripts/check-links.sh
```

## 安装要求

Olive 项目本身对运行环境无强制要求，仅需标准的 Git 客户端即可进行版本管理。以下表格列出了推荐使用的工具以及可选依赖，用于获得更完整的资源管理体验。

| 依赖项 | 必需性 | 说明 |
|--------|--------|------|
| Git (>=2.25) | 必需 | 用于克隆仓库、提交变更、查看历史记录及分支管理。 |
| 任意 Markdown 编辑器 | 必需 | 用于查看和编辑 `.md` 资源文件，推荐 VSCode 或 Typora。 |
| live-server 或类似工具 | 可选 | 提供本地 HTTP 服务，以网页形式预览资源列表的渲染效果。 |
| curl (>=7.68) | 可选 | 用于执行链接可达性检查脚本，检测外部资源是否可访问。 |
| jq (>=1.6) | 可选 | 若需要将资源列表与 JSON 格式互转，则需安装此命令行 JSON 处理器。 |
| Python 3 (>=3.8) | 可选 | 用于运行部分辅助转换脚本（如书签 HTML 转 Markdown 列表）。 |

## 文档导航

下表按照不同使用阶段和读者角色，划分了文档目录结构及其对应的核心问题，帮助用户快速定位所需信息。

| 层面 | 目录/文件 | 回答的问题 |
|------|-----------|------------|
| 入门指南 | `docs/getting-started.md` | 如何第一次克隆仓库并添加第一个资源链接？资源文件的命名规范是什么？ |
| 资源编辑 | `docs/editing-syntax.md` | 每个资源条目应包含哪些字段？如何添加标签和备注？是否支持多行描述？ |
| 链接检查 | `docs/link-verification.md` | 如何批量检查所有链接的有效性？检查结果如何解读？如何自动修复常见失效模式？ |
| 进阶集成 | `docs/integration-guide.md` | 如何将 Olive 资源列表嵌入到 MkDocs 或 VitePress 站点中？如何通过 GitHub Actions 定时检查链接状态并生成报告？ |

## 资源列表

以下为 Olive 资源汇总表中收录的所有外部链接，按主题分组展示。所有 URL 均按照用户提供的原始格式原样列出，未做任何协议、域名或路径的修改。

### 核心技术资源

- <code>https://github.com/zerxonhy/olive/blob/main/gardenrocket.md</code>

- <code>https://github.com/zerxonhy/olive/blob/main/goldenatlas.md</code>

- <code>https://github.com/zerxonhy/olive/blob/main/goldencedar.md</code>

- <code>https://github.com/zerxonhy/olive/blob/main/goldenfalcon.md</code>

### 基础设施与工具

- <code>https://github.com/zerxonhy/olive/blob/main/harborhorizon.md</code>

- <code>https://github.com/zerxonhy/olive/blob/main/horizonlantern.md</code>

## 项目结构

项目目录采用模块化分层设计，根目录下主要包含资源清单、文档、脚本及配置文件夹。以下 ASCII 树状图展示了完整的目录结构及其职责说明。

```
olive/
├── README.md                     # 项目主文档，包含概述、快速开始和基本使用说明
├── LICENSE                       # MIT 许可证文件，声明开源许可条款
├── .gitignore                    # Git 忽略规则，排除临时文件、本地配置和依赖目录
├── docs/                         # 文档目录，存放面向不同用户角色的详细指南
│   ├── getting-started.md        # 入门教程：首次配置与资源添加流程
│   ├── editing-syntax.md         # 资源文件编辑语法规范，字段定义与示例
│   ├── link-verification.md      # 链接检查脚本使用方法与报告解读
│   └── integration-guide.md      # 将资源列表集成到静态站点或 CI 流水线的方案
├── resources/                    # 核心资源清单目录，每个分类对应一个子目录
│   ├── core/                     # 核心技术相关资源（如框架、库、规范）
│   │   ├── gardenrocket.md       # 对应 gardenrocket 资源条目
│   │   ├── goldenatlas.md        # 对应 goldenatlas 资源条目
│   │   ├── goldencedar.md        # 对应 goldencedar 资源条目
│   │   └── goldenfalcon.md       # 对应 goldenfalcon 资源条目
│   └── infra/                    # 基础设施与工具类资源（如监控、CI、容器）
│       ├── harborhorizon.md      # 对应 harborhorizon 资源条目
│       └── horizonlantern.md     # 对应 horizonlantern 资源条目
├── scripts/                      # 辅助脚本目录，存放自动化工具
│   ├── check-links.sh            # 基于 curl 的批量链接可达性检查脚本
│   └── import-bookmarks.py       # 将浏览器书签 HTML 转换为 Olive Markdown 格式的 Python 脚本
└── templates/                    # 资源文件模板目录，提供标准条目格式示例
    └── resource-template.md      # 推荐的资源条目 Markdown 模板，包含必填字段与注释
```

## 贡献指南

我们欢迎并感谢任何形式的贡献，包括但不限于新增或更新资源链接、改进文档、提交脚本增强或报告问题。请遵循以下步骤以确保贡献过程顺畅：

1.  **Fork 本仓库并创建功能分支**：从主仓库的 `main` 分支创建一个新的分支，分支命名建议采用 `feature/resource-name` 或 `fix/description` 格式，以便清晰区分变更类型。

2.  **遵循资源文件格式规范**：在 `resources/` 对应分类目录下添加或修改 `.md` 文件。每个资源条目必须包含标题、原始 URL、收录日期和简要描述。若需新增分类，请同步更新 `docs/editing-syntax.md` 中的分类说明。

3.  **执行链接检查脚本进行验证**：在提交前，请于项目根目录运行 `bash scripts/check-links.sh`，确保新增或修改的链接均可正常访问。若脚本检测到失效链接，请先修复或添加备注说明。

4.  **提交变更并编写清晰的 Commit 信息**：使用 `git commit -m "docs(resources): add xxx link"` 格式，提交信息应简明扼要地说明变更内容和原因，便于后续追溯。

5.  **发起 Pull Request 至主仓库**：将您的分支推送到个人 Fork 仓库，然后通过 GitHub 界面发起 Pull Request 到 `zerxonhy/olive` 的 `main` 分支。请在 PR 描述中简要列出变更点，并关联相关 Issue（如有）。

## 常见问题

**Q: 资源文件中的 URL 链接发生变化时，应该如何处理？**

A: 当发现某个资源链接已失效或永久重定向时，请直接编辑对应的 `.md` 文件，将 `url` 字段更新为最新的有效地址，并在 `remarks` 字段中注明变更日期和原因。提交时使用 `git commit -m "fix(resources): update url for xxx"` 格式。建议定期（例如每月）运行一次链接检查脚本，及时发现并处理失效链接。

**Q: 是否可以将 Olive 资源列表部署为公开的在线导航网站？**

A: 可以。Olive 的 Markdown 资源文件可以直接被 MkDocs、VitePress 或 Hugo 等静态站点生成器读取。推荐使用 VitePress，因为其内置对 Markdown 表格和代码块的良好支持。您只需在 VitePress 配置文件中将 `docs/` 目录设为源目录，并将 `resources/` 目录下的文件通过导航栏或侧边栏进行索引即可。生成后的静态文件可部署到 GitHub Pages、Cloudflare Pages 或任意 Web 服务器上。

**Q: 如何批量导入大量现有书签到 Olive 系统中？**

A: 项目提供了 `scripts/import-bookmarks.py` 辅助脚本，支持从浏览器导出的 HTML 书签文件（兼容 Chrome、Firefox 和 Edge）转换为 Olive 格式的 Markdown 文件。使用方法为：`python scripts/import-bookmarks.py --input bookmarks.html --output resources/core/`。该脚本会自动解析书签文件夹结构，将其映射为分类子目录，并将每个书签转换为独立的 `.md` 文件。对于 JSON 格式的书签导出，可先使用 `jq` 转换为中间格式后再导入。

## 许可证

MIT License

版权所有 (c) 2026 zerkonhy

特此授予任何获得本软件及相关文档文件（"软件"）副本的人免费使用本软件的权利，包括但不限于使用、复制、修改、合并、出版、发行、再许可和/或销售本软件副本的权利，并允许获得本软件的人这样做，但须符合以下条件：

上述版权声明和本许可声明应包含在本软件的所有副本或主要部分中。

本软件按 "原样" 提供，不作任何明示或暗示的保证，包括但不限于适销性、特定用途适用性和非侵权性的保证。在任何情况下，作者或版权持有人均不对因本软件或本软件的使用或其他交易而产生的任何索赔、损害赔偿或其他责任负责，无论是在合同诉讼、侵权诉讼还是其他诉讼中。

> 外链数量: 6 | 生成时间: 2026-07-21 04:27:05
