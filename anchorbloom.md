# Olive Resource Bridge

Olive Resource Bridge 是一个面向技术文档维护者、开源项目贡献者和知识库管理者的外链资源归集与标准化呈现工具。项目定位为“资源外链的治理中间层”，不直接托管内容，而是通过结构化的 Markdown 文档将分散于各处的技术规范、设计说明、操作手册等外链资源进行统一编目、分类导航和状态标注，解决大型项目或技术社区中“链接散落、说明缺失、上下文断裂”的典型问题。目标用户包括技术文档工程师、开源社区运营者、内部知识库管理员以及需要长期维护大量外链引用的开发团队。

本项目本身是一个纯文档型仓库，所有资源以 Markdown 文件形式组织，通过约定的 Frontmatter 和目录结构实现可检索、可校验、可版本追踪的外链台账能力。配合 CI 脚本可自动检测链接失效、更新时间和格式合规性，适用于中大型 monorepo 的文档子项目或独立的技术资源导航站。

## 功能概览

- **外链归集与分类**：每个资源条目独立成文件，支持按主题、批次、状态等多维度标签分类，便于人工审阅和自动化扫描。

- **标准化元数据模板**：提供统一的 Markdown Frontmatter 模板，包含链接地址、原始来源、抓取日期、失效风险等级、备选联系人等字段，确保归集过程可追溯。

- **链接状态自动检测**：结合 GitHub Actions 或本地脚本，定期对已归集的 URL 进行 HEAD 请求检测，自动标记失效或重定向链接，并生成状态报表。

- **多级目录索引生成**：根据资源文件的目录层级和标签信息，自动生成按字母序、按批次或按主题的索引表格，方便快速定位。

- **变更历史与审阅记录**：每个资源文件的 Git 历史直接作为变更日志，配合提交信息规范，可清晰追踪每次增删改的原因和责任人。

- **批量导入与去重提示**：支持从现有 CSV 或 JSON 列表批量生成资源文件，并自动检测重复 URL 或高度相似的标题，减少人工核对成本。

- **Markdown 渲染兼容性优化**：所有资源描述统一使用标准 Markdown 语法，确保在 GitHub、GitLab、本地编辑器及静态站点生成器中呈现一致。

## 应用场景

- **技术文档中心的外链治理**：大型开源项目文档中常引用数十个外部规范、SDK 下载页、API 参考站。使用 Olive Resource Bridge 将这些外链集中归入 `resources/` 目录，并在主文档中通过相对路径引用索引文件，当外部链接变更时只需更新一处。

- **开源社区贡献者入门导航**：新贡献者往往不清楚需要阅读哪些设计文档、编码规范或讨论记录。通过本项目的批次目录（如 `batch_102/`），可将特定版本或特定模块的所有参考链接整合为一个入口页面，降低入门门槛。

- **内部知识库的定期链接审计**：企业 Wiki 或 Confluence 中积累了大量历史外链，每年需要合规审计。将链接清单导出后通过本项目模板重新组织，利用自动化检测脚本生成失效报告，按优先级推动修复。

- **技术资源聚合站的底层数据源**：若希望搭建一个静态资源导航站点，可直接将本项目作为数据层，通过脚本读取所有 Markdown 文件的元数据生成 JSON API，供前端页面消费，实现内容与呈现分离。

## 快速开始

以下操作基于 Linux/macOS 环境，Windows 用户可使用 WSL 或 Git Bash。

```bash
# 1. 克隆项目仓库
git clone https://github.com/zerxonhy/olive-resource-bridge.git
cd olive-resource-bridge

# 2. 安装依赖（仅用于本地检测脚本，基于 Node.js）
npm install

# 3. 运行链接状态检测（示例）
npm run check:links -- --batch=102
```

若仅需使用文档结构而不运行脚本，可直接复制 `docs/` 和 `resources/` 目录到您的项目中，并按模板格式添加资源文件。

## 安装要求

本项目的核心产物为 Markdown 文档，本身无运行时依赖。若需要使用附带的检测工具脚本，请参照下表准备环境：

| 依赖组件 | 必需版本 | 说明 |
|---------|---------|------|
| Node.js | 18.x 或 20.x LTS | 用于运行链接检测及索引生成脚本 |
| npm | 9.x 或以上 | 包管理器，用于安装 `axios`、`markdown-link-extractor` 等工具库 |
| Git | 2.30 或以上 | 版本控制，用于克隆及提交变更记录 |
| Shell (bash/zsh) | 任意 POSIX 兼容 | 执行快速开始中的命令脚本 |
| Markdown 编辑器 | 任意 | 推荐支持 Frontmatter 语法高亮和表格格式化，如 VSCode 配合 markdownlint |

## 文档导航

| 层面 | 目录/文件 | 回答的问题 |
|------|----------|-----------|
| 资源归集层 | `resources/batch_102/` | 如何按批次存放原始外链文件？每个文件的 Frontmatter 应包含哪些字段？ |
| 索引视图层 | `docs/index.md` | 如何查看当前所有已归集资源的分类总览和状态摘要？ |
| 自动化工具层 | `scripts/check-links.js` | 如何对所有归集链接进行批量可用性检测并生成失效报告？ |
| 规范约定层 | `CONTRIBUTING.md` | 新增或修改资源文件时应遵循什么提交信息格式和目录命名规则？ |

## 资源列表

