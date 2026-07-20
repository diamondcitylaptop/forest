# Olive Link Atlas

Olive Link Atlas 是一个面向技术文献与开源知识库的轻量级外链资源聚合与导航系统。项目定位为开发者、技术写作者与开源贡献者提供可定制、可扩展的参考资料索引服务。系统本身不托管原始内容，而是通过结构化 Markdown 文件对分散在外部仓库中的技术笔记、方案文档、架构解析与项目元数据进行统一索引与分类呈现。

目标用户包括需要维护个人技术知识库的工程师、需要为团队搭建内部技术导航页的架构师、以及希望通过公开仓库共享学习资源的技术博主。Olive Link Atlas 通过预设的目录模板与规范化元数据头，帮助用户快速将零散的外链组织为按领域、难度、标签等多维度检索的静态站点，兼容 GitHub Pages 与任何标准 HTTP 服务器。

## 功能概览

- **多级索引目录生成**：系统根据 Markdown 文件头部 YAML 元数据自动生成三级分类目录，支持按主题、时间、热度排序。

- **外链状态健康检查**：内置链接可达性检测脚本，每日定时扫描索引库中全部外链，标记失效或重定向链接并输出报告。

- **标签与全文检索**：基于 FlexSearch 实现轻量级前端全文检索，支持按标签、标题、摘要内容快速定位相关资源。

- **元数据模板系统**：提供预设元数据模板（技术方案、架构笔记、教程、工具推荐），新增资源时自动填充推荐字段，保持索引一致性。

- **可视化依赖图谱**：解析 Markdown 文件中的相互引用关系，生成基于 D3.js 的力导向依赖关系图，直观展示资源间的关联强度。

- **版本化变更日志**：每次索引更新自动生成 CHANGELOG 片段，记录新增、删除或修改的条目，支持按版本回滚目录状态。

- **RSS 订阅源输出**：为每级分类生成独立 RSS 2.0 订阅源，方便用户通过阅读器跟踪特定领域资源更新。

- **暗色主题与阅读模式**：内置三种配色方案（亮色、暗色、高对比度），并支持“阅读模式”一键隐藏侧栏与导航，聚焦正文内容。

## 应用场景

- **个人技术博客的扩展资源页**：博主可将 Olive Link Atlas 部署为博客的子站点，用于整理和分享写作过程中参考的外部技术文章、官方文档和开源项目地址，避免在单篇博文中堆砌过长链接列表。

- **开源社区的知识库入口**：开源项目维护者可以使用 Olive Link Atlas 构建社区维基的导航页，将贡献者指南、设计文档、会议记录、外部参考实现等资源按模块分类，降低新贡献者的上手门槛。

- **企业内部的团队技术雷达**：技术团队可将系统部署在内网，用于收集和分类团队成员推荐的框架、工具、最佳实践文章，通过标签和依赖图谱发现团队内部的技术共识与知识缺口。

- **技术课程的学习路线索引**：在线教育平台或技术培训讲师可以围绕课程大纲，用 Olive Link Atlas 组织每章节的延伸阅读材料、视频链接和代码示例仓库，形成可复用的课程资源包。

- **个人阅读清单与稍后读管理**：开发者可将日常浏览中遇到的有价值技术内容快速记录为 Markdown 条目，借助标签和检索功能构建私人技术文献库，替代传统书签管理方式。

## 快速开始

以下步骤帮助您在本地环境完成 Olive Link Atlas 的克隆、依赖安装与开发服务器运行。

```bash
# 1. 克隆项目仓库
git clone https://github.com/zerxonhy/olive.git
cd olive

# 2. 安装 Node.js 依赖
npm install

# 3. 启动开发服务器（默认端口 3000）
npm run dev
```

执行上述命令后，在浏览器中访问 <code>http://localhost:3000</code> 即可预览系统首页。系统默认加载 `./content` 目录下的示例索引数据，您可以在此基础上修改或替换为自己的资源条目。

