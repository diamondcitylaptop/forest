# Olive 技术资源索引

Olive 是一个面向开发者与运维工程师的技术资源外链汇总与导航系统。本项目不直接托管文档或代码库，而是以结构化目录方式，聚合分散于网络的高质量技术笔记、配置指南与架构分析文档。Olive 的目标用户包括后端开发人员、SRE 工程师、基础设施架构师以及技术决策者。通过集中管理外部技术资源链接，Olive 帮助团队减少信息检索成本，统一知识入口，并在内部建立可审计、可追溯的技术参考资料库。

本项目适用于需要频繁查阅外部技术方案、配置模板或故障排查案例的团队。Olive 本身不存储任何文档内容，仅提供链接索引与分类描述，所有原始内容均指向外部仓库。项目维护者定期检查链接有效性，并更新分类标签。Olive 可作为团队内部知识中台的补充组件，也可独立部署为静态导航页面。

## 功能概览

- **按技术领域分类索引** 每个资源链接按所属技术栈（如容器编排、云原生网络、性能调优）进行一级分类，便于快速定位。

- **文档元数据标注** 对每个外链资源提取文档类型（指南、参考、故障排查、设计决策）、目标读者与预估阅读时长。

- **版本与时效性标记** 标注每个文档所对应的软件版本或发布日期，帮助用户判断内容是否与当前环境兼容。

- **关键词全文检索** 基于标题和描述提供轻量级检索能力，支持多关键词组合查询。

- **外部链接状态监控** 定期发送 HTTP HEAD 请求验证链接可用性，并在管理界面标注异常状态。

- **私有化部署支持** 提供单页 HTML 输出与 Nginx 静态托管配置，适用于内网隔离环境。

- **RESTful API 输出** 以 JSON 格式返回全量资源列表，供内部自动化脚本或监控系统调用。

## 应用场景

1. **新成员入职技术栈速查** 团队新加入的开发者可通过 Olive 快速浏览团队推荐的外部参考文档，覆盖容器网络、存储配置、性能基准等主题，缩短上手周期。

2. **故障排查时的快速参考** 当线上服务出现异常时，运维人员可通过 Olive 定位到之前标记过的外部排查案例或配置参数说明，减少在搜索引擎中反复试错的时间。

3. **架构评审前的背景阅读** 在进行系统架构评审或技术选型之前，团队成员可查阅 Olive 中收录的相关外部设计文档与技术对比分析，作为决策依据的补充材料。

4. **内部知识库的外延补充** 团队内部 Wiki 仅记录定制化方案，而 Olive 作为外延层提供通用技术原理与官方最佳实践，两者相互补充形成完整知识体系。

5. **离线环境下的文档镜像规划** 对于网络受限的生产环境，Olive 的资源列表可导出为下载清单，供批量镜像工具使用，实现外部文档的内部离线归档。

## 快速开始

以下步骤指导用户在本地环境部署 Olive 静态导航站点。本项目采用纯静态 HTML + CSS + JavaScript 构建，无需后端服务或数据库。

```bash
# 步骤 1：克隆项目仓库
git clone https://github.com/zerxonhy/olive.git
cd olive

# 步骤 2：安装依赖（仅用于本地开发构建，生产环境无需依赖）
# 项目使用 Node.js 18+ 与 npm 进行资源索引构建
npm install

# 步骤 3：构建静态站点
# 该命令会扫描 ./resources 目录下的元数据文件，生成 index.html 与 data.json
npm run build

# 步骤 4：启动本地预览服务（默认监听端口 8080）
npm run serve
```

完成上述步骤后，访问 `http://localhost:8080` 即可查看导航首页。如需部署至生产环境，将 `./dist` 目录内容复制到 Web 服务器根目录即可。

## 安装要求

| 依赖项 | 必需版本 | 说明 |
|---|---|---|
| Node.js | 18.x 或更高 | 用于执行构建脚本与本地服务，生产环境无需安装 |
| npm | 9.x 或更高 | 依赖管理工具，随 Node.js 一同安装 |
| Git | 2.25 或更高 | 用于克隆仓库及版本管理 |
| 现代 Web 浏览器 | Chrome 90+ / Firefox 88+ / Edge 90+ | 用于浏览导航页面，支持 ES6 与 CSS Grid |
| Web 服务器（生产） | Nginx 1.18+ / Apache 2.4+ | 生产环境推荐，仅需静态文件托管能力，无需额外模块 |
| 网络连通性 | 出站 HTTPS 可达 | 用于链接状态监控功能，若为内网离线环境可禁用该功能 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 用户指南 | `/docs/user-guide.md` | 如何使用 Olive 查找资源、如何提交新链接建议、如何反馈链接失效 |
| 维护者手册 | `/docs/maintainer-guide.md` | 如何更新资源分类、如何检查链接有效性、如何构建新版本静态站点 |
| 架构设计 | `/docs/architecture.md` | Olive 的项目结构设计、构建流程、数据流与扩展性说明 |
| API 参考 | `/docs/api-reference.md` | 如何通过 HTTP API 获取 JSON 格式的资源列表，以及 API 参数说明 |
| 部署指南 | `/docs/deployment.md` | 如何在生产环境部署 Olive，包括 Nginx 配置示例与 HTTPS 设置建议 |
| 贡献规范 | `/docs/contributing.md` | 外部贡献者如何提交 Pull Request、代码风格要求与 Commit Message 格式 |

## 资源列表

### 容器与编排

