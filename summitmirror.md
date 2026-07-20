# Olive Resource Atlas

Olive Resource Atlas 是一个面向开发者、技术研究人员与开源项目维护者的结构化外链与元数据资源汇总工具。该项目不直接存储或托管任何用户生成内容，而是以索引表（Index Table）的形式，将分散在多个代码仓库、文档站点与在线服务中的高价值技术资源进行规范化整理，并通过统一的访问入口提供快速查询、版本追踪与引用关系分析能力。

项目定位为“技术资源的资源”，即元数据聚合层。其目标用户包括需要频繁查阅跨项目文档的工程师、进行技术选型的架构师、编写技术书籍或教程的内容创作者，以及希望系统化梳理自身项目外部依赖关系的开源维护者。Olive Resource Atlas 通过将资源链接、文档快照引用、镜像站点状态、版本哈希与更新时间等关键信息整合为结构化记录，帮助用户避免链接失效、版本错乱与信息分散等问题，从而提升技术信息检索的效率与准确性。

## 功能概览

- **多源资源索引管理**：支持将来自不同 GitHub 仓库、在线文档平台与静态站点中的 Markdown 文件、配置文件与日志文件注册为资源条目，每条记录包含原始 URL、本地缓存路径、最后校验状态与内容哈希值。

- **链接状态与可用性监控**：对已收录的资源链接进行周期性可达性检测与内容变更嗅探，自动标记失效链接、内容更新节点与重定向路径，并将结果输出为结构化状态报告。

- **镜像与备选路径关联**：针对同一份内容可能存在于多个镜像地址或不同分支路径的情况，提供关联映射功能，允许用户在同一资源记录下挂载多个备选 URL，并标注其优先级与同步延迟。

- **标签与分类树浏览**：资源条目支持自定义标签（Tag）与分类路径（Category Path），用户可按项目名、主题领域、文件类型或维护状态进行多维度筛选与排序。

- **变更历史与快照对比**：每次资源内容发生变更时，系统自动记录前次快照的摘要信息，并提供基于行的文本对比视图，便于用户追踪文档演进过程。

- **批量导入与导出接口**：提供 JSON 与 CSV 格式的批量导入导出功能，支持从现有文档清单或站点地图中批量生成资源条目，也可将索引数据导出用于外部工具集成。

- **权限与只读镜像模式**：支持将整个资源索引部署为只读静态站点，允许用户在不依赖数据库的情况下直接通过浏览器浏览所有已收录资源信息，适合内网或离线环境使用。

## 应用场景

- **开源项目文档站点的外链整理**：当开源项目的 README 或 Wiki 中引用了大量外部资源（如设计规范、协议文本、参考实现）时，维护者可使用 Olive Resource Atlas 为这些外链建立独立索引，并在资源失效时快速定位替代链接，避免文档中出现死链。

- **技术培训课程的材料打包**：技术讲师或培训机构在准备课程材料时，通常需要引用数十篇技术博客、官方 API 文档与视频教程链接。通过 Olive Resource Atlas，可将这些资源统一注册为课程专属资源集，并生成一份包含所有链接状态与摘要的静态报告，分发给学员作为参考资料。

- **多仓库依赖文档的版本追踪**：微服务架构或大型单体项目中，不同模块的文档可能分散在多个 Git 仓库中。Olive Resource Atlas 允许运维人员将所有模块的 README、架构说明与部署手册的原始链接统一收录，并通过变更嗅探功能及时发现文档更新，从而降低因文档版本不一致导致的沟通成本。

- **离线环境下的文档镜像索引**：在无互联网接入的内网开发环境中，团队可预先将所需的外部文档缓存至内部服务器，并使用 Olive Resource Atlas 记录缓存地址与原始地址的映射关系。开发者通过查询索引即可快速获取可用的内部文档地址，无需手动记忆或维护本地书签。

## 快速开始

以下命令演示如何从 GitHub 克隆项目仓库、安装依赖并启动开发服务。

```bash
# 克隆仓库
git clone https://github.com/zerxonhy/olive-resource-atlas.git

# 进入项目目录
cd olive-resource-atlas

# 安装 Python 依赖（推荐使用虚拟环境）
python -m venv venv
source venv/bin/activate  # Windows 请使用 venv\Scripts\activate
pip install -r requirements.txt

# 初始化本地资源索引数据库
python manage.py migrate

# 加载示例资源条目（包含本项目的默认外链集合）
python manage.py loaddata fixtures/initial_resources.json

# 启动开发服务器
python manage.py runserver
```

访问 http://127.0.0.1:8000 即可浏览本地索引界面。如需执行链接状态检测，请运行：

```bash
python manage.py check_links --timeout 5 --retry 2
```

