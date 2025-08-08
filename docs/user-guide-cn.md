# BMad-Method BMAd Code 用户指南

本指南将帮助您理解和有效使用 BMad 方法进行敏捷AI驱动的规划和开发。

## BMad 计划和执行工作流程

首先，这是完整的标准绿地项目（Greenfield）规划+执行工作流程。棕地项目（Brownfield）非常相似，但建议先理解这个绿地项目流程，即使在处理棕地项目之前，先在一个简单项目上实践。BMad 方法需要安装到您的新项目文件夹的根目录。对于规划阶段，您可以选择使用强大的网络代理来完成，可能会以更低的成本获得更高质量的结果，而不是在某些代理工具中提供您自己的API密钥或积分。对于规划，强大的思考模型和更大的上下文——以及与代理作为合作伙伴工作将获得最佳结果。

如果您要在棕地项目（现有项目）中使用 BMad 方法，请查看 **[在棕地项目中工作](./working-in-the-brownfield.md)**。

如果您看不到下面渲染的图表，可以将 Markdown All in One 和 Markdown Preview Mermaid Support 插件安装到 VSCode（或其分支克隆版本）。使用这些插件，如果在打开时右键单击标签页，应该会有打开预览的选项，或者查看IDE文档。

### 规划工作流程（Web UI 或强大的IDE代理）

在开发开始之前，BMad 遵循结构化的规划工作流程，为提高成本效益，最好在Web UI中完成：

```mermaid
graph TD
    A["开始：项目想法"] --> B{"可选：分析师研究"}
    B -->|是| C["分析师：头脑风暴（可选）"]
    B -->|否| G{"项目简介可用？"}
    C --> C2["分析师：市场研究（可选）"]
    C2 --> C3["分析师：竞争对手分析（可选）"]
    C3 --> D["分析师：创建项目简介"]
    D --> G
    G -->|是| E["PM：从简介创建PRD（快速通道）"]
    G -->|否| E2["PM：交互式PRD创建（更多问题）"]
    E --> F["创建包含FRs、NFRs、Epics & Stories的PRD"]
    E2 --> F
    F --> F2{"需要UX？"}
    F2 -->|是| F3["UX专家：创建前端规范"]
    F2 -->|否| H["架构师：从PRD创建架构"]
    F3 --> F4["UX专家：为Lovable/V0生成UI提示（可选）"]
    F4 --> H2["架构师：从PRD + UX规范创建架构"]
    H --> I["PO：运行主检查清单"]
    H2 --> I
    I --> J{"文档对齐？"}
    J -->|是| K["规划完成"]
    J -->|否| L["PO：更新Epics & Stories"]
    L --> M["根据需要更新PRD/架构"]
    M --> I
    K --> N["📁 切换到IDE（如果在Web代理平台）"]
    N --> O["PO：分片文档"]
    O --> P["准备SM/Dev周期"]

    style A fill:#f5f5f5,color:#000
    style B fill:#e3f2fd,color:#000
    style C fill:#e8f5e9,color:#000
    style C2 fill:#e8f5e9,color:#000
    style C3 fill:#e8f5e9,color:#000
    style D fill:#e8f5e9,color:#000
    style E fill:#fff3e0,color:#000
    style E2 fill:#fff3e0,color:#000
    style F fill:#fff3e0,color:#000
    style F2 fill:#e3f2fd,color:#000
    style F3 fill:#e1f5fe,color:#000
    style F4 fill:#e1f5fe,color:#000
    style G fill:#e3f2fd,color:#000
    style H fill:#f3e5f5,color:#000
    style H2 fill:#f3e5f5,color:#000
    style I fill:#f9ab00,color:#fff
    style J fill:#e3f2fd,color:#000
    style K fill:#34a853,color:#fff
    style L fill:#f9ab00,color:#fff
    style M fill:#fff3e0,color:#000
    style N fill:#1a73e8,color:#fff
    style O fill:#f9ab00,color:#fff
    style P fill:#34a853,color:#fff
```

#### Web UI 到IDE的转换

**关键转换点**：一旦PO确认文档对齐，您必须从Web UI切换到IDE以开始开发工作流程：

1. **复制文档到项目**：确保 `docs/prd.md` 和 `docs/architecture.md` 在您项目的docs文件夹中（或您可以在安装期间指定的自定义位置）
2. **切换到IDE**：在您首选的Agentic IDE中打开您的项目
3. **文档分片**：使用PO代理对PRD进行分片，然后对架构进行分片
4. **开始开发**：开始接下来的核心开发周期

### 核心开发周期（IDE）

一旦规划完成并且文档已分片，BMad 遵循结构化的开发工作流程：

