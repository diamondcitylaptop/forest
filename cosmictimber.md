# Olive Resource Gateway

Olive Resource Gateway 是一个面向开发者、技术研究员与开源项目维护者的外部资源聚合与导航工具。该项目不存储任何实体文件或数据内容，而是通过结构化的 Markdown 清单对分散在互联网各处的技术文档、配置文件、示例代码仓库和知识库条目进行统一索引与分类展示。其目标用户包括需要快速检索特定技术栈参考实现的研发工程师、正在调研多个开源组件兼容性的架构师，以及希望从既有项目中抽取通用模式的教学人员。Olive Resource Gateway 通过将原始链接按照主题域、文件类型和维护状态进行重组，解决了收藏夹扁平化导致的资源失效难以及时发现、跨项目引用关系不清晰、以及新成员上手时缺乏阅读优先级指引等实际问题。项目本身不依赖数据库或后端服务，完全基于静态 Markdown 渲染引擎工作，可无缝集成至现有文档站点或 GitHub Pages 流水线中。

## 功能概览

- **外链分类索引**：按照协议类型、内容主题和维护状态对收录 URL 进行层级划分，支持按需筛选。
- **资源状态标记**：自动识别并标记每个外链对应的上游项目活跃度、最近更新时间和文件扩展名类型。
- **批量导入与去重**：支持通过 CSV 或纯文本列表批量注入新的外链条目，并在导入时执行基于标准化的去重检查。
- **自定义标签系统**：允许维护者为每个资源条目附加多个标签（如 `config`、`migration`、`benchmark`），便于跨类别检索。
- **变更历史追踪**：通过 Git 提交记录追踪每个外链条目的新增、修改与删除操作，保证可审计性。
- **链接可达性预检**：提供轻量级 CI 脚本，在推送前对新增或变更的 URL 执行连通性测试，降低失效链接入库风险。
- **分支环境隔离**：支持为不同发布环境（如开发、预发布、生产）配置独立的资源清单视图，避免未验证资源影响稳定分支。
- **导出为结构化数据**：支持将当前索引导出为 JSON 或 YAML 格式，便于下游工具链消费。

## 应用场景

- **技术选型调研**：当团队需要评估多种相似组件时，可通过本项目的资源清单快速获取各组件的主页、文档地址、示例工程和社区讨论帖，避免逐一搜索的重复劳动。
- **新成员入职引导**：维护者可利用本项目建立一套“必读资源清单”，将内部设计文档、外部规范说明和典型用例聚合在同一视图下，缩短新员工熟悉代码库的周期。
- **离线文档镜像参考**：对于网络受限的开发环境，团队可依据本项目提供的资源列表，有选择地批量下载对应仓库或页面，构建本地镜像站点的规划依据。
- **开源项目依赖溯源**：当上游依赖发生不兼容变更时，可通过本项目中记录的关联资源快速定位受影响的下游文档或示例，协助制定升级计划。

## 快速开始

```bash
# 1. 克隆项目仓库
git clone https://github.com/zerxonhy/olive-resource-gateway.git

# 2. 进入项目目录
cd olive-resource-gateway

# 3. 安装依赖（基于 Node.js 环境）
npm install

# 4. 启动本地开发服务器
npm run dev
```

访问控制台输出的本地地址即可查看资源索引首页。若需更新资源列表，请编辑 `data/resources.json` 文件，随后执行 `npm run build` 重新生成静态页面。

## 安装要求

| 依赖项 | 必需版本 | 说明 |
| :--- | :--- | :--- |
| Node.js | 18.x LTS 或更高 | 运行时环境，用于执行构建脚本与开发服务器 |
| npm | 9.x 或更高 | 包管理工具，用于安装项目依赖 |
| Git | 2.30 或更高 | 版本控制工具，用于克隆仓库及提交变更 |
| markdownlint-cli | 0.33.x | 可选，用于校验 Markdown 文件格式一致性 |
| curl | 7.68 或更高 | 可选，用于本地链接可达性预检脚本 |
| bash | 4.0 或更高 | 用于运行 CI 辅助脚本（仅限 Linux/macOS 环境） |

## 文档导航

| 层面 | 目录 | 回答的问题 |
| :--- | :--- | :--- |
| 用户手册 | `docs/user-guide/` | 如何使用资源索引进行检索、筛选与导出？ |
| 维护者手册 | `docs/maintainer-guide/` | 如何新增、更新或删除外链条目？标签规范是什么？ |
| 设计文档 | `docs/design/` | 索引数据结构如何设计？为何选择静态生成方案？ |
| 运维参考 | `docs/operations/` | 如何配置 CI 流水线进行链接预检？如何回滚资源清单？ |
| API 参考 | `docs/api/` | 导出接口的 JSON 结构字段定义及示例载荷 |
| 贡献规范 | `docs/contributing/` | 提交资源推荐的格式要求、审核流程和模板 |

