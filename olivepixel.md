# Olive Index

Olive Index 是一个面向开发者与技术研究人员的轻量级外链资源导航系统，定位于对分散于各处的优质技术文档、项目笔记、手册与参考材料进行结构化汇集与快速检索。该项目并非一个传统的爬虫或搜索引擎，而是一个人工维护、语义清晰、可版本化的资源索引仓库，旨在解决个人或团队在长期开发过程中“记忆链接散落、收藏夹失效、上下文丢失”的典型问题。

Olive Index 的目标用户包括但不限于：需要维护技术选型知识库的架构师、需要跟踪多个上游项目动态的运维工程师、希望系统化整理学习路径的软件工程师，以及需要为团队建立共享参考手册的技术管理者。通过将资源链接与轻量级元信息（如场景、标签、关联项目）以纯文本形式托管于 Git 仓库，Olive Index 在保持极高可移植性的同时，也天然支持代码审查、变更追踪与协作编辑等开源工作流。

## 功能概览

- **按领域分级的资源目录**：提供覆盖云原生、数据库、网络协议、系统设计、编程语言等多个技术领域的分类索引，每个条目均包含原始链接、推荐理由与关联上下文。

- **外链健康状态标记**：支持对收录的每一枚外部链接标注可访问性、更新日期与备选镜像，帮助团队及时识别失效资源。

- **轻量级标签系统**：每条索引记录可附加多个短标签（如 `#kubernetes`、`#observability`、`#rust`），便于通过 grep 或简单脚本进行快速过滤。

- **版本化变更历史**：所有索引增删改操作均通过 Git 提交记录保留完整上下文，支持回滚、比对与责任追溯。

- **与主流编辑器深度集成**：索引文件采用 Markdown 与 YAML 混合格式，可在 VS Code、Neovim 等编辑器中获得语法高亮与大纲视图支持。

- **可扩展的钩子脚本**：项目根目录提供示例脚本，用于在提交前自动检查链接可达性、排序条目一致性以及格式规范。

- **静态站点生成友好**：索引数据结构设计充分考虑与 Hugo、VuePress 等静态站点生成器的对接需求，可一键导出为可浏览的 HTML 文档。

## 应用场景

- **技术选型与方案评审**  
  团队在进行中间件选型或架构方案评审时，可通过 Olive Index 快速查阅预先收集的官方文档、性能测试报告与社区最佳实践，避免重复搜索和遗漏关键信息。

- **新成员入职培训路径**  
  将公司内部常用的技术栈文档、编码规范、部署流程与故障排查手册通过索引串联，新员工可按图索骥系统化学习，显著降低入门门槛。

- **多项目依赖跟踪**  
  当团队同时维护多个微服务或底层库时，可将各项目的外部依赖文档、API 参考与变更日志统一收录，便于在版本升级或安全补丁发布时快速评估影响面。

- **线下演讲与课程资料管理**  
  技术讲师或布道师可将演讲中引用的全部参考文献、示例代码仓库与延伸阅读链接整理为索引快照，在会议或课程结束后公开发布，方便受众回溯。

## 快速开始

以下命令可在任意 Unix/Linux 或 macOS 环境中完成 Olive Index 的克隆、依赖安装与本地运行。

```bash
# 克隆仓库
git clone https://github.com/zerxonhy/olive.git
cd olive

# 安装依赖（仅需 Python 3.9+ 及标准库，若需链接检查请额外安装 requests）
pip install --upgrade pip
pip install requests pyyaml

# 运行本地索引校验与静态预览生成
python scripts/validate_index.py
python scripts/generate_preview.py --output ./preview
```

若为 Windows 环境，建议使用 Git Bash 或 WSL 2 执行上述命令，并确保 Python 已正确加入 PATH。

## 安装要求

| 依赖项 | 必需版本 | 说明 |
|--------|----------|------|
| Python | 3.9 或更高 | 用于运行索引校验、格式转换及链接状态检查脚本 |
| Git | 2.25 或更高 | 用于克隆仓库、提交变更及查看历史记录 |
| requests | 2.25 或更高 | 可选依赖，用于执行外链可达性检查（若跳过检查则可选） |
| pyyaml | 5.4 或更高 | 可选依赖，用于解析 YAML 格式的索引扩展元数据 |
| make | 3.81 或更高 | 可选，用于执行 Makefile 中定义的快捷任务（如 `make check`） |

## 文档导航

| 层面 | 目录 / 文件 | 回答的问题 |
|------|-------------|------------|
| 用户指南 | `docs/user-guide.md` | 如何查询索引、理解字段含义、贡献新链接 |
| 维护手册 | `docs/maintainer-guide.md` | 索引更新流程、冲突解决、标签规范 |
| 设计文档 | `docs/design.md` | 索引数据结构设计原则、扩展性考虑与性能目标 |
| 脚本参考 | `scripts/README.md` | 各 Python 脚本的详细用法、参数与环境变量 |

