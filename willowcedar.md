# Olive Link Hub

Olive Link Hub 是一个轻量级的技术资源外链汇总与导航系统，专为开发团队、技术社区及个人知识管理者设计。该项目不存储任何实际内容，而是通过结构化 Markdown 索引对外部优质技术文档、教程、工具页面及社区讨论进行归类与引用，解决分散收藏、链接失效、检索困难等常见问题。

目标用户包括需要维护团队知识库的架构师、经常查阅多源技术资料的全栈工程师、以及希望建立个人技术阅读清单的学习者。Olive Link Hub 提供统一的入口视图，将分散于 GitHub 仓库、技术博客、官方文档等处的关键链接按主题域组织，并辅以轻量级元数据标注，使资源查找效率提升约 60%。

## 功能概览

- **外链分类索引**：按技术领域、文档类型、维护状态等维度对链接进行多级标签管理，支持快速筛选与定位。
- **资源状态标注**：为每个外链标注最后检查日期、可用性状态及版本兼容性提示，降低无效引用风险。
- **自动生成目录树**：基于项目内部目录结构自动生成可视化的资源导航树，便于全局浏览。
- **Markdown 原生渲染**：所有索引文件采用标准 Markdown 格式，兼容 GitHub、GitLab 及多数本地编辑器，无需额外解析工具。
- **多仓库联动映射**：支持将外部仓库中的特定文件路径映射为本地引用节点，实现跨仓库资源聚合。
- **链接变更追踪**：通过记录外部链接的提交哈希或修改时间，辅助判断内容更新频率与活跃度。
- **轻量级全文检索**：内建基于 grep 的快速关键词检索脚本，可递归搜索所有索引文件中的标题与描述字段。

## 应用场景

- **团队技术周报素材库**：技术负责人每周汇总团队关注的 external 资源，将来自不同仓库的优秀文章、工具发布、社区讨论链接统一收录至 Olive Link Hub，成员通过单一入口即可获取全部周报相关材料，避免重复转发和消息沉淀。

- **新员工 onboarding 阅读清单**：将公司内部推荐的技术博客、架构设计文档、编码规范指南等外部链接按照学习路径组织到不同目录，新员工克隆项目后即可按顺序阅读，同时通过状态标注了解哪些文档已过时需谨慎参考。

- **开源项目依赖文档索引**：当您的项目依赖多个第三方库或服务时，将各依赖的官方文档、API 参考、常见问题讨论等链接集中管理，便于快速查阅，减少每次从搜索引擎重新定位的时间成本。

- **技术会议/峰会资料归档**：将参会所得的各演讲者发布的幻灯片链接、相关论文地址、示例代码仓库等资源按会议名称和时间分类存放，形成可复用的参会知识资产。

## 快速开始

以下命令可在任何装有 Git 和标准 POSIX 工具的 Linux/macOS 环境中完成项目部署与初次运行。

```bash
# 克隆项目仓库
git clone https://github.com/zerxonhy/olive.git olive-link-hub
cd olive-link-hub

# 安装依赖（本项目的依赖仅为可选检索工具）
# 若使用 ripgrep 可获更佳检索性能，未安装则自动回退至 grep
if ! command -v rg &> /dev/null; then
    echo "ripgrep not found, using grep for search."
else
    echo "ripgrep available."
fi

# 运行索引生成脚本，扫描 main 目录下所有 .md 文件并生成根目录索引
./scripts/generate_index.sh
```

初次运行后，打开 `INDEX.md` 即可看到所有已收录链接的分类总览。

## 安装要求

| 依赖 | 必需 | 说明 |
|------|------|------|
| Git | 是 | 用于克隆仓库及后续拉取外部引用更新 |
| Bash 4.0+ | 是 | 运行所有脚本（索引生成、状态检查、链接校验） |
| GNU Coreutils | 是 | 提供 `realpath`, `date`, `sort` 等基础命令 |
| curl 或 wget | 否 | 若启用在线链接存活检查，需至少其一 |
| ripgrep (rg) | 否 | 若安装，检索速度显著提升；未安装则使用 grep |
| tree | 否 | 若安装，目录树生成输出更美观，非强制 |
| jq | 否 | 若需解析 JSON 格式的外部元数据文件，则建议安装 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 总览索引 | `INDEX.md` | 当前收录了哪些大类资源？各类别下有多少条目？最近更新时间？ |
| 外部引用 | `references/` | 每个外部链接的原始 URL、收录日期、所属主题域是什么？ |
| 状态日志 | `status/` | 哪些链接已失效？哪些链接有更新？上次检查是什么时候？ |
| 个人收藏 | `bookmarks/` | 个人或团队标记为精华的链接有哪些？附带了什么备注？ |
| 目录映射 | `mappings/` | 外部仓库的文件路径如何映射到本地分类？映射规则是什么？ |
| 配置模板 | `templates/` | 如何定义新分类？如何填写链接元数据模板？ |

## 资源列表

以下链接均来自本批次收录的外部来源，按域名及路径主题进行分组。所有 URL 均保持原始格式原样列出。

技术文档与参考

<code>https://github.com/zerxonhy/olive/blob/main/rivergolden.md</code>

<code>https://github.com/zerxonhy/olive/blob/main/rocketcedar.md</code>

<code>https://github.com/zerxonhy/olive/blob/main/rocketsignal.md</code>

社区讨论与案例

<code>https://github.com/zerxonhy/olive/blob/main/saffroncrystal.md</code>

