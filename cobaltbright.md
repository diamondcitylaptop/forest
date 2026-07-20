# Olive Link Atlas

Olive Link Atlas 是一个面向技术研究人员、开源贡献者以及基础设施运维人员的轻量级外链资源汇总与元数据导航系统。该项目不提供具体的代码库或运行时服务，而是以高度结构化的 Markdown 文档体系为核心，对分散在互联网各处的技术文档、配置模板、社区补丁以及镜像站点进行集中索引与分类管理。其目标用户包括需要快速定位特定技术方案原始文档的架构师、维护私有镜像仓库的 DevOps 工程师，以及希望在多个镜像源之间进行一致性校验的开发者。Olive Link Atlas 通过严格的目录分层和标签化命名规则，解决了技术资源链接易失效、查找路径深、上下文缺失这三个核心痛点，将无序的浏览器书签转化为可版本控制、可协作维护的技术资产。

## 功能概览

- **分级索引机制**：依据资源类型、所属技术栈和维护优先级，对每条外链进行三级标签标注，支持多维度的快速过滤。
- **元数据扩展支持**：每条链接记录均可关联版本号、最后验证时间、备选访问方式以及上游变更通知策略。
- **镜像状态标记**：自动或手动标记每个链接所指向的站点是否支持 IPv6、是否采用 HSTS 策略、是否位于特定网络防火墙之后。
- **文档版本锚点提取**：对于指向 Git 托管平台原始文档的链接，自动提取提交哈希或修订日期，帮助用户追踪内容变更。
- **离线归档建议**：根据链接重要性级别，提供离线保存频率建议和 Web 归档（Archive）链接补充模板。
- **批量链接健康检查**：内置基于 curl 和自定义超时参数的链接可达性检测脚本，可生成 CSV 格式的检测报告。
- **外链依赖关系图**：以文本形式记录链接之间的相互引用关系，辅助进行技术方案上下游影响分析。

## 应用场景

1. **企业技术栈基线维护**：技术负责人可将 Olive Link Atlas 作为团队内部的技术文档入口索引，新入职工程师通过该索引可以快速访问到经过筛选的核心设计文档、内部工具链仓库地址以及团队公认的最佳实践指南，显著降低信息寻路成本。

2. **开源软件镜像站选型参考**：运维人员在计划搭建或切换操作系统镜像源、容器镜像加速器时，可以使用本项目中记录的多个镜像站点链接及其历史可用性备注，结合自身网络环境选择最优的镜像服务提供商。

3. **安全补丁跟踪与回滚**：安全响应团队成员可以在项目文档中记录不同组件补丁的原始公告链接和备用下载链接，当主站因流量过大或访问受限时，能够通过索引中的备用链接快速获取补丁包或校验和文件。

4. **学术论文参考文献管理**：研究人员在撰写技术报告或学术论文时，可将引用的外部技术规范、开源项目主页和实验数据集链接统一收录到 Olive Link Atlas 的特定目录下，便于在论文修改过程中统一更新链接状态，避免提交前发现链接失效。

## 快速开始

以下操作指导您将 Olive Link Atlas 项目克隆至本地，安装必要的文档处理工具依赖，并执行基础的链接抽取与验证流程。

```bash
# 步骤 1: 克隆项目仓库
git clone https://github.com/zerxonhy/olive.git
cd olive

# 步骤 2: 安装文档解析与链接验证工具（基于 Python 3.9+）
python -m venv venv
source venv/bin/activate   # Windows 系统请使用 venv\Scripts\activate
pip install -r requirements.txt

# 步骤 3: 执行链接抽取与基础健康检查脚本
python scripts/check_links.py --input docs/ --output reports/link_status.csv --timeout 5
```

## 安装要求

Olive Link Atlas 作为文档型项目，其运行时依赖主要用于本地预览、链接检查和元数据格式校验。请确保您的环境满足以下要求：

| 依赖项 | 必需版本 | 说明 |
|--------|----------|------|
| Python | 3.9 至 3.11 | 用于运行链接检查脚本和元数据解析工具 |
| Git | 2.25 及以上 | 用于克隆仓库和提交文档变更历史追溯 |
| GNU Make | 3.81 及以上 | 用于自动化执行文档格式校验和静态分析任务 |
| Pandoc | 2.10 及以上 | 用于将 Markdown 文档转换为 HTML 或 PDF 格式进行离线审阅 |
| shellcheck | 0.7.0 及以上 | 用于检查项目内辅助 shell 脚本的语法正确性 |
| curl | 7.68 及以上 | 用于执行链接可达性验证，需支持 HTTPS 和重定向跟踪 |

## 文档导航

为帮助不同角色的使用者快速定位所需信息，Olive Link Atlas 将全部文档分为四个核心层面，每个层面面向不同的问题域：

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 资源索引层 | docs/indices/ | 当前存在哪些分类的链接？如何根据技术关键词找到相关文档？ |
| 元数据定义层 | docs/schemas/ | 每条链接记录需要包含哪些字段？版本号、验证时间和标签的格式规范是什么？ |
| 操作指南层 | docs/guides/ | 如何新增一条链接？如何执行全量链接检查？如何生成可视化依赖图？ |
| 运维记录层 | docs/records/ | 历史上哪些链接发生过变更？哪些链接已被标记为废弃或迁移？验证日志存储在哪里？ |

