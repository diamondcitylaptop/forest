# Olive Link Aggregator

Olive Link Aggregator 是一个面向开发者与技术研究人员的轻量级外链资源汇总与导航系统。该项目定位为技术信息的中转枢纽，通过结构化的 Markdown 文档仓库，将分散于 GitHub 议题、技术博客、官方公告及社区讨论中的优质外部链接进行集中收录、分类索引与版本追踪。Olive 本身不存储具体内容，仅提供可靠的链接映射与状态检测机制，帮助用户快速定位特定技术主题下的权威资料，避免信息碎片化带来的检索效率损失。

项目主要解决以下问题：技术社区中高价值外链常散落在评论、PR 描述或临时文档中，缺乏统一的沉淀入口；现有书签工具缺乏协作能力，无法以团队形式维护链接库；官方文档更新后旧链接失效，缺少主动的链接状态监测。Olive 通过将外链管理纳入 Git 工作流，利用提交历史与议题关联实现可追溯的链接生命周期管理，适用于个人知识库构建、团队技术文档增强以及开源项目的外部依赖梳理等场景。

## 功能概览

- **分级链接索引**：支持按技术领域、文档类型、维护状态对链接进行多维度标签标记，每个链接条目包含标题、描述、标签列表及最后验证时间，便于快速筛选与排序。

- **自动化状态检测**：内置周期性 HTTP 请求检测机制，对已收录链接进行可达性检查，自动标记失效链接并生成告警日志，支持手动触发重新验证。

- **Markdown 原生编辑**：所有链接数据以人类可读的 Markdown 文件存储，无需数据库，可直接通过文本编辑器或在线 IDE 修改，完全兼容 Git 版本控制。

- **协作维护工作流**：支持通过 Pull Request 提交新链接或修改现有条目，维护者可在合并前进行内容审核与链接验证，确保收录质量。

- **链接关系图谱**：提供简单的引用关系分析，可展示链接之间的相互引用次数以及外部域名聚合统计，帮助识别核心信息源。

- **快速检索接口**：提供基于文件名匹配与标签过滤的轻量级检索能力，支持通过命令行工具或 HTTP 端点查询，便于集成到其他自动化脚本中。

## 应用场景

- **技术团队内部知识库增强**：团队可将日常开发中参考的官方 API 文档、社区解决方案、性能调优案例等外链统一收录至 Olive 仓库，新成员入职时通过克隆仓库即可获得全套参考资源，避免从零开始搜集。

- **开源项目外部依赖追踪**：开源项目维护者可使用 Olive 记录依赖库的文档链接、迁移指南及版本发布公告，当依赖项发生重大更新时，可通过 Olive 的链接状态检测快速判断相关文档是否仍有效，辅助升级决策。

- **技术博客与教程引用管理**：技术内容创作者在撰写系列文章时，使用 Olive 集中存放所有参考文献链接，文章仅需引用 Olive 中的条目 ID，后期若链接变更只需在 Olive 中更新一处，无需逐一修改多篇文章。

- **社区资源共建共享**：技术社区运营者可搭建 Olive 实例作为社区推荐资源库，鼓励成员通过 PR 贡献优质外链，经审核后合并，形成由社区驱动、持续更新的技术导航站点。

## 快速开始

以下步骤将指导您在本地完成 Olive Link Aggregator 的克隆、依赖安装与基础运行。

```bash
# 克隆项目仓库
git clone https://github.com/zerxonhy/olive.git
cd olive

# 安装 Python 依赖（推荐使用虚拟环境）
python3 -m venv venv
source venv/bin/activate  # Windows 下使用 venv\Scripts\activate
pip install -r requirements.txt

# 执行链接状态检测脚本
python scripts/check_links.py --target ./blob --report ./reports

# 启动本地检索服务（默认端口 8080）
python scripts/serve.py --port 8080
```

完成上述操作后，您可以通过浏览器访问 <code>http://localhost:8080</code> 查看当前已收录的链接列表及状态概览。若仅需使用链接数据，可直接浏览 <code>./blob</code> 目录下的 Markdown 文件。

## 安装要求

