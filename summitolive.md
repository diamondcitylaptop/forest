# Orbit Resource Aggregator

Orbit Resource Aggregator is a curated technical index and external link collection system designed for developers, researchers, and technical writers who need to organize, categorize, and retrieve distributed documentation assets across multiple repositories. The project addresses the common problem of fragmented technical references by providing a structured aggregation layer over diverse markdown-based knowledge bases.

This project targets maintainers of large documentation ecosystems, open-source contributors who need to cross-reference materials across projects, and technical teams that require a centralized lookup system for shared resources without migrating existing content. Orbit does not host or replicate the original resources but provides a consistent navigation and discovery interface over them.

## 功能概览

- **Multi-Source Link Harvesting** - Automatically extracts and normalizes external URLs from markdown files within configured repository branches, supporting both relative and absolute path resolutions.

- **Categorized Index Generation** - Groups collected links into predefined taxonomies such as architecture guides, API references, deployment playbooks, and troubleshooting manuals based on filename patterns and directory structures.

- **Version-Aware Reference Tracking** - Maintains a manifest of last-seen commit hashes for each source file, enabling detection of stale or updated external references.

- **Markdown Metadata Extraction** - Parses YAML frontmatter, heading hierarchies, and code-block annotations from source documents to enrich the index with context tags, difficulty levels, and estimated reading times.

- **Cross-Reference Dependency Mapping** - Builds a directed graph of internal hyperlinks between the aggregated resources to surface related content and identify orphaned pages.

- **Search Query Normalization** - Provides a simple grep-based search interface over titles, descriptions, and tags with support for case-insensitive and partial-match queries.

- **Export to Static Site Format** - Generates a single HTML page or JSON feed from the index for integration into documentation portals, internal wikis, or CI/CD pipeline artifacts.

- **Periodic Refresh Scheduling** - Includes a cron-compatible scheduler script that can be invoked via GitHub Actions or systemd timers to rebuild the index on a daily or weekly cadence.

## 应用场景

1. **Documentation Portal Consolidation** - A technical writing team managing three separate product documentation repositories uses Orbit to generate a unified resource index. Writers can query the index to locate all references to a specific API endpoint across all repositories without opening each project individually.

2. **Onboarding Knowledge Base for New Engineers** - An engineering organization maintains a sprawling internal wiki with hundreds of markdown files. Orbit aggregates links from the wiki's deep directory structure into a flat, searchable table, reducing the time new hires spend discovering existing troubleshooting guides and architectural decision records.

3. **Open-Source Project Dependency Auditing** - A maintainer of a large monorepo wants to identify all external links pointing to deprecated CDN endpoints or unmaintained libraries. Orbit extracts every external URL from the repository's markdown files, allowing the maintainer to run a bulk link-checker script against the aggregated list.

4. **Cross-Repo Release Note Correlation** - A release manager needs to trace feature announcements across multiple component repositories. Orbit indexes the release notes directory from each repo and provides a chronological view with direct links to the original markdown files, simplifying the creation of combined release summaries.

5. **Technical SEO and Link Equity Analysis** - A content strategist for a developer advocacy program uses Orbit to collect all outbound links from blog posts and tutorials. The aggregated list is then analyzed for broken links, redirect chains, and opportunities to add internal backlinks to newer content.

## 快速开始

```bash
# 1. Clone the repository
git clone https://github.com/your-org/orbit-resource-aggregator.git
cd orbit-resource-aggregator

# 2. Install dependencies (Python 3.9+ required)
pip install -r requirements.txt

# 3. Configure source repositories in config.yaml
#    Edit the 'sources' section to point to your target repositories and branches

# 4. Run the aggregation script
python scripts/aggregate.py --config config.yaml --output index.json

# 5. Generate a static HTML overview
python scripts/export_html.py --input index.json --output docs/index.html

# 6. (Optional) Schedule periodic updates
#    Add a cron job or GitHub Actions workflow to run aggregate.py daily
```

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|----------|----------|------|
| Python | 3.9 - 3.11 | 核心运行环境；3.12 尚未经过完整测试 |
| PyYAML | 6.0.1 或更新 | 用于解析 config.yaml 和元数据 frontmatter |
| requests | 2.31.0 或更新 | 用于远程仓库文件获取和链接可达性预检 |
| markdown | 3.5.0 或更新 | 用于提取标题、链接和代码块语言标签 |
| GitPython | 3.1.40 或更新 | 用于本地仓库克隆、分支切换和 commit 哈希读取 |
| pytest | 8.0.0 或更新 | 仅开发测试时需要；生产环境可不安装 |
| ruff | 0.3.0 或更新 | 代码 lint 和格式化工具，仅开发者需要 |
| pre-commit | 3.6.0 或更新 | Git 钩子框架，用于提交前自动检查 |
| pandas | 2.2.0 或更新 | 可选，用于导出 CSV 格式索引报表 |
| jinja2 | 3.1.3 或更新 | 用于 HTML 导出模板渲染 |

