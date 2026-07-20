# Olive 技术资源索引与工程规范参考库

Olive 是一个面向基础设施工程师、分布式系统开发者和技术文档撰写者的外链资源汇总与工程规范索引项目。本项目不提供具体的运行时软件或库，而是以精心维护的 Markdown 文档集合形式，沉淀各类系统设计模式、网络协议调优记录、灾难恢复案例以及跨语言服务治理的实战笔记。Olive 的目标用户包括 SRE 团队、技术决策者以及希望深入理解生产环境最佳实践的中高级开发人员。通过本项目，用户可以获得高度结构化的技术决策参考，减少在各类官方文档和社区讨论之间的跳转与信息过滤成本，提升架构评审和故障排查的效率。

## 功能概览

- 多维度技术方案索引：按协议栈、数据平面、控制平面等维度对分散的技术笔记和方案对比文档进行统一编目，每条索引附带原始出处链接与摘要。

- 结构化工程规范参考：收录与 API 设计、错误码治理、日志规范、可观测性指标命名相关的规范草稿和团队共识文档，便于在新项目启动时快速对齐标准。

- 基础设施容灾模式汇总：提供多活架构、主备切换、数据同步冲突处理等场景的典型模型描述，并关联到具体的实现案例和已知缺陷记录。

- 性能调优与内核参数笔记：整理网络拥塞控制、文件系统缓存策略、JVM 或 Erlang VM 调优的实测参数表格，附带变更影响评估清单。

- 跨语言 RPC 交互模式库：涵盖 gRPC、Thrift、自定义 TCP 协议等常见 RPC 框架下的超时控制、重试风暴预防、熔断状态机设计等模式说明。

- 配置管理与密钥轮转策略：汇总环境变量分层、配置中心接入、密钥版本化更新、审计日志留存等方面的操作规范与脚本片段。

- 团队协作与文档工具链：提供关于技术文档写作风格、Markdown 排版规范、变更记录维护、ADR（架构决策记录）模板的使用指引。

## 应用场景

1. 新项目技术选型阶段：架构师可以通过 Olive 中的方案对比文档和外部参考链接，快速评估不同消息队列或数据库代理在类似业务规模下的表现，避免重复进行基础调研。

2. 故障复盘与根因分析：SRE 团队在处理完线上事故后，可参照项目中的灾难恢复模式描述和已知缺陷记录，补充自身的故障库，并对照规范检查是否存在监控盲区或变更流程漏洞。

3. 团队技术培训与新人 onboarding：新入职的开发人员可以通过阅读 Olive 汇总的工程规范和最佳实践笔记，了解团队在分布式事务、幂等性设计、接口版本管理等方面的统一思路，缩短熟悉代码库的时间。

4. 技术文档标准化评审：技术文档撰写者可将 Olive 中的 Markdown 排版规范和 ADR 模板作为基线，对内部 wiki 或 RFC 文档进行格式和内容完整性检查，提升文档的可维护性。

## 快速开始

以下命令演示如何将 Olive 项目克隆至本地，并安装推荐的文档预览与链接检查工具链，最后启动一个本地静态预览服务以便浏览所有索引内容。

```bash
# 克隆项目仓库
git clone https://github.com/zerxonhy/olive.git
cd olive

# 安装文档依赖工具（假设使用 Node.js 生态的 markdownlint-cli 和 link-checker）
npm install -g markdownlint-cli @tools/link-checker

# 运行链接有效性检查（建议在提交前执行）
link-checker ./**/*.md

# 使用任意静态服务器预览文档，例如使用 Python 内置模块
python3 -m http.server 8000 --directory .
```

## 安装要求

| 依赖项 | 必需性 | 说明 |
|--------|--------|------|
| Git 2.30 或更高版本 | 必需 | 用于克隆仓库和管理文档版本，建议开启 GPG 签名验证提交。 |
| Node.js 14.x LTS 或 16.x | 推荐 | 用于运行 markdownlint 和自定义链接检查脚本，非运行时依赖但建议安装以通过 CI 检查。 |
| Python 3.8 或更高版本 | 可选 | 用于快速启动本地 HTTP 预览服务，或运行项目内附带的部分数据转换脚本。 |
| markdownlint-cli 0.31.0+ | 推荐 | 用于检查 Markdown 文档格式一致性，确保标题层级、列表缩进等符合社区规范。 |
| link-checker 工具（任意实现） | 推荐 | 用于定期扫描所有文档中的外部和内部链接有效性，避免链接失效影响阅读体验。 |
| 支持 CommonMark 规范的 Markdown 解析器 | 必需 | 用于正确渲染文档中的表格、代码块和嵌套列表，建议使用 GitHub 风格的 Markdown。 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 基础编目 | /docs/indexing/ | 项目包含了哪些技术领域的外链？如何按网络层、应用层、数据层快速筛选文档？ |
| 规范与模板 | /docs/standards/ | API 设计约束、错误码区间分配、ADR 模板的结构是怎样的？变更记录应包含哪些字段？ |
| 案例与复盘 | /docs/case-studies/ | 过去典型故障的根因、恢复时间线、改进措施分别记录在哪里？如何借鉴到当前系统？ |
| 工具与脚本 | /scripts/ | 项目附带哪些辅助脚本用于检查链接、生成目录树、统计文档字数？它们的使用参数是什么？ |
| 外部资源映射 | /docs/external-mapping/ | 各个外部链接与内部文档之间的映射关系如何维护？当外部文档更新时如何追踪变化？ |
| 贡献者指引 | /CONTRIBUTING.md | 如何提交新的外链索引？如何更新已有的方案对比表格？评审流程和耗时大约是多久？ |

