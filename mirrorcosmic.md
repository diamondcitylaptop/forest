# Olive Link Aggregator

Olive Link Aggregator 是一个面向技术文档维护者、开源项目运营者和知识库管理员的轻量级外链汇总与资源导航系统。该项目定位于解决分散在多个仓库、多个文档中的外部参考链接难以统一管理、难以版本追踪、难以批量校验的痛点，提供一套基于纯文本 Markdown 的集中化链接登记与分类方案。

Olive 本身不渲染网页、不提供数据库、不运行后台服务，它仅通过约定目录结构和规范化 Markdown 文件头部元数据，使团队能够以极低的学习成本维护一套可演进、可审计、可自动化检查的外部资源索引。目标用户包括技术写作团队、开源社区文档维护者、企业内部知识库管理员，以及任何需要长期管理大量外链资源的个人开发者。

## 功能概览

- **分级链接登记**：每个资源条目支持必填字段（目标 URL、简要描述、维护人、添加入口时间）和可选字段（过期检测周期、替代链接、标签分组），适配不同严格程度的项目管理需求。

- **自动过期提示**：配合 CI 定时任务，可根据配置的检测周期自动扫描链接状态，对返回 4xx/5xx 或连接超时的条目生成警告报告，并推送至指定 Issue 或邮件列表。

- **分组标签与多维度筛选**：支持为每个链接打上多个标签（如 `#documentation`、`#api_reference`、`#community`、`#tool`），便于按主题、用途、维护团队等维度快速筛选和输出子列表。

- **版本历史追踪**：所有变更通过 Git 提交记录保留，每次新增、修改或删除链接均关联提交信息，可追溯任意链接在任意时间点的状态与描述变更原因。

- **批量导入与导出**：支持从 CSV 或 JSON 文件批量导入链接条目，并支持将当前索引导出为结构化 JSON 或 HTML 摘要页面，用于生成静态站点侧边栏或嵌入内部仪表板。

- **Markdown 原生兼容**：所有链接记录存储为标准的 Markdown 列表或表格，可直接被主流 Git 托管平台（GitHub、GitLab、Gitea）渲染展示，无需额外解析工具即可人工阅读。

- **CI 原生集成示例**：项目提供 GitHub Actions、GitLab CI 和 Jenkins Pipeline 的参考配置文件，帮助用户在数分钟内为自己的仓库启用自动链接健康检查。

## 应用场景

- **开源项目文档站外链接维护**：开源项目 README、用户指南、开发者文档中往往引用大量外部依赖、教程、规范标准。使用 Olive 可将这些外部链接从正文分离，统一登记在 `references/` 目录下，正文仅保留简短引用 ID，既降低正文冗杂度，又便于定期批量检查链接有效性。

- **企业内部技术知识库外网资源索引**：企业技术团队在构建内部 Wiki 或 Confluence 空间时，常需要引用外网技术博客、官方 SDK 文档、第三方工具官网。Olive 的标签分组和过期检测功能可帮助知识库管理员快速识别哪些外链已失效，及时更新或替换，避免团队成员访问死链。

- **技术社区导航页的版本化维护**：技术社区或兴趣小组维护的导航网站（如 Awesome List 系列）需要长期跟踪大量资源链接。使用 Olive 的版本历史追踪能力，每次更新均可关联 Pull Request 评审，确保新增链接经过审核，同时保留旧链接的变更记录，便于回滚或审计。

- **个人书签与学习资源库的规范化管理**：开发者个人维护的技术书签集合或学习路径资源库，通常散落于浏览器书签或零散的笔记文件中。Olive 提供了一套可移植、可跨设备同步的纯文本管理方案，配合 Git 仓库可实现多终端同步和变更历史回溯。

## 快速开始

以下步骤指导您在本地环境完成 Olive Link Aggregator 的克隆、依赖安装和首次运行示例。

```bash
# 克隆项目仓库
git clone https://github.com/zerxonhy/olive.git
cd olive

# 安装依赖（项目本身无运行依赖，此处为 CI 校验脚本的 Python 依赖）
pip install -r requirements.txt

# 运行示例链接校验脚本（默认扫描 links/ 目录下所有 .md 文件）
python scripts/check_links.py --source ./links --output ./reports/link_status.json

# 生成静态摘要 HTML（用于本地预览）
python scripts/build_index.py --input ./links --template ./templates/index.tpl --output ./dist/index.html
```

