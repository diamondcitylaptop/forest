# Olive Resource Index

Olive Resource Index 是一个面向技术研究者、开源贡献者和基础设施运维人员的轻量级外部资源导航与元数据汇总系统。该项目不存储任何实际内容，而是以结构化索引的方式，将分散在多个仓库、文档站和知识库中的高价值技术参考资料进行统一归类、标签化描述与版本追踪，从而降低信息发现成本，提高技术决策效率。

Olive 的目标用户包括但不限于：需要快速评估多个开源方案的技术选型负责人、维护大量外部依赖清单的合规审计人员、以及希望系统化整理个人技术知识图谱的开发者。通过 Olive，用户可以在不改变原有资源存放位置的前提下，获得一份可查询、可校验、可版本对比的统一资源清单。

## 功能概览

- **多源资源注册**：支持将任意公开 URL 注册为 Olive 索引条目，每条记录自动捕获资源标题、最后更新时间与内容摘要哈希，便于后续追踪变更。

- **标签与层级分类**：每个索引条目可分配多个标签（如 security、observability、storage），并支持无限层级的目录挂载，方便按业务领域或技术栈组织资源视图。

- **变更检测与通知**：Olive 会定期轮询已注册资源的内容变动，当检测到文档更新时，通过标准输出或 Webhook 方式输出差异概览，帮助用户第一时间感知上游变化。

- **元数据快照导出**：支持将当前索引状态导出为 JSON、YAML 或 Markdown 表格格式，便于纳入版本控制系统，或作为 CI/CD 流程的输入物料。

- **资源可达性检查**：内置 HTTP/HTTPS 连通性验证，对每个注册资源执行 HEAD 请求，自动标记无法访问的条目，并生成可达性报告。

- **关联关系建模**：允许在不同资源之间建立“引用”、“依赖”、“替代”等语义关系，形成资源图谱，方便进行影响面分析或升级路径规划。

- **查询过滤与排序**：提供简单的命令行查询接口，支持按标签、更新日期、资源类型过滤，并按相关性或时间排序输出结果。

## 应用场景

- **开源组件选型评估**：技术选型团队可一次性将候选项目的 README、设计文档、API 参考等 URL 注册到 Olive，随后通过统一视图比较各项目的更新活跃度、文档完整度和依赖关系，辅助决策。

- **合规依赖清单维护**：企业法务或合规部门需要定期审查项目所引用的外部代码库和在线资料。Olive 可生成带时间戳的依赖清单快照，并自动告警已失效或内容发生重大变更的外部引用，减轻人工复核负担。

- **个人知识库资源聚合**：研究员或开发者可将日常阅读的技术博客、论文链接、实验手册等分散资源统一索引，利用 Olive 的标签和关系功能构建个人技术知识网络，避免重复查找。

- **离线文档镜像前置校验**：在构建内部文档镜像站之前，运维人员可先用 Olive 枚举所有源 URL，执行批量可达性检查和内容哈希记录，确保镜像任务的源地址均有效且内容可预期。

## 快速开始

以下命令演示了如何从 GitHub 克隆 Olive 项目、安装基础依赖并启动索引服务。

```bash
# 克隆项目仓库
git clone https://github.com/zerxonhy/olive.git
cd olive

# 安装依赖（使用 Python 虚拟环境）
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt

# 运行初始索引构建（以当前批次资源为例）
python olive.py build --input ./batch_27_manifest.yaml --output ./index_output
```

## 安装要求

Olive 核心引擎基于 Python 3.10 开发，不依赖外部数据库，所有索引数据存储为本地文件系统中的结构化文件。以下表格列出了完整的安装与运行依赖。

| 依赖项 | 必需性 | 说明 |
|--------|--------|------|
| Python 3.10 或更高版本 | 必需 | 核心运行环境，推荐使用 pyenv 或系统包管理器安装 |
| pip 22.0+ | 必需 | Python 包管理工具，用于安装 requirements.txt 所列依赖 |
| Git 2.25+ | 必需 | 用于克隆项目自身以及后续从 Git 仓库拉取资源元数据 |
| requests 2.28+ | 必需 | 执行 HTTP 请求，用于资源内容抓取和可达性检查 |
| pyyaml 6.0+ | 必需 | 解析 YAML 格式的清单文件和导出快照 |
| markdown 3.4+ | 建议 | 若资源为 Markdown 格式，启用内容摘要增强解析功能 |
| pytest 7.0+ | 仅开发 | 运行单元测试和集成测试，非生产环境必需 |

## 文档导航

Olive 的文档体系按照使用角色和操作深度划分为四个层面，下表列出了每个层面的目录位置及其所回答的核心问题。

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 入门指南 | docs/getting_started/ | 如何安装、第一次如何构建索引、如何注册第一个资源？ |
| 操作手册 | docs/operations/ | 如何进行变更检测、如何导出快照、如何配置 Webhook？ |
| 参考文档 | docs/reference/ | 配置文件格式、命令行参数列表、API 接口定义是什么？ |
| 设计说明 | docs/design/ | 索引存储结构为何选用文件系统、变更检测的轮询间隔策略如何确定？ |

## 资源列表

