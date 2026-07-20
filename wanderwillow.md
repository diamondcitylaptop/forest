# Olive Link Atlas

Olive Link Atlas 是一个面向技术文档工程师、开源项目维护者以及开发者知识管理者的外链资源归集与规范化治理工具。该项目不提供新的内容生产范式，而是聚焦于解决技术社区中广泛存在的“资源链接散落、版本关联缺失、引用状态不可查”这一基础性问题。其目标用户包括需要批量整理历史遗留文档链接的团队、希望建立标准化外链引用清单的开源项目维护者，以及需要对外部依赖资源进行合规性审查的企业内部技术作者。

Olive Link Atlas 通过将一组预设的 Markdown 文件索引视为可追溯的链接节点，建立起一个轻量级的本地化资源关系网络。它并不替代现有的文档站点或代码仓库，而是作为辅助层，帮助用户快速识别特定批次文档中的外链分布、协议一致性以及路径格式合法性。项目核心逻辑围绕“链接指纹”与“状态快照”展开，适用于需要定期复核外部引用有效性的各类技术写作场景。

## 功能概览

- **批次化链接归集**：支持按指定批次（如第 20/107 批）导入并隔离管理一组外链资源，确保大规模文档重构过程中的链接可追溯性。

- **协议与格式规范性检查**：自动扫描并标记不符合预期格式规范的 URL 条目，例如协议头缺失、大小写不一致或结尾多余斜杠，并提供批量修复建议。

- **资源状态快照生成**：针对每个归集批次生成静态快照文件，记录当前批次内所有链接的原始来源、所属文件路径及最后检查时间戳。

- **Markdown 引用树渲染**：基于给定的链接列表，自动生成结构化 Markdown 表格与目录树视图，便于嵌入技术文档或项目 README 中作为外链附录。

- **依赖关系图导出**：分析链接之间的相对路径关联与跨文件引用，输出轻量级依赖矩阵，辅助评估外部资源变更对本地文档的影响面。

- **变更追踪与差异比对**：支持对比不同批次之间的链接集合差异，清晰展示新增、删除或变更的 URL 条目，适用于文档版本升级场景。

- **配置化忽略规则**：允许用户自定义忽略特定域名或路径模式的检查规则，避免内网地址或动态参数链接被误报为异常项。

## 应用场景

- **技术文档仓库外链审计**：当技术文档团队需要定期检查文档中引用的外部图片、规范文档或第三方库地址是否仍然可访问时，可使用 Olive Link Atlas 导入指定目录下的所有 Markdown 文件，快速生成外链清单并标记异常项。

- **开源项目 README 资源章节自动生成**：开源项目维护者可以利用本工具将散落在各个子模块文档中的参考链接统一提取并聚合为资源列表，避免手动维护导致的遗漏或重复。

- **企业内部知识库迁移前的链接盘点**：在进行知识库平台迁移或域名更换前，使用 Olive Link Atlas 对旧站点中的所有外链进行快照记录，生成迁移前后的映射校验表，降低链接失效风险。

- **合规性审查中的第三方依赖记录**：对于需要对外披露第三方组件或服务依赖的合规团队，可通过本工具从多个技术文档中抽取所有外部 URL，形成结构化的依赖申报材料。

## 快速开始

以下步骤演示如何获取 Olive Link Atlas 源码、安装基础依赖并执行一次示例批次的外链归集操作。

```bash
# 克隆项目仓库
git clone https://github.com/zerxonhy/olive-link-atlas.git

# 进入项目目录
cd olive-link-atlas

# 安装 Python 依赖（要求 Python 3.9 及以上）
pip install -r requirements.txt

# 执行示例批次归集（第 20/107 批）
python atlas.py --batch 20 --total 107 --input ./samples/links.txt --output ./reports/
```

## 安装要求

| 依赖项 | 必需版本 | 说明 |
|--------|----------|------|
| Python | 3.9 及以上 | 核心运行环境，用于执行链接解析与归集逻辑 |
| pip | 22.0 及以上 | Python 包管理工具，用于安装项目依赖库 |
| Git | 2.30 及以上 | 用于克隆项目仓库及版本控制操作 |
| Markdown 解析库 | markdown-it-py 2.2.0 | 用于解析 Markdown 文件中的链接元素 |
| 网络请求库 | httpx 0.24.0 | 用于执行链接可达性探测（可选，可禁用） |
| 测试框架 | pytest 7.2.0 | 仅开发测试时需要，用于运行单元测试 |
| 代码格式化工具 | black 23.0.0 | 仅开发贡献时需要，用于保持代码风格一致 |

## 文档导航

| 层面 | 目录/文件 | 回答的问题 |
|------|-----------|------------|
| 用户指南 | docs/user-guide/batch-import.md | 如何导入自定义批次链接、如何配置忽略规则以及如何解读快照报告 |
| 管理员手册 | docs/admin/check-policies.md | 如何自定义协议检查策略、如何设置链接超时阈值以及如何集成到 CI 流程 |
| 开发参考 | docs/developer/api-reference.md | 核心类 LinkCollector、BatchProcessor 和 ReportGenerator 的接口定义与扩展方法 |
| 常见工作流 | docs/workflows/migration-audit.md | 如何利用本工具在文档迁移前后进行链接差异对比与状态校验 |

## 资源列表

本批次（第 20/107 批）包含以下 6 个外链资源条目，均来源于用户指定的原始数据。所有链接按其在源文件中的路径分组展示，以便于对照原始仓库结构。

