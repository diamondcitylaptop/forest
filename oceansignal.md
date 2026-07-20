# Olive Index

Olive Index 是一个面向开发者和技术研究人员的轻量级外链资源归集与导航系统。该项目定位于将分散在多个仓库、文档和讨论线程中的高价值技术链接进行结构化整理，并通过静态索引页面的形式提供快速访问。Olive Index 不存储实际内容，仅提供指向原始资源的可靠引用，适用于个人知识库构建、团队技术栈梳理以及开源项目外部依赖的透明化展示。

目标用户包括需要维护大量外部参考链接的文档维护者、希望统一管理项目周边资源的技术负责人，以及需要快速定位特定主题下多个相关站点的研究人员。Olive Index 本身不依赖数据库或后端服务，完全基于 Markdown 和静态文件生成，适合与 GitHub Pages、Vercel 等静态托管平台无缝集成。

## 功能概览

- **结构化链接归集**：支持按技术领域、项目阶段或文档类型对 URL 进行多级分类，每个链接条目可附加简短说明与标签。
- **版本化引用追踪**：通过记录链接的添加时间和校验信息，帮助团队追踪外部资源的变更情况，降低链接失效风险。
- **全静态页面生成**：基于模板引擎将链接数据渲染为纯 HTML 页面，无需运行时解析，保证高可用性和极低访问延迟。
- **Markdown 驱动配置**：所有链接数据以 Markdown 文件形式存储，便于版本控制、审阅和离线编辑，无需学习专有格式。
- **自动生成索引视图**：根据链接的元数据自动生成按字母排序、按日期排序或按标签筛选的多种索引视图，提升浏览效率。
- **外部状态指示器**：集成简单的链接可达性检查机制，在构建阶段标记可能失效的 URL，辅助维护者及时更新。
- **嵌入式引用预览**：支持在链接条目中嵌入关键摘要片段（如仓库描述、文章首段），帮助读者在不跳转的情况下初步了解内容。
- **多仓库联合索引**：能够从多个外部仓库的特定路径下聚合链接文件，实现跨项目的统一资源导航。

## 应用场景

- **开源项目外部依赖公示**：开源项目维护者可以使用 Olive Index 列出项目所引用的全部第三方库、文档站点或参考文章，确保依赖关系的透明性，方便下游用户追溯。
- **技术团队内部知识导航**：技术团队可将团队常用的内部工具地址、云服务控制台、代码仓库镜像和 CI/CD 流水线链接统一收录至 Olive Index，作为新成员入职时的快速参考入口。
- **个人研究专题汇总**：研究人员在调研某个技术领域（如分布式存储、WebAssembly 或图数据库）时，可以使用 Olive Index 整理收藏的论文链接、实验环境地址和社区讨论串，形成结构化的个人知识索引。
- **文档站点的外部参考附录**：技术文档撰写者可以将文档中引用的大量外部链接单独抽离到 Olive Index 中管理，使正文更加精简，同时附录部分保持自动同步更新。

## 快速开始

以下命令演示了从代码仓库克隆 Olive Index 到本地环境、安装基础依赖并启动开发预览服务的完整流程。

```bash
# 克隆仓库
git clone https://github.com/zerxonhy/olive.git olive-index
cd olive-index

# 安装依赖（基于 Node.js 静态生成器）
npm install

# 运行构建与预览服务
npm run build
npm run serve
```

执行上述命令后，Olive Index 会扫描 `./links` 目录下的所有 Markdown 链接定义文件，生成对应的静态页面，并在本地 8080 端口启动预览服务器。用户可通过浏览器访问 `http://localhost:8080` 查看生成的索引首页。

## 安装要求

| 依赖项 | 必需版本 | 说明 |
|--------|----------|------|
| Node.js | >= 18.0.0 | 用于运行构建脚本和本地开发服务器 |
| npm | >= 9.0.0 | 依赖管理和任务执行工具 |
| Git | >= 2.30.0 | 用于克隆仓库和版本控制操作 |
| Python | >= 3.9（可选） | 仅当启用外部链接校验脚本时需要 |
| curl | >= 7.68.0（可选） | 用于构建阶段的外部 URL 可达性测试 |
| Markdown 解析器 | 内置依赖 | 用于解析链接定义文件中的元数据块 |
| 模板引擎 | 内置依赖 | 用于将链接数据渲染为 HTML 页面 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 用户手册 | `/docs/user-guide.md` | 如何使用 Olive Index 管理个人链接集？如何添加、删除或修改条目？ |
| 配置参考 | `/docs/configuration.md` | 索引页面的标题、排序规则、分类标签等配置项如何设置？ |
| 构建与部署 | `/docs/deployment.md` | 如何将 Olive Index 部署到 GitHub Pages、Netlify 或自有服务器？ |
| 扩展开发 | `/docs/development.md` | 如何自定义页面模板、增加新的索引视图或集成外部数据源？ |
| API 约定 | `/docs/api-convention.md` | 链接定义文件的 Markdown 格式规范及元数据字段说明 |
| 故障排查 | `/docs/troubleshooting.md` | 构建失败、链接校验超时或页面渲染异常时如何快速定位问题？ |

## 资源列表

### 核心参考资源（Olive 仓库内部）

<code>https://github.com/zerxonhy/olive/blob/main/oceanpearl.md</code>

<code>https://github.com/zerxonhy/olive/blob/main/oceanzephyr.md</code>

