# Olive Resource Index

Olive Resource Index 是一个面向技术调研、文档归档与外部知识库引用的轻量级资源导航系统。项目定位为“技术资源的外链汇总站”，主要服务于需要频繁查阅分散于各处的技术文档、RFC 规范、开源仓库 README 以及内部知识沉淀的开发者、技术写作者与团队知识管理员。Olive 本身不存储大型二进制文件或完整的第三方文档副本，而是通过结构化的 Markdown 索引文件、可定制的标签体系以及基于 Git 的版本追踪，帮助用户从杂乱的浏览器书签和零散笔记中解脱出来，建立可维护、可共享、可审计的外部资源引用清单。

Olive 的核心价值在于将“资源链接”提升为“资源条目”，每个条目均可附带收录人、收录时间、状态标记、简要摘要和关联标签。项目默认采用纯静态 Markdown 渲染，无需数据库或后端服务，可直接部署于 GitHub Pages、Vercel 或任何支持静态站点的托管平台。同时，Olive 提供了可选的命令行工具，用于校验链接可用性、生成资源索引 JSON 以及批量导入导出书签，适合作为团队内部文档站点的上游数据源。

## 功能概览

- **结构化资源索引**：基于 Markdown 文件组织资源条目，每个文件对应一个资源分类或主题域，支持嵌套目录，便于按项目、技术栈或业务模块划分。

- **自动链接校验**：内置链接可用性检查工具，可定期扫描所有收录的外部 URL，标记失效链接并生成报告，减少文档中的“死链”污染。

- **标签与全文检索**：通过简单的前置元数据（YAML Front Matter）为每个资源条目附加标签、优先级和状态，配合静态站点生成器可实现基于标签的过滤和全文搜索。

- **版本化变更记录**：所有资源新增、修改或删除操作均通过 Git 提交记录追踪，支持回溯任意时间点的资源列表状态，满足审计与变更管理需求。

- **多格式导出**：支持将索引内容导出为 JSON、CSV 或 HTML 书签文件（.html），便于导入浏览器、Obsidian 或其他知识管理工具。

- **自定义元数据扩展**：允许用户为资源条目定义自定义字段（如“关联项目”“内部评审状态”“到期复查日期”），满足企业内部合规或流程管理要求。

- **低维护成本**：纯文本文件存储，无外部依赖，可使用任何文本编辑器或 IDE 直接编辑，学习曲线平缓，适合纳入现有 GitOps 工作流。

## 应用场景

- **技术团队内部知识库导航**：团队可将 Olive 作为微服务架构下各服务文档、API 规范、部署手册和监控面板的入口索引，替代零散的 Wiki 页面或浏览器收藏夹，确保新成员能快速找到关键外部参考。

- **开源项目外部依赖整理**：开源维护者可使用 Olive 梳理项目所依赖的第三方库文档、标准协议链接、社区论坛和示例代码仓库，将其纳入项目 docs 目录，降低贡献者的学习门槛。

- **技术调研与竞品分析归档**：在进行技术选型或竞品分析时，调研人员可通过 Olive 分类保存竞品官网、技术白皮书、性能测试报告和社区讨论帖，并为每条资源添加评估结论或摘要，形成可共享的调研知识库。

- **个人学习路径管理**：开发者可将 Olive 用作个人技术学习地图，按学习主题（如 Rust 生命周期、Kubernetes 调度器、分布式共识算法）组织外部教程、视频链接和实验代码仓库，并跟踪学习进度与复习提醒。

## 快速开始

以下命令演示了如何从 GitHub 克隆 Olive 项目、安装基础依赖并启动本地预览服务。

```bash
# 克隆项目仓库
git clone https://github.com/zerxonhy/olive.git
cd olive

# 安装依赖（基于 Node.js 环境，使用 npm）
npm install

# 构建静态资源索引并启动本地开发服务器
npm run build
npm run serve
```

执行完毕后，打开浏览器访问 `http://localhost:8080` 即可查看 Olive 生成的资源索引首页。默认示例数据包含若干技术文档和开源项目的引用条目，您可在此基础上编辑或替换 `./resources` 目录下的 Markdown 文件。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---------|---------|------|
| Node.js | 16.x 或更高 | 用于运行构建脚本、链接校验工具和本地服务器 |
| npm | 8.x 或更高 | 包管理器，用于安装项目依赖 |
| Git | 2.25 或更高 | 用于克隆仓库、版本管理和提交变更记录 |
| 操作系统 | Linux / macOS / Windows (WSL2 推荐) | 跨平台支持，但 Windows 原生环境建议使用 PowerShell 7 |
| 浏览器 | 现代浏览器（Chrome 90+ / Firefox 88+ / Edge 90+） | 仅用于预览静态站点，非运行时强制依赖 |
| 可选：Python 3.9+ | 仅当启用高级链接校验扩展时需要 | 用于运行额外的异步请求测试脚本 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|-----------|
| 用户指南 | `/docs/user-guide/` | 如何添加新资源条目？如何批量导入浏览器书签？如何配置标签体系？ |
| 管理员手册 | `/docs/admin/` | 如何设置团队协作流程？如何配置自动链接校验的定时任务？如何迁移已有资源数据？ |
| 开发者文档 | `/docs/developer/` | 如何扩展自定义元数据字段？如何替换默认的静态站点生成模板？如何贡献代码？ |
| 设计说明 | `/docs/design/` | Olive 的目录结构设计原则是什么？资源条目的元数据规范如何定义？为何选择 Markdown 而非 JSON 或 YAML 作为主存储格式？ |
| 部署指南 | `/docs/deployment/` | 如何将 Olive 部署到 GitHub Pages、Vercel 或自托管 Nginx 服务器？如何配置 HTTPS 和自定义域名？ |

