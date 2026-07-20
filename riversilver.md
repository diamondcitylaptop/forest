# Olive Resource Atlas

Olive Resource Atlas 是一个面向开发人员、技术研究人员与开源项目维护者的结构化外链资源汇总系统。该项目不直接托管原始内容，而是通过严格的 Markdown 索引机制，将分散在网络各处的技术文档、配置模版、实验报告与参考实现进行归类与版本化记录。Olive Resource Atlas 的目标用户包括需要快速查阅特定技术细节的工程师、希望追踪外部依赖变更的项目负责人，以及需要为团队建立内部知识库的技术管理者。该项目通过统一的资源描述格式与清晰的目录层级，解决了外链资源易失效、关联关系不明确、回溯困难等常见问题，使得资源引用具备可审计性与可维护性。

## 功能概览

- **资源快照索引**：对每条外部资源记录其标题、上游来源、最后检查时间与状态标记，支持快速筛选有效与疑似失效链接。
- **多级分类标签**：每条资源可归属至任意数量的分类标签，例如“网络配置”、“安全审计”、“性能调优”或“框架迁移”，便于按主题聚合。
- **版本关联追踪**：支持记录资源所对应的软件版本或协议版本，便于在技术栈升级时批量复核相关外链。
- **变更历史记录**：所有资源条目的新增、更新与删除操作均记录操作时间与操作人，满足团队协作场景下的审计需求。
- **健康检查报告**：内置链接可达性检查脚本，可定期输出检查结果，并以状态码与响应时间的形式记录在资源描述中。
- **外部引用关系图**：基于资源之间的相互引用生成简单的依赖关系视图，帮助理解技术决策的影响范围。
- **导出与迁移工具**：支持将资源列表导出为 JSON、YAML 或纯文本表格格式，便于迁移至其他知识管理平台。

## 应用场景

- **技术选型调研**：团队在引入新的中间件或框架时，可通过 Olive Resource Atlas 快速查阅社区已有的实践案例、性能对比报告与已知问题讨论，减少重复搜索成本。
- **遗留系统文档重构**：对于缺乏维护的老旧项目，维护者可使用该资源汇总系统重新整理所有外部依赖的官方文档地址、社区补丁链接与迁移指南，使系统可维护性得到恢复。
- **离线环境镜像准备**：在需要搭建离线开发环境时，运维人员可依据资源列表逐一下载所需资源，确保所有外部引用均有对应的本地缓存或替代访问方案。
- **合规性审查**：安全或法务团队可通过资源汇总表审查项目所引用的外部服务是否满足数据主权要求、许可证兼容性要求以及协议版本合规性。

## 快速开始

以下步骤帮助您在本地环境快速部署 Olive Resource Atlas 实例，并开始录入和管理外链资源。

```bash
# 1. 克隆项目仓库
git clone https://github.com/zerxonhy/olive-atlas.git
cd olive-atlas

# 2. 安装依赖（需要 Python 3.9+ 及 pip）
pip install -r requirements.txt

# 3. 初始化本地数据库与配置模板
python scripts/init_db.py --env development

# 4. 运行开发服务器
python app.py --host 127.0.0.1 --port 8080
```

启动成功后，可通过浏览器访问 `http://127.0.0.1:8080` 查看资源总览面板。首次运行将自动创建示例资源条目，您可基于示例修改或删除。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Python | 3.9 - 3.11 | 核心运行环境，3.12 及以上暂未完全适配 |
| SQLite | 3.35.0+ | 内置数据库引擎，用于存储资源元数据与变更日志 |
| Git | 2.25.0+ | 用于克隆仓库及后续版本更新 |
| pip | 21.0+ | Python 包管理器，用于安装项目依赖 |
| requests | 2.28.0+ | 用于健康检查脚本中的 HTTP 探测 |
| pyyaml | 6.0+ | 用于导出资源列表为 YAML 格式 |
| markdown | 3.4.0+ | 用于渲染资源备注中的轻量级格式化文本 |
| pytest | 7.2.0+ | 仅开发测试时需要，生产环境可不安装 |

## 文档导航

| 层面 | 目录位置 | 回答的问题 |
|---|---|---|
| 用户手册 | `docs/user_guide/` | 如何添加新资源、如何修改已有资源、如何执行健康检查、如何导出列表 |
| 管理员指南 | `docs/admin_guide/` | 如何配置检查脚本定时任务、如何迁移数据库、如何备份资源快照 |
| 开发参考 | `docs/dev_reference/` | 数据表结构说明、核心 API 接口定义、自定义标签扩展方法 |
| 设计决策 | `docs/design_decisions/` | 为何选择 SQLite 而非其他数据库、状态标记的语义定义、资源去重策略 |

## 资源列表

本项目的核心资源收录均来源于上游 olive 仓库的配置参考文件。以下为当前已收录的全部外链资源，按文件主题进行分组展示。每条资源均保留用户提供的原始 URL 格式，不进行任何协议补全或域名规范化处理。

### 基础配置与样式资源

- <code>https://github.com/zerxonhy/olive/blob/main/marbleamber.md</code>
- <code>https://github.com/zerxonhy/olive/blob/main/marblegolden.md</code>
- <code>https://github.com/zerxonhy/olive/blob/main/marblejade.md</code>

### 扩展功能与主题资源

