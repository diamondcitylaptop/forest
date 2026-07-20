# Olive Link Atlas

Olive Link Atlas 是一个面向技术研究、数据挖掘与数字取证领域的结构化外链资源汇总系统。项目定位为高可靠性技术资源导航工具，主要服务于安全研究员、渗透测试工程师、威胁情报分析师以及开源情报（OSINT）调查人员。Olive Link Atlas 通过人工筛选与社区贡献相结合的方式，持续收录经过验证的网络基础设施线索、技术文献镜像、安全公告存档及数字足迹关联数据，帮助用户在复杂网络环境中快速定位关键信息节点，降低信息检索与交叉验证的时间成本。

与通用型书签管理工具或网络收藏夹不同，Olive Link Atlas 强调资源的可追溯性、分类严谨性与长期可用性验证。每个收录条目均附带上下文标签、镜像状态标记及最后核查时间戳，确保用户在不依赖搜索引擎的情况下仍能获得高质量的技术起点。项目本身不存储任何第三方内容，仅提供指向原始资源的标准化引用路径，符合开源情报收集工作的合规性要求。

## 功能概览

- **结构化资源索引**：按技术领域、数据来源与文件类型对链接进行多维度分类，支持快速筛选与批量导出。

- **镜像状态监控**：对收录的每个外链资源记录可访问状态与响应时间，便于识别失效或迁移的节点。

- **版本化快照引用**：关联 GitHub 仓库中的特定提交记录，确保引用指向固定版本的技术文档或配置文件，避免内容漂移。

- **标签与全文检索**：基于关键词标签体系与资源描述字段实现轻量级检索，支持模糊匹配与正则表达式过滤。

- **社区贡献工作流**：提供标准化的资源提交模板与审核流程，允许外部开发者通过 Pull Request 新增或更新链接条目。

- **离线缓存建议**：针对高频访问的核心资源，生成推荐的本地镜像缓存策略，辅助内网离线环境下的研究场景。

- **外链关系图谱**：自动解析资源之间的相互引用关系，以文本化形式呈现关联路径，辅助溯源分析。

## 应用场景

- **威胁情报关联分析**：安全分析师在调查特定恶意软件家族或高级持续性威胁组织时，可通过 Olive Link Atlas 快速定位相关的技术分析报告、网络基础设施域名及样本哈希值存档页，缩短威胁建模与指标提取时间。

- **数字取证证据链梳理**：取证人员在处理涉及多平台日志与网络流量的案件时，可利用本项目的分类链接体系，系统性地访问各平台官方取证指南、日志格式规范及时间戳转换工具，保障取证流程的标准化。

- **开源情报信息交叉验证**：OSINT 调查员在核实公开来源信息时，借助项目内收录的镜像站点与历史存档链接，对比不同来源同一信息的一致性，识别可能的篡改或虚假信息。

- **安全培训实验环境搭建**：安全课程讲师或实验室管理员可依据本项目汇总的配置手册、漏洞复现环境模板及测试数据集下载链接，快速为学员搭建符合课程要求的实验网络拓扑。

## 快速开始

以下指令适用于 Linux / macOS 及 Windows WSL 环境，用于完成项目仓库克隆、依赖安装与本地预览服务的启动。

```bash
# 步骤 1：克隆仓库
git clone https://github.com/zerxonhy/olive.git
cd olive

# 步骤 2：安装轻量级静态服务器（以 Python 内置模块为例，亦可使用 Node.js serve 等替代）
python3 -m pip install --user markdown
python3 -m pip install --user pyyaml

# 步骤 3：运行本地索引生成脚本并启动预览服务
python3 scripts/build_index.py --input ./links --output ./docs/index.html
python3 -m http.server 8000 --directory ./docs
```

执行完成后，在浏览器中访问 `http://localhost:8000` 即可查看本地编译后的资源汇总页面。如需更新资源列表，请编辑 `links/` 目录下的 YAML 数据文件，随后重新运行构建脚本。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Python | 3.8 及以上 | 运行索引构建脚本与本地服务器的基础解释器 |
| pip | 22.0 及以上 | 管理 Python 依赖包，用于安装 markdown 与 pyyaml |
| Git | 2.25 及以上 | 克隆仓库及后续拉取社区更新内容 |
| 网络连接 | 出站 443/80 可达 | 首次构建时需访问 GitHub 原始内容以校验资源元数据 |
| 磁盘空间 | 建议 200 MB 以上 | 存储仓库副本及本地生成的索引缓存文件 |
| 操作系统 | Linux / macOS / Windows WSL2 | 脚本基于 POSIX 兼容环境开发，Windows 原生命令行未经充分测试 |

## 文档导航

