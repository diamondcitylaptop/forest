# Olive Resource Navigator

Olive Resource Navigator 是一个面向技术团队与独立开发者的轻量级外链资源归集与导航系统。项目本身不存储任何实际内容，而是以结构化 Markdown 索引的方式，对分散在多个仓库、文档站点、技术博客中的优质外部链接进行统一归类、标注与快速检索。其核心定位是“技术外链的元数据层”，帮助用户从杂乱的书签或零散笔记中脱离，建立可维护、可共享、可版本化的资源地图。

目标用户包括需要维护团队技术文档库的架构师、长期跟踪多个开源项目的开发者、以及希望系统化整理个人学习路径的研究者。Olive Resource Navigator 通过提供固定的目录模板、标签规范与资源状态标记（如有效/失效/更新中），使得上千条外链可以在一个仓库内被清晰管理，并支持通过 CI 流程自动检查链接可用性。

## 功能概览

- **统一资源登记** 提供标准化的 Markdown 条目模板，每条外链记录包含标题、原始 URL、所属领域、添加日期与简短摘要，确保所有资源条目格式一致。

- **多级分类目录** 内置三级分类体系（领域/子领域/主题），支持通过目录树快速定位资源块，同时允许用户自定义扩展分类层级。

- **链接状态检测** 集成外部链接可用性检查脚本，可定期运行并生成失效链接报告，标记于对应条目中，便于及时更新或移除。

- **快速全文检索** 基于 Markdown 文件的原生文本搜索，支持 grep 或 ripgrep 命令行工具，亦可配合静态站点生成器构建可在线检索的 HTML 页面。

- **资源版本快照** 每次提交均可作为资源集合的一个版本快照，支持回退至任意历史状态，适用于团队协作场景下的变更追溯。

- **外部索引同步** 提供导入脚本，可将浏览器书签 HTML 导出文件、CSV 表格或特定格式的 JSON 列表批量转换为 Olive 资源条目，降低初始迁移成本。

- **标签与权重系统** 支持为每条资源打上多个自定义标签，并可设置重要性权重（如核心/参考/延伸），便于后续按优先级筛选或生成专题报告。

## 应用场景

- **团队技术文档库维护** 研发团队可将 Olive Resource Navigator 作为统一入口，汇集所有内部使用的 API 文档、设计规范、部署指南及第三方依赖官网，新成员通过浏览目录即可快速了解技术栈全貌。

- **开源项目学习路径整理** 正在研究某一开源生态（如云原生或前端框架）的开发者，可以将相关官方文档、社区博客、示例项目、性能测试报告等外链按学习阶段归集，形成从入门到进阶的完整路径。

- **技术选型调研支撑** 在进行中间件或数据库选型时，使用 Olive 记录各候选产品的官网、性能对比文章、生产案例、安全公告等链接，横向对比时可直接从目录中调取，避免重复搜索。

- **个人知识库外链管理** 长期积累的技术书签数量庞大且分类混乱，利用 Olive 的分类与标签功能重新整理，并配合链接状态检查清理失效资源，使个人知识库保持高可用性。

- **峰会与会议资料归档** 参加完技术峰会后，可将会议日程、演讲幻灯片链接、相关论文或视频回放地址统一归入 Olive，并按年份/主题建立子目录，形成可长期保存的会议资料库。

## 快速开始

以下命令演示如何获取项目仓库、安装基础依赖并启动本地预览服务。

```bash
# 克隆项目仓库
git clone https://github.com/your-org/olive-resource-navigator.git
cd olive-resource-navigator

# 安装依赖（假设使用 Node.js 生态，如实际项目可替换为对应包管理器）
npm install

# 运行本地开发服务器，预览资源索引页面
npm run dev
```

执行成功后，访问控制台输出的本地地址（通常为 http://localhost:3000）即可查看资源导航首页。

## 安装要求

| 依赖项 | 必需版本 | 说明 |
|--------|----------|------|
| Node.js | 18.x 或 20.x LTS | 运行时环境，用于执行构建脚本与本地服务器 |
| npm | 9.x 或 10.x | 包管理器，用于安装项目依赖 |
| Git | 2.30 及以上 | 版本控制工具，用于克隆仓库与提交变更 |
| ripgrep (rg) | 13.0 及以上 | 可选依赖，用于提供高性能全文搜索能力 |
| Python | 3.9 及以上 | 仅当使用链接状态检测脚本时需要，脚本基于 Python 编写 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 入门指南 | docs/getting-started.md | 如何快速创建第一条资源条目并提交？分类目录如何设计？ |
| 分类规范 | docs/categorization.md | 内置分类体系有哪些层级？如何新增自定义分类？标签命名有什么建议？ |
| 链接检测 | docs/link-checker.md | 如何运行链接可用性检查？失效链接如何处理？检测结果如何解读？ |
| 导入导出 | docs/import-export.md | 支持哪些外部格式导入？如何备份全部资源条目为 CSV 或 JSON？ |

## 资源列表

以下为项目初始收录的外部资源条目，按来源与内容领域划分。所有 URL 均直接引用自上游仓库，未作任何改写。