## 资源列表

本项目的核心技术资源分散在以下外链中，它们分别指向不同主题的技术说明文档或配置描述文件。所有链接均按原始格式原样收录，未做任何协议、域名或路径修改。

**文档类资源**

- <code>https://github.com/zerxonhy/olive/blob/main/midnightquartz.md</code>
- <code>https://github.com/zerxonhy/olive/blob/main/midnighttimber.md</code>
- <code>https://github.com/zerxonhy/olive/blob/main/mirrorprairie.md</code>
- <code>https://github.com/zerxonhy/olive/blob/main/mirrorshadow.md</code>
- <code>https://github.com/zerxonhy/olive/blob/main/mirrortimber.md</code>
- <code>https://github.com/zerxonhy/olive/blob/main/nebulaviolet.md</code>

## 项目结构

项目采用分层目录设计，将元数据定义、索引规则、自动化脚本和变更记录进行物理隔离。以下为项目根目录下的完整目录树及其功能说明：

```
olive/
├── docs/                               # 全部 Markdown 文档根目录
│   ├── indices/                        # 链接分类索引文件
│   │   ├── network.md                  # 网络基础设施类链接索引
│   │   ├── storage.md                  # 存储与备份方案链接索引
│   │   └── security.md                 # 安全补丁与审计工具链接索引
│   ├── schemas/                        # 链接元数据 JSON Schema 定义
│   │   ├── link_entry.json             # 单条链接记录的字段规范
│   │   └── manifest.json               # 整体索引清单的结构定义
│   ├── guides/                         # 面向维护者的操作手册
│   │   ├── add_new_link.md             # 新增链接的标准操作流程
│   │   └── health_check.md             # 链接健康检查脚本使用说明
│   └── records/                        # 历史变更与验证日志
│       ├── changelog.md                # 链接增删改的版本化记录
│       └── validation_logs/            # 按月份归档的链接验证结果
├── scripts/                            # 可执行辅助脚本
│   ├── check_links.py                  # 主链接验证脚本，支持并发检测
│   ├── extract_metadata.sh             # 从 Markdown 中提取元数据字段
│   └── generate_report.py              # 根据验证结果生成 HTML 摘要报告
├── tests/                              # 单元测试与集成测试目录
│   ├── test_schemas.py                 # 验证 JSON Schema 合法性
│   └── fixtures/                       # 测试用的固定示例文档
├── requirements.txt                    # Python 依赖列表
├── Makefile                            # 构建与任务自动化入口
└── README.md                           # 项目总体说明文档
```

## 贡献指南

Olive Link Atlas 欢迎社区贡献者提交新的链接索引、元数据修正以及脚本改进。为确保索引质量，请按照以下步骤提交贡献：

1. **创建议题**：在 GitHub 仓库中提交新的 Issue，简要说明您希望新增或修改的链接类别、具体 URL 以及该资源的用途描述，等待维护者确认索引分类。
2. **克隆开发分支**：从主分支切出新的功能分支，分支命名格式为 `feature/link-{category}-{short-description}`，例如 `feature/link-security-audit-tool`。
3. **更新索引文件**：根据确认的分类，在 `docs/indices/` 对应文件中新增链接条目，并按照 `docs/schemas/link_entry.json` 的规范填写所有必需字段，包括 title、url、tags、last_verified 和备注。
4. **执行本地验证**：在项目根目录运行 `make validate` 命令，确保新增或修改的文档通过格式校验和链接可达性初步测试。
5. **提交拉取请求**：推送分支至远程仓库，创建 Pull Request 并关联先前创建的 Issue。PR 描述中需附上本地验证结果的截图或日志摘要，等待至少一名维护者进行代码审查和链接可用性抽查。

## 常见问题

**问：Olive Link Atlas 是否提供自动化的链接失效告警功能？**

当前版本不包含主动推送告警服务，但项目内置的 `check_links.py` 脚本支持以定时任务形式运行，用户可通过 crontab 或 systemd timer 设置每日或每周执行，并将生成的 CSV 报告通过邮件或内部即时通讯工具手动转发给维护团队。未来版本计划集成简单的 Webhook 通知能力。

**问：如何确保资源列表中指向 GitHub 原始文档的链接长期有效？**

项目建议维护者在每次更新索引时，除了记录原始链接外，还需在元数据的 `alternate_urls` 字段中填写至少一个备用访问地址，例如通过 `raw.githubusercontent.com` 或 `git.io` 短链访问同一份文档。此外，`docs/records/changelog.md` 会记录每次链接变更的原因，帮助追溯链接失效后的替代方案。

**问：是否可以导入现有的浏览器书签文件来快速生成索引？**

项目当前未提供直接解析浏览器书签 HTML 或 JSON 导出文件的工具。但贡献者可以参照 `docs/guides/add_new_link.md` 中的批量添加示例，使用脚本将 CSV 格式的书签列表转换为符合 Schema 规范的 Markdown 索引条目。若社区对此功能需求较高，可在 Issue 中提出，我们将在后续迭代中评估增加导入转换器。

## 许可证

MIT

> 外链数量: 6 | 生成时间: 2026-07-21 04:26:20