- <code>https://github.com/zerxonhy/olive/blob/main/marblelantern.md</code>
- <code>https://github.com/zerxonhy/olive/blob/main/marblepixel.md</code>
- <code>https://github.com/zerxonhy/olive/blob/main/marblesignal.md</code>

## 项目结构

Olive Resource Atlas 采用分层模块化设计，核心代码、配置、文档与测试目录严格分离，便于维护与扩展。以下为项目根目录的完整结构树示意。

```
olive-atlas/
├── app.py                          # 应用程序主入口，初始化路由与中间件
├── requirements.txt                # 生产环境与开发环境通用依赖列表
├── config/
│   ├── default.yaml                # 默认配置参数（端口、数据库路径、日志等级）
│   ├── development.yaml            # 开发环境覆盖配置，开启调试模式
│   └── production.yaml             # 生产环境覆盖配置，关闭调试、启用缓存
├── core/
│   ├── __init__.py                 # 核心模块初始化
│   ├── resource.py                 # 资源实体类定义，包含校验与序列化逻辑
│   ├── tag.py                      # 标签管理模块，支持层级标签与合并操作
│   ├── history.py                  # 变更历史记录模块，基于 SQLite 触发器实现
│   └── checker.py                  # 链接健康检查引擎，支持并发探测与超时控制
├── storage/
│   ├── __init__.py                 # 存储适配器接口定义
│   ├── sqlite_adapter.py           # SQLite 数据库具体实现，包含建表语句与 CRUD
│   └── schema.sql                  # 独立存储的 SQL 模式定义文件，便于人工审查
├── api/
│   ├── __init__.py                 # API 蓝图初始化
│   ├── v1_resources.py             # 资源相关 RESTful 端点（GET/POST/PUT/DELETE）
│   └── v1_health.py                # 健康检查状态查询端点与触发接口
├── scripts/
│   ├── init_db.py                  # 数据库初始化脚本，可指定环境参数
│   ├── import_from_markdown.py     # 从 Markdown 列表批量导入资源的工具
│   └── export_to_json.py           # 将当前全部资源导出为 JSON 格式文件
├── tests/
│   ├── unit/                       # 单元测试目录，按模块划分测试文件
│   │   ├── test_resource.py
│   │   ├── test_tag.py
│   │   └── test_checker.py
│   └── integration/                # 集成测试目录，模拟完整 API 调用流程
│       └── test_api_flow.py
├── docs/                           # 完整文档目录，内容与导航表格对应
│   ├── user_guide/
│   ├── admin_guide/
│   ├── dev_reference/
│   └── design_decisions/
└── README.md                       # 项目首页说明文档（即本文档）
```

## 贡献指南

Olive Resource Atlas 欢迎外部贡献者参与改进。请遵循以下步骤提交您的变更。

1. 在 GitHub 上复刻（Fork）本仓库至您的个人账户，并将复刻后的仓库克隆至本地开发环境。请确保您的 Git 全局配置已正确设置用户名与邮箱。
2. 从 `main` 分支切出新功能分支，分支命名建议使用 `feature/简要描述` 或 `fix/问题编号` 格式。对于较大的变更，建议先在 `issues` 中创建讨论议题，再开始编码。
3. 在本地完成代码或文档修改后，请确保所有现有单元测试能够通过，并为新增功能补充相应的测试用例。测试执行命令为 `pytest tests/`。
4. 提交代码时，请使用清晰且语义化的提交信息，格式建议为 `类型: 简短描述`，例如 `fix: 修复健康检查超时设置未生效的问题`。提交前请运行代码格式化工具 `black` 与静态检查 `pylint`。
5. 推送变更至您的复刻仓库，并通过 GitHub 界面发起拉取请求（Pull Request）至本项目的 `main` 分支。请求描述中请关联相关议题编号，并简要说明变更内容与测试结果。

## 常见问题

**问：资源列表中的外部链接如果失效了，系统会如何处理？**

答：系统不会自动删除或修改失效链接。健康检查脚本会定期检测每条资源的可达性，并将状态码和错误信息记录在资源条目的扩展字段中。用户可通过管理面板查看所有失效链接的汇总报告，并手动决定是更新链接地址、添加备注说明，还是将资源标记为“已废弃”。项目维护者建议每月至少运行一次健康检查，以保证资源列表的可靠性。

**问：是否可以导入其他格式的外链数据，例如浏览器书签或 CSV 文件？**

答：当前版本内置了从 Markdown 列表导入的脚本工具。对于其他格式，我们推荐先将数据转换为 Markdown 无序列表，每行包含标题和 URL，然后使用 `import_from_markdown.py` 进行导入。后续版本计划增加对 Netscape 书签格式和标准 CSV 格式的直接支持。如有紧急导入需求，可参考 `docs/dev_reference/` 中的适配器扩展指南自行编写临时转换脚本。

**问：Olive Resource Atlas 是否支持多用户权限管理？**

答：当前版本为单用户设计，所有操作均不设权限校验，适合个人开发者或小型团队内部使用。若需要多用户支持，建议将系统部署在具备基础认证网关（如 HTTP Basic Auth 或 OAuth2 Proxy）的环境后，再由网关层控制访问权限。项目路线图显示，多用户角色管理（只读、编辑、管理员）预计在 v2.0 版本中提供。

## 许可证

MIT License

Copyright (c) 2026 Olive Resource Atlas Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

> 外链数量: 6 | 生成时间: 2026-07-21 04:27:01