检测结果将输出至 `reports/link_status_<timestamp>.json` 文件中。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Python | 3.10 及以上 | 核心运行环境，用于执行资源索引管理、链接检测与数据导入导出逻辑。 |
| Django | 4.2 LTS | Web 框架，提供管理后台、ORM 与模板渲染能力，用于构建索引浏览界面。 |
| Celery | 5.3 及以上 | 分布式任务队列，用于异步执行链接可达性检测与内容变更嗅探任务。 |
| Redis | 7.0 及以上 | 作为 Celery 的消息代理（Broker）与结果后端（Result Backend），缓存临时状态数据。 |
| SQLite / PostgreSQL | SQLite 3.35+ 或 PostgreSQL 14+ | 主数据存储引擎，SQLite 适用于开发与小型部署，PostgreSQL 推荐用于生产环境。 |
| Git | 2.30 及以上 | 用于克隆资源仓库、获取文件历史记录与计算内容哈希值。 |
| curl / wget | 最新稳定版 | 链接检测模块的底层 HTTP 请求工具，用于获取响应头与内容摘要。 |
| Node.js（可选） | 18.x 及以上 | 若启用前端资源构建（如管理界面优化），需要 Node.js 与 npm 支持。 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 用户手册 | `docs/user_guide/` | 如何注册资源条目、如何查看链接状态、如何使用批量导入导出功能、如何配置只读镜像模式。 |
| 管理员指南 | `docs/admin_guide/` | 如何部署生产环境、如何配置 Celery 与 Redis 连接、如何设置周期性链接检测任务、如何备份与恢复索引数据库。 |
| 开发参考 | `docs/dev_reference/` | 资源条目数据模型定义、链接检测模块的扩展接口、自定义标签分类规则、REST API 端点说明与请求示例。 |
| 运维与监控 | `docs/ops/` | 日志配置说明、性能指标采集方法、告警规则推荐（如链接失效比例超过阈值）、健康检查端点使用方式。 |

## 资源列表

本项目的初始资源索引基于以下原始外链集合构建。所有链接均按其所属主题类别进行分组，以便快速定位。

### 核心文档参考

该组资源指向同一仓库下不同主题的 Markdown 文档，内容涵盖系统设计、部署方案与调优参数等。

- <code>https://github.com/zerxonhy/olive/blob/main/midnighttimber.md</code>

- <code>https://github.com/zerxonhy/olive/blob/main/mirrorprairie.md</code>

- <code>https://github.com/zerxonhy/olive/blob/main/mirrorshadow.md</code>

- <code>https://github.com/zerxonhy/olive/blob/main/mirrortimber.md</code>

- <code>https://github.com/zerxonhy/olive/blob/main/nebulaviolet.md</code>

- <code>https://github.com/zerxonhy/olive/blob/main/oceanolive.md</code>

## 项目结构

项目代码组织遵循 Django 应用标准布局，同时融合了资源索引管理、链接检测与前端静态资源等模块。

```
olive-resource-atlas/
├── manage.py                      # Django 项目管理入口
├── requirements.txt               # Python 依赖清单
├── .env.example                   # 环境变量配置模板（含数据库连接、Redis 地址等）
├── config/                        # 项目配置目录
│   ├── settings.py               # 主配置文件（含应用注册、中间件、模板与静态文件路径）
│   ├── celery.py                 # Celery 应用定义与任务导入
│   └── urls.py                   # 根路由配置
├── apps/                          # 所有自定义 Django 应用
│   ├── resources/                # 资源索引核心应用：定义 Resource、LinkSnapshot、Tag 等模型
│   │   ├── models.py             # 数据模型（含资源条目、备选路径、变更历史）
│   │   ├── views.py              # 资源列表、详情、搜索与状态视图
│   │   ├── tasks.py              # 异步任务：链接检测、内容哈希计算、状态更新
│   │   └── management/           # 自定义命令行命令（如 check_links、import_resources）
│   ├── monitor/                  # 监控与报告应用：生成链接状态报表、统计指标
│   │   ├── detectors.py          # 内容变更嗅探器实现（基于响应头 ETag 与 Last-Modified）
│   │   └── reporters.py          # 状态报告生成器（JSON / Markdown / HTML 格式）
│   └── api/                      # RESTful API 应用：对外提供资源查询与状态获取接口
│       ├── serializers.py        # 资源条目与状态数据的序列化器
│       └── viewsets.py           # API 视图集（支持分页、筛选与排序）
├── static/                        # 前端静态资源（CSS、JavaScript、图标）
│   ├── css/                      # 基于 Bootstrap 5 的自定义样式
│   └── js/                       # 前端交互脚本（如筛选器联动、状态标签切换）
├── templates/                     # Django 模板文件
│   ├── base.html                 # 基础布局模板
│   ├── resource_list.html        # 资源列表页模板
│   └── resource_detail.html      # 资源详情页模板（含变更历史与镜像地址）
├── fixtures/                      # 初始数据加载文件（含本项目的资源示例）
│   └── initial_resources.json    # 包含上述 6 个原始资源链接的初始数据集
├── reports/                       # 链接检测报告输出目录（自动生成，不纳入版本控制）
├── logs/                          # 应用日志存储目录（按日期滚动）
└── scripts/                       # 辅助运维脚本
    ├── backup_db.sh              # 数据库备份脚本
    └── deploy_static.sh          # 静态资源部署至 CDN 或对象存储的脚本
```