若您尚未准备 Python 环境，也可直接使用提供的 Docker 镜像运行一次性校验任务：

```bash
docker run -v $(pwd)/links:/links olive/checker:latest --source /links
```

## 安装要求

| 依赖项 | 必需版本 | 说明 |
|--------|----------|------|
| Python | 3.8 及以上 | 用于运行链接校验脚本和索引生成脚本 |
| Git | 2.20 及以上 | 用于版本控制和提交历史追踪 |
| pip | 20.0 及以上 | 用于安装 Python 依赖包 |
| requests | 2.25.0 及以上 | Python HTTP 库，用于链接状态检测 |
| pyyaml | 5.4.0 及以上 | 用于解析可选的 YAML 元数据配置 |
| markdown | 3.3.0 及以上 | 用于将链接列表渲染为 HTML 摘要时解析 Markdown |
| 网络连通性 | 不适用 | 校验脚本需要访问外网以检测链接状态，内网环境需配置代理 |

## 文档导航

| 层面 | 目录 / 文档 | 回答的问题 |
|------|-------------|------------|
| 用户入门 | `docs/quickstart.md` | 如何快速新建一个链接条目？如何运行第一次校验？如何解读校验报告？ |
| 配置参考 | `docs/configuration.md` | 如何自定义标签别名？如何配置忽略特定链接的过期检测？如何设置代理？ |
| 维护指南 | `docs/maintenance.md` | 如何批量更新链接描述？如何处理过期链接的替换流程？如何归档旧链接？ |
| 集成指南 | `docs/integration.md` | 如何在 GitHub Actions 中集成自动校验？如何将生成的 JSON 报告导入其他系统？ |
| 贡献规范 | `CONTRIBUTING.md` | 新增链接的评审标准是什么？描述字段的书写规范有哪些？如何提交变更？ |
| 常见问题 | `docs/faq.md` | 为何某些正常链接被报告为超时？如何处理 SSL 证书校验失败？ |

## 资源列表

### 核心索引文件

本批次共包含 6 个资源链接，均为 Olive 项目默认示例索引中的参考文档条目，用于演示不同标签分类和描述格式。

<code>https://github.com/zerxonhy/olive/blob/main/meadowisland.md</code>

<code>https://github.com/zerxonhy/olive/blob/main/meadowzephyr.md</code>

<code>https://github.com/zerxonhy/olive/blob/main/midnightocean.md</code>

<code>https://github.com/zerxonhy/olive/blob/main/midnightquartz.md</code>

<code>https://github.com/zerxonhy/olive/blob/main/midnighttimber.md</code>

<code>https://github.com/zerxonhy/olive/blob/main/mirrorprairie.md</code>

上述文件均位于 Olive 项目主仓库的根目录下，分别对应不同主题的链接集合示例。其中 `meadow*` 前缀文件偏向自然语言处理与文本分析工具的资源汇集，`midnight*` 前缀文件偏向系统运维与网络协议参考，`mirrorprairie.md` 则作为混合类别示例，展示跨领域链接的组织方式。

## 项目结构

```
olive/
├── .github/
│   └── workflows/                  # GitHub Actions 工作流配置
│       ├── check_links_daily.yml   # 每日定时执行链接校验
│       └── pr_validate.yml         # Pull Request 时触发增量校验
├── links/                          # 主要链接登记目录（按主题分子目录）
│   ├── ai/                         # 人工智能与机器学习相关链接
│   │   ├── models.md               # 预训练模型下载与对比页
│   │   └── datasets.md             # 公开数据集索引
│   ├── devops/                     # DevOps 与 SRE 工具链链接
│   │   ├── ci_cd.md                # CI/CD 平台与最佳实践
│   │   └── monitoring.md           # 监控告警系统文档
│   ├── networking/                 # 网络协议与基础设施参考
│   │   ├── protocols.md            # HTTP/3、QUIC 等规范链接
│   │   └── security.md             # TLS、证书与安全头信息
│   └── _templates/                 # 新增链接条目的模板文件
│       ├── default.md              # 通用链接登记模板
│       └── api_ref.md              # API 文档专用模板
├── scripts/                        # 工具脚本目录
│   ├── check_links.py              # 主校验脚本，支持多线程并发检测
│   ├── build_index.py              # 生成 JSON / HTML 摘要的构建脚本
│   └── utils/                      # 通用工具函数包
│       ├── parsers.py              # Markdown 条目解析器
│       └── reporters.py            # 报告格式化输出（控制台/JSON/Markdown）
├── reports/                        # 校验报告输出目录（自动生成，不纳入版本控制）
│   ├── latest.json                 # 最新一次完整校验的 JSON 结果
│   └── history/                    # 历史报告归档（按日期命名）
├── templates/                      # 静态摘要渲染模板
│   └── index.tpl                   # HTML 模板文件，包含样式与布局占位
├── tests/                          # 单元测试与集成测试
│   ├── test_parsers.py             # 解析器模块测试
│   └── test_checker.py             # 链接检测逻辑测试
├── requirements.txt                # Python 依赖声明
├── README.md                       # 项目主文档（本文档）
├── CONTRIBUTING.md                 # 贡献者指南
├── LICENSE                         # MIT 许可证全文
└── .gitignore                      # Git 忽略规则（含 reports/ 与 __pycache__/）
```

