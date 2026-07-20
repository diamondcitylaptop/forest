# Olive Link Atlas

Olive Link Atlas 是一个面向开发者、技术研究人员与信息架构师的外部资源导航与元数据聚合工具。该项目不直接托管内容，而是通过结构化方式组织、标注和校验分散在多个数据源中的技术文档、配置示例与参考资料，帮助团队或个人在复杂信息环境中快速定位有效资源。Olive Link Atlas 适用于需要频繁引用外部链接的文档工程、技术写作、知识库维护以及依赖链追踪等场景，其核心价值在于将无结构的 URL 集合转化为可检索、可版本化、可审计的链接资产清单。

## 功能概览

- **链接元数据提取**：自动从目标 URL 指向的 Markdown 或纯文本文件中抽取标题、一级标题结构、代码块语言标签以及最后修改时间推测。
- **多源合并与去重**：支持将多个来源的链接列表按规范化的 URL 格式进行合并，识别重复条目并保留优先级最高的元数据版本。
- **状态健康检查**：对收录的每个外部链接执行可配置的 HTTP HEAD/GET 请求，检测返回状态码、重定向链及响应时间，标记失效或高风险链接。
- **标签与分类引擎**：基于 URL 路径关键词、文件名后缀和内容特征自动生成分类标签（如“文档”、“配置”、“示例”、“协议”），并允许用户自定义标签覆盖。
- **版本差异对比**：当上游资源更新时，通过内容哈希比对识别变更，生成变更摘要报告，便于审查依赖内容的稳定性。
- **输出格式适配**：支持将结构化链接数据导出为 Markdown 表格、JSON 清单、HTML 目录页或 CSV 报告，满足不同文档工具链的集成需求。

## 应用场景

- **技术文档站点的外链管理**：当技术文档中包含大量参考链接时，使用 Olive Link Atlas 可以自动校验链接可用性，并在每次构建时生成链接状态仪表板，避免文档中出现死链。
- **开源项目依赖资源追踪**：对于依赖多个外部配置仓库或数据文件的工程，可利用本工具定期抓取链接元数据，对比文件哈希值，及时发现上游非兼容变更。
- **知识库迁移前的链接审计**：在企业知识库从旧 Wiki 迁移至新平台前，通过 Olive Link Atlas 批量导出所有外链及其上下文信息，辅助确定保留、更新或删除策略。
- **法规合规性链接归档**：需要定期记录引用外部政策、标准或法律文件的链接状态时，本工具可提供带时间戳的快照报告，满足合规审计的证据留存要求。

## 快速开始

以下步骤适用于 Linux/macOS 环境，Windows 用户建议使用 WSL2 或 Git Bash。

```bash
# 1. 克隆项目仓库
git clone https://github.com/zerxonhy/olive.git
cd olive

# 2. 安装 Python 依赖（建议使用虚拟环境）
python3 -m venv venv
source venv/bin/activate
pip install --upgrade pip
pip install -r requirements.txt

# 3. 准备链接清单文件（默认读取 assets/links.txt）
# 将需要管理的 URL 逐行写入该文件，每行一条

# 4. 运行核心扫描任务
python main.py --input assets/links.txt --output reports/ --check-status

# 5. 查看生成的报告
cat reports/link_status.md
```

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Python | 3.9 及以上 | 核心运行环境，低于此版本将导致类型注解解析异常 |
| pip | 21.0 及以上 | 依赖安装工具，旧版本可能无法解析 pyproject.toml |
| requests | 2.28.0 | 用于 HTTP 健康检查及内容获取，支持超时与重试配置 |
| beautifulsoup4 | 4.11.0 | 可选依赖，用于解析 HTML 类型的链接目标以提取文本摘要 |
| git | 2.25.0 | 仅当需要从私有仓库克隆子模块或更新子项目时作为外部工具依赖 |
| 网络访问 | 出站 80/443 | 运行健康检查时需要目标服务器可连通，代理需单独配置环境变量 |
| 磁盘空间 | 至少 50MB | 用于存储日志、缓存元数据及生成的报告文件，大项目建议 200MB+ |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 用户手册 | docs/user_guide.md | 如何配置输入源、调整检查频率、自定义标签规则及导出报告格式 |
| 配置参考 | docs/config_schema.yaml | 所有可用的配置项及其默认值、类型约束和环境变量覆盖方式 |
| 架构设计 | docs/architecture.md | 模块划分、数据流方向、扩展点设计以及缓存策略的详细说明 |
| 故障排查 | docs/troubleshooting.md | 常见网络错误、SSL 证书问题、内存占用过高及日志定位方法 |

## 资源列表

本批次收录的外部资源均来自 Olive 项目主仓库下的文档分支，涵盖不同主题的技术备忘与配置片段。

核心参考文档