## 安装要求

| 依赖 | 必需 | 说明 |
|------|------|------|
| Node.js 18.x 或更高 | 是 | 运行构建脚本与开发服务器，推荐使用 LTS 版本 |
| npm 9.x 或更高 | 是 | 包管理器，用于安装项目依赖 |
| Git 2.30 或更高 | 是 | 克隆仓库并管理内容版本 |
| 现代浏览器（Chrome/Firefox/Edge 最新两个版本） | 是 | 前端界面运行环境，需支持 ES Module |
| 网络连接 | 是 | 首次启动需下载依赖包；健康检查功能需要访问外链 |
| 磁盘空间 ≥ 200 MB | 否 | 用于存储项目源码、依赖和索引缓存 |
| Python 3.9 或更高 | 否 | 仅当需要使用高级链接分析脚本时需要 |
| Docker 20.10 或更高 | 否 | 仅当需要容器化部署时安装 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 用户指南 | `/docs/user-guide/` | 如何添加新资源条目？如何自定义分类？如何导入/导出索引数据？如何配置 RSS 订阅源？ |
| 开发参考 | `/docs/developer/` | 系统架构是怎样的？如何扩展元数据模板？如何替换前端检索库？API 接口定义在哪里？ |
| 运维手册 | `/docs/operations/` | 如何部署到生产环境？如何配置定时健康检查？如何迁移索引数据到新服务器？如何备份版本化变更日志？ |
| 设计决策 | `/docs/design/` | 为什么选择 FlexSearch 而非 Lunr？目录层级深度为何限制为三级？元数据字段的设计依据是什么？ |

## 资源列表

以下资源为 Olive Link Atlas 当前收录的外部技术笔记与方案文档。所有条目均来自公共仓库，系统仅提供索引与导航功能，不修改或转存原始内容。

### 技术方案与架构笔记

- <code>https://github.com/zerxonhy/olive/blob/main/willowvelvet.md</code>
- <code>https://github.com/zerxonhy/olive/blob/main/amberocean.md</code>
- <code>https://github.com/zerxonhy/olive/blob/main/amberwillow.md</code>

### 设计文档与概念原型

- <code>https://github.com/zerxonhy/olive/blob/main/anchorbloom.md</code>
- <code>https://github.com/zerxonhy/olive/blob/main/anchormaple.md</code>

### 综合参考与扩展阅读

- <code>https://github.com/zerxonhy/olive/blob/main/atlascanvas.md</code>

## 项目结构

```
olive/
├── content/                         # 索引数据源目录
│   ├── categories/                  # 分类定义文件（YAML 格式）
│   │   ├── architecture.yaml        # 架构设计类分类规则
│   │   ├── backend.yaml             # 后端开发类分类规则
│   │   └── frontend.yaml            # 前端开发类分类规则
│   ├── entries/                     # 资源条目目录（每个 Markdown 文件对应一条外链）
│   │   ├── willowvelvet.md          # 索引条目：willowvelvet 技术笔记
│   │   ├── amberocean.md            # 索引条目：amberocean 方案文档
│   │   ├── amberwillow.md           # 索引条目：amberwillow 实践记录
│   │   ├── anchorbloom.md           # 索引条目：anchorbloom 设计稿
│   │   ├── anchormaple.md           # 索引条目：anchormaple 原型说明
│   │   └── atlascanvas.md           # 索引条目：atlascanvas 综合参考
│   └── tags/                        # 标签库（维护全局可用标签列表）
│       ├── architecture.json
│       ├── database.json
│       └── networking.json
├── scripts/                         # 工具脚本
│   ├── health-check.js              # 外链可达性检测脚本
│   ├── generate-sitemap.js          # 生成站点地图
│   └── migrate-index.js             # 索引数据迁移工具
├── src/                             # 前端源码
│   ├── components/                  # Vue 组件（搜索栏、目录树、依赖图谱）
│   ├── layouts/                     # 页面布局模板
│   ├── styles/                      # 主题样式（亮色/暗色/高对比度）
│   └── utils/                       # 检索、解析、渲染工具函数
├── public/                          # 静态资源（图标、字体、默认封面图）
├── docs/                            # 用户文档、开发文档、运维手册
├── config/                          # 系统配置文件
│   ├── site.toml                    # 站点全局配置（标题、描述、导航栏链接）
│   └── health.toml                  # 健康检查超时、重试、通知配置
├── tests/                           # 单元测试与集成测试
├── Dockerfile                       # 容器化部署定义
├── package.json                     # Node.js 项目依赖清单
├── README.md                        # 项目入口文档（本文件）
└── LICENSE                          # MIT 许可证文本
```