| 依赖项 | 是否必需 | 说明 |
|--------|----------|------|
| Python 3.9 或更高版本 | 是 | 运行检测脚本与检索服务的运行时环境 |
| pip 与 venv 模块 | 是 | Python 包管理与虚拟环境创建，确保依赖隔离 |
| Git 2.25 或更高版本 | 是 | 克隆仓库、提交变更及与远程仓库交互 |
| 网络连接（HTTP/HTTPS） | 是 | 执行链接可达性检测时需要访问外部域名 |
| 可选：Docker Engine 20.10+ | 否 | 若使用容器化部署方式，需要 Docker 环境 |
| 可选：GNU Make 4.0+ | 否 | 若使用 Makefile 简化命令组合，需要 Make 工具 |

## 文档导航

| 层面 | 目录/文件 | 回答的问题 |
|------|-----------|------------|
| 链接条目存储 | <code>./blob/*.md</code> | 每个 Markdown 文件对应一个链接条目，包含标题、URL、描述、标签及验证时间戳，如何新增或修改单个链接？ |
| 分类索引 | <code>./indices/tags.json</code> | 标签聚合索引，记录每个标签下关联的链接文件名列表，如何按技术领域批量查找链接？ |
| 检测报告 | <code>./reports/last_run.log</code> | 最近一次链接状态检测的完整日志，包含每个链接的响应码与响应时间，如何判断哪些链接已失效？ |
| 配置参考 | <code>./config/settings.yaml</code> | 检测超时阈值、重试次数、报告输出格式等运行时参数，如何调整检测频率与超时策略？ |
| 贡献模板 | <code>./.github/PULL_REQUEST_TEMPLATE.md</code> | 新链接提交通用的 PR 模板，包含必填字段与验证清单，如何规范化提交新链接？ |
| 命令行手册 | <code>./docs/cli_usage.md</code> | 所有支持的命令行子命令与参数详解，如何在不启动服务的情况下仅运行链接检测？ |

## 资源列表

以下为当前项目收录的全部外部资源链接，按文件名称分类整理。所有链接均来自用户原始数据，未经任何修改。

核心文档资源

- <code>https://github.com/zerxonhy/olive/blob/main/cedarcoral.md</code>
- <code>https://github.com/zerxonhy/olive/blob/main/cedarwillow.md</code>
- <code>https://github.com/zerxonhy/olive/blob/main/cloudbright.md</code>
- <code>https://github.com/zerxonhy/olive/blob/main/coralmaple.md</code>
- <code>https://github.com/zerxonhy/olive/blob/main/coralsaffron.md</code>
- <code>https://github.com/zerxonhy/olive/blob/main/cosmicamber.md</code>

上述资源均为 Olive 项目仓库内 <code>./blob</code> 目录下的 Markdown 文档，每个文件独立描述一个外部链接条目。文件名采用自然词汇组合，便于记忆与命令行补全。用户可通过直接访问这些 GitHub 原始链接查看具体条目内容，或通过 Olive 的检索服务进行批量查询。

## 项目结构

项目采用模块化目录布局，核心数据与逻辑分离，便于维护与扩展。以下为主要目录与文件的功能说明。

```
olive/
├── blob/                           # 链接条目存储目录，每个文件一个链接
│   ├── cedarcoral.md               # 条目：标题、URL、描述、标签、验证时间
│   ├── cedarwillow.md              # 条目：技术文档类链接
│   ├── cloudbright.md              # 条目：云基础设施相关链接
│   ├── coralmaple.md               # 条目：前端框架生态链接
│   ├── coralsaffron.md             # 条目：性能优化与监控链接
│   ├── cosmicamber.md              # 条目：系统设计及架构链接
│   └── ...                         # 其他条目文件
├── scripts/                        # 可执行脚本与辅助工具
│   ├── check_links.py              # 主检测脚本，遍历 blob 执行 HTTP 验证
│   ├── serve.py                    # 简易检索服务，基于 Flask 或 http.server
│   ├── generate_index.py           # 根据标签生成 JSON 索引文件
│   └── utils/                      # 公共函数库，含网络请求与日志格式化
├── indices/                        # 自动生成的索引与聚合数据
│   ├── tags.json                   # 标签到文件名的映射
│   ├── domains.json                # 域名聚合统计
│   └── last_verified.json          # 各链接最近一次验证时间
├── reports/                        # 检测报告存储目录
│   ├── last_run.log                # 完整检测日志（含成功/失败/超时）
│   ├── failures.csv                # 仅记录失效链接的 CSV 表格
│   └── summary.json                # 检测汇总统计（总数/成功率/平均响应）
├── config/                         # 项目配置文件
│   ├── settings.yaml               # 主配置：超时、重试、并发数、报告路径
│   └── user_agents.txt             # 轮询使用的 User-Agent 列表
├── docs/                           # 用户文档与设计说明
│   ├── cli_usage.md                # 命令行详细使用手册
│   ├── api_design.md               # 检索服务 API 设计文档
│   └── contribution_guide.md       # 贡献者详细指引（含链接提交规范）
├── .github/                        # GitHub 社区配置文件
│   ├── PULL_REQUEST_TEMPLATE.md    # PR 模板，引导填写链接信息
│   ├── ISSUE_TEMPLATE/             # 议题模板（报告失效链接/建议新链接）
│   └── workflows/                  # GitHub Actions 工作流定义
│       └── daily_check.yml         # 每日自动运行链接检测
├── requirements.txt                # Python 依赖声明（requests, pyyaml 等）
├── Makefile                        # 常用命令封装（install, check, serve）
└── README.md                       # 项目主文档（即本文档）
```

## 贡献指南

项目欢迎并鼓励社区贡献。无论您是提交新链接、修复检测逻辑还是完善文档，请遵循以下步骤以保证协作流程顺畅。

1.  **查找或创建议题**：在提交 Pull Request 之前，请先在 Issues 页面查找是否已有相关议题。若为新链接建议或失效报告，请创建新议题并详细描述链接内容及推荐理由，避免重复工作。

2.  **派生仓库并创建分支**：将主仓库派生至个人账户，然后克隆派生仓库至本地。创建独立功能分支，分支命名建议使用 <code>feature/add-link-{name}</code> 或 <code>fix/update-{link-id}</code> 格式。

3.  **按照模板修改内容**：新增链接时，在 <code>./blob</code> 目录下新建 Markdown 文件，文件名需具有描述性。文件内容请严格遵循现有条目的元数据格式，包括标题、URL、描述、标签列表及初始验证时间。若为更新现有链接，请同步更新验证时间戳。

4.  **本地执行检测验证**：在提交前，请运行 <code>python scripts/check_links.py --target ./blob</code> 确保您新增或修改的链接可通过 HTTP 可达性检测。若链接返回状态码不为 2xx 或 3xx，请在 PR 描述中注明原因。

5.  **发起 Pull Request**：将本地分支推送至您的派生仓库，然后向主仓库的 <code>main</code> 分支发起 PR。PR 标题应简明扼要，内容需填写 PR 模板中的所有字段。维护者将在 48 小时内进行审核，审核通过后即合并入主分支。

## 常见问题

**问：检测脚本报告某链接失效，但我在浏览器中可以正常访问，这是为什么？**

答：可能原因包括：1) 检测脚本的 User-Agent 与浏览器不同，目标服务器可能拦截了非浏览器请求。您可以在 <code>config/user_agents.txt</code> 中配置更接近真实浏览器的 UA 字符串。2) 目标服务器存在频率限制，检测脚本的并发请求可能触发临时封锁。请尝试降低 <code>config/settings.yaml</code> 中的并发数。3) 脚本默认不跟随某些特定的 JavaScript 重定向，若链接依赖前端跳转，请改为直接提供最终落地 URL。

**问：如何批量导入现有的书签文件（如 Chrome 导出的 HTML）？**

答：当前版本未提供直接导入功能，但您可以使用 <code>scripts/utils/convert_bookmarks.py</code> 脚本（需自行创建）将标准的 Netscape 书签格式转换为 Olive 条目格式。转换后请手动检查每个条目标签的准确性，并运行检测脚本确保链接有效。社区计划在下个版本中提供官方导入工具。

**问：Olive 是否支持私有化部署并限制访问权限？**

答：Olive 本身仅为静态 Markdown 文件加可选检索服务，不包含用户认证系统。若需要私有化部署，推荐将仓库设置为私有仓库，并通过 GitHub 的访问控制管理团队成员。检索服务可通过反向代理添加基础认证（如 HTTP Basic Auth），或仅允许本地回环地址访问，具体配置请参考 <code>docs/api_design.md</code> 中的安全建议章节。

## 许可证

本项目采用 MIT 许可证。您可以在遵守许可证条款的前提下自由使用、修改、分发本软件，包括商业用途。完整许可证文本请参见项目根目录下的 <code>LICENSE</code> 文件。

> 外链数量: 6 | 生成时间: 2026-07-21 04:27:03