<code>https://github.com/zerxonhy/olive/blob/main/cedarwillow.md</code>

<code>https://github.com/zerxonhy/olive/blob/main/cloudbright.md</code>

### 网络与存储

<code>https://github.com/zerxonhy/olive/blob/main/coralmaple.md</code>

<code>https://github.com/zerxonhy/olive/blob/main/coralsaffron.md</code>

### 性能与可观测性

<code>https://github.com/zerxonhy/olive/blob/main/cosmicamber.md</code>

<code>https://github.com/zerxonhy/olive/blob/main/cosmicbright.md</code>

## 项目结构

```
olive/
├── .github/                         # GitHub 社区模板与自动化工作流
│   └── workflows/
│       └── link-checker.yml         # 每周定时执行外链可用性检查
├── assets/                          # 静态资源文件
│   ├── css/
│   │   └── main.css                 # 全局样式表（响应式设计）
│   ├── js/
│   │   ├── app.js                   # 前端渲染逻辑与检索功能
│   │   └── api-client.js            # 封装 fetch 调用，获取资源数据
│   └── icons/                       # 分类图标（SVG 格式）
├── config/                          # 项目配置文件目录
│   ├── categories.json              # 资源分类定义（名称、颜色、排序权重）
│   └── build-settings.json          # 构建工具参数（输出路径、压缩选项）
├── docs/                            # 项目文档（用户指南、维护手册等）
│   ├── user-guide.md
│   ├── maintainer-guide.md
│   ├── architecture.md
│   ├── api-reference.md
│   ├── deployment.md
│   └── contributing.md
├── scripts/                         # 构建与维护脚本
│   ├── build.js                     # 核心构建脚本，生成 index.html 与 data.json
│   ├── validate-links.js            # 外链有效性校验工具（使用 headless 请求）
│   └── generate-sitemap.js          # 生成站点地图，用于 SEO 或内部导航
├── resources/                       # 资源元数据存放目录（每个外链对应一个 .json 文件）
│   ├── cedarwillow.json
│   ├── cloudbright.json
│   ├── coralmaple.json
│   ├── coralsaffron.json
│   ├── cosmicamber.json
│   └── cosmicbright.json
├── templates/                       # HTML 模板文件（EJS 语法）
│   ├── index.ejs                    # 首页模板，包含分类网格与检索框
│   └── detail.ejs                   # 资源详情页模板（展示完整元数据）
├── tests/                           # 单元测试与集成测试
│   ├── unit/
│   │   └── metadata-parser.test.js  # 测试元数据解析函数
│   └── integration/
│       └── build-output.test.js     # 测试构建输出是否符合预期结构
├── .gitignore
├── LICENSE                          # MIT 许可证文件
├── package.json                     # npm 项目声明文件
├── package-lock.json                # 依赖锁定文件
└── README.md                        # 项目说明文件（即本文档）
```

## 贡献指南

1. **提交资源建议** 若您希望向 Olive 添加新的外链资源，请在本仓库的 Issue 中提交链接地址、建议分类以及简要说明（50-200 字）。项目维护者将评估链接内容的质量与相关性后决定是否收录。

2. **更新元数据文件** 如果您发现某个已有资源的分类、描述或标签不准确，可 fork 本仓库并修改 `./resources/` 下对应的 JSON 文件，然后提交 Pull Request。请确保修改后的 JSON 格式合法且保留原有字段结构。

3. **报告失效链接** 当您发现某个外链无法访问时，请在 Issue 中标记 `[broken-link]` 并附上链接地址。维护者将验证后更新状态或移除该资源。若您有可替代的新链接，也欢迎一并提供。

4. **完善项目文档** 若您发现文档中存在错别字、表述不清或遗漏的章节，可提交 Pull Request 修改 `./docs/` 下的 Markdown 文件。文档修改应保持技术化、正式的语言风格，不使用 emoji 与口语化表达。

5. **改进构建脚本** 如果您熟悉 Node.js 开发，欢迎优化 `./scripts/build.js` 的性能、增加新的构建功能或修复已知缺陷。提交前请运行 `npm test` 确保现有测试用例全部通过。

## 常见问题

**问：Olive 是否提供在线演示站点？**  
答：本项目当前不提供公共演示站点，因为 Olive 的设计目标是为团队内部提供私有化导航服务。您可按照快速开始章节的步骤在本地构建并预览效果。若您需要查看站点功能演示，建议使用 `npm run serve` 启动本地服务后通过浏览器访问。未来版本可能会提供 Docker 镜像以简化部署流程。

**问：如何确保收录的外链内容不会丢失或变更？**  
答：Olive 作为外链索引项目，不存储原始文档内容，因此无法保证第三方链接永久有效。项目维护者通过 GitHub Actions 定时执行链接可用性检查（每周一次），并在检测到 HTTP 4xx/5xx 状态码时在管理界面标记为「异常」。同时，每个资源条目都包含 `last_verified` 字段记录最后检查时间，建议用户结合互联网存档服务（如 Wayback Machine）作为备查手段。

**问：我可以将 Olive 用于商业项目吗？**  
答：可以。Olive 采用 MIT 许可证，允许商业使用、修改、分发和私有化部署。您无需向本项目支付任何费用或公开您的修改源码。但请注意，Olive 本身仅为链接索引工具，不构成对第三方文档版权的授权，请用户遵守原始文档的许可证要求。

## 许可证

MIT

> 外链数量: 6 | 生成时间: 2026-07-21 04:26:20