<code>https://github.com/zerxonhy/olive/blob/main/olivemeadow.md</code>

<code>https://github.com/zerxonhy/olive/blob/main/oliveprairie.md</code>

<code>https://github.com/zerxonhy/olive/blob/main/orbitmidnight.md</code>

<code>https://github.com/zerxonhy/olive/blob/main/orbitolive.md</code>

## 项目结构

```
olive-index/
├── .github/                         # GitHub 工作流与 issue 模板
│   └── workflows/
│       └── build.yml                # CI 自动构建与部署配置
├── bin/                             # 可执行脚本
│   ├── generate.js                  # 主生成器入口
│   └── check-links.sh              # 外部链接可达性检查脚本
├── docs/                            # 项目文档
│   ├── user-guide.md               # 用户手册
│   ├── configuration.md            # 配置参数说明
│   └── deployment.md               # 部署指南
├── links/                           # 链接定义文件目录（核心数据）
│   ├── core/                        # 核心基础链接
│   │   ├── infrastructure.md        # 基础设施相关链接
│   │   └── protocols.md             # 协议与标准链接
│   ├── ecosystem/                   # 生态项目链接
│   │   ├── frontend.md              # 前端框架与工具
│   │   └── backend.md               # 后端服务与库
│   └── references/                  # 参考文档与论文
│       ├── papers.md                # 学术论文链接
│       └── blogs.md                 # 技术博客汇总
├── templates/                       # 页面模板（Handlebars）
│   ├── index.hbs                    # 首页模板
│   ├── category.hbs                 # 分类视图模板
│   └── detail.hbs                   # 链接详情页模板
├── public/                          # 静态资源输出目录（构建后）
│   ├── css/
│   │   └── style.css                # 全局样式
│   └── js/
│       └── filter.js                # 前端筛选交互脚本
├── scripts/                         # 辅助工具脚本
│   ├── import-from-json.js          # 从 JSON 导入链接数据
│   └── validate-links.js            # 验证链接格式与元数据完整性
├── test/                            # 单元测试
│   ├── parser.test.js               # 链接解析器测试
│   └── generator.test.js            # 页面生成器测试
├── .eslintrc.json                   # ESLint 代码规范配置
├── .gitignore                       # Git 忽略文件列表
├── package.json                     # npm 项目清单
├── README.md                        # 项目主文档（本文件）
└── LICENSE                          # MIT 许可证文本
```

## 贡献指南

Olive Index 欢迎各类贡献，包括但不限于新增链接条目、改进文档、修复构建错误以及提出功能建议。请遵循以下步骤参与贡献。

1. 从 GitHub 复刻本项目至个人账户，并在本地克隆复刻后的仓库。创建新的功能分支，分支名称应简明描述本次贡献的主题，例如 `feature/add-ai-links` 或 `fix/broken-url-checker`。
2. 在 `links/` 目录下的相应分类文件中添加或修改链接条目，请确保每条链接均包含有效的标题、完整 URL（遵循原始格式）以及至少一个分类标签。新增链接后，本地运行 `npm run test` 确保所有测试用例通过，并执行 `npm run build` 验证构建过程无报错。
3. 提交代码时使用清晰的提交信息，格式建议为 `<类型>: <简短描述>`，例如 `feat: add new links for machine learning` 或 `docs: update deployment guide`。提交前请确保代码已通过 ESLint 检查。
4. 将分支推送至复刻仓库，然后通过 GitHub 界面发起 Pull Request 至本项目的 `main` 分支。请在 PR 描述中详细说明本次更改的内容、动机以及是否有破坏性变更。
5. 项目维护者将审阅 PR，可能提出修改意见。请积极回应反馈并更新代码。合并后，您的贡献将出现在下一轮构建的索引页面中。

## 常见问题

**问：Olive Index 能否自动检测并修复失效的外部链接？**

答：Olive Index 在构建阶段会通过 `check-links.sh` 脚本对配置为需要检查的 URL 发起 HEAD 请求，并生成一份可达性报告。该报告会标记超时或返回 4xx/5xx 状态的链接，但不会自动修改或删除条目。维护者需根据报告手动更新或移除失效链接。若需完全自动化处理，建议结合 GitHub Actions 的定时任务和自动 PR 机制，但默认不启用。

**问：如何将 Olive Index 部署到我的 GitHub Pages 上？**

答：首先在仓库的 `Settings` -> `Pages` 中将构建源设置为 `gh-pages` 分支。然后在本地运行 `npm run build`，将生成的 `public/` 目录内容提交到 `gh-pages` 分支。也可以直接使用项目自带的 GitHub Actions 工作流（`.github/workflows/build.yml`），该工作流会在每次推送到 `main` 分支时自动构建并部署到 `gh-pages` 分支。部署完成后，访问 `https://<用户名>.github.io/olive-index/` 即可看到索引页面。

**问：Olive Index 是否支持多语言界面？**

答：当前版本仅提供中文界面，但项目模板引擎支持国际化扩展。开发人员可以在 `templates/` 目录下创建不同语言版本的模板文件，并通过构建参数指定语言。同时，链接定义文件中的说明字段支持多语言键值对格式，但需要自行扩展解析逻辑。若社区对此有强烈需求，后续版本将考虑内置 i18n 支持。

## 许可证

MIT

> 外链数量: 6 | 生成时间: 2026-07-21 04:26:20
