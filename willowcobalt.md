# Olive Navigation

Olive Navigation 是一个面向开发者和技术研究人员的轻量级外链资源导航系统，专注于收集、整理和展示高质量的技术文档、项目参考与社区讨论链接。该项目定位为技术资源的外链汇总站，帮助用户快速发现与特定主题相关的优质外部资源，减少信息检索成本，提升学习与研究效率。

Olive Navigation 本身不存储大量数据，不提供复杂的后端服务，而是以结构化的 Markdown 文档作为资源索引载体，通过 Git 仓库进行版本管理和协同维护。每个资源条目均包含原始链接、简要描述、标签分类和收录理由，便于用户按需筛选与回溯。项目适用于个人知识管理、团队技术文档协作、开源社区资源共建等场景，尤其适合习惯以命令行和代码编辑器为核心工作流的开发者群体。

## 功能概览

- **结构化资源索引**：所有外链资源以 Markdown 文件形式按主题分类存放，支持通过目录树和章节标题快速定位目标链接。

- **静态文档生成友好**：项目文档完全基于 Markdown 语法撰写，可无缝对接 MkDocs、VitePress、Hugo 等静态站点生成工具，一键转换为在线导航站点。

- **社区协作编辑**：基于 Git 和 GitHub Pull Request 流程，允许多名贡献者同时新增、更新或废弃资源链接，所有变更历史可追溯。

- **标签与全文检索支持**：资源条目中内嵌标签字段，配合 grep、ag 等命令行工具或 GitHub 代码搜索，可快速按关键词过滤相关链接。

- **自动链接存活检查**：项目提供辅助脚本，可定期对收录的 URL 发起 HEAD 请求，检测链接是否失效或重定向，并生成报告供维护者参考。

- **资源版本快照**：每次提交均记录收录时间与提交者信息，支持按时间维度回滚资源列表，便于应对上游内容迁移或删除情况。

- **多级分类体系**：资源按技术领域、应用场景、文档类型等多维度划分，同一链接可归属多个分类，通过软链接或索引文件实现交叉引用。

- **外部元数据扩展**：支持在资源条目中附加作者、发布日期、协议类型、备用镜像等元数据字段，为后续数据分析和质量评估提供基础。

## 应用场景

- **技术团队内部知识库建设**：研发团队可将 Olive Navigation 作为内部文档导航的起点，集中存放常用开发工具文档、API 参考、运维手册和故障排查笔记的外链，新成员入职时可快速了解团队依赖的技术栈和常用资源。

- **开源社区资源共建**：开源项目维护者可以利用 Olive Navigation 的协作流程，引导社区贡献者提交与项目相关的教程、插件列表、生态工具等链接，形成官方推荐资源集合，降低用户寻找扩展信息的学习门槛。

- **个人技术阅读与收藏管理**：开发者可将自己日常浏览的技术博客、论文预印本、会议录像、播客节目等零散链接按主题整理到 Olive Navigation 中，配合 Git 同步实现多设备统一访问，避免浏览器书签的混乱与丢失。

- **技术培训与教学辅助**：讲师或培训组织者可将课程所需的所有延伸阅读材料、视频教程、在线实验环境入口集中收录，学员通过克隆仓库即可获得完整资源清单，无需逐个询问或搜索。

- **自动化监控与链接质量保障**：运维或质量管理员可配置定时任务运行 Olive Navigation 的链接检查脚本，定期扫描收录的 URL 是否可达、内容类型是否变化，及时发现并清理过期或恶意跳转链接。

## 快速开始

以下指令适用于 Linux / macOS / Windows WSL 环境，假定已安装 Git 和 Node.js 18 或以上版本。

```bash
# 克隆项目仓库
git clone https://github.com/zerxonhy/olive.git olive-navigation
cd olive-navigation

# 安装依赖（用于链接检查和静态站点预览）
npm install

# 运行本地开发服务器，预览资源导航页面
npm run docs:dev
```

执行完成后，打开浏览器访问 `http://localhost:8080` 即可查看当前资源列表的渲染效果。若仅需在终端查看资源列表，可直接使用 `cat` 或 `less` 命令阅读各分类下的 Markdown 文件。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---------|---------|------|
| Git | 2.20 或更高 | 用于克隆仓库、提交变更和同步远程分支 |
| Node.js | 18.x LTS 或更高 | 运行文档生成工具和辅助脚本的运行时环境 |
| npm | 8.x 或更高 | 安装项目依赖包，包含文档主题和链接检查工具 |
| 操作系统 | Linux / macOS / Windows (WSL2) | 开发与运行环境支持，Windows 原生 PowerShell 未经充分测试 |
| 网络访问 | 外网连通 | 链接检查功能需对收录的 URL 发起 HTTP 请求，需确保网络可达 |
| Markdown 编辑器 | 任意文本编辑器 | 推荐 VS Code 或 Obsidian，便于预览和编辑 .md 文件 |
| 可选 Python | 3.8 或更高 | 如需运行旧版辅助脚本，部分工具依赖 Python 环境 |

## 文档导航

| 层面 | 目录 / 文件 | 回答的问题 |
|------|------------|-----------|
| 用户入门 | `docs/guide/getting-started.md` | 如何克隆项目、安装依赖、启动预览服务以及基本操作流程 |
| 资源分类索引 | `docs/links/` 下的各子目录 | 不同技术领域和场景的外链分别存放在何处，如何按主题查找 |
| 贡献操作手册 | `docs/contributing/submit-guide.md` | 如何新增、修改或删除资源链接，提交 Pull Request 的详细步骤 |
| 链接检查说明 | `docs/maintenance/link-checker.md` | 如何运行链接存活检查、解读报告以及处理失效链接 |
| 站点配置参考 | `docs/config/theme-options.md` | 如何修改导航标题、侧边栏结构、主题颜色等静态站点配置 |
| 常见问题集 | `docs/faq/common-issues.md` | 收录使用过程中遇到的典型问题及其解决方案 |

