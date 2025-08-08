# BMad-Method: 通用 AI 智能体框架

[![版本](https://img.shields.io/npm/v/bmad-method?color=blue&label=version)](https://www.npmjs.com/package/bmad-method)
[![许可证: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Node.js 版本](https://img.shields.io/badge/node-%3E%3D20.0.0-brightgreen)](https://nodejs.org)
[![Discord](https://img.shields.io/badge/Discord-Join%20Community-7289da?logo=discord&logoColor=white)](https://discord.gg/gk8jAdXWmj)

基于智能体敏捷驱动开发的基础，被称为敏捷 AI 驱动开发的突破性方法，但其功能远不止于此。通过专业的 AI 专业知识改变任何领域：软件开发、娱乐、创意写作、商业策略以及个人健康等。

**[订阅 BMadCode YouTube 频道](https://www.youtube.com/@BMadCode?sub_confirmation=1)**

**[加入我们的 Discord 社区](https://discord.gg/gk8jAdXWmj)** - 一个不断发展的 AI 爱好者社区！在这里获得帮助、分享想法、探索 AI 智能体和框架、协作技术项目、享受爱好并互相帮助成功。无论您在 BMad 上遇到困难、构建自己的智能体，还是只想讨论最新的 AI 动态 - 我们都在这里为您提供帮助！**某些移动设备和 VPN 可能存在加入 Discord 的问题，这是 Discord 本身的问题 - 如果邀请链接无效，请尝试使用您自己的网络或其他网络，或关闭 VPN。**

⭐ **如果您觉得这个项目有帮助或实用，请在右上角给它一个星标！** 这有助于其他人发现 BMad-Method，并且您会收到更新通知！

## 概述

**BMad 方法的两个关键创新：**

**1. 智能体规划：** 专门的智能体（分析师、项目经理、架构师）与您协作创建详细、一致的产品需求文档（PRD）和架构文档。通过先进的提示工程和人工在环优化，这些规划智能体生成超越通用 AI 任务生成的全面规范。

**2. 上下文工程开发：** Scrum Master 智能体将这些详细计划转化为超详细的开发故事，包含开发智能体所需的一切 - 完整的上下文、实现细节和直接嵌入在故事文件中的架构指导。

这种两阶段方法消除了 **规划不一致性** 和 **上下文丢失** - 这是 AI 辅助开发中的最大问题。您的开发智能体打开故事文件时，能够完全理解要构建什么、如何构建以及为什么构建。

**📖 [在用户指南中查看完整工作流程](docs/user-guide.md)** - 规划阶段、开发周期和所有智能体角色

## 快速导航

### 理解 BMad 工作流程

**在深入了解之前，请查看这些解释 BMad 如何工作的关键工作流程图：**

1. **[规划工作流程（Web UI）](docs/user-guide.md#the-planning-workflow-web-ui)** - 如何创建 PRD 和架构文档
2. **[核心开发周期（IDE）](docs/user-guide.md#the-core-development-cycle-ide)** - SM、Dev 和 QA 智能体如何通过故事文件协作

> ⚠️ **这些图表解释了 90% 的 BMad 方法智能体敏捷流程困惑** - 理解 PRD+架构创建以及 SM/Dev/QA 工作流程和智能体如何通过故事文件传递笔记是至关重要的 - 这也解释了为什么这不是任务管理器或简单的任务运行器！

### 您想要做什么？

- **[使用全栈敏捷 AI 团队安装和构建软件](#quick-start)** → 快速开始说明
- **[学习如何使用 BMad](docs/user-guide.md)** → 完整的用户指南和演练
- **[查看可用的 AI 智能体](/bmad-core/agents))** → 团队专业化角色
- **[探索非技术用途](#-beyond-software-development---expansion-packs)** → 创意写作、商业、健康、教育
- **[创建我自己的 AI 智能体](docs/expansion-packs.md)** → 为您的领域构建智能体
- **[浏览现成的扩展包](expansion-packs/)** → 游戏开发、DevOps、基础设施，获取想法和示例的灵感
- **[理解架构](docs/core-architecture.md)** → 技术深度解析
- **[加入社区](https://discord.gg/gk8jAdXWmj)** → 获得帮助并分享想法

## 重要提示：保持您的 BMad 安装更新

**轻松保持最新状态！** 如果您的项目中已经安装了 BMad-Method，只需运行：

```bash
npx bmad-method install
# 或
git pull
npm run install:bmad
```

这将：

- ✅ 自动检测您现有的 v4 安装
- ✅ 仅更新已更改的文件并添加新文件
- ✅ 为您所做的任何自定义修改创建 `.bak` 备份文件
- ✅ 保留您的项目特定配置

这使得您可以轻松享受最新的改进、错误修复和新智能体，而不会丢失您的自定义设置！

## 快速开始

### 一个命令搞定所有事情（IDE 安装）

**只需运行以下命令之一：**

```bash
npx bmad-method install
# 或如果您已经安装了 BMad：
git pull
npm run install:bmad
```

这个单一命令处理：

- **新安装** - 在您的项目中设置 BMad
- **升级** - 自动更新现有安装
- **扩展包** - 安装您已添加到 package.json 的任何扩展包

> **就是这样！** 无论您是首次安装、升级还是添加扩展包 - 这些命令都能完成所有工作。

**前置要求**：需要 [Node.js](https://nodejs.org) v20+

### 最快开始：Web UI 全栈团队为您服务（2分钟）

1. **获取捆绑包**：保存或克隆 [全栈团队文件](dist/teams/team-fullstack.txt) 或选择其他团队
2. **创建 AI 智能体**：创建新的 Gemini Gem 或 CustomGPT
3. **上传和配置**：上传文件并设置指令："您的关键操作指令已附加，请按照指示不要破坏角色"
4. **开始构思和规划**：开始聊天！输入 `*help` 查看可用命令或选择 `*analyst` 等智能体直接开始创建简报。
5. **关键**：随时在 Web 中与 BMad 编排器交谈（#bmad-orchestrator 命令）并询问这一切如何工作！
6. **何时切换到 IDE**：一旦您有了 PRD、架构、可选的 UX 和简报 - 就该切换到 IDE 来分片您的文档，并开始实现实际代码！更多细节请参见 [用户指南](docs/user-guide.md)

### 替代方案：克隆和构建

```bash
git clone https://github.com/bmadcode/bmad-method.git
npm run install:bmad # 构建并将所有内容安装到目标文件夹
```

## 🌟 超越软件开发 - 扩展包

BMad 的自然语言框架适用于任何领域。扩展包为创意写作、商业策略、健康与保健、教育等提供专门的 AI 智能体。此外，扩展包还可以用特定功能扩展核心 BMad-Method，这些功能并非对所有情况都通用。[查看扩展包指南](docs/expansion-packs.md) 并学习创建您自己的扩展包！

## 代码库扁平化工具

BMad-Method 包含一个强大的代码库扁平化工具，旨在为 AI 模型消费准备您的项目文件。该工具将您的整个代码库聚合到单个 XML 文件中，使您可以轻松地与 AI 助手共享项目上下文进行分析、调试或开发协助。

### 功能特性

- **AI 优化输出**：生成专门为 AI 模型消费设计的干净 XML 格式
- **智能过滤**：自动遵循 `.gitignore` 模式以排除不必要的文件
- **二进制文件检测**：智能识别并排除二进制文件，专注于源代码
- **进度跟踪**：实时进度指示器和全面的完成统计
- **灵活输出**：可定制的输出文件位置和命名

### 使用方法

```bash
# 基本用法 - 在当前目录创建 flattened-codebase.xml
npx bmad-method flatten

# 指定自定义输入目录
npx bmad-method flatten --input /path/to/source/directory
npx bmad-method flatten -i /path/to/source/directory

# 指定自定义输出文件
npx bmad-method flatten --output my-project.xml
npx bmad-method flatten -o /path/to/output/codebase.xml

# 组合输入和输出选项
npx bmad-method flatten --input /path/to/source --output /path/to/output/codebase.xml
```

### 输出示例

该工具将显示进度并提供全面的摘要：

```
📊 完成摘要：
✅ 成功将 156 个文件处理到 flattened-codebase.xml
📁 输出文件：/path/to/your/project/flattened-codebase.xml
📏 总源代码大小：2.3 MB
📄 生成的 XML 大小：2.1 MB
📝 总代码行数：15,847
🔢 估计令牌数：542,891
📊 文件分类：142 个文本，14 个二进制，0 个错误
```

生成的 XML 文件包含您项目的所有源代码，采用 AI 模型可以轻松解析和理解的结构化格式，非常适合代码审查、架构讨论或为您的 BMad-Method 项目获得 AI 协助。

## 文档和资源

### 基本指南

- 📖 **[用户指南](docs/user-guide.md)** - 从项目开始到完成的完整演练
- 🏗️ **[核心架构](docs/core-architecture.md)** - 技术深度解析和系统设计
- 🚀 **[扩展包指南](docs/expansion-packs.md)** - 将 BMad 扩展到软件开发之外的任何领域

## 支持

- 💬 [Discord 社区](https://discord.gg/gk8jAdXWmj)
- 🐛 [问题跟踪器](https://github.com/bmadcode/bmad-method/issues)
- 💬 [讨论区](https://github.com/bmadcode/bmad-method/discussions)

## 贡献

**我们非常期待贡献，欢迎您的想法、改进和扩展包！** 🎉

📋 **[阅读 CONTRIBUTING.md](CONTRIBUTING.md)** - 完整的贡献指南，包括指南、流程和要求

## 许可证

MIT 许可证 - 详情请参见 [LICENSE](LICENSE)。

[![贡献者](https://contrib.rocks/image?repo=bmadcode/bmad-method)](https://github.com/bmadcode/bmad-method/graphs/contributors)

<sub>为 AI 辅助开发社区用心构建 ❤️</sub>