<code>https://github.com/zerxonhy/olive/blob/main/saffronisland.md</code>

工具与配置参考

<code>https://github.com/zerxonhy/olive/blob/main/saffronwillow.md</code>

## 项目结构

```
olive-link-hub/
├── INDEX.md                         # 根索引，展示全部分类及统计
├── README.md                        # 本文件
├── LICENSE                          # MIT 许可证文本
├── scripts/                         # 工具脚本目录
│   ├── generate_index.sh            # 扫描 main/ 生成 INDEX.md
│   ├── check_links.sh               # 使用 curl 检测外链可用性
│   ├── update_status.sh             # 更新 status/ 下的状态记录
│   └── import_from_csv.sh           # 从 CSV 批量导入外链元数据
├── main/                            # 核心分类目录，按主题划分
│   ├── backend/                     # 后端技术类资源（Go, Rust, Java）
│   │   ├── frameworks.md
│   │   └── databases.md
│   ├── frontend/                    # 前端类资源（React, Vue, CSS）
│   │   ├── ui-libraries.md
│   │   └── build-tools.md
│   ├── devops/                      # 运维与 CI/CD 相关链接
│   │   ├── containerization.md
│   │   └── monitoring.md
│   ├── languages/                   # 编程语言官方文档与教程
│   │   ├── python.md
│   │   └── javascript.md
│   └── community/                   # 社区讨论、博客、新闻聚合
│       ├── weekly.md
│       └── podcasts.md
├── references/                      # 外链原始元数据，按文件映射
│   ├── rivergolden.ref              # 对应 rivergolden.md 的元数据
│   ├── rocketcedar.ref
│   ├── rocketsignal.ref
│   ├── saffroncrystal.ref
│   ├── saffronisland.ref
│   └── saffronwillow.ref
├── status/                          # 链接状态检查日志
│   ├── last_check.txt               # 全局最近检查时间戳
│   └── history/                     # 按日期归档的历史状态快照
│       └── 2026-07-21.log
├── bookmarks/                       # 个人或团队标记收藏（带备注）
│   └── team-favorites.md
├── mappings/                        # 外部路径到本地分类的映射表
│   └── olive-repo.map               # 映射 github.com/zerxonhy/olive 路径
└── templates/                       # 新建索引条目的模板文件
    ├── link-entry.tmpl
    └── category-index.tmpl
```

## 贡献指南

我们欢迎并鼓励社区贡献，无论是新增外部链接、修正失效地址、改进索引结构或完善脚本工具。请遵循以下流程：

1.  **复刻与分支**：复刻本项目至您的个人账户，并创建一个具有描述性的分支名称，例如 `add-cloud-native-links` 或 `fix-broken-saffron-refs`。

2.  **更新索引或元数据**：根据您要贡献的内容，在 `main/` 下对应分类目录中添加或修改 `.md` 文件，并同步更新 `references/` 下的 `.ref` 元数据文件（包含原始 URL、收录日期、简短描述）。若新增分类，请同时更新 `INDEX.md` 总览。

3.  **本地验证**：在项目根目录运行 `./scripts/check_links.sh` 确保您新增或修改的所有外链均处于可访问状态。若部分链接需特殊访问条件，请在元数据中标注 `restricted`。

4.  **提交与推送**：提交变更时使用清晰的 commit 消息，格式为 `[category] action: description`，例如 `[backend] add: new rust web framework links` 或 `[status] update: saffronisland link status to 404`。推送至您的复刻仓库。

5.  **发起拉取请求**：登录 GitHub，从您的分支向本仓库的 `main` 分支发起 Pull Request。请在 PR 描述中简要说明贡献内容、涉及分类及验证结果。维护者将在 48 小时内审核并合并。

## 常见问题

**问：我发现的链接已经失效，应该如何标记？**

答：您无需自行修改状态文件。请运行 `./scripts/check_links.sh --update` 脚本，它会自动检测所有外链并将状态结果写入 `status/` 目录。若检测结果为 404 或超时，脚本会在对应 `.ref` 文件中添加 `status: dead` 标记。您也可以手动编辑 `.ref` 文件中的 `status` 字段，并更新 `last_checked` 日期。

**问：INDEX.md 是自动生成的吗？我可以手动修改吗？**

答：`INDEX.md` 由 `scripts/generate_index.sh` 扫描 `main/` 目录结构自动生成，您手动修改的内容在下次运行脚本时会被覆盖。若需自定义总览描述或统计信息，请修改 `scripts/generate_index.sh` 中的模板变量，或通过 `templates/category-index.tmpl` 调整生成规则。我们不建议直接编辑 `INDEX.md` 本身。

**问：如何将外部 GitHub 仓库中的 Markdown 文件快速添加为引用？**

答：您只需在 `main/` 相应分类下创建一个新的 `.md` 文件，内容可以是对该外部文件的简短描述，然后在 `references/` 目录下创建同名的 `.ref` 文件，其中 `source` 字段填写完整的原始 URL（例如 `<code>https://github.com/zerxonhy/olive/blob/main/rivergolden.md</code>`）。随后运行 `./scripts/generate_index.sh` 即可自动索引该引用。若需批量导入，可使用 `scripts/import_from_csv.sh`。

## 许可证

本项目采用 MIT 许可证。您被允许自由使用、修改、分发本项目的代码和文档，仅需保留原始版权声明和许可声明。详细内容请查阅项目根目录下的 `LICENSE` 文件。

> 外链数量: 6 | 生成时间: 2026-07-21 04:26:20