以下为第 102/107 批次所收录的全部原始资源链接，按文件主题归类。所有链接均严格保持用户提供的原始格式。

### 批次核心资源

- <code>https://github.com/zerxonhy/olive/blob/main/oliveprairie.md</code>
- <code>https://github.com/zerxonhy/olive/blob/main/orbitmidnight.md</code>
- <code>https://github.com/zerxonhy/olive/blob/main/orbitolive.md</code>
- <code>https://github.com/zerxonhy/olive/blob/main/orbitpearl.md</code>
- <code>https://github.com/zerxonhy/olive/blob/main/pearlanchor.md</code>
- <code>https://github.com/zerxonhy/olive/blob/main/pixelbridge.md</code>

### 补充说明

上述链接指向同一个上游仓库 `zerxonhy/olive` 的不同文档文件，分别对应以下主题（根据文件名推断，仅供参考）：
- `oliveprairie`：草原主题配色或地理信息参考
- `orbitmidnight`：深色轨道风格设计说明
- `orbitolive`：橄榄绿轨道系统组件
- `orbitpearl`：珍珠色轨道界面规范
- `pearlanchor`：珍珠锚定模块的配置示例
- `pixelbridge`：像素桥接协议的过渡方案

本批次资源将在 `resources/batch_102/` 下为每个文件建立对应的 `.md` 归集记录，包含原始链接、归集日期、初步标签和状态备注。

## 项目结构

```
olive-resource-bridge/
├── .github/                         # GitHub 相关配置
│   └── workflows/
│       └── link-check.yml           # 每周一自动执行链接检测
├── docs/                            # 项目文档与使用指南
│   ├── index.md                     # 首页导航及快速索引
│   ├── schema.md                    # Frontmatter 字段定义与示例
│   └── troubleshooting.md           # 常见操作问题排查
├── resources/                       # 核心资源归集目录
│   ├── batch_102/                   # 第 102 批次资源文件
│   │   ├── oliveprairie.md          # 对应原始链接的归集记录
│   │   ├── orbitmidnight.md
│   │   ├── orbitolive.md
│   │   ├── orbitpearl.md
│   │   ├── pearlanchor.md
│   │   └── pixelbridge.md
│   ├── batch_103/                   # 预留后续批次
│   └── _templates/                  # 新建资源文件的模板
│       └── default.md
├── scripts/                         # 工具脚本
│   ├── check-links.js               # 核心检测脚本，输出失效列表
│   ├── generate-index.js            # 根据目录生成索引表格
│   └── import-csv.js                # 从 CSV 批量导入外链
├── .markdownlint.json               # Markdown 格式检查规则
├── package.json                     # npm 依赖及脚本入口
├── CONTRIBUTING.md                  # 贡献指南详情
└── README.md                        # 本文件
```

## 贡献指南

我们欢迎并鼓励社区贡献者参与资源归集和工具改进。请遵循以下步骤：

1. **阅读规范约定**：仔细阅读 `CONTRIBUTING.md` 中的 Frontmatter 字段定义、目录命名规则以及提交信息格式要求。所有新增或修改的资源文件必须通过 `markdownlint` 检查。

2. **创建分支并新增资源**：从 `main` 分支切出新的功能分支，命名格式为 `feat/batch-xxx-add` 或 `fix/link-update`。在对应的批次目录下新增 `.md` 文件，或更新现有文件的元数据字段。

3. **本地运行检测脚本**：在提交前执行 `npm run check:links -- --batch=102`，确保所有链接状态为有效或已正确标记为待处理。若检测到失效链接，请在文件中备注 `status: broken` 并填写备注说明。

4. **提交变更并推送**：提交信息必须遵循 `[batch-102] 类型: 简要描述` 格式，例如 `[batch-102] add: 归集 oliveprairie 资源`。推送后发起 Pull Request，至少需一名维护者审阅。

5. **合并后更新索引**：PR 合并后，CI 将自动执行 `generate-index.js` 更新 `docs/index.md`，您无需手动操作。若 CI 失败，请检查合并后的文件格式是否正确。

## 常见问题

**问：如果原始链接失效了，我应该直接修改 Markdown 文件中的 URL 还是新增一条记录？**

答：建议保留原始 URL 不变，在其 Frontmatter 中添加 `status: broken` 和 `broken_since: YYYY-MM-DD` 字段，并在备注中说明新链接地址或替代方案。若确定永久替换，可另建一个新文件，并在旧文件中通过 `redirect_to` 字段指向新文件。这样可完整保留历史审计线索。

**问：检测脚本是否支持需要特殊请求头或认证的链接？**

答：当前基础版本仅发送标准 `HEAD` 请求，不支持自定义 Cookie 或 Bearer Token。对于需要认证的内部链接，请在资源文件的 `notes` 字段中标注“内部访问受限”，检测脚本会将其跳过并标记为 `skip-auth`。后续版本计划支持通过环境变量注入认证头。

**问：如何将本项目迁移到我的 GitLab 或 Gitee 仓库中使用？**

答：本项目的核心是文档结构和脚本，与 GitHub 无强绑定。您只需将全部文件复制到目标仓库，并将 `.github/workflows/` 替换为对应平台的 CI 配置文件（如 GitLab CI 的 `.gitlab-ci.yml`）。脚本中的 `process.env.GITHUB_ACTIONS` 环境变量判断逻辑可按需移除或替换。

## 许可证

MIT

> 外链数量: 6 | 生成时间: 2026-07-21 04:27:24