## 文档导航

| 层面 | 目录/文件 | 回答的问题 |
|------|-----------|------------|
| 用户手册 | docs/user-guide/configuration.md | 如何配置源仓库路径、分支、包含/排除模式？ |
| 用户手册 | docs/user-guide/output-formats.md | 支持哪些导出格式（JSON、HTML、CSV）？如何自定义模板？ |
| 运维指南 | docs/operations/scheduling.md | 如何设置定期自动刷新？CI/CD 集成的最佳实践是什么？ |
| 开发参考 | docs/development/plugin-architecture.md | 如何编写自定义链接处理器或元数据提取器？ |
| 开发参考 | docs/development/api-reference.md | 核心类（LinkHarvester、IndexBuilder、Exporter）的公开方法签名 |
| 故障排查 | docs/troubleshooting/common-errors.md | 遇到 "repository not found" 或 "invalid ref" 错误时如何解决？ |
| 贡献规范 | CONTRIBUTING.md | 提交 PR 的流程、代码风格检查、commit message 格式要求 |

## 资源列表

### 核心索引源文件

以下 markdown 文件构成了本项目的初始参考资源集合，均托管于外部仓库 zerkonhy/olive。这些文件提供了不同主题的技术笔记、架构片段和配置示例，Orbit 的默认配置中已将这些路径注册为待采集源。

<<code>https://github.com/zerxonhy/olive/blob/main/orbitmidnight.md</code>>

<<code>https://github.com/zerxonhy/olive/blob/main/orbitolive.md</code>>

<<code>https://github.com/zerxonhy/olive/blob/main/orbitpearl.md</code>>

<<code>https://github.com/zerxonhy/olive/blob/main/pearlanchor.md</code>>

<<code>https://github.com/zerxonhy/olive/blob/main/pixelbridge.md</code>>

<<code>https://github.com/zerxonhy/olive/blob/main/pixelgarden.md</code>>

## 项目结构

```
orbit-resource-aggregator/
├── config/                               # 配置文件目录
│   ├── default.yaml                      # 默认全局配置（日志级别、超时、重试策略）
│   ├── sources.yaml                      # 源仓库列表（URL、分支、扫描路径）
│   └── taxonomy.yaml                     # 分类映射规则（关键词到类别）
├── src/                                  # 核心源代码
│   ├── harvester/                        # 链接采集模块
│   │   ├── git_client.py                 # GitPython 封装，处理克隆和拉取
│   │   ├── markdown_parser.py            # 使用 markdown 库提取链接和元数据
│   │   └── filter_engine.py              # 包含/排除模式匹配逻辑
│   ├── index/                            # 索引构建模块
│   │   ├── builder.py                    # 组装索引数据结构（去重、分类、排序）
│   │   ├── graph.py                      # 内部链接依赖图计算
│   │   └── serializer.py                 # 序列化为 JSON/CSV/MessagePack
│   ├── exporters/                        # 输出导出模块
│   │   ├── html_generator.py             # 基于 Jinja2 模板生成静态 HTML
│   │   ├── json_api.py                   # 生成符合 OpenAPI 规范的 JSON 端点
│   │   └── markdown_summary.py           # 生成人类可读的 markdown 汇总报表
│   └── utils/                            # 通用工具函数
│       ├── url_normalizer.py             # 协议、末尾斜杠、锚点清理
│       ├── logger.py                     # 结构化日志（JSON 格式，支持 ELK）
│       └── validator.py                  # 链接可达性检查（HEAD 请求）
├── scripts/                              # 可执行脚本
│   ├── aggregate.py                      # 主入口，执行完整采集-构建-导出流程
│   ├── export_html.py                    # 单独重新生成 HTML 而不重新采集
│   └── check_stale.py                    # 检查源文件 commit 变化，输出变更列表
├── tests/                                # 单元测试和集成测试
│   ├── unit/                             # 针对每个模块的独立测试用例
│   ├── integration/                      # 端到端测试（使用本地 mock 仓库）
│   └── fixtures/                         # 测试用的示例 markdown 文件集合
├── docs/                                 # 用户文档和开发者文档
│   ├── user-guide/                       # 安装、配置、运行、故障排查
│   ├── operations/                       # 备份、恢复、性能调优
│   └── development/                      # 插件开发、贡献指南、API 稳定承诺
├── .github/                              # GitHub Actions 工作流
│   └── workflows/
│       ├── ci.yml                        # 每次 push 运行 lint、test、build
│       └── schedule.yml                  # 每日凌晨 2 点运行 aggregate.py
├── requirements.txt                      # 生产环境依赖列表（固定版本）
├── requirements-dev.txt                  # 开发环境额外依赖（pytest, ruff, pre-commit）
├── pyproject.toml                        # 项目元数据（名称、版本、作者、许可证）
├── Makefile                              # 常用任务快捷命令（install, test, lint, clean）
└── README.md                             # 本文件
```