```mermaid
graph TD
    A["开发阶段开始"] --> B["SM：审查上一个Story的开发/QA注释"]
    B --> B2["SM：从分片的Epic +架构起草下一个Story"]
    B2 --> B3{"PO：验证Story草稿（可选）"}
    B3 -->|请求验证| B4["PO：根据工件验证Story"]
    B3 -->|跳过验证| C{"用户批准"}
    B4 --> C
    C -->|批准| D["Dev：顺序任务执行"]
    C -->|需要修改| B2
    D --> E["Dev：实施任务 + 测试"]
    E --> F["Dev：运行所有验证"]
    F --> G["Dev：标记为准备审查 + 添加注释"]
    G --> H{"用户验证"}
    H -->|请求QA审查| I["QA：高级开发审查 + 主动重构"]
    H -->|无需QA批准| M["重要：验证所有回归测试和Linting都通过"]
    I --> J["QA：审查、重构代码、添加测试、记录注释"]
    J --> L{"QA决定"}
    L -->|需要开发工作| D
    L -->|批准| M
    H -->|需要修复| D
    M --> N["重要：在继续之前提交您的更改！"]
    N --> K["标记Story为完成"]
    K --> B

    style A fill:#f5f5f5,color:#000
    style B fill:#e8f5e9,color:#000
    style B2 fill:#e8f5e9,color:#000
    style B3 fill:#e3f2fd,color:#000
    style B4 fill:#fce4ec,color:#000
    style C fill:#e3f2fd,color:#000
    style D fill:#e3f2fd,color:#000
    style E fill:#e3f2fd,color:#000
    style F fill:#e3f2fd,color:#000
    style G fill:#e3f2fd,color:#000
    style H fill:#e3f2fd,color:#000
    style I fill:#f9ab00,color:#fff
    style J fill:#ffd54f,color:#000
    style K fill:#34a853,color:#fff
    style L fill:#e3f2fd,color:#000
    style M fill:#ff5722,color:#fff
    style N fill:#d32f2f,color:#fff
```

## 安装

### 可选

如果您想在Web中使用Claude（Sonnet 4或Opus）、Gemini Gem（2.5 Pro）或自定义GPT进行规划：

1. 导航到 `dist/teams/`
2. 复制 `team-fullstack.txt`
3. 创建新的Gemini Gem或CustomGPT
4. 上传文件并说明："您的关键操作说明已附加，不要按照指示打破角色"
5. 输入 `/help` 查看可用命令

### IDE项目设置

```bash
# 交互式安装（推荐）
npx bmad-method install
```

## 特殊代理

有两个bmad代理——将来它们将合并到单一的bmad-master中。

### BMad-Master

这个代理可以执行所有其他代理可以执行的任何任务或命令，除了实际的story实施。此外，这个代理可以在Web中通过访问知识库向您解释BMad方法，并向您解释有关过程的任何内容。

如果您不想在开发之外在不同的代理之间切换，这个代理适合您。请记住，随着上下文的增长，代理的性能会下降，因此指示代理压缩对话并以压缩对话作为初始消息开始新对话很重要。经常这样做，最好在每个story实施后。

### BMad-Orchestrator

这个代理不应该在IDE中使用，它是一个重量级的特殊用途代理，利用大量上下文可以变形为任何其他代理。它的存在仅仅是为了促进Web包中的团队。如果您使用Web包，您将看到BMad Orchestrator的欢迎。

### 代理如何工作

#### 依赖系统

每个代理都有一个YAML部分来定义其依赖关系：

```yaml
dependencies:
  templates:
    - prd-template.md
    - user-story-template.md
  tasks:
    - create-doc.md
    - shard-doc.md
  data:
    - bmad-kb.md
```

**关键点：**

- 代理只加载他们需要的资源（精简上下文）
- 依赖关系在打包过程中自动解析
- 资源在代理之间共享以保持一致性

#### 代理交互

**在IDE中：**

```bash
# 一些IDE，比如Cursor或Windsurf，使用手动规则，所以交互使用'@'符号
@pm Create a PRD for a task management app
@architect Design the system architecture
@dev Implement the user authentication

# 一些，比如Claude Code使用斜杠命令代替
/pm Create user stories
/dev Fix the login bug
```

#### 交互模式

- **增量模式**：逐步与用户输入交互
- **YOLO模式**：最少交互的快速生成

## IDE集成

### IDE最佳实践

- **上下文管理**：只保留相关文件在上下文中，保持文件尽可能精简和专注
- **代理选择**：为任务使用适当的代理
- **迭代开发**：在小的、专注的任务中工作
- **文件组织**：保持干净的项目结构
- **定期提交**：经常保存您的工作

## 技术偏好系统

BMad通过位于`.bmad-core/data/`中的`technical-preferences.md`文件包含个性化系统——这可以帮助PM和架构师推荐您对设计模式、技术选择或您想放在这里的任何其他内容的偏好。

### 与Web包一起使用

创建自定义Web包或上传到AI平台时，包含您的`technical-preferences.md`内容，确保代理从一开始就具有您的偏好。

## 核心配置

`bmad-core/core-config.yaml`文件是一个关键配置，使BMad能够与不同的项目结构无缝工作，将来会有更多选项可用。目前最重要的是yaml中的devLoadAlwaysFiles列表部分。

### 开发者上下文文件

定义开发代理应该始终加载哪些文件：

```yaml
devLoadAlwaysFiles:
  - docs/architecture/coding-standards.md
  - docs/architecture/tech-stack.md
  - docs/architecture/project-structure.md
```

您需要通过对架构进行分片来验证这些文档是否存在，它们尽可能精简，并包含您希望开发代理始终加载到其上下文中的确切信息。这些是代理将遵循的规则。

随着您的项目增长和代码开始建立一致的模式，编码标准应该减少到只包含代理仍然犯的标准。代理将查看文件中的周围代码以推断与当前任务相关的编码标准。

## 获取帮助

- **Discord社区**：[加入Discord](https://discord.gg/gk8jAdXWmj)
- **GitHub问题**：[报告错误](https://github.com/bmadcode/bmad-method/issues)
- **文档**：[浏览文档](https://github.com/bmadcode/bmad-method/docs)
- **YouTube**：[BMadCode频道](https://www.youtube.com/@BMadCode)

## 结论

记住：BMad旨在增强您的开发过程，而不是替代您的专业知识。将其作为强大工具来加速您的项目，同时保持对设计决策和实施细节的控制。