## 资源列表

本节按文档主题类别对项目收录的全部外部资源进行分组罗列。每个资源链接均严格按照原始来源复制，未做任何协议、域名或路径的修改。

基础设施与网络通信层参考

<code>https://github.com/zerxonhy/olive/blob/main/shadowbridge.md</code>

<code>https://github.com/zerxonhy/olive/blob/main/shadowcobalt.md</code>

<code>https://github.com/zerxonhy/olive/blob/main/signalcedar.md</code>

安全通道与信号协议参考

<code>https://github.com/zerxonhy/olive/blob/main/signalquartz.md</code>

<code>https://github.com/zerxonhy/olive/blob/main/silverhorizon.md</code>

<code>https://github.com/zerxonhy/olive/blob/main/silverisland.md</code>

## 项目结构

```text
olive/
├── .github/                     # GitHub 社区健康文件与 PR 模板
│   └── PULL_REQUEST_TEMPLATE.md # 要求提交者填写链接变更类型和验证结果
├── docs/
│   ├── indexing/                # 按技术栈和协议分类的外链索引表
│   │   ├── network-layer.md     # 四层负载均衡、ECMP、BGP 相关参考
│   │   ├── application-layer.md # HTTP/gRPC/WebSocket 网关与重试策略
│   │   └── data-layer.md        # 分布式存储、事务隔离级别、备份策略
│   ├── standards/               # 工程规范与架构决策记录模板
│   │   ├── api-style-guide.md   # URI 命名、HTTP 方法、状态码使用规范
│   │   ├── error-catalog.md     # 全局错误码区间分配表（含预留段）
│   │   └── adr-template.md      # 轻量级架构决策记录编写模板
│   ├── case-studies/            # 典型故障分析与性能调优案例
│   │   ├── cache-stampede.md    # 缓存击穿与 dogpile 预防案例
│   │   ├── connection-pool.md   # 连接池泄漏排查与修复过程
│   │   └── failover-sim.md      # 混沌工程实验记录与恢复时间目标验证
│   ├── external-mapping/        # 外部链接与内部文档的映射关系表
│   │   └── url-inventory.yaml   # YAML 格式存储每个外部文档的摘要和关联标签
│   └── README.md                # 文档区入口，指向各分类索引
├── scripts/                     # 本地开发和检查辅助脚本
│   ├── check-links.sh           # 递归检查所有 .md 文件中的 HTTP/HTTPS 链接
│   ├── generate-tree.sh         # 自动生成项目目录树并插入到 README 中
│   └── lint-staged.js           # 配合 pre-commit 对暂存文档做格式校验
├── .markdownlint.yaml           # markdownlint 规则配置文件
├── .gitignore                   # 忽略本地预览缓存和编辑器临时文件
├── CONTRIBUTING.md              # 贡献者指南，详细说明新增外链的流程
├── LICENSE                      # MIT 许可证全文
└── README.md                    # 项目主文档（即本文档）
```

## 贡献指南

1. 首先阅读项目根目录下的 CONTRIBUTING.md 文件，了解关于外链索引更新、规范文档修订和案例追加的基本流程，并签署贡献者许可协议（CLA）。

2. 创建新的功能分支，分支命名建议采用 `feat/index-update-xxx` 或 `fix/broken-link-xxx` 格式。确保所有新增或修改的 Markdown 文件通过 markdownlint 检查且无语法错误。

3. 若新增外部资源链接，需在 `docs/external-mapping/url-inventory.yaml` 中补充该链接的摘要描述、技术标签以及推荐阅读优先级。若更新已有规范文档，需同步更新文档头部的最后修改日期和版本号。

4. 提交变更前，在项目根目录执行 `./scripts/check-links.sh` 对本次变更涉及的文档以及受影响的索引页进行链接有效性检查，确保没有 404 或被拒绝访问的链接。

5. 发起 Pull Request 至主分支，并在 PR 描述中勾选对应的检查项清单，包括链接有效性、格式规范、映射表完整性等。至少需要一名项目维护者审阅通过后方可合并。

## 常见问题

Q: 项目中的外链文档如果发生内容变更或迁移，Olive 会如何应对？

A: 项目维护者会通过定期的链接检查脚本和自动化的日程任务，扫描所有已收录的外部链接。若发现链接失效或目标内容发生重大变化，维护者将及时在 `url-inventory.yaml` 中标记状态，并尝试寻找替代链接或更新摘要描述。社区贡献者也可以通过提交 Issue 或 Pull Request 来报告链接异常。

Q: 我能否将 Olive 中的规范模板直接复制到公司内部项目中使用？

A: 可以。本项目采用 MIT 许可证，允许自由使用、复制、修改和分发。但请注意，模板中的某些具体数值（如错误码区间、超时阈值）可能源自特定系统的调优经验，直接复制前应根据自身业务规模和基础设施进行调整。

Q: 如何快速定位我感兴趣的技术领域对应的外链？

A: 推荐先查看 `docs/indexing/` 目录下的分类索引文件，例如网络层相关的参考集中在 `network-layer.md`，应用层相关集中在 `application-layer.md`。每个索引文件内部按子主题分组，并提供直达外部资源的链接以及简要的适用场景说明。此外，`url-inventory.yaml` 文件支持按标签过滤，可供高级用户编写自动化查询脚本。

## 许可证

MIT License

Copyright (c) 2026 Olive Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

> 外链数量: 6 | 生成时间: 2026-07-21 04:26:20