## 贡献指南

1.  **Fork 仓库并创建功能分支** - 从主分支 checkout 一个新的分支，命名格式为 `feature/描述性名称` 或 `fix/问题编号`。确保分支名称简洁明了，例如 `feature/add-gitlab-support`。

2.  **安装开发依赖并运行测试** - 执行 `pip install -r requirements-dev.txt` 安装所有开发工具。运行 `make test` 确认现有测试全部通过。新增功能或修复缺陷时，需同步编写对应的单元测试，测试覆盖率不应低于 85%。

3.  **更新文档和示例配置** - 如果您的更改影响了配置格式、命令行参数或输出结构，必须同步更新 `docs/` 目录下的相关文档以及 `config/default.yaml` 中的示例值。所有新增加的配置项需要添加注释说明其用途和合法取值。

4.  **提交前运行代码格式化和 Lint** - 使用 `make lint` 调用 ruff 进行静态检查，使用 `make format` 自动修正格式问题。提交信息必须遵循约定式提交规范（Conventional Commits），例如 `feat: add support for SSH git URLs` 或 `fix: handle empty markdown files gracefully`。

5.  **发起 Pull Request 并关联 Issue** - 将您的分支推送到您 fork 的仓库，然后向本仓库的 main 分支发起 PR。PR 描述中应清晰说明变更内容、测试结果以及是否破坏了向后兼容性。如有对应的 GitHub Issue，请在描述中使用 `Closes #issue编号` 进行关联。

## 常见问题

**Q: 采集过程中遇到 "Rate limit exceeded" 错误，如何解决？**

A: 该错误通常来自对 GitHub API 的匿名请求限制（每小时 60 次）。解决方案有两种：一是在 `config/sources.yaml` 中配置个人访问令牌（PAT），通过 `github_token` 字段传入，认证后的限制为每小时 5000 次；二是将源仓库配置为使用 SSH 克隆方式（`git@github.com:...`），并确保本地已缓存了仓库副本，此时仅通过 GitPython 进行本地读取，不会触发 API 速率限制。建议生产环境同时采用 PAT 和本地缓存策略。

**Q: 导出的 HTML 页面中部分链接显示为相对路径，无法正确跳转，怎么处理？**

A: 这是因为源 markdown 文件中的内部链接使用了相对路径（如 `../other.md`），而 Orbit 默认将其原样保留。若需要将相对路径转换为指向源仓库的绝对 URL，请在 `config/default.yaml` 中将 `resolve_relative_links` 设置为 `true`，并在 `sources.yaml` 中为每个源仓库指定 `base_url` 字段（例如 `https://github.com/zerxonhy/olive/blob/main/`）。转换后的链接将拼接为完整 URL 形式，确保在任何环境下均可访问。

**Q: 索引构建速度较慢，尤其是扫描大型仓库时，有没有优化建议？**

A: 首先，使用 `filter_engine` 中的 `exclude_patterns` 排除 `vendor/`、`node_modules/`、`dist/` 等非文档目录，可显著减少扫描文件数。其次，启用 `cache_enabled: true` 会缓存每个文件的最后修改时间戳和提取结果，仅当文件实际变更时才重新解析。最后，考虑将 `max_workers` 参数调整为 4 或 8，启用多线程并行解析（默认单线程）。对于超过 5000 个 markdown 文件的仓库，建议将扫描分批执行，或使用 `--since` 参数仅增量处理最近提交。

## 许可证

MIT

> 外链数量: 6 | 生成时间: 2026-07-21 04:26:20
