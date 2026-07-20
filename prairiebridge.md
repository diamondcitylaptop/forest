# Olive Link Atlas

Olive Link Atlas 是一个面向技术内容策展人与开源文档维护者的结构化外链资源聚合工具。该项目不提供新的技术框架或算法，而是解决一个长期被忽视的工程问题：分散在多个仓库、Issue 和团队内部 Wiki 中的高价值参考链接，缺乏统一的元数据描述、版本追踪与可用性校验机制。Olive Link Atlas 定位于“链接即代码”的轻量级基础设施，通过将外链资源抽象为可版本化、可审计、可自动化检测的 Markdown 条目，帮助技术团队在文档体系、学习路径编排与依赖关系引用中建立可靠的外部资源索引层。

目标用户包括技术文档工程师、开源项目维护者、技术社区运营人员以及内部知识管理平台的建设者。Olive Link Atlas 不依赖任何外部数据库或云服务，完全基于 Git 仓库与静态 Markdown 文件运行，确保索引数据在任何离线环境下均可完整访问与二次加工。

## 功能概览

**链接条目模板化录入** 提供标准化 Markdown 前头信息块，支持标题、原始 URL、归档日期、内容摘要、标签与关联项目等字段的结构化定义，便于后续自动化工具解析与校验。

**批量链接存活检测** 内置基于 curl 与 HTTP 状态码的轻量级检测脚本，可定期对索引中所有外链发起连通性检查，并生成报告标记失效或重定向的链接，帮助维护者及时更新或移除失效资源。

**多维度标签分类体系** 支持对每个链接条目赋予多个层级标签，例如 编程语言、基础设施、论文、视频教程、官方文档 等，并基于标签生成动态分类视图，便于不同角色的用户快速定位所需资源类型。

**版本历史与变更追踪** 每个链接条目的新增、修改与删除操作均通过 Git 提交记录完整保留，支持按时间范围回溯链接集合的变化状态，满足团队内部审计与变更管理需求。

**自定义输出渲染引擎** 提供可配置的模板引擎，支持将内部索引数据渲染为面向最终用户的纯 HTML 静态站点、面向 CI/CD 流程的 JSON 摘要文件，或面向文档嵌入的纯 Markdown 引用块，无需额外转换工具。

**第三方资源导入适配器** 提供针对常见书签导出格式（HTML 书签、Pinboard JSON、Raindrop.io CSV）的转换脚本，降低从既有收藏体系迁移至 Olive Link Atlas 的成本。

## 应用场景

**技术文档中心的外部参考管理** 当开源项目文档中包含大量指向外部规范、论文或工具站点的引用时，维护者可使用 Olive Link Atlas 建立独立的链接索引仓库。每个索引条目记录原始 URL 及本地缓存摘要，当外部站点变更或下线时，索引检测脚本会及时告警，避免文档中出现大量死链影响用户体验。

**团队内部学习路径编排** 技术培训负责人可将系列教程、视频、交互式练习平台等资源按学习阶段整理为多个索引集合，并通过标签体系标记难度等级与前置依赖。新成员可依照索引顺序进行系统性学习，同时培训负责人可随时增删条目并同步更新学习路径文档。

**多仓库共享资源归一化** 在微服务架构或大型 monorepo 项目中，不同子项目往往重复引用相同的第三方库文档、API 参考或运维手册。Olive Link Atlas 可作为中心化外链注册表，各子项目通过脚本从该索引中按标签筛选所需链接，统一来源，减少冗余维护。

**开源社区内容聚合周报** 社区运营人员可将本周讨论热度较高的外部文章、工具发布公告、相关会议演讲等链接录入索引，并利用渲染引擎一键生成周报 Markdown 草稿，大幅减少手动排版与重复核对 URL 的时间。

## 快速开始

以下命令演示了如何获取 Olive Link Atlas 项目代码、安装基础依赖并执行首次索引初始化。

```bash
# 克隆项目仓库
git clone https://github.com/zerxonhy/olive-link-atlas.git
cd olive-link-atlas

# 安装依赖（Python 3.9+ 与 pip）
python -m venv venv
source venv/bin/activate  # Windows 下为 venv\Scripts\activate
pip install -r requirements.txt

# 执行首次索引构建与本地预览
python atlas.py build --source ./entries --output ./site
python atlas.py serve --port 8000
```