## 贡献指南

1. **提交新资源条目**：在 `content/entries/` 目录下新建 Markdown 文件，文件名建议使用英文小写与连字符。文件头部必须包含 YAML 元数据块，至少指定 `title`、`url`、`category` 和 `tags` 字段。提交前请运行 `npm run validate` 校验元数据格式。

2. **完善现有索引信息**：若发现已收录资源链接失效、分类错误或摘要描述不准确，可编辑对应的 Markdown 文件并提交 Pull Request。请在 PR 描述中注明变更理由，并附上本地 `npm run build` 的构建成功截图。

3. **新增分类或标签**：如需扩展一级分类或添加新的全局标签，请在 `content/categories/` 或 `content/tags/` 下新增对应文件，并确保所有受影响的条目均已同步更新分类或标签引用。变更需包含相关条目的批量更新提交。

4. **改进系统功能**：欢迎提交功能增强或缺陷修复的代码变更。请先阅读 `/docs/developer/` 下的架构说明，确保变更符合现有模块划分和编码规范。所有新功能必须附带至少一个单元测试用例。

5. **完善文档**：文档更新同样视为有效贡献。您可以在 `/docs/` 目录下补充使用示例、故障排查步骤或 FAQ 条目。文档变更应保持与技术实现版本一致，避免过时信息。

## 常见问题

**Q：系统能否索引私有仓库中的 Markdown 文件？**  
A：Olive Link Atlas 本身仅读取本地 `content/entries/` 目录下的 Markdown 文件，该目录可存放任意外链 URL，包括私有仓库的原始内容地址。但健康检查功能检测私有链接时需要配置相应的访问凭证（如 GitHub Personal Access Token），您可以在 `config/health.toml` 中设置 `github_token` 字段。若未配置凭证，私有链接将被标记为“无法验证”而非“失效”。

**Q：如何迁移已有的大量书签或浏览器收藏夹数据？**  
A：系统未提供直接的浏览器书签导入工具，但您可以使用 `scripts/import-bookmarks.js` 脚本（需自行编写解析逻辑，参考示例模板）将 Netscape 格式的 HTML 书签导出文件转换为符合系统规范的 Markdown 条目。更推荐的做法是使用社区维护的 bookmark-converter 工具先将书签转为 CSV，再通过脚本生成 Markdown 文件。具体转换模板请参考 `/docs/user-guide/import-export.md`。

**Q：健康检查脚本的运行频率是多少？会对外部站点造成压力吗？**  
A：默认配置下健康检查脚本每日凌晨 3:00 执行一次，且检查间隔设置为 2 秒，对所有外链逐个发送 HEAD 请求。单个站点的请求超时时间为 5 秒，不会连续重试。该频率对绝大多数外部站点的正常访问不构成压力。若您希望降低频率，可在 `config/health.toml` 中调整 `cron_schedule` 字段。

## 许可证

本项目采用 MIT 许可证。您可以在遵守许可证条款的前提下自由使用、修改、分发本系统，包括商业用途。完整的许可证文本请参见项目根目录下的 LICENSE 文件。

> 外链数量: 6 | 生成时间: 2026-07-21 04:27:02