| 层面 | 目录/文档 | 回答的问题 |
|---|---|---|
| 用户手册 | `docs/user-guide.md` | 如何使用分类筛选、检索语法及导出功能；如何理解资源状态标识 |
| 维护者指南 | `docs/maintainer-guide.md` | 资源审核标准、更新周期、镜像有效性检查流程及冲突处理策略 |
| 数据格式规范 | `docs/data-format.md` | YAML 条目字段定义、标签白名单、引用关系语法及示例说明 |
| API 参考 | `docs/api-reference.md` | 构建脚本的命令行参数、环境变量配置及输出目录结构约定 |

## 资源列表

### 核心技术镜像与文档存档

<code>https://github.com/zerxonhy/olive/blob/main/mirrorshadow.md</code>

<code>https://github.com/zerxonhy/olive/blob/main/mirrortimber.md</code>

### 扩展分析与实验性链接

<code>https://github.com/zerxonhy/olive/blob/main/nebulaviolet.md</code>

<code>https://github.com/zerxonhy/olive/blob/main/oceanolive.md</code>

### 补充数据索引与关联条目

<code>https://github.com/zerxonhy/olive/blob/main/oceanpearl.md</code>

<code>https://github.com/zerxonhy/olive/blob/main/oceanzephyr.md</code>

## 项目结构

```
olive/
├── .github/                         # GitHub 社区配置文件目录
│   └── PULL_REQUEST_TEMPLATE.md     # PR 提交模板，引导贡献者填写资源变更信息
├── docs/                            # 编译后的静态文档输出目录
│   ├── index.html                   # 主资源汇总页面，由构建脚本生成
│   └── assets/                      # CSS 与前端辅助样式文件
├── links/                           # 资源数据源目录，所有 YAML 条目存放于此
│   ├── core/                        # 核心稳定资源，经过人工复核
│   │   ├── security.yaml            # 安全工具与漏洞数据库相关链接
│   │   └── osint.yaml               # 开源情报平台与搜索引擎链接
│   ├── community/                   # 社区提交资源，处于审核观察期
│   │   └── pending/                 # 待审核的新提交条目暂存区
│   └── archive/                     # 已失效或迁移资源的归档记录，保留历史引用
├── scripts/                         # 工具脚本目录
│   ├── build_index.py               # 主构建脚本，解析 YAML 并生成 HTML 索引
│   ├── check_health.py              # 外链可用性检查脚本，支持定时任务调用
│   └── utils/                       # 公共函数库，包含 YAML 解析与日志格式化
├── tests/                           # 单元测试与集成测试用例
│   ├── test_parser.py               # 测试 YAML 解析器的容错性与字段完整性
│   └── fixtures/                    # 测试用的固定数据集样本
├── .gitignore                       # Git 忽略规则，排除本地缓存与临时文件
├── LICENSE                          # MIT 许可证全文
└── README.md                        # 项目入口文档，即当前文件
```

## 贡献指南

1. 复刻本仓库至个人账号，在本地新建功能分支，分支命名建议采用 `feat/add-resource-{category}` 或 `fix/update-link-{id}` 格式。

2. 在 `links/community/pending/` 目录下新建 YAML 文件，或直接编辑现有分类文件，按照 `docs/data-format.md` 中定义的字段规范添加或修改资源条目，务必填写 `source_url`、`title`、`tags`、`last_verified` 及 `notes` 字段。

3. 运行本地构建脚本与健康检查脚本，确保新增条目格式正确且目标 URL 可达：`python3 scripts/build_index.py --check`。

4. 提交变更并推送到复刻仓库，随后向本仓库的 `main` 分支发起 Pull Request。PR 描述中需明确说明新增资源的用途、来源以及为何适合收录。

5. 等待维护者审核。审核期间可能会要求补充证据或调整分类。审核通过后，条目将从 `pending` 目录迁移至 `core` 或相应归档目录。

## 常见问题

**问：项目中的外链资源是否会存储第三方内容副本？**

答：不会。Olive Link Atlas 仅保存指向原始资源的 URL 字符串及其元数据描述，不缓存、不代理、不转发任何第三方文件内容。用户访问各链接时直接与原始服务器交互，项目方不承担第三方内容的可用性及合法性责任。

**问：如何报告失效链接或建议替换镜像？**

答：推荐通过 GitHub Issues 提交反馈，选择 `Broken Link` 标签并附上资源名称与当前访问结果。亦可直接按照贡献指南提交 PR，将失效链接的 `status` 字段更新为 `offline`，并在 `notes` 中备注替代地址。

**问：是否可以仅使用本项目提供的脚本离线生成索引而不联网？**

答：可以。构建脚本默认从本地 `links/` 目录读取数据，不强制联网。但健康检查功能与资源元数据中的 `last_verified` 时间戳更新需要网络访问权限。若完全离线，可预先将仓库完整克隆并跳过 `--check` 参数执行构建。

## 许可证

MIT

> 外链数量: 6 | 生成时间: 2026-07-21 04:27:01