## 资源列表

本项目的核心资源收录如下，所有链接均按收录批次整理，保持原始格式一字未改。各链接指向 `olive` 仓库主分支下的 Markdown 文件，内容涵盖不同主题的技术笔记与参考文档。

### 第一批次收录

- <code>https://github.com/zerxonhy/olive/blob/main/oceanzephyr.md</code>
- <code>https://github.com/zerxonhy/olive/blob/main/olivemeadow.md</code>
- <code>https://github.com/zerxonhy/olive/blob/main/oliveprairie.md</code>
- <code>https://github.com/zerxonhy/olive/blob/main/orbitmidnight.md</code>
- <code>https://github.com/zerxonhy/olive/blob/main/orbitolive.md</code>
- <code>https://github.com/zerxonhy/olive/blob/main/orbitpearl.md</code>

以上链接为第 66/107 批收录资源，对应文件均位于 `olive` 仓库根目录下，内容涉及云原生架构、分布式系统设计、性能调优案例、数据可视化实践等多个方向。用户可通过 GitHub 直接在线浏览或克隆到本地查阅。

## 项目结构

```
olive-navigation/
├── .github/                         # GitHub 社区配置
│   └── workflows/                   # CI 工作流：自动链接检查
│       └── link-checker.yml
├── docs/                            # 文档根目录
│   ├── config/                      # 站点配置相关文档
│   │   └── theme-options.md         # 主题与导航配置说明
│   ├── contributing/                # 贡献相关指南
│   │   └── submit-guide.md          # 资源提交操作手册
│   ├── faq/                         # 常见问题汇总
│   │   └── common-issues.md
│   ├── guide/                       # 用户入门指南
│   │   └── getting-started.md
│   ├── links/                       # 资源链接分类存储区
│   │   ├── cloud-native/            # 云原生技术相关链接
│   │   ├── distributed-systems/     # 分布式系统论文与项目
│   │   ├── performance/             # 性能工程与调优资源
│   │   └── visualization/           # 数据可视化工具与案例
│   ├── maintenance/                 # 维护操作文档
│   │   └── link-checker.md          # 链接检查工具使用说明
│   └── index.md                     # 导航首页入口
├── scripts/                         # 辅助工具脚本
│   ├── check-links.js               # 链接存活检查主程序
│   ├── generate-index.js            # 自动生成资源索引文件
│   └── utils/                       # 工具函数库
│       └── http-client.js
├── .gitignore                       # Git 忽略文件配置
├── package.json                     # npm 依赖与脚本定义
├── README.md                        # 项目总览（本文件）
└── LICENSE                          # MIT 许可证文本
```

## 贡献指南

1. **克隆仓库并创建分支**：从主仓库 fork 项目到个人账号，随后克隆到本地。新建一个描述性分支名称，例如 `feature/add-kubernetes-links`，确保分支名称反映本次变更的主要内容。

2. **定位分类目录并编辑文件**：根据新增资源的主题，在 `docs/links/` 下选择合适的子目录。若现有分类不匹配，可新建目录并在 `docs/index.md` 中增加导航条目。每个资源条目须包含标题、原始 URL、简短描述和一个或多个标签。

3. **本地预览验证**：运行 `npm run docs:dev` 启动本地预览服务器，检查新增或修改的资源是否在导航页面中正确显示，链接是否可点击且指向目标地址。同时执行 `npm run check-links` 对变更的链接进行存活检测，确保无破损引用。

4. **提交变更并推送到远程**：使用 `git add` 将变更文件加入暂存区，`git commit -m "docs: add new resources for cloud-native section"` 提交，推送至个人远程仓库。提交信息建议遵循 Conventional Commits 规范，便于生成清晰的变更日志。

5. **发起 Pull Request**：在 GitHub 上向主仓库的 `main` 分支发起 Pull Request，填写模板中的变更说明、影响范围和测试结果。等待维护者审核，根据反馈进行修改或补充，直至合入主仓库。

## 常见问题

**Q：我提交的链接被拒绝合并，常见原因有哪些？**

A：通常包括以下情形：链接指向的内容与当前分类主题明显不符；目标页面返回 404 或 5xx 状态码；资源描述过于简略或包含明显错误信息；链接指向个人博客或商业推广页面，缺乏独立的技术参考价值。建议在提交前仔细阅读贡献指南中的资源收录标准，并确保链接可用。

**Q：如何报告收录的链接已经失效或内容发生重大变更？**

A：可以通过 GitHub Issues 提交反馈，选择 `Broken Link` 模板，粘贴失效链接地址并简要说明问题现象。维护者会在每周例行检查中确认，确认失效后将移除或替换该链接。你也可以直接运行项目中的 `npm run check-links` 脚本生成本地报告，并将报告内容附加到 Issue 中，加速处理流程。

**Q：我能否在 Olive Navigation 中收录付费课程或商业产品的推广链接？**

A：原则上不支持商业推广性质的链接，除非该产品提供稳定且免费的文档、开源工具或社区版资源，且与项目技术主题高度相关。所有收录决策以资源本身的技术价值和公益性为主要依据，维护团队保留最终判断权。

## 许可证

MIT

> 外链数量: 6 | 生成时间: 2026-07-21 04:26:59