执行完成后，访问 `http://localhost:8000` 即可查看默认的链接索引静态站点。若仅需使用命令行检测工具，可跳过站点构建步骤，直接运行：

```bash
python atlas.py check --entries ./entries --report ./reports/status.json
```

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---------|---------|------|
| Python | 3.9 及以上 | 核心运行环境，用于执行构建、检测与渲染脚本 |
| Git | 2.25 及以上 | 版本控制与变更追踪基础，用于提交记录解析 |
| curl | 7.68 及以上 | 链接存活检测所使用的底层 HTTP 请求工具 |
| Markdown 解析库 | Python-markdown 3.3.6 | 用于将索引条目前头信息与正文内容分离解析 |
| Jinja2 | 3.0.0 及以上 | 模板渲染引擎，负责将索引数据转换为 HTML 或 JSON 输出 |
| pytest | 7.0.0 及以上 | 可选依赖，仅在运行单元测试与集成测试时需要 |

## 文档导航

| 层面 | 目录位置 | 回答的问题 |
|------|----------|------------|
| 用户手册 | docs/user-guide/ | 如何录入新链接、如何运行检测、如何自定义输出模板 |
| 管理员指南 | docs/admin-guide/ | 如何部署私有索引服务、如何配置 CI 自动检测流水线 |
| 开发者文档 | docs/developer-guide/ | 如何扩展导入适配器、如何增加新的输出格式插件 |
| 设计决策记录 | docs/adr/ | 为何选择 Markdown 作为存储格式、为何不采用数据库方案、标签体系的设计权衡 |
| 常见工作流示例 | docs/examples/ | 从浏览器书签导入、从 Notion 数据库迁移、与 MkDocs 整合的实操步骤 |
| API 参考 | docs/api/ | 各核心模块（解析器、检测器、渲染器、导入器）的函数签名与配置参数说明 |

## 资源列表

本索引项目所聚合的外部技术资源均收录于 `entries/` 目录下的各分类子目录中。以下列表为当前版本已归档的全部原始链接条目，按主题领域分组。每个条目保留其原始 URL 格式，未做任何协议或域名改写。

技术规范与标准参考

<code>https://github.com/zerxonhy/olive/blob/main/timbersaffron.md</code>

<code>https://github.com/zerxonhy/olive/blob/main/velvetcedar.md</code>

工具链与中间件文档

<code>https://github.com/zerxonhy/olive/blob/main/velvetisland.md</code>

<code>https://github.com/zerxonhy/olive/blob/main/velvetrocket.md</code>

性能优化与架构案例

<code>https://github.com/zerxonhy/olive/blob/main/violettimber.md</code>

社区运维与监控实践

<code>https://github.com/zerxonhy/olive/blob/main/willowsilver.md</code>

## 项目结构

```
olive-link-atlas/
├── atlas.py                 # 主入口脚本，整合构建、检测、渲染与服务器功能
├── requirements.txt         # Python 依赖声明文件
├── pyproject.toml           # 项目元数据与构建系统配置
├── entries/                 # 链接条目存储目录，所有 Markdown 索引文件存放于此
│   ├── standards/           # 技术规范与标准相关条目，含 RFC 与 W3C 等
│   ├── tools/               # 工具链与中间件文档条目
│   ├── architecture/        # 架构设计与性能优化案例条目
│   └── operations/          # 运维监控与 SRE 实践条目
├── src/                     # 核心源代码目录
│   ├── parser/              # Markdown 前头信息与正文解析模块
│   ├── checker/             # 链接存活检测模块，基于 curl 与并发控制
│   ├── renderer/            # 模板渲染引擎与 HTML/JSON 输出生成器
│   └── importer/            # 第三方书签格式导入适配器集合
├── tests/                   # 单元测试与集成测试用例
│   ├── test_parser.py       # 解析器模块测试
│   ├── test_checker.py      # 检测器模块测试
│   └── test_renderer.py     # 渲染器模块测试
├── templates/               # Jinja2 模板文件，用于生成静态站点页面
│   ├── base.html            # 基础页面框架
│   ├── index.html           # 首页条目列表模板
│   └── detail.html          # 单一条目详情页模板
├── reports/                 # 检测报告输出目录，默认存放 JSON 格式的检查结果
└── docs/                    # 完整项目文档，包含用户手册、管理员指南与 ADR 记录
    ├── user-guide/
    ├── admin-guide/
    ├── developer-guide/
    ├── adr/
    ├── examples/
    └── api/
```