## 贡献指南

我们欢迎并鼓励社区开发者以多种形式参与 Olive Resource Atlas 的改进与扩展。请遵循以下步骤提交贡献。

1. **查阅问题追踪器与路线图**：访问项目的 GitHub Issues 页面，查找标记为 `help wanted` 或 `good first issue` 的待办事项。如计划实现新功能或进行重大改动，建议先通过 Issue 与维护团队沟通设计思路，避免重复工作。

2. **派生仓库并创建功能分支**：将主仓库派生至个人账号下，并基于 `main` 分支创建新的功能分支（例如 `feature/add-import-from-sitemap` 或 `fix/link-detector-timeout`）。分支命名应简洁描述改动内容。

3. **编写或更新测试用例**：所有新增功能或缺陷修复必须包含对应的单元测试或集成测试，测试文件放置在相应应用的 `tests/` 目录下。确保现有测试套件全部通过后再提交。

4. **遵循代码风格与文档规范**：Python 代码应遵循 PEP 8 规范，并确保通过 `flake8` 与 `black` 检查。所有新增的公共函数、类与方法必须包含 docstring 注释。若改动涉及用户可见行为，需同步更新 `docs/` 目录下的对应文档。

5. **提交拉取请求（Pull Request）**：将功能分支推送至派生仓库，并向主仓库的 `main` 分支发起拉取请求。PR 标题应简明扼要，正文需详细说明改动背景、实现方式与测试覆盖情况。维护团队将在 3 个工作日内进行评审，并可能提出修改意见。

## 常见问题

**链接检测任务执行时出现超时或连接拒绝错误，应如何处理？**

链接检测模块默认使用 `curl` 或 `urllib` 发送 HTTP 请求，超时时间可在执行 `check_links` 命令时通过 `--timeout` 参数调整（单位秒）。对于频繁超时的目标站点，建议先在 `config/settings.py` 中的 `LINK_CHECK_OPTIONS` 配置项中设置 `"verify_ssl": false` 以绕过 SSL 证书校验（仅限内网或测试环境）。若目标站点存在反爬机制，可配置 `"user_agent"` 模拟常用浏览器标识。对于永久失效的链接，可通过管理后台将其状态手动标记为 `broken`，并在资源备注中记录替代地址。

**如何将本地索引数据迁移到生产环境的 PostgreSQL 数据库中？**

首先在生产环境的 PostgreSQL 中创建目标数据库与用户，并授予完整读写权限。然后在 `config/settings.py` 中将 `DATABASES` 配置中的 `ENGINE` 改为 `django.db.backends.postgresql`，并填写正确的 `NAME`、`USER`、`PASSWORD`、`HOST` 与 `PORT`。执行 `python manage.py migrate` 创建表结构。若需迁移现有数据，可使用 `python manage.py dumpdata --exclude auth.permission --exclude contenttypes > data.json` 导出开发数据，再通过 `python manage.py loaddata data.json` 导入生产数据库。建议在迁移前完整备份生产数据库。

**资源索引中的 Markdown 文件内容变更时，系统如何感知并更新记录？**

系统通过两种机制感知变更：定时轮询与 Webhook 触发。定时轮询由 Celery 周期性任务执行，默认每 24 小时对所有资源条目的原始 URL 发送 HEAD 或 GET 请求，比较响应头中的 `ETag` 或 `Last-Modified` 值与本地记录。若检测到不一致，则自动拉取完整内容并计算新哈希值，同时生成变更对比记录。Webhook 触发方式适用于 GitHub 或 GitLab 仓库，用户可在仓库设置中添加 Payload URL 指向本系统的 `/api/webhook/github` 端点，当目标文件发生推送事件时，系统将立即执行增量更新。

## 许可证

MIT License

Copyright (c) 2026 Olive Resource Atlas Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

> 外链数量: 6 | 生成时间: 2026-07-21 04:26:20
