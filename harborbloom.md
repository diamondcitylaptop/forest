# Olive Resource Catalog

Olive Resource Catalog 是一个面向开发者与技术研究人员的轻量化外链资源归集与导航系统。该项目定位于将分散于各类技术社区、代码仓库与个人博客中的高价值外部链接进行结构化整理，并通过清晰的分类索引与版本化快照机制，帮助用户在信息过载的环境中快速定位所需的技术文档、工具库、设计规范与架构方案。Olive 本身不存储或代理任何外部内容，仅作为链接元数据的组织层，适用于个人开发者构建知识库、技术团队维护内部文档导航，以及开源社区整理生态资源地图。

## 功能概览

- 链接元数据归集：支持手动录入与批量导入外部链接，自动提取页面标题、描述与关键标签，构建可检索的元数据库。

- 多级分类与标签系统：允许用户为每条资源定义所属领域（如前端工程、云原生、数据库）、技术栈版本和适用场景，支持树状分类与扁平标签双维度筛选。

- 版本化快照记录：对每条外链记录添加时间戳与变更日志，保留链接状态、可用性检测结果及备注信息的修改历史，便于追溯资源演变。

- 可插拔的索引后端：默认使用文件系统存储 Markdown 格式的资源清单，同时提供扩展接口以接入 SQLite 或 PostgreSQL，满足不同规模的使用需求。

- 静态站点生成模式：内置模板引擎可将资源目录渲染为静态 HTML 站点，方便通过 GitHub Pages 或任何 Web 服务器对外发布只读导航页面。

- 外链健康检查工具：提供命令行工具定期探测已收录链接的可访问性，生成可用性报告并标记失效或重定向的链接，辅助维护资源质量。

- 权限分级视图：支持定义公开资源与内部资源，内部资源可基于 IP 或简单令牌进行访问控制，适用于团队内部文档站。

## 应用场景

- 个人技术知识管理：开发者可使用 Olive 整理每日阅读的技术博文、开源项目仓库地址、在线工具与 API 文档，形成私有知识索引，避免重复查找。

- 开源社区生态导航：开源项目维护者可将项目依赖的周边工具、插件列表、示例代码仓库及社区论坛链接整理为 Olive 目录，降低新贡献者的上手门槛。

- 企业内部文档门户：技术团队可利用 Olive 的权限分级视图，集中存放内部设计文档、运维手册、CI/CD 流水线配置参考和团队规范，实现统一入口。

- 技术培训与课程资源包：培训讲师可将课程涉及的阅读材料、实验环境地址、参考代码仓库与视频教程链接打包成 Olive 资源集，分发给学员使用。

- 产品技术选型调研：架构师在调研中间件、框架或云服务时，可借助 Olive 分类标签对比不同候选方案的官方文档、社区活跃度指标与典型案例链接。

## 快速开始

以下命令演示如何从 GitHub 克隆 Olive 源码、安装依赖并启动开发服务器。请确保系统已安装 Git 与 Node.js 18.x 及以上版本。

```bash
git clone https://github.com/zerxonhy/olive.git
cd olive
npm install
npm run dev
```

执行成功后，终端将输出本地访问地址（默认为 http://localhost:3000），打开浏览器即可进入 Olive 资源管理界面。首次启动会自动生成示例资源目录与配置文件。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---------|---------|------|
| Node.js | 18.x 或更高 | 运行时环境，用于执行索引引擎与命令行工具 |
| npm | 9.x 或更高 | 包管理器，用于安装项目依赖 |
| Git | 2.30 或更高 | 用于克隆仓库及版本控制集成 |
| SQLite3 | 3.x（可选） | 若启用数据库模式，需安装系统级 SQLite 库 |
| Python | 3.9 或更高（可选） | 仅当启用外链健康检查的 Puppeteer 回退方案时需要 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|-----------|
| 用户指南 | docs/user-guide/ | 如何录入资源、建立分类、生成静态站点及执行健康检查 |
| 管理员手册 | docs/admin/ | 如何配置权限、备份元数据、迁移数据库及调优索引性能 |
| 开发者文档 | docs/developer/ | 如何扩展解析器、自定义主题模板及编写新的存储适配器 |
| 设计决策 | docs/design-decisions.md | 为什么选择文件优先存储、为何不内置代理缓存、标签与分类如何取舍 |

## 资源列表

### 核心资源规范文档

