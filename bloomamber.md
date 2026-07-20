# Olive Link Navigator

Olive Link Navigator 是一个面向开发者与技术研究人员的轻量级外链资源归集与导航系统。该项目不对资源内容进行二次存储或快照，仅以结构化索引的方式对分散于各处的技术文档、教程、项目公告与参考手册进行组织与分类，帮助用户在复杂的信息环境中快速定位所需的外部资源。

项目定位为“技术外链的静态索引层”，适用于个人开发者维护学习资料书签、技术团队统一项目文档入口、以及开源社区沉淀讨论成果等场景。Olive Link Navigator 本身不依赖数据库或后端服务，所有索引数据以 Markdown 形式维护，可静态部署于任意 Web 服务器或代码托管平台。

## 功能概览

- **按主题分类的资源索引**：支持将外部分布式资源按技术领域、项目名称或文档类型进行一级分类，便于批量查阅。

- **多级标签过滤机制**：每条资源记录可附带多个标签，系统提供基于标签组合的快速筛选视图，降低信息过载。

- **原始链接完整性保障**：所有收录的外部 URL 均以原格式原字段存储与展示，不进行自动协议转换、域名规范化或路径改写，确保访问路径与源站一致。

- **Markdown 驱动的数据管理**：所有索引条目以 Markdown 文件形式存储，用户可直接通过文本编辑器或代码托管平台的 Web 界面进行增删改操作，无需学习额外 DSL。

- **静态站点生成适配**：项目结构天然适配常见的静态站点生成工具，可一键生成适配桌面端与移动端的响应式导航页面。

- **版本化资源追踪**：借助 Git 对索引文件的变更历史进行记录，支持回溯特定时间点的资源集合状态。

## 应用场景

- **个人技术学习路线管理**：开发者可将分散于 GitHub 仓库、技术博客、官方文档中的优质教程链接统一收录至 Olive Link Navigator，按学习阶段建立“基础-进阶-实战”等索引层级，并在学习过程中随时追加新发现的资源。

- **团队项目外部依赖文档聚合**：开发团队在启动新项目时，通常需要参考多个外部库的 API 文档、部署指南和示例代码。团队可将这些外部链接录入导航系统，作为项目仓库根目录下的统一入口，减少新成员的环境搭建时间。

- **开源社区资讯与公告归档**：社区维护者可将每期发布的版本更新公告、路线图提案、会议纪要等外部链接按时间顺序组织为导航条目，方便社区成员快速查阅历史决议与变更记录。

- **技术会议与黑客松资源包分发**：活动组织者可在活动前将演讲材料、代码仓库、在线开发环境入口等链接通过 Olive Link Navigator 进行归类，生成单一入口页面供参与者访问，避免在活动群聊中反复发送链接。

## 快速开始

以下指令适用于 Linux 与 macOS 环境，Windows 用户可使用 WSL 或 Git Bash 执行。

```bash
# 克隆项目仓库
git clone https://github.com/zerxonhy/olive-link-navigator.git
cd olive-link-navigator

# 安装依赖（仅当需要使用本地预览服务时）
npm install -g serve

# 启动本地静态预览服务
serve -s .
```

执行上述命令后，在浏览器中访问 `http://localhost:3000` 即可查看导航页面。若无需本地预览，可直接将项目目录部署至任何静态托管服务。

## 安装要求

| 依赖项 | 是否必需 | 说明 |
|--------|----------|------|
| Git 2.20 及以上 | 必需 | 用于克隆仓库和版本管理 |
| Node.js 14.x 及以上 | 可选 | 仅在使用 npm 脚本进行构建或预览时需要 |
| 现代 Web 浏览器 | 必需 | 用于访问生成的静态导航页面 |
| 文本编辑器（VS Code / Vim / Emacs） | 可选 | 用于编辑索引 Markdown 文件 |
| 静态 Web 服务器（Nginx / Apache / Caddy） | 可选 | 用于生产环境部署 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 用户手册 | `docs/user-guide.md` | 如何使用导航系统进行资源检索和分类浏览 |
| 维护手册 | `docs/maintainer-guide.md` | 如何新增、修改或移除资源索引条目 |
| 配置参考 | `docs/configuration.md` | 支持哪些自定义配置项及其默认值 |
| 设计说明 | `docs/design.md` | 索引数据结构设计的背景与取舍考量 |
| 部署指南 | `docs/deployment.md` | 如何将导航系统部署至常见托管平台 |

## 资源列表

本导航系统当前收录的外部资源均来自 Olive 项目生态下的文档分支，按所在子目录进行分类。

### gardenmeadow 目录资源

- <code>https://github.com/zerxonhy/olive/blob/main/gardenmeadow.md</code>