## 贡献指南

Olive Link Atlas 欢迎任何形式的贡献，包括但不限于新增索引条目、改进检测脚本性能、完善文档以及提交 bug 修复。请遵循以下步骤：

1. 在 GitHub 上 fork 本项目仓库，并克隆至本地开发环境。建议在新建的 feature 分支上进行所有改动，分支命名格式为 `feature/简短描述` 或 `fix/问题编号`。

2. 若为新增链接条目，请在 `entries/` 下选择或创建合适的分类子目录，并按照 `docs/user-guide/entry-template.md` 中定义的模板格式填写 Markdown 文件，确保前头信息包含 title、url、tags、date_archived 及 summary 字段。若为代码改动，请确保所有新增函数包含 docstring，并在 `tests/` 下补充对应的测试用例。

3. 提交前运行完整测试套件，确保所有已有测试通过且新代码的测试覆盖率不低于 80%。执行命令 `pytest tests/` 可运行全部测试，执行 `python atlas.py check --entries ./entries` 可验证当前索引中所有链接的有效性，避免引入已失效资源。

4. 提交 commit 时请使用语义化提交信息格式，例如 `feat: 新增 Rust 官方文档链接条目`、`fix: 修复检测器超时设置未生效的问题`、`docs: 更新快速开始中的 Python 版本要求`。提交后 push 至个人 fork，并通过 GitHub 界面发起 Pull Request 到主仓库的 main 分支。

5. Pull Request 描述中请清晰说明本次改动的内容、影响范围以及是否涉及破坏性变更。项目维护者会在 3 个工作日内进行 review，并可能提出修改意见。合并后您的贡献将被列入项目的贡献者列表。

## 常见问题

**Q: Olive Link Atlas 是否可以与现有的静态站点生成器如 MkDocs 或 Hugo 整合使用？**

A: 可以。Olive Link Atlas 提供了独立的渲染输出层，您可以选择生成纯 Markdown 引用块或 JSON 摘要文件。若您使用 MkDocs，可将 `atlas.py build --format markdown` 的输出内容通过 `mkdocs.yml` 中的 `extra_javascript` 或 `markdown_extensions` 机制嵌入页面；若使用 Hugo，则可将 JSON 输出放置于 `data/` 目录下，通过模板中的 `getJSON` 函数动态渲染链接列表。详细整合步骤参见 `docs/examples/mkdocs-integration.md` 与 `docs/examples/hugo-integration.md`。

**Q: 检测脚本如何处理需要特殊认证或带有反爬机制的链接？**

A: 当前检测脚本默认仅发送标准 User-Agent 头并遵循 HTTP 重定向，超时时间设置为 10 秒。对于需要 token 或 cookie 认证的链接，检测器会将其状态标记为 `requires_auth` 而非 `failed`，并在报告中额外记录认证提示。您可以通过修改 `src/checker/config.py` 中的全局请求头配置或传入自定义 headers 参数来适配内部工具的检测需求。对于高度动态的页面，建议结合人工定期抽查。

**Q: 索引中的链接条目数量增长到数千条后，构建和检测性能是否会出现瓶颈？**

A: Olive Link Atlas 在设计之初已考虑规模化场景。检测模块默认采用 10 个并发 worker 进行请求，对于 2000 个链接的完整检查可在 5 至 8 分钟内完成（取决于网络延迟与目标站点响应速度）。构建与渲染阶段仅涉及本地文件读取和模板生成，不涉及数据库查询，因此性能主要受限于磁盘 I/O 和 Markdown 解析速度。在 5000 条目规模下，完整构建耗时不超过 15 秒。若条目数量超过 10000，建议使用 `--filter` 参数按标签或日期范围分批检测，以降低单次运行时间。

## 许可证

MIT

> 外链数量: 6 | 生成时间: 2026-07-21 04:27:02