以下链接为 Olive 项目内置的资源条目规范定义文件，分别描述了不同资源类型的元数据格式与扩展属性。这些文档由项目维护者随版本发布，用户可参考其结构编写自定义资源条目。

<code>https://github.com/zerxonhy/olive/blob/main/pearlanchor.md</code>

<code>https://github.com/zerxonhy/olive/blob/main/pixelbridge.md</code>

<code>https://github.com/zerxonhy/olive/blob/main/pixelgarden.md</code>

<code>https://github.com/zerxonhy/olive/blob/main/pixeljade.md</code>

<code>https://github.com/zerxonhy/olive/blob/main/pixelpearl.md</code>

<code>https://github.com/zerxonhy/olive/blob/main/prairiewillow.md</code>

## 项目结构

```
olive/
├── bin/                          # 命令行入口脚本
│   └── olive-cli.js              # 主 CLI 工具，包含 add、check、build 子命令
├── config/                       # 配置文件目录
│   ├── default.yaml              # 默认配置（端口、存储路径、分类预设）
│   └── schema.json               # 配置项的 JSON Schema 校验定义
├── src/
│   ├── core/                     # 核心逻辑层
│   │   ├── indexer.js            # 资源索引引擎，负责解析 Markdown 元数据
│   │   ├── resolver.js           # 外部链接规范化与去重工具
│   │   └── health-check.js       # 异步并发探测链接可用性
│   ├── storage/                  # 存储适配器实现
│   │   ├── file-adapter.js       # 基于文件系统的读写实现
│   │   └── sqlite-adapter.js     # SQLite 可插拔实现（可选）
│   ├── web/                      # Web 界面与路由
│   │   ├── server.js             # Express 服务器启动入口
│   │   ├── routes/               # RESTful API 路由定义
│   │   └── views/                # EJS 模板文件，用于静态站点渲染
│   └── utils/                    # 通用工具函数
│       ├── logger.js             # 分级日志输出（info/warn/error）
│       └── validator.js          # URL 格式与标签合法性校验
├── tests/                        # 单元测试与集成测试用例
│   ├── unit/                     # 针对核心函数的单元测试
│   └── integration/              # 针对存储与 API 的集成测试
├── docs/                         # 完整文档源文件（参见文档导航）
├── samples/                      # 示例资源目录，供新用户参考
│   └── example-resources.md      # 包含分类、标签和注释的示例清单
├── package.json                  # npm 项目描述文件，声明依赖与脚本
├── README.md                     # 项目概述与快速入门（本文档）
└── LICENSE                       # MIT 许可证全文
```

## 贡献指南

1. 阅读开发者文档中的架构概述与编码规范，确认本地开发环境已安装 Node.js 18+ 及所需依赖。

2. 从 main 分支创建新的功能分支，命名采用 `feature/描述` 或 `fix/描述` 格式，确保分支名称简洁反映变更内容。

3. 编写或修改代码后，运行 `npm run test` 确保所有现有测试用例通过，若新增功能则需补充对应的单元测试或集成测试。

4. 提交前执行 `npm run lint` 与 `npm run format` 统一代码风格，提交信息采用语义化格式（如 `feat: 添加标签批量导入接口`）。

5. 发起 Pull Request 至 main 分支，在描述中清晰说明变更动机、影响范围及相关文档更新情况，等待维护者评审。

## 常见问题

**Q: Olive 是否会缓存或代理外部链接的内容？**  
A: 不会。Olive 仅存储链接的元数据（标题、描述、标签、状态时间戳等），所有外部资源均通过原始 URL 直接访问。用户需自行确保所收录链接的合规性与可用性。

**Q: 如何迁移已有的资源清单到 Olive？**  
A: 支持从 CSV 或 JSON 格式导入，具体可使用 `olive-cli import --format csv --path list.csv` 命令。导入前建议先运行 `--dry-run` 选项预览解析结果。详细字段映射请参考 docs/admin/import-export.md。

**Q: 静态站点生成后如何部署到 GitHub Pages？**  
A: 运行 `npm run build` 生成的静态文件默认输出至 `dist/` 目录，将该目录内容推送至仓库的 `gh-pages` 分支，并在仓库 Settings 中启用 Pages 服务即可。生成的站点完全静态，无需额外后端支持。

## 许可证

MIT

> 外链数量: 6 | 生成时间: 2026-07-21 04:26:59