## 贡献指南

1. **阅读贡献规范**：首先阅读 `CONTRIBUTING.md` 文件，了解链接条目标题格式、描述字数限制（20-200 字符）、标签使用约定以及审核周期预期。

2. **克隆并创建分支**：从主仓库派生（Fork）或个人克隆后，为每次变更创建独立分支，分支命名建议采用 `feat/add-<topic>-links` 或 `fix/update-<broken-link>` 格式。

3. **新增或修改链接条目**：在对应主题子目录下编辑 Markdown 文件，每条链接需包含 `[链接名称](URL)` 形式，并在紧跟的段落或列表中填写描述、标签和维护人信息。提交前运行 `python scripts/check_links.py --source ./links --local-only` 进行本地语法校验。

4. **提交变更并推送**：提交信息应遵循约定式提交规范（Conventional Commits），例如 `feat(ai): add huggingface transformers documentation` 或 `fix(networking): update expired RFC link`。推送至远程分支后创建 Pull Request。

5. **等待审核与自动校验**：Pull Request 将触发 GitHub Actions 工作流，自动执行全量或增量链接校验。审核人员将基于校验报告和条目规范进行评审，通过后合并至主分支。

## 常见问题

**问：校验脚本报告某个链接为超时（Timeout），但我用浏览器打开是正常的，是什么原因？**

答：此情况通常由网络环境差异引起。Olive 校验脚本默认使用 `requests` 库的 10 秒超时设置，且不携带浏览器常见的 Cookie 或 JavaScript 执行环境。若目标服务器对非浏览器 User-Agent 有访问限制或响应较慢，可能触发超时。解决方案：在链接条目元数据中添加 `timeout: 30` 自定义字段（单位秒），或通过 `--timeout` 全局参数调整。若仍失败，可使用 `--ignore-urls` 参数将该链接加入忽略列表，并备注人工确认状态。

**问：如何将 Olive 用于私有 GitLab 或 Gitea 实例中的多个仓库？**

答：Olive 的设计与 Git 托管平台解耦。您可以将 `links/` 目录及其脚本复制到任一 Git 仓库中，并配置相应的 CI 流水线（参考 `docs/integration.md` 中的 GitLab CI 示例）。对于多仓库场景，推荐使用 Git Submodule 或 Git Subtree 将 Olive 的核心脚本和模板作为公共子模块引入，各仓库仅维护各自的 `links/` 子目录，从而实现脚本统一更新与链接数据分散管理。

**问：链接条目中的描述字段是否支持 Markdown 格式？校验脚本会解析其中的 URL 吗？**

答：描述字段支持轻量 Markdown（如加粗、斜体、行内代码），但校验脚本默认仅解析标准的 `[text](url)` 模式以及裸 URL（以 `http://` 或 `https://` 开头的纯链接）。描述中的 Markdown 链接会被正常提取并校验，而普通文本中的 URL 若未使用链接语法或尖括号包裹，则不会被视为链接条目，避免误报。若希望某 URL 不被校验，可在其行尾添加 `<!-- ignore -->` 注释，校验脚本会自动跳过。

## 许可证

本项目采用 MIT 许可证。您可以自由使用、修改、分发本项目代码及文档，包括用于商业目的，但需保留原始版权声明和许可声明。详见项目根目录下的 LICENSE 文件。

> 外链数量: 6 | 生成时间: 2026-07-21 04:27:01
