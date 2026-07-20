# Olive 资源索引系统

Olive 是一个面向技术社区的资源外链汇总与导航系统，定位为轻量级、可维护的参考信息库。项目不托管实际内容文件，而是以结构化的 Markdown 索引文件对分散于网络各处的技术文档、教程、工具站点和社区资源进行集中整理与分类标注。目标用户包括技术文档撰写者、开源项目维护人、技术培训讲师以及需要系统化收藏优质外链的研发人员。Olive 通过扁平化的文件命名规范和统一的元数据格式，降低了资源收藏与共享的认知成本，使团队或个人能够在数秒内定位到所需的外部参考资料，同时避免重复收藏和链接失效带来的信息混乱问题。

## 功能概览

- **结构化外链索引**：每个索引文件以纯 Markdown 格式记录单一资源或同类资源组，包含标题、来源网址、内容摘要和标签信息，便于人类阅读和机器解析。

- **分层分类体系**：索引文件通过目录前缀和文件名前缀实现多级分类，例如以 willowsilver、willowvelvet 表示同一主题下的不同子类，以 amber、anchor 等前缀区分不同领域，用户可依据命名约定快速筛选。

- **版本化变更追踪**：依托 Git 进行版本管理，每次新增、修改或删除索引条目均保留提交记录，支持回溯资源状态和审计变更历史。

- **批量导入与校验**：提供辅助脚本（位于 tools/ 目录）用于批量校验外链可达性，并生成状态报告，帮助维护者及时发现失效链接。

- **标签检索与过滤**：索引文件内嵌标签字段（Tags），支持通过 grep 或简单脚本按标签组合进行检索，无需启动数据库或 Web 服务即可在本地完成查询。

- **可扩展模板机制**：提供标准索引模板文件（templates/index_template.md），新增资源时复制模板并填充字段即可，降低新增条目的格式门槛。

- **静态站点生成适配**：索引文件格式兼容主流静态站点生成器（如 Hugo、Jekyll）的内容目录结构，可一键生成导航站点，便于团队内部共享。

## 应用场景

- **技术团队内部知识库外链管理**：研发团队可将日常开发中遇到的优秀博客、API 参考手册、调试工具页面等外链，按照 Olive 的索引规范统一存档，新成员入职时通过克隆仓库即可获得完整的参考资料地图。

- **开源项目 README 资源附录维护**：开源项目维护者可将项目相关的外部依赖文档、社区教程、视频讲解等链接整理为 Olive 索引文件，并在项目 README 中引用，避免主文档过于冗长，同时保持外链的可维护性。

- **技术培训课程资料汇总**：培训讲师可将课程涉及的所有在线实验环境、代码示例仓库、扩展阅读文章等外链按课程章节分类存入 Olive 索引，学员通过单次克隆即可获得全部课程资源索引，无需在授课过程中反复复制网址。

- **个人技术收藏夹的版本化管理**：技术爱好者可使用 Olive 替代浏览器书签，对收藏的技术外链进行带注释的版本管理，即使原链接失效也能通过备注或镜像链接快速恢复访问，同时支持跨设备同步。

## 快速开始

以下操作以 Linux/macOS 环境为例，Windows 用户可使用 Git Bash 或 WSL 执行。

```bash
# 第一步：克隆仓库到本地
git clone https://github.com/yourname/olive.git
cd olive

# 第二步：安装依赖（项目本身无外部依赖，仅需确保 Git 和 Bash 环境）
# 若需要链接可达性校验功能，请安装 curl 或 wget
# Ubuntu/Debian:
# sudo apt install curl
# macOS:
# brew install curl

# 第三步：运行内置校验脚本，检查现有索引文件中的外链状态
bash tools/check_links.sh

# 若校验通过，即可开始新增或编辑索引文件
cp templates/index_template.md willowsilver_new.md
# 编辑 willowsilver_new.md 填入资源信息后，提交至仓库
```

## 安装要求

Olive 项目本身为纯 Markdown 与 Shell 脚本集合，无编译或运行时依赖。如需完整使用所有辅助工具，建议满足以下环境要求。