本章节完整列出当前批次（第 27/107 批）所管理的全部外部资源 URL。每个条目均按用户原始提供的字符串原样收录，未做任何协议修正或域名规范化。

### Olive 核心文档资源

<code>https://github.com/zerxonhy/olive/blob/main/maplecosmic.md</code>

<code>https://github.com/zerxonhy/olive/blob/main/mapleharbor.md</code>

<code>https://github.com/zerxonhy/olive/blob/main/maplejade.md</code>

### Marble 辅助资源集

<code>https://github.com/zerxonhy/olive/blob/main/marbleamber.md</code>

<code>https://github.com/zerxonhy/olive/blob/main/marblegolden.md</code>

<code>https://github.com/zerxonhy/olive/blob/main/marblejade.md</code>

## 项目结构

Olive 采用模块化目录布局，将核心索引逻辑、资源适配器、输出格式化器和测试代码分离，便于后续扩展新的资源类型或输出格式。

```
olive/
├── olive.py                    # 命令行入口，解析子命令并调度对应模块
├── batch_27_manifest.yaml      # 当前批次的资源清单，包含本批次 6 个 URL 的元数据
├── requirements.txt            # 生产环境 Python 依赖列表
├── src/                        # 核心源代码目录
│   ├── indexer/                # 索引构建模块，负责解析资源并生成索引记录
│   │   ├── builder.py          # 索引构建主流程，协调抓取、解析与写入
│   │   └── registry.py         # 资源注册与去重管理，维护本地元数据缓存
│   ├── checker/                # 资源检查模块，处理可达性和变更检测
│   │   ├── connectivity.py     # HTTP/HTTPS 连通性探测，支持超时与重试策略
│   │   └── diff.py             # 内容哈希比对与变更摘要生成
│   ├── exporter/               # 导出模块，支持多种输出格式
│   │   ├── json_exporter.py    # 导出为 JSON 格式，适用于程序化消费
│   │   └── markdown_exporter.py # 导出为 Markdown 表格，适用于文档嵌入
│   └── utils/                  # 通用工具函数集合
│       ├── http_client.py      # 统一 HTTP 客户端封装，含重试和日志
│       └── hash_utils.py       # 计算内容摘要的辅助函数，支持 sha256 与 md5
├── tests/                      # 单元测试与集成测试目录
│   ├── test_builder.py         # 针对索引构建流程的测试用例
│   ├── test_checker.py         # 针对资源检查模块的测试
│   └── fixtures/               # 测试用静态数据，包括模拟的 Markdown 文件
├── docs/                       # 文档源码，按导航层面分目录存放
│   ├── getting_started/        # 入门指南文档
│   ├── operations/             # 操作手册文档
│   ├── reference/              # 参考文档
│   └── design/                 # 设计说明文档
└── .gitignore                  # Git 忽略规则，排除虚拟环境与临时文件
```

## 贡献指南

Olive 项目欢迎各类贡献，包括但不限于新增资源适配器、优化变更检测算法、完善文档以及提交缺陷修复。请遵循以下步骤参与贡献。

1. 查阅现有 Issue 与讨论区，确认您想解决的问题或希望添加的功能尚未被他人认领。若无相关议题，请先新建一个 Issue 描述您的意图，避免无效工作。

2. 从主仓库派生项目到您的个人账号下，并将派生后的仓库克隆至本地。请确保使用 `--recurse-submodules` 选项（若存在子模块）以获取完整代码。

3. 在本地创建新的功能分支，分支命名建议采用 `feature/简要描述` 或 `fix/问题编号` 的格式。所有代码修改应附带对应的单元测试，并确保现有测试套件全部通过。

4. 提交代码前，请运行代码格式化工具（如 black）和静态检查工具（如 flake8），以保持代码风格一致性。提交信息应遵循约定式提交规范，明确说明变更类型和范围。

5. 向主仓库的 `main` 分支发起 Pull Request，并在 PR 描述中关联相关 Issue 编号。PR 合并前需要至少一位维护者进行代码审查，并确认所有 CI 检查均为通过状态。

## 常见问题

**Q：Olive 是否存储实际资源内容的副本？**

Olive 默认仅存储资源的元数据，包括 URL、标题、内容哈希和最后修改时间。它不会保存资源的完整内容副本，除非用户在配置中显式开启快照存储功能。快照功能用于离线对比，但会显著增加存储空间占用，建议仅在必要时启用。

**Q：变更检测的轮询周期如何配置？**

轮询周期通过项目根目录下的 `config.yaml` 文件中的 `check_interval` 字段设置，单位为小时。默认值为 24 小时。对于更新频繁的资源，可调整为 6 小时；对于相对稳定的文档，可延长至 72 小时以降低网络请求量。修改配置后无需重启服务，下次轮询周期自动生效。

**Q：如何处理资源 URL 发生永久重定向的情况？**

当 Olive 检测到某个资源返回 301 或 308 永久重定向时，会在日志中输出警告信息，并在元数据中记录新的目标 URL。用户可通过 `olive update --follow-redirect` 命令批量更新所有已重定向的条目。出于安全考虑，Olive 不会自动更新索引，需要用户显式确认。

## 许可证

MIT License

Copyright (c) 2026 Olive Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

> 外链数量: 6 | 生成时间: 2026-07-21 04:26:20