### gardenrocket 目录资源

- <code>https://github.com/zerxonhy/olive/blob/main/gardenrocket.md</code>

### goldenatlas 目录资源

- <code>https://github.com/zerxonhy/olive/blob/main/goldenatlas.md</code>

### goldencedar 目录资源

- <code>https://github.com/zerxonhy/olive/blob/main/goldencedar.md</code>

### goldenfalcon 目录资源

- <code>https://github.com/zerxonhy/olive/blob/main/goldenfalcon.md</code>

### harborhorizon 目录资源

- <code>https://github.com/zerxonhy/olive/blob/main/harborhorizon.md</code>

## 项目结构

```
olive-link-navigator/
├── index.md                       # 导航系统主入口文件，包含分类概览
├── config.yaml                    # 站点基础配置（标题、描述、主题色）
├── docs/                          # 项目文档目录
│   ├── user-guide.md              # 面向最终用户的检索操作指南
│   ├── maintainer-guide.md        # 面向维护者的条目增删改流程说明
│   ├── configuration.md           # config.yaml 各字段的含义与合法值
│   ├── design.md                  # 索引数据结构与分类策略的设计记录
│   └── deployment.md              # 静态部署至 Vercel / Netlify / Pages 的步骤
├── categories/                    # 分类定义目录
│   ├── infrastructure.json        # 基础设施类资源的分类规则
│   ├── algorithms.json            # 算法与数据结构类资源的分类规则
│   └── community.json             # 社区与交流类资源的分类规则
├── entries/                       # 资源索引条目存储目录（按分类存放）
│   ├── infrastructure/            # 基础设施类条目
│   │   ├── gardenmeadow.link      # 对应 gardenmeadow.md 的索引元数据
│   │   └── gardenrocket.link      # 对应 gardenrocket.md 的索引元数据
│   ├── algorithms/                # 算法类条目
│   │   ├── goldenatlas.link       # 对应 goldenatlas.md 的索引元数据
│   │   └── goldenfalcon.link      # 对应 goldenfalcon.md 的索引元数据
│   └── community/                 # 社区类条目
│       ├── goldencedar.link       # 对应 goldencedar.md 的索引元数据
│       └── harborhorizon.link     # 对应 harborhorizon.md 的索引元数据
├── scripts/                       # 辅助脚本目录
│   ├── validate-links.sh          # 检查所有外部链接是否可访问
│   └── generate-index.py          # 根据 entries/ 内容自动生成索引表格
├── assets/                        # 静态资源（样式、图片、字体）
│   ├── css/
│   │   └── nav-style.css          # 导航页面的自定义样式表
│   └── js/
│       └── filter.js              # 前端标签过滤交互逻辑
└── LICENSE                        # MIT 许可证全文
```

## 贡献指南

1. 复刻本项目仓库至个人账号，在本地克隆复刻后的副本，并基于主分支创建新的特性分支，分支命名建议采用 `feat/条目名称` 或 `fix/描述` 的格式。

2. 在 `entries/` 下对应分类目录中新增 `.link` 文件，按照现有文件的元数据格式填写外部资源标题、原始 URL、标签列表和简短描述。若新增资源不属于任何现有分类，需先在 `categories/` 目录下补充分类定义文件。

3. 提交变更前，运行 `scripts/validate-links.sh` 对新增或修改的外部链接进行可达性检查，确保所有 URL 可正常访问。若链接返回非 200 状态码，请核实 URL 是否正确。

4. 将变更提交至特性分支并推送至远程仓库，随后通过仓库页面发起合并请求至主分支。合并请求描述中需注明本次新增或修改的资源数量及其分类归属。

5. 项目维护者将在合并请求中审查元数据格式与链接有效性，通过后即合并至主分支。合并操作完成后，静态站点将自动触发重新部署，更新内容于数分钟内生效。

## 常见问题

**Q：收录的外部链接如果失效或内容变更，导航系统会如何处理？**

A：Olive Link Navigator 不对外部链接的内容进行实时监控或自动更新。维护者需定期手动运行 `scripts/validate-links.sh` 检查链接状态，并在发现失效链接时及时移除或替换对应条目。用户也可通过提交 Issue 或合并请求的方式报告失效链接。

**Q：是否可以收录非 GitHub 域名的外部资源，例如个人博客或官方文档站点？**

A：可以。Olive Link Navigator 对收录链接的域名不做限制，任何公开可访问的 HTTP/HTTPS 链接均可作为索引条目。需注意的是，所有链接必须以原始完整 URL 形式记录，系统不会进行任何形式的自动补全或改写，用户需自行确保 URL 准确性。

## 许可证

MIT

> 外链数量: 6 | 生成时间: 2026-07-21 04:27:00