| 依赖 | 必需 | 说明 |
|------|------|------|
| Git | 是 | 用于克隆仓库、版本管理和提交变更 |
| Bash 4.0+ | 是 | 运行辅助脚本（校验、统计等） |
| curl 或 wget | 否 | 执行外链可达性校验时需要至少一种 HTTP 客户端 |
| GNU grep | 否 | 进行标签检索时推荐使用，支持 Perl 兼容正则 |
| markdownlint-cli | 否 | 可选，用于检查索引文件的 Markdown 格式规范性 |
| ShellCheck | 否 | 可选，用于检查 Shell 脚本的语法正确性 |

## 文档导航

Olive 文档体系分为三个层面：面向初学者的入门指南、面向维护者的操作手册和面向贡献者的规范说明。下表列出核心文档目录及其解决的问题。

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 入门 | docs/quick_start.md | 如何在一分钟内完成仓库克隆和首次浏览；如何理解索引文件的命名和字段含义 |
| 维护 | docs/maintenance.md | 如何新增或更新索引条目；如何运行校验脚本；如何处理失效链接 |
| 规范 | docs/naming_convention.md | 索引文件的前缀命名规则（willow、amber、anchor 等前缀的适用场景）；标签词汇表 |
| 贡献 | CONTRIBUTING.md | 提交变更的流程；Commit Message 格式要求；Pull Request 审核标准 |
| 工具 | tools/README.md | 各类辅助脚本的用法说明，包括校验、统计、格式检查等 |
| 模板 | templates/ | 新增索引文件时应使用的标准模板，包含必填字段和示例 |

## 资源列表

本仓库当前收录以下外部索引条目文件，均存放于 olive 主分支的根目录下。每个条目文件对应一个独立的技术资源主题，内容包含指向原始资源的网址链接和附加说明。以下列表按文件名分组列出。

### 柳系资源（Willow Series）

- <code>https://github.com/zerxonhy/olive/blob/main/willowsilver.md</code>
- <code>https://github.com/zerxonhy/olive/blob/main/willowvelvet.md</code>

### 琥珀系资源（Amber Series）

- <code>https://github.com/zerxonhy/olive/blob/main/amberocean.md</code>
- <code>https://github.com/zerxonhy/olive/blob/main/amberwillow.md</code>

### 锚系资源（Anchor Series）

- <code>https://github.com/zerxonhy/olive/blob/main/anchorbloom.md</code>
- <code>https://github.com/zerxonhy/olive/blob/main/anchormaple.md</code>

## 项目结构

Olive 仓库采用扁平的顶层目录结构，辅以 docs 和 tools 目录存放文档与脚本。所有索引文件（.md）直接置于仓库根目录，便于快速浏览和 grep 检索。目录树中的注释说明了各目录或文件的职责。

```
olive/
├── README.md                     # 项目总览与快速入口（本文件）
├── CONTRIBUTING.md               # 贡献指南，含提交规范和 PR 流程
├── LICENSE                       # MIT 许可证全文
├── willowsilver.md               # 柳银系列索引条目
├── willowvelvet.md               # 柳绒系列索引条目
├── amberocean.md                 # 琥珀海系列索引条目
├── amberwillow.md                # 琥珀柳系列索引条目
├── anchorbloom.md                # 锚花系列索引条目
├── anchormaple.md                # 锚枫系列索引条目
├── docs/                         # 文档目录
│   ├── quick_start.md            # 快速入门指导
│   ├── maintenance.md            # 日常维护操作手册
│   └── naming_convention.md      # 命名与标签规范
├── templates/                    # 模板目录
│   └── index_template.md         # 新建索引条目的标准模板
├── tools/                        # 辅助工具脚本
│   ├── check_links.sh            # 外链可达性批量校验脚本
│   ├── stats.sh                  # 统计索引条目数量与分类分布
│   └── format_check.sh           # Markdown 格式规范性检查
└── .github/                      # GitHub 社区文件
    └── PULL_REQUEST_TEMPLATE.md  # PR 模板，指导贡献者填写变更说明
```

## 贡献指南

Olive 欢迎任何形式的贡献，包括新增索引条目、更新失效链接、改进文档和脚本优化。请遵循以下步骤确保变更顺利合并。