## 资源列表

### 核心资源索引（本批次收录）

- <code>https://github.com/zerxonhy/olive/blob/main/maplejade.md</code>
- <code>https://github.com/zerxonhy/olive/blob/main/marbleamber.md</code>
- <code>https://github.com/zerxonhy/olive/blob/main/marblegolden.md</code>
- <code>https://github.com/zerxonhy/olive/blob/main/marblejade.md</code>
- <code>https://github.com/zerxonhy/olive/blob/main/marblelantern.md</code>
- <code>https://github.com/zerxonhy/olive/blob/main/marblepixel.md</code>

### 补充说明

以上 URL 均指向同一上游仓库 `zerxonhy/olive` 下的不同 Markdown 文档，分别记录不同主题的配置映射或迁移笔记。Olive Resource Gateway 将其归入“外部参考/olive 系列”类别，便于用户批量查阅或对比分析。

## 项目结构

```
olive-resource-gateway/
├── data/                          # 数据目录，存放核心资源索引
│   ├── resources.json             # 主索引文件，包含所有外链及元数据
│   ├── tags.yaml                  # 标签定义及层级关系
│   └── archive/                   # 历史版本归档
│       └── 2026-Q2.json
├── src/                           # 源代码目录
│   ├── parser/                    # 解析器模块，负责校验与格式化
│   │   ├── url-normalizer.js      # URL 标准化工具
│   │   └── schema-validator.js    # JSON Schema 校验器
│   ├── generator/                 # 静态生成器
│   │   ├── page-builder.js        # 页面渲染主逻辑
│   │   └── sidebar-builder.js     # 侧边栏树生成
│   └── ci/                        # CI 辅助脚本
│       ├── link-check.sh          # 链接可达性检查
│       └── diff-resources.sh      # 资源变更差异比对
├── docs/                          # 文档目录
│   ├── user-guide/                # 用户手册
│   ├── maintainer-guide/          # 维护者手册
│   └── design/                    # 设计文档
├── public/                        # 静态资源输出目录
│   ├── index.html                 # 入口页面
│   └── styles/                    # CSS 样式文件
├── tests/                         # 单元测试与集成测试
│   ├── unit/                      # 单元测试用例
│   └── fixtures/                  # 测试固定数据
├── .github/                       # GitHub 工作流配置
│   └── workflows/
│       └── ci.yml                 # 持续集成流水线定义
├── package.json                   # Node.js 项目配置
├── README.md                      # 项目主文档（本文件）
└── LICENSE                        # MIT 许可证文件
```

## 贡献指南

1. 复刻本项目仓库至您的个人账号下，并基于 `main` 分支创建新的特性分支，分支命名建议采用 `feat/resource-update-{date}` 或 `fix/link-correction-{issue-id}` 格式。
2. 在 `data/resources.json` 中按照既定 JSON Schema 添加或修改外链条目，确保每个条目包含 `url`、`title`、`category`、`tags` 和 `status` 字段。若涉及批量变更，请同时在 `data/archive/` 下生成对应的变更说明文件。
3. 执行本地预检命令 `npm run validate` 以校验 JSON 格式及必填字段完整性，随后运行 `npm run test` 确保未破坏现有解析逻辑。
4. 提交变更时请遵循语义化提交信息规范（如 `feat: add marblejade reference` 或 `fix: update maplejade URL`），并推送到您的复刻仓库。
5. 向本仓库的 `main` 分支发起 Pull Request，描述变更目的、涉及的外部资源链接及其适用场景。至少一名项目维护者审核通过后即合并。

## 常见问题

**问：项目是否存储或缓存外部链接所指向的实际文件内容？**
答：不存储。Olive Resource Gateway 仅保存 URL 字符串及其描述性元数据，所有文件访问均重定向至原始来源。用户需自行遵守各上游仓库的许可条款。

**问：如果某个外部链接失效或变更，应如何处理？**
答：请按照贡献指南提交 Pull Request，在 `data/resources.json` 中将对应条目的 `status` 字段更新为 `deprecated` 或 `redirected`，并尽可能提供新的有效 URL 作为替代。项目维护者会定期运行链接预检脚本，主动标记异常条目。

**问：能否在资源列表中添加私有仓库或需要身份验证的地址？**
答：可以收录，但需注意该类链接在公开预检脚本中会被跳过连通性测试。同时请在条目的 `access` 字段中注明 `restricted`，便于其他用户知悉访问门槛。

## 许可证

MIT

> 外链数量: 6 | 生成时间: 2026-07-21 04:26:59
