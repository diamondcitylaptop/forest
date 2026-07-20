# Olive Resource Catalog

Olive Resource Catalog 是一个面向开发者与开源技术爱好者的外链资源聚合与导航工具。该项目以轻量级、可扩展的 Markdown 索引体系为核心，将分散在多个仓库与文档中的优质技术链接进行结构化整理，帮助用户快速定位到特定领域的项目文档、配置示例与架构说明。Olive 本身不存储大型二进制文件，也不托管运行时依赖，而是作为一个语义化的资源指针系统，为团队或个人提供清晰、可维护的外部参考链路管理方案。

Olive 的目标用户包括：需要维护多仓库文档索引的技术负责人、希望建立个人知识外链体系的开源贡献者，以及希望通过标准化链接结构降低项目协作成本的小型研发团队。通过 Olive，用户可以将零散的 GitHub 文档链接按主题、模块或里程碑进行归类，并在统一的目录树中呈现，从而避免重复检索和链接失散的问题。

## 功能概览

- **链接分类索引**：支持按文档主题、仓库模块或更新频率对 URL 进行分组，每个分组可独立维护和版本追踪。
- **Markdown 原生驱动**：所有链接数据以 Markdown 文件形式存储，兼容 GitHub、GitLab 等主流代码托管平台的在线预览与编辑。
- **轻量级目录树生成**：基于项目文件夹结构自动生成 ASCII 目录树，便于在 README 中直观展示资源组织方式。
- **外链状态检查接口**：提供简单的 Shell 脚本，用于批量检测已收录 URL 的可访问性，降低链接失效风险。
- **版本化快照备注**：允许为每个链接添加可选的版本号或提交哈希备注，方便追溯文档内容变更节点。
- **场景化标签系统**：支持为链接打上“部署”、“配置”、“API 参考”等自定义标签，提高检索效率。
- **低侵入式集成**：无需修改现有仓库的工作流，仅通过维护独立索引文件即可实现资源导航功能。

## 应用场景

1. **微服务文档聚合**  
   当团队维护多个微服务仓库时，每个仓库的 README 或 docs 目录下可能都有独立的部署说明。Olive 可用于创建顶层索引文件，将各服务的核心文档链接汇总到一个页面中，方便新成员快速了解整体架构。

2. **开源项目外链备份**  
   个人开发者或开源社区常依赖外部教程、视频或博客作为补充材料。Olive 可以帮助记录这些外部资源的原始链接，并在项目搬迁或重构时快速核对引用关系。

3. **技术评估与选型记录**  
   在技术调研阶段，工程师需要对比多个框架或工具的官方文档、性能测试报告和社区案例。通过 Olive 建立临时索引，可以系统性地保留所有参考链接，避免遗忘或混淆。

4. **多版本文档切换**  
   当项目存在多个大版本并行维护时，不同版本的文档可能位于不同的分支或标签下。Olive 允许按版本维度组织链接，帮助用户迅速定位到正确版本的说明文件。

5. **离线文档准备清单**  
   对于需要在无网络环境下工作的场景，Olive 可以列出所有需要提前下载的文档页面或离线包来源，作为准备工作的检查清单。

## 快速开始

以下步骤将指导您在本地环境完成 Olive Resource Catalog 的克隆、依赖安装与基础运行。

```bash
# 1. 克隆项目仓库
git clone https://github.com/zerxonhy/olive.git
cd olive

# 2. 安装基础依赖（仅需 Python 3 和标准库）
python3 -m venv venv
source venv/bin/activate

# 3. 运行本地资源索引生成脚本
python3 scripts/build_index.py --input ./links --output ./README.md
```

若您不需要运行构建脚本，也可以直接编辑 `./links` 目录下的 Markdown 文件来手动维护链接列表。项目本身不强制依赖任何第三方包，Python 环境仅用于辅助自动化整理。

## 安装要求

| 依赖 | 必需 | 说明 |
|------|------|------|
| Python 3.8 或更高版本 | 是 | 用于运行索引构建与链接检查辅助脚本 |
| Git 2.20 或更高版本 | 是 | 用于克隆仓库及版本管理操作 |
| bash 4.0 或更高版本 | 否 | 仅当使用外链状态检查脚本时需要 |
| curl 或 wget | 否 | 用于外部链接可用性检测，非核心功能 |
| markdownlint-cli | 否 | 可选，用于保持索引文件的 Markdown 格式一致性 |
| tree 命令行工具 | 否 | 可选，用于生成更详细的目录树结构展示 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 用户入门 | `docs/quickstart.md` | 如何在一个新项目中初始化 Olive 索引结构？ |
| 链接维护 | `docs/link-management.md` | 如何添加、更新或删除资源链接？如何批量检查链接状态？ |
| 自定义扩展 | `docs/customization.md` | 是否支持自定义标签分类？如何修改目录树生成逻辑？ |
| 团队协作 | `docs/collaboration.md` | 多人同时维护索引时如何避免冲突？如何审查链接变更？ |
| 故障排查 | `docs/troubleshooting.md` | 遇到链接无法访问、脚本报错或目录结构混乱时如何处理？ |
| 版本历史 | `CHANGELOG.md` | 每个版本更新了哪些链接分类、修复了哪些路径错误？ |