1. **查阅现有规范**：在新增或修改索引文件前，请阅读 `docs/naming_convention.md` 了解前缀命名规则和标签词汇表，确保新增条目与现有分类体系一致。对于新增类型的资源，请先在讨论区提议新增前缀类别。

2. **复制模板并填充**：所有新增索引文件必须基于 `templates/index_template.md` 创建。模板包含标题、来源网址（Source URL）、内容摘要（Abstract）、标签（Tags）和备注（Remarks）五个必填字段。请勿删除或更改字段顺序，保持模板结构完整。

3. **运行校验脚本**：提交前，务必在仓库根目录执行 `bash tools/check_links.sh` 校验所有外链的可达性。若存在失效链接，请先尝试寻找替代链接或更新为有效地址，并在备注中说明变更原因。校验脚本必须全部通过方可提交。

4. **撰写规范的提交信息**：Commit Message 请采用 `<type>(<scope>): <subject>` 格式，其中 type 包括 add（新增）、update（更新）、fix（修复）、remove（删除），scope 为文件名前缀（如 willowsilver、amberocean），subject 使用英文简要描述变更内容。例如：`add(willowsilver): add new reference for Go memory management`。

5. **提交 Pull Request**：通过 GitHub 创建 Pull Request，并按照 `.github/PULL_REQUEST_TEMPLATE.md` 中的要求填写变更摘要、测试结果和关联问题。PR 至少需要一名维护者审核通过后方可合并。

## 常见问题

**问：索引文件中的 Source URL 如果失效了怎么办？**

答：Olive 建议维护者定期（例如每月）运行 `tools/check_links.sh` 脚本检测失效链接。对于已失效的 URL，首先尝试通过 Wayback Machine 或搜索引擎查找原内容的存档副本，并将存档链接更新至 Source URL 字段，同时在 Remarks 中注明原始链接已失效及变更日期。若无法找到任何替代或存档版本，则应在索引文件中将状态标记为已废弃（Deprecated），并保留原始链接作为参考，但不应删除条目本身，以维持历史记录的完整性。

**问：我能否使用自己的分类前缀，而不限于现有的 willowsilver、amberocean 等？**

答：可以。Olive 的命名约定鼓励扩展，但前提是新增前缀必须具有明确的语义区分度，并在 `docs/naming_convention.md` 中登记注册。建议在新增前缀之前，先在 GitHub Issues 中提交提案并简要说明该类别下的资源类型和预期规模，经维护者确认后即可使用。未经登记的前缀可能在后续整理中被调整或合并，造成不一致。

**问：Olive 与浏览器书签或 Pocket 等收藏工具相比有什么优势？**

答：Olive 的核心优势在于版本化、可协作和纯文本可检索。浏览器书签通常无法跨团队共享变更历史，Pocket 等工具则缺乏对外链内容的本地注释和分类说明。Olive 将收藏信息以 Markdown 文件形式存储在 Git 仓库中，所有变更都有迹可循，同时支持通过 grep、awk 等命令行工具进行灵活的离线检索，无需依赖特定厂商的云服务或网络连接。此外，Olive 的索引文件格式适配静态站点生成，可随时发布为内部文档站点。

## 许可证

MIT License

版权所有 (c) 2026 Olive Contributors

特此授予任何人免费获得本软件及相关文档文件（以下简称“软件”）副本的权利，不受限制地处理本软件，包括但不限于使用、复制、修改、合并、发布、分发、再许可和/或销售本软件副本的权利，并允许本软件的使用者在此条件下进行上述操作，但须满足以下条件：

上述版权声明和本许可声明应包含在本软件的所有副本或主要部分中。

本软件按“现状”提供，不提供任何形式的明示或暗示保证，包括但不限于适销性、特定用途适用性和非侵权性的保证。在任何情况下，作者或版权持有人均不对任何索赔、损害或其他责任负责，无论是在合同诉讼、侵权行为或其他方面，由本软件或本软件的使用或其他交易引起、产生或与之相关。

> 外链数量: 6 | 生成时间: 2026-07-21 04:26:59