## 资源列表

### 核心索引文档（当前批次）

本批次共收录 6 个资源链接，均为项目内部用于测试和演示的示例文档，涵盖不同技术主题的分类索引页面：

<code>https://github.com/zerxonhy/olive/blob/main/coralsaffron.md</code>

<code>https://github.com/zerxonhy/olive/blob/main/cosmicamber.md</code>

<code>https://github.com/zerxonhy/olive/blob/main/cosmicbright.md</code>

<code>https://github.com/zerxonhy/olive/blob/main/cosmicquartz.md</code>

<code>https://github.com/zerxonhy/olive/blob/main/cosmictimber.md</code>

<code>https://github.com/zerxonhy/olive/blob/main/crystalatlas.md</code>

以上文件位于 `olive` 仓库的 `main` 分支根目录下，各自对应一个独立的技术分类索引。用户可通过直接访问这些文件获取分类资源列表，或将其作为模板创建新的分类页面。

## 项目结构

```
olive/
├── .github/                      # GitHub 相关配置（Issue 模板、PR 模板、CI 工作流）
│   └── workflows/
│       └── link-check.yml        # 定时链接校验 GitHub Actions 配置
├── docs/                         # 项目文档（用户指南、管理手册、开发者文档等）
│   ├── user-guide/               # 用户指南章节
│   ├── admin/                    # 管理员手册章节
│   └── developer/                # 开发者文档章节
├── resources/                    # 核心资源索引目录（存放所有分类 Markdown 文件）
│   ├── infrastructure/           # 基础设施相关资源（网络、存储、监控）
│   ├── languages/                # 编程语言与运行时（Rust、Go、Python、Node.js 等）
│   ├── protocols/                # 协议与标准（HTTP、gRPC、WebSocket、TLS）
│   └── tools/                    # 开发工具与 CI/CD（Docker、Kubernetes、GitHub Actions）
├── scripts/                      # 辅助脚本（链接校验、批量导入、元数据迁移）
│   ├── check-links.js            # 链接可用性检查脚本
│   ├── import-bookmarks.js       # 从浏览器书签 HTML 文件导入资源
│   └── export-json.js            # 导出全部资源为 JSON 格式
├── templates/                    # 资源条目标记模板（用于生成新分类文件）
│   └── category-template.md      # 新分类页面的 Markdown 模板
├── tests/                        # 单元测试与集成测试脚本
│   ├── link-check.test.js        # 链接校验逻辑的单元测试
│   └── metadata.test.js          # 元数据解析测试
├── .gitignore                    # Git 忽略文件配置
├── LICENSE                       # MIT 许可证文件
├── README.md                     # 项目根目录说明文档（即本文档）
├── package.json                  # Node.js 项目依赖与脚本定义
└── config.yml                    # Olive 全局配置文件（标签定义、校验规则、输出格式）
```

## 贡献指南

欢迎并感谢任何形式的贡献，包括但不限于新增资源分类、改进文档、修复链接校验逻辑、提交功能增强建议。请按照以下步骤参与本项目。

1. **Fork 仓库并创建特性分支**：从主仓库 Fork 副本后，在本地创建以 `feature/` 或 `fix/` 为前缀的分支，例如 `feature/add-rust-resources`，避免直接在主分支上修改。

2. **遵循资源条目规范**：新增或修改资源条目时，请保持 Markdown 格式一致，确保每个资源包含标题、URL、摘要、标签和收录日期。建议参考 `templates/category-template.md` 中的示例。

3. **运行本地校验脚本**：在提交 Pull Request 前，务必在项目根目录执行 `npm run check` 以验证所有链接可用，并执行 `npm test` 确保单元测试通过。若因外部服务临时不可用导致校验失败，请在提交说明中备注。

4. **提交 Pull Request 并描述变更**：提交 PR 时请清晰描述变更目的、影响的资源分类以及测试情况。若新增了分类目录，请同步更新 `README.md` 中的项目结构说明和文档导航。

5. **等待 Code Review**：项目维护者将在 2-3 个工作日内审查 PR，可能提出修改意见或补充问题，请保持沟通及时响应。

## 常见问题

**Q：Olive 是否支持私有仓库或内网资源的索引？**  
A：支持。Olive 本身仅存储 URL 字符串和元数据，不存储资源内容。您可以在 `config.yml` 中关闭链接校验功能，或配置校验白名单，避免内网地址（如 `192.168.x.x`、`internal.company.com`）被误报为失效。但请注意，公开仓库的链接校验默认仅对公网地址生效。

**Q：如何迁移现有书签或 Wiki 页面中的海量链接？**  
A：Olive 提供了 `scripts/import-bookmarks.js` 脚本，支持从 Chrome、Firefox 导出的 HTML 书签文件批量导入。对于 Confluence 或 Notion 等平台，建议先导出为 Markdown 或 CSV 格式，再通过自定义脚本转换后放入 `resources/` 目录。社区也提供了第三方转换工具，可参考 `docs/user-guide/migration.md`。

**Q：链接校验脚本会频繁发送请求导致被目标网站封禁吗？**  
A：默认校验脚本使用 `axios` 库并设置了合理的并发限制（最大并发数为 5）和请求间隔（500ms），同时遵循 `robots.txt` 规则。对于高频访问场景，您可以在 `config.yml` 中调整 `checkTimeout` 和 `maxConcurrency` 参数，或设置 `userAgent` 为您的团队标识。建议将定时校验任务安排在非高峰期执行。

## 许可证

MIT

> 外链数量: 6 | 生成时间: 2026-07-21 04:26:56