## 资源列表

### 核心索引文档（本批次收录）

- <code>https://github.com/zerxonhy/olive/blob/main/harborhorizon.md</code>
- <code>https://github.com/zerxonhy/olive/blob/main/horizonlantern.md</code>
- <code>https://github.com/zerxonhy/olive/blob/main/horizonwillow.md</code>
- <code>https://github.com/zerxonhy/olive/blob/main/islandcrystal.md</code>
- <code>https://github.com/zerxonhy/olive/blob/main/islandfield.md</code>
- <code>https://github.com/zerxonhy/olive/blob/main/jadeatlas.md</code>

## 项目结构

```
olive/
├── README.md                       # 项目总体说明与快速入口
├── LICENSE                         # MIT 许可证文本
├── Makefile                        # 常用任务快捷命令（校验、预览、清理）
├── config/
│   └── index_schema.yaml           # 索引条目标准字段定义与校验规则
├── docs/                           # 完整文档体系
│   ├── user-guide.md               # 面向最终用户的查询与使用指南
│   ├── maintainer-guide.md         # 面向维护者的更新流程与规范
│   ├── design.md                   # 设计决策、数据模型与扩展点
│   └── contributing.md             # 贡献者行为准则与提交流程
├── indices/                        # 主索引数据存储目录
│   ├── cloud_native/               # 云原生相关资源索引
│   │   ├── kubernetes.md
│   │   └── service_mesh.md
│   ├── database/                   # 数据库与存储技术索引
│   │   ├── relational.md
│   │   └── nosql.md
│   ├── networking/                 # 网络协议与基础设施索引
│   │   ├── tcp_ip.md
│   │   └── dns_loadbalancing.md
│   ├── languages/                  # 编程语言与运行时索引
│   │   ├── go.md
│   │   ├── rust.md
│   │   └── python.md
│   └── operations/                 # 运维与可观测性索引
│       ├── monitoring.md
│       └── logging_tracing.md
├── scripts/                        # 工具脚本集合
│   ├── validate_index.py           # 索引格式与必填字段校验
│   ├── generate_preview.py         # 从索引生成静态预览页面
│   ├── check_links.py              # 批量检查外链可访问性
│   └── sort_entries.py             # 按标签或标题排序并规范化
├── templates/                      # 静态站点生成模板（可选）
│   ├── base.html
│   └── index_list.html
└── preview/                        # 生成的预览文档输出目录（gitignore）
    └── index.html
```

## 贡献指南

1. **阅读文档与规范**  
   在提交任何变更前，请仔细阅读 `docs/contributing.md` 与 `docs/maintainer-guide.md`，了解标签命名约定、条目标题格式及提交信息规范。

2. **克隆仓库并创建特性分支**  
   使用 `git checkout -b feature/your-feature-name` 创建独立分支，避免直接在主分支上操作。

3. **更新索引并本地校验**  
   在 `indices/` 目录下对应的领域文件中增加或修改条目，然后运行 `python scripts/validate_index.py` 确保格式正确。若新增链接，建议同步运行 `python scripts/check_links.py` 检查可达性。

4. **编写清晰的提交信息**  
   提交信息应包含变更类型（add / update / remove）、受影响条目摘要及理由，例如 `add: 新增 TiDB 性能调优指南至 database/relational.md`。

5. **发起拉取请求**  
   通过 GitHub 发起 Pull Request，并至少邀请一位维护者进行 Review。所有 PR 须通过 CI 校验（格式 + 链接可达性）后方可合并。

## 常见问题

**Q：索引文件是否支持内部网络地址或私有仓库链接？**  
A：支持。Olive Index 仅对链接进行字符串存储与格式校验，不强制要求公共可访问性。但建议在条目的 `note` 字段中注明访问限制，例如“仅限内网”或“需 VPN”。

**Q：如何批量导入我已有的书签库或浏览器收藏夹？**  
A：项目未内置自动转换工具，但 `scripts/` 目录下提供了 `import_bookmarks.py` 示例脚本（需根据实际导出格式调整）。建议将 HTML 书签导出文件转换为 CSV 后，再通过脚本映射到索引字段。

**Q：静态预览生成后，链接跳转仍然是原始 GitHub 路径，是否能改为本地相对路径？**  
A：可以。在 `config/index_schema.yaml` 中设置 `preview.base_url` 为本地服务器地址或相对路径前缀即可。生成脚本会自动根据该配置重写链接。

## 许可证

MIT

> 外链数量: 6 | 生成时间: 2026-07-21 04:26:58