## 资源列表

以下链接为 Olive Resource Catalog 当前收录的外部资源原文地址，按所属文档主题进行分类展示。所有链接均保持用户提供的原始格式，未做任何协议或域名修正。

### 像素风格主题文档

<code>https://github.com/zerxonhy/olive/blob/main/pixelgarden.md</code>

<code>https://github.com/zerxonhy/olive/blob/main/pixeljade.md</code>

<code>https://github.com/zerxonhy/olive/blob/main/pixelpearl.md</code>

### 自然元素主题文档

<code>https://github.com/zerxonhy/olive/blob/main/prairiewillow.md</code>

### 石英系列主题文档

<code>https://github.com/zerxonhy/olive/blob/main/quartzhorizon.md</code>

<code>https://github.com/zerxonhy/olive/blob/main/quartzjade.md</code>

上述链接均指向同一仓库下的不同 Markdown 文件，分别对应不同的视觉风格配置、组件说明或布局样例。用户可根据需要直接访问原始文件，或通过 Olive 的索引脚本批量拉取本地缓存。

## 项目结构

```
olive/
├── README.md                  # 项目总览与快速入口
├── CHANGELOG.md               # 版本变更记录
├── LICENSE                    # MIT 许可证文件
├── .gitignore                 # Git 忽略规则
├── links/                     # 核心链接索引目录
│   ├── pixel/                 # 像素风格主题链接分组
│   │   ├── garden.md          # pixelgarden 文档引用
│   │   ├── jade.md            # pixeljade 文档引用
│   │   └── pearl.md           # pixelpearl 文档引用
│   ├── natural/               # 自然元素主题链接分组
│   │   └── willow.md          # prairiewillow 文档引用
│   └── quartz/                # 石英系列主题链接分组
│       ├── horizon.md         # quartzhorizon 文档引用
│       └── jade.md            # quartzjade 文档引用
├── scripts/                   # 辅助脚本目录
│   ├── build_index.py         # 索引构建主脚本
│   ├── check_links.sh         # 外链可用性批量检测脚本
│   └── utils.py               # 公共工具函数
├── docs/                      # 详细文档目录
│   ├── quickstart.md          # 快速入门指南
│   ├── link-management.md     # 链接维护手册
│   ├── customization.md       # 自定义配置说明
│   ├── collaboration.md       # 团队协作规范
│   └── troubleshooting.md     # 常见问题排错
├── tests/                     # 单元测试与集成测试
│   ├── test_build.py          # 索引构建逻辑测试
│   └── fixtures/              # 测试用固定数据样例
└── templates/                 # 模板文件目录
    └── link_entry.tmpl        # 新链接条目的推荐 Markdown 模板
```

## 贡献指南

欢迎并感谢您为 Olive Resource Catalog 项目贡献新的链接索引、改进脚本逻辑或完善文档内容。请遵循以下步骤参与贡献：

1. **提交前自检**  
   确保您新增或修改的链接指向公开可访问的文档页面，且链接内容与现有分组主题一致。避免收录临时性、私有化或频繁变更的 URL。

2. **创建分支与变更**  
   从最新的 `main` 分支创建您的特性分支，命名格式为 `feature/your-feature-name` 或 `fix/issue-description`。所有链接变更应同步更新 `links/` 目录下对应的分类文件。

3. **运行本地验证**  
   执行 `scripts/check_links.sh` 检查您新增的链接是否可正常访问，并运行 `python3 scripts/build_index.py` 确保 README 中的资源列表能够正确生成。

4. **提交拉取请求**  
   提交 PR 时请在描述中明确说明新增链接的主题、目的以及是否涉及现有分类的重构。确保 PR 标题简洁清晰，并关联相关 Issue（如有）。

5. **等待审核与合并**  
   项目维护者将在 3 个工作日内审核您的 PR，可能会要求补充说明或调整分类。合并后您的贡献将被记录在 `CHANGELOG.md` 的“贡献者”部分。

## 常见问题

**Q：Olive 是否必须运行 Python 脚本才能更新 README 中的资源列表？**  
A：不是必须的。Python 脚本仅用于自动化合并与格式化，方便批量操作。您也可以直接在 `links/` 目录下手动编辑 Markdown 文件，然后手动复制到 README 的“资源列表”章节。但推荐使用脚本以保持格式一致性。

**Q：如果外部链接失效，我应该如何处理？**  
A：如果检测到某个链接无法访问，请先在 `links/` 对应文件中将该条目注释或标记为 `[deprecated]`，然后尝试在仓库中查找替代文档。若找不到替代，可提交 Issue 通知维护团队，我们会尝试联系原始作者或更新为存档链接。

**Q：我可以添加非 GitHub 域名的链接吗？**  
A：可以。Olive 不限制链接的域名或协议，只要是公开可读的文档页面即可。但建议优先选择稳定性较高的站点，并确保链接不包含临时会话参数或动态令牌。

## 许可证

MIT License。详见项目根目录下的 LICENSE 文件。您可以在遵守许可证条款的前提下自由使用、修改和分发本项目代码及索引数据。

> 外链数量: 6 | 生成时间: 2026-07-21 04:27:25