### 核心索引文件

<code>https://github.com/zerxonhy/olive/blob/main/summitfield.md</code>

<code>https://github.com/zerxonhy/olive/blob/main/timberbright.md</code>

<code>https://github.com/zerxonhy/olive/blob/main/timbercoral.md</code>

<code>https://github.com/zerxonhy/olive/blob/main/timbersaffron.md</code>

### 扩展索引文件

<code>https://github.com/zerxonhy/olive/blob/main/velvetcedar.md</code>

<code>https://github.com/zerxonhy/olive/blob/main/velvetisland.md</code>

## 项目结构

项目采用分层目录结构，将配置、源码、文档与资源索引明确分离。以下为核心目录与文件布局。

```
olive-resource-navigator/
├── config/                         # 项目全局配置文件
│   ├── categories.json             # 内置分类体系定义（领域/子领域层级）
│   └── check-settings.json         # 链接检测超时、重试、排除规则配置
├── src/                            # 核心源码目录
│   ├── cli/                        # 命令行入口脚本（导入、检测、导出）
│   │   ├── import.js               # 外部书签/CSV 导入逻辑
│   │   └── check.js               # 链接可用性检测主程序
│   ├── lib/                        # 公共工具函数库
│   │   ├── markdown-parser.js      # Markdown 条目解析与校验
│   │   └── url-validator.js        # URL 格式标准化与状态检查
│   └── templates/                  # 资源条目 Markdown 模板
│       └── entry-template.md       # 新建条目时使用的标准骨架
├── resources/                      # 实际资源索引文件存放位置
│   ├── core/                       # 核心索引（对应用户提供的 summitfield 等文件）
│   │   ├── summitfield.md
│   │   ├── timberbright.md
│   │   ├── timbercoral.md
│   │   └── timbersaffron.md
│   └── extended/                   # 扩展索引（对应 velvetcedar 等文件）
│       ├── velvetcedar.md
│       └── velvetisland.md
├── docs/                           # 详细文档（入门、分类规范、链接检测、导入导出）
│   ├── getting-started.md
│   ├── categorization.md
│   ├── link-checker.md
│   └── import-export.md
├── scripts/                        # 辅助运维脚本
│   ├── daily-check.sh              # 每日定时执行链接检测的 Shell 脚本
│   └── generate-report.py          # 根据检测结果生成 HTML 报告的 Python 脚本
├── tests/                          # 单元测试与集成测试用例
│   ├── test-parser.js              # Markdown 解析器测试
│   └── test-validator.js           # URL 校验器测试
├── package.json                    # Node.js 项目依赖声明
├── README.md                       # 项目主说明文档（即本文档）
└── LICENSE                         # MIT 许可证文件
```

## 贡献指南

Olive Resource Navigator 欢迎外部贡献者参与改进。无论是添加新的资源条目、完善分类体系，还是优化检测脚本，都请遵循以下流程。

1.  **查阅现有规范**：在提交新条目或修改分类前，请先阅读 `docs/categorization.md` 了解当前分类结构与标签命名约定，确保变更保持一致性。

2.  **创建分支并提交变更**：从主分支创建特性分支（如 `feature/add-resource-xxx`），在该分支上添加或修改 `resources/` 目录下的 Markdown 文件。每次提交请写明清晰的变更说明。

3.  **运行链接检测**：在推送前，请在本地执行链接检测脚本（`npm run check`），确保新增或修改的条目中不包含已失效的外部链接。如检测到失效，请更新条目状态或替换为有效链接。

4.  **发起拉取请求**：将特性分支推送至远程仓库并发起 Pull Request。在 PR 描述中概述变更内容、影响范围以及是否涉及新增分类。等待维护者审阅。

5.  **更新文档**：若变更涉及新增功能或修改使用流程，请同步更新 `docs/` 目录下的对应文档，以保证文档与代码保持一致。

## 常见问题

**Q: 我可以使用其他编程语言运行检测脚本吗？**

A: 当前提供的链接检测脚本基于 Python 实现，但您完全可以替换为自己的检测工具。项目只在 `config/check-settings.json` 中定义检测参数，实际执行命令可在 `scripts/daily-check.sh` 中配置为任意可执行程序。

**Q: 如何处理资源条目中的外部链接失效问题？**

A: 当检测脚本报告某条链接失效后，建议首先访问该链接确认是否临时不可达。若确认永久失效，则可在对应条目中移除该 URL，或将其移入 `resources/archived/` 子目录并添加 `[已失效]` 标记。同时建议查找替代链接并更新条目。

**Q: 是否支持多人同时编辑同一资源文件？**

A: 由于资源文件为普通 Markdown 文本，Git 本身能够合并大部分非冲突修改。若多人同时编辑同一文件的相邻行，Git 会自动合并；若修改同一行内容，则需手动解决冲突。推荐团队采用“按领域分工”策略，避免频繁编辑相同文件。

## 许可证

MIT License

Copyright (c) 2026 Olive Resource Navigator Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

> 外链数量: 6 | 生成时间: 2026-07-21 04:26:20