**来源：olive 仓库主分支**

<code>https://github.com/zerxonhy/olive/blob/main/brightpixel.md</code>

<code>https://github.com/zerxonhy/olive/blob/main/brightsilver.md</code>

<code>https://github.com/zerxonhy/olive/blob/main/canvasmarble.md</code>

<code>https://github.com/zerxonhy/olive/blob/main/canvassignal.md</code>

<code>https://github.com/zerxonhy/olive/blob/main/cedarcoral.md</code>

<code>https://github.com/zerxonhy/olive/blob/main/cedarwillow.md</code>

## 项目结构

项目采用模块化分层设计，核心归集逻辑与展示层分离，便于后续扩展其他输入输出格式。

```
olive-link-atlas/
├── atlas.py                     # 命令行入口，解析用户参数并调度核心流程
├── requirements.txt             # 生产环境依赖列表
├── config/
│   ├── default.yaml             # 默认检查规则，包括超时时间、忽略域名列表
│   └── schema.json              # 快照输出 JSON Schema 定义
├── core/
│   ├── __init__.py
│   ├── collector.py             # 链接收集器，负责从文本源提取 URL
│   ├── processor.py             # 批次处理器，执行格式规范性与状态检查
│   ├── reporter.py              # 报告生成器，输出 Markdown 与 JSON 格式结果
│   └── validator.py             # 协议与路径校验器，包含大小写与斜杠检查逻辑
├── models/
│   ├── __init__.py
│   ├── link_entry.py            # 链接条目数据类，存储原始 URL、来源文件、状态
│   └── batch_manifest.py        # 批次清单数据类，记录批次编号、总量与时间戳
├── parsers/
│   ├── __init__.py
│   ├── markdown_parser.py       # 基于 markdown-it-py 的 Markdown 链接解析器
│   └── plaintext_parser.py      # 纯文本链接提取器，用于非 Markdown 源文件
├── output/                      # 默认输出目录，存放生成的快照与报告文件
│   ├── reports/
│   └── snapshots/
├── tests/                       # 单元测试目录，覆盖核心解析与校验逻辑
│   ├── test_collector.py
│   ├── test_validator.py
│   └── fixtures/                # 测试用样本文件
├── docs/                        # 项目文档源码
│   ├── user-guide/
│   ├── admin/
│   ├── developer/
│   └── workflows/
└── .github/
    └── workflows/               # GitHub Actions CI 配置，用于自动化测试与 lint 检查
        └── ci.yml
```

## 贡献指南

Olive Link Atlas 欢迎社区贡献，无论是问题报告、功能建议还是代码提交。请遵循以下步骤参与项目开发。

1. 在 GitHub 上 fork 本仓库，并克隆到本地开发环境。确保使用 Python 3.9 及以上版本，并安装所有开发依赖（包含在 dev-requirements.txt 中）。

2. 新建一个功能分支，分支名称应简要描述本次变更内容，例如 `feature/add-json-export` 或 `fix/url-encoding-issue`。所有变更请附带对应的单元测试用例，测试覆盖率不得低于 85%。

3. 提交代码前，请运行 black 和 flake8 进行代码格式与风格检查，并确保所有 pytest 测试用例通过。提交信息请遵循 Conventional Commits 规范，使用 `feat:`、`fix:`、`docs:` 等前缀。

4. 发起 Pull Request 到主仓库的 `main` 分支，并在 PR 描述中清晰说明变更目的、影响范围以及相关测试结果。PR 将被至少一位维护者审阅，审阅通过后合并。

5. 若发现缺陷或希望提出新功能，请先在 Issues 区域搜索是否已有类似讨论，避免重复。新建 Issue 时请使用提供的模板，并尽可能提供复现步骤或使用场景说明。

## 常见问题

**问：Olive Link Atlas 是否会对链接进行实际的网络访问以验证可用性？**

默认情况下，工具仅进行语法格式和协议规范性检查，不会主动发起 HTTP 请求。若需要验证链接的可达性，可在配置文件中将 `network_check_enabled` 设置为 `true`，并设置合理的超时时间。此时工具会使用 httpx 库对每个链接发送 HEAD 请求以检查响应状态，但请注意这可能会增加执行时间并受网络环境影响。

**问：如何处理链接中包含动态参数或内网地址的情况？**

您可以在配置文件的 `ignore_patterns` 字段中添加正则表达式规则，例如匹配 `.*internal\.corp\.com.*` 或 `.*\?session_id=.*`。匹配到这些模式的链接将被跳过格式检查和网络探测，仅作为静态条目记录在快照中。同时，您也可以通过 `allowed_protocols` 配置项限制仅检查 `https` 和 `http` 协议，忽略 `ftp`、`mailto` 等其他类型。

**问：项目是否支持 Windows 操作系统？**

Olive Link Atlas 基于 Python 编写，理论上支持所有主流操作系统，包括 Windows、macOS 和 Linux。但文件路径处理部分在 Windows 上需要使用反斜杠或原始字符串，建议在配置文件中使用 `path_style: windows` 选项自动适配。项目核心开发与测试环境为 Ubuntu 22.04 LTS 与 macOS Ventura，Windows 平台下的 CI 测试覆盖正在完善中。

## 许可证

MIT

> 外链数量: 6 | 生成时间: 2026-07-21 04:26:20