- <code>https://github.com/zerxonhy/olive/blob/main/riverdelta.md</code>
- <code>https://github.com/zerxonhy/olive/blob/main/rivergolden.md</code>
- <code>https://github.com/zerxonhy/olive/blob/main/rocketcedar.md</code>
- <code>https://github.com/zerxonhy/olive/blob/main/rocketsignal.md</code>
- <code>https://github.com/zerxonhy/olive/blob/main/saffroncrystal.md</code>
- <code>https://github.com/zerxonhy/olive/blob/main/saffronisland.md</code>

## 项目结构

```
olive/
├── main.py                         # 入口程序，解析命令行参数并调度核心流程
├── config.yaml                     # 主配置文件，包含超时、重试、标签规则等
├── requirements.txt                # 生产环境依赖清单
├── pyproject.toml                  # 项目元数据与构建配置（PEP 621）
├── assets/                         # 静态资源目录
│   ├── links.txt                   # 默认输入文件，每行一个 URL
│   └── user_tags.yaml              # 用户自定义标签映射表
├── src/                            # 源代码根目录
│   ├── core/                       # 核心模块
│   │   ├── fetcher.py              # 负责 HTTP 请求与内容获取，含重试与超时逻辑
│   │   ├── parser.py               # 从 HTML/Markdown 提取标题、代码块及元数据
│   │   ├── checker.py              # 执行状态码检测、重定向跟踪与响应时间统计
│   │   └── hasher.py               # 计算内容哈希，用于版本差异判断
│   ├── storage/                    # 存储与缓存层
│   │   ├── cache.py                # 基于磁盘的键值缓存，减少重复网络请求
│   │   └── report_builder.py       # 将结构化数据组装为不同格式的报告对象
│   ├── exporters/                  # 输出适配器
│   │   ├── markdown_exporter.py    # 生成 Markdown 表格与状态徽章
│   │   ├── json_exporter.py        # 输出 JSON 清单，兼容前端工具链
│   │   └── html_exporter.py        # 生成带样式的 HTML 目录页面
│   └── utils/                      # 通用辅助函数
│       ├── logger.py               # 分级日志输出，支持文件与控制台双通道
│       └── validators.py           # URL 规范化、域名白名单校验等
├── tests/                          # 单元测试与集成测试目录
│   ├── test_fetcher.py
│   ├── test_parser.py
│   └── fixtures/                   # 测试用模拟响应体
└── docs/                           # 用户与开发者文档
    ├── user_guide.md
    ├── architecture.md
    ├── config_schema.yaml
    └── troubleshooting.md
```

## 贡献指南

1. 查阅问题追踪器中的未指派事项，或通过讨论区提出新的功能需求，等待核心维护者确认范围后再开始编码，避免重复工作。
2. 派生项目仓库到个人账户，在派生副本中创建特性分支，分支命名遵循 `feature/简述` 或 `fix/简述` 格式。
3. 编写或修改代码时，请同步更新对应的单元测试用例，并确保所有现有测试通过（`pytest tests/`）。对于新增的外部依赖，需在 `requirements.txt` 中标注版本约束并在 `pyproject.toml` 中补充说明。
4. 提交 pull request 前，执行代码格式化工具 `black` 和 `isort`，并确保无静态检查警告（`flake8`）。PR 描述中需清晰列明改动点、测试覆盖情况及是否影响现有配置格式。
5. 文档类变更（包括新增资源链接或更正说明）无需经过完整测试流程，但仍需通过 PR 提交，并等待至少一位维护者审阅。所有 PR 合并前必须解决冲突且 CI 流水线为绿色。

## 常见问题

**问：健康检查时遇到 SSL 证书验证失败如何处理？**

默认情况下，系统会验证 SSL 证书的有效性。若目标站点使用自签名证书或内部 CA，请在配置文件中将 `ssl_verify` 设为 `false`，或通过环境变量 `OLIVE_SSL_VERIFY=0` 临时关闭。不推荐在生产环境中关闭验证，建议将内部 CA 证书添加到系统信任链中。

**问：大量链接同时检查导致网络超时或连接数过多怎么办？**

可通过配置文件调整并发数（`max_workers` 参数，默认 10）和单次请求超时时间（`timeout_seconds`，默认 30 秒）。对于超大链接列表（超过 1000 条），建议启用 `--batch` 模式，将任务分批执行并写入中间缓存，避免内存溢出。同时可配置 `retry_times` 为 2 至 3 次，提高不稳定网络下的成功率。

**问：如何将导出的 Markdown 报告自动集成到 CI 流程中？**

Olive Link Atlas 支持非交互式运行，可通过命令行参数 `--output-dir` 指定报告输出路径。在 GitHub Actions 或 GitLab CI 中，可添加定时任务步骤，运行扫描后将生成的 `link_status.md` 作为构建产物归档，或通过 API 推送到 Wiki 仓库。若需在 PR 中触发检查，可结合 `--diff-only` 参数仅对比当前变更涉及的新增链接，减少执行时间。

## 许可证

MIT

> 外链数量: 6 | 生成时间: 2026-07-21 04:26:20
