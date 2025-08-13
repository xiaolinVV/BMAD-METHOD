# BMAD 多根工作区全栈开发最佳实践

## 概述

本文档适用于使用 BMAD 方法进行多根工作区全栈开发的场景，特别是包含一个后端项目和多个前端项目的遗留系统维护和迭代开发。

## 适用场景

- 多根工作区项目（一个后端 + N 个前端）
- 需要频繁进行跨前后端的全栈开发
- 遗留系统的渐进式重构和维护
- 团队需要同时处理多个相关的前端项目

## 项目结构设计

### 推荐的工作区结构

```
workspace/
├── .bmad-core/                    # 工作区级 BMAD 配置
│   ├── core-config.yaml          # 核心配置文件
│   └── data/
│       ├── technical-preferences.md  # 技术偏好配置
│       └── bmad-kb.md            # 知识库
├── backend/                       # 后端项目
│   ├── .bmad-core/
│   │   └── core-config.yaml       # 后端特定配置
│   ├── docs/
│   │   ├── prd.md                # 后端 PRD
│   │   ├── architecture.md        # 后端架构文档
│   │   └── architecture/          # 后端架构细分文档
│   │       ├── api-specs.md       # API 规范
│   │       ├── database-schema.md # 数据库结构
│   │       ├── endpoints.md       # 端点文档
│   │       └── business-logic.md  # 业务逻辑
│   └── ...                        # 后端源代码
├── frontend-app1/                 # 前端项目1
│   ├── .bmad-core/
│   │   └── core-config.yaml       # 前端特定配置
│   ├── docs/
│   │   ├── prd.md                # 前端 PRD
│   │   ├── architecture.md        # 前端架构文档
│   │   └── architecture/          # 前端架构细分文档
│   │       ├── api-integration.md # API 集成文档
│   │       ├── component-standards.md # 组件标准
│   │       └── state-management.md # 状态管理
│   └── ...                        # 前端源代码
├── frontend-app2/                 # 前端项目2
│   └── ...                        # 类似结构
└── shared/                        # 共享资源
    └── docs/
        ├── api-standards.md       # API 标准
        ├── data-flow.md          # 数据流图
        ├── error-handling.md     # 错误处理规范
        └── coding-standards.md   # 编码标准
```

## 核心配置

### 1. 工作区级配置 (workspace/.bmad-core/core-config.yaml)

```yaml
# 工作区级核心配置
markdownExploder: true
prd:
  prdFile: docs/prd.md
  prdVersion: v4
  prdSharded: true
  prdShardedLocation: docs/prd
  epicFilePattern: epic-{n}*.md
architecture:
  architectureFile: docs/architecture.md
  architectureVersion: v4
  architectureSharded: true
  architectureShardedLocation: docs/architecture
customTechnicalDocuments: null

# 关键配置：跨项目文档自动加载
devLoadAlwaysFiles:
  # 后端项目文档（前端开发时自动加载）
  - ../backend/docs/architecture/api-specs.md
  - ../backend/docs/architecture/endpoints.md
  - ../backend/docs/architecture/database-schema.md
  - ../backend/docs/architecture/business-logic.md
  
  # 前端项目文档（后端开发时自动加载）
  - ../frontend-app1/docs/architecture/api-integration.md
  - ../frontend-app1/docs/architecture/component-standards.md
  - ../frontend-app1/docs/architecture/state-management.md
  - ../frontend-app2/docs/architecture/api-integration.md
  - ../frontend-app2/docs/architecture/component-standards.md
  
  # 共享标准文档
  - ../shared/docs/api-standards.md
  - ../shared/docs/data-flow.md
  - ../shared/docs/error-handling.md
  - ../shared/docs/coding-standards.md
  
  # 当前项目的架构文档
  - docs/architecture/coding-standards.md
  - docs/architecture/tech-stack.md
  - docs/architecture/source-tree.md

devDebugLog: .ai/debug-log.md
devStoryLocation: docs/stories
slashPrefix: BMad
```

### 2. 技术偏好配置 (workspace/.bmad-core/data/technical-preferences.md)

```markdown
# 用户-定义的偏好模式和配置

## 项目级技术偏好

### 架构模式
- 后端：微服务架构，RESTful API 设计
- 前端：组件化开发，状态管理使用 Redux/Vuex
- 数据库：关系型数据库 + 缓存层

### 技术栈偏好
- 后端语言：Node.js / Java / Python (根据实际情况选择)
- 前端框架：React / Vue (根据实际情况选择)
- 数据库：MySQL / PostgreSQL (根据实际情况选择)
- 缓存：Redis

### 代码规范
- 命名约定：驼峰命名法
- 注释规范：JSDoc / Python Docstring
- 错误处理：统一的错误码和错误信息格式
- 日志规范：结构化日志，包含请求追踪 ID

### API 设计规范
- RESTful API 设计
- 统一的响应格式
- API 版本控制
- 认证和授权机制

### 数据库设计规范
- 表名命名规范
- 字段命名规范
- 索引设计原则
- 数据迁移策略

### 测试策略
- 单元测试覆盖率要求
- 集成测试策略
- 端到端测试策略
- 性能测试要求

## 前端项目特定偏好

### 组件设计
- 组件命名规范
- Props 设计原则
- 状态管理策略
- 样式解决方案

### API 集成
- HTTP 客户端选择
- 请求拦截器配置
- 错误处理策略
- 缓存策略

## 后端项目特定偏好

### 代码结构
- 分层架构
- 依赖注入
- 中间件使用
- 异常处理

### 数据库操作
- ORM 使用
- 事务管理
- 查询优化
- 连接池配置

## 跨项目集成偏好

### 数据一致性
- 数据格式标准化
- 验证规则统一
- 错误处理一致
- 日志格式统一

### 部署和运维
- 容器化策略
- CI/CD 流程
- 监控和告警
- 配置管理
```

## 工作流程

### 1. 项目初始化阶段

#### 1.1 安装 BMAD 方法

```bash
# 在工作区根目录执行
npx bmad-method install
```

#### 1.2 创建工作区级配置

```bash
# 创建工作区级配置目录
mkdir -p .bmad-core/data
mkdir -p shared/docs

# 复制配置模板
cp backend/.bmad-core/core-config.yaml .bmad-core/
# 然后按照上面的示例修改工作区级配置
```

#### 1.3 生成项目文档

```bash
# 在每个子项目中执行
cd backend
npx bmad-method flatten

cd ../frontend-app1
npx bmad-method flatten

cd ../frontend-app2
npx bmad-method flatten
```

#### 1.4 使用 Web UI 进行系统分析

```bash
# 上传 flattened 文件到 Web UI
# 使用以下命令分析系统架构
@architect
*document-project

# 创建系统维护策略
@pm
*create-brownfield-prd
```

### 2. 日常开发流程

#### 2.1 创建跨端 Story

```bash
# 根据需求大小选择合适的命令

# 小修小补（单个功能点）
@pm
*create-brownfield-story

# 中等功能（1-3 个相关功能）
@pm
*create-brownfield-epic

# 大型功能（多个 epics）
@pm
*create-brownfield-prd
```

#### 2.2 Story 创建最佳实践

```markdown
---
# Story 标题：跨端功能变更示例

## 影响范围
- 后端：用户服务 API
- 前端：用户信息组件
- 数据库：用户表新增字段

## 前端变更
- 修改用户信息展示组件
- 新增手机号验证功能
- 更新表单验证逻辑

## 后端变更
- 新增手机号验证 API
- 更新用户信息接口
- 添加数据库字段

## 数据一致性检查
- API 响应格式验证
- 数据类型匹配检查
- 错误处理一致性

## 依赖关系
- 前端依赖后端 API 更新
- 后端依赖数据库 schema 变更
- 需要协调发布顺序
---
```

#### 2.3 开发实现

```bash
# 开发代理会自动加载所有相关文档
@dev
*develop-story

# 开发代理会自动：
# 1. 读取 story 的跨端需求
# 2. 加载 devLoadAlwaysFiles 中的所有相关文档
# 3. 验证前后端依赖关系
# 4. 检查 API 接口匹配
# 5. 确保数据一致性
# 6. 提供跨端修改建议
```

#### 2.4 质量保证

```bash
# 代码审查
@qa
review-story

# 运行测试
@dev
run-tests

# 验证所有功能
@dev
execute-checklist story-dod-checklist
```

### 3. 定期维护流程

#### 3.1 技术债务管理

```bash
# 每季度进行一次技术债务评估
@architect
*document-project

# 创建技术债务偿还计划
@pm
*create-brownfield-prd
```

#### 3.2 文档同步

```bash
# 定期更新架构文档
@architect
*create-brownfield-architecture

# 更新 API 文档
@architect
*document-project
```

## 常见场景处理

### 场景1：修改前端功能需要验证后端接口

**问题**：前端组件需要调用新的后端 API，需要确保接口存在且数据格式匹配。

**解决方案**：
1. 创建跨端 story，明确标注前后端变更
2. 开发代理会自动加载后端 API 文档进行验证
3. 如果后端接口不存在，会提示需要先创建后端接口
4. 确保数据类型和格式完全匹配

**示例 Story**：
```markdown
---
## 前端变更
- 修改用户信息组件，新增手机号字段显示
- 添加手机号验证逻辑
- 更新表单提交逻辑

## 后端变更
- 新增 GET /api/user/phone 接口
- 更新 PUT /api/user/profile 接口支持手机号
- 添加手机号验证逻辑

## 验证要点
- API 接口存在性检查
- 数据类型匹配验证
- 错误处理一致性检查
---
```

### 场景2：修改后端接口需要更新前端调用

**问题**：后端 API 接口变更，需要更新所有相关的前端调用。

**解决方案**：
1. 创建跨端 story，明确标注 API 变更影响范围
2. 开发代理会自动查找所有依赖该 API 的前端代码
3. 提供前端代码修改建议
4. 确保所有前端项目都得到更新

**示例 Story**：
```markdown
---
## 后端变更
- 修改用户信息 API 响应格式
- 新增字段：lastLoginTime
- 修改字段：userName → fullName

## 前端影响范围
- frontend-app1: 用户信息组件
- frontend-app2: 用户详情页面
- frontend-app1: 用户列表组件

## 前端变更
- 更新所有相关组件的数据结构
- 修改表单字段映射
- 更新类型定义
---
```

### 场景3：数据库 Schema 变更

**问题**：数据库表结构变更，需要同步更新后端 API 和前端组件。

**解决方案**：
1. 创建跨端 story，包含完整的变更链
2. 使用数据库迁移脚本
3. 确保后端 API 适配新的数据结构
4. 更新前端组件以处理新的数据格式

**示例 Story**：
```markdown
---
## 数据库变更
- 用户表新增字段：phoneNumber
- 创建数据库迁移脚本
- 更新数据验证规则

## 后端变更
- 更新用户模型
- 修改用户信息 API
- 添加手机号验证逻辑

## 前端变更
- 更新用户信息表单
- 添加手机号输入框
- 更新表单验证逻辑
---
```

### 场景4：废弃功能清理

**问题**：识别和清理不再使用的功能，确保安全移除。

**解决方案**：
1. 使用 `@architect *document-project` 分析系统
2. 识别废弃功能和代码
3. 创建专门的清理 story
4. 逐步移除，确保不影响核心业务

**示例 Story**：
```markdown
---
## 废弃功能识别
- 旧的用户导入功能（已停用6个月）
- 旧的通知系统（已被新系统替代）
- 未使用的 API 接口

## 清理计划
- 移除前端相关组件
- 删除后端 API 接口
- 清理数据库表
- 更新文档

## 风险控制
- 使用功能开关确保安全移除
- 保留数据库备份
- 分批次逐步清理
---
```

## 配置优化技巧

### 1. 动态配置管理

可以根据当前活跃项目动态调整配置：

```yaml
# 在 technical-preferences.md 中定义
active_projects:
  backend: true
  frontend-app1: true
  frontend-app2: false  # 暂时不活跃的项目

# 然后在 core-config.yaml 中使用条件加载
devLoadAlwaysFiles:
  - ../backend/docs/architecture/api-specs.md
  - ../frontend-app1/docs/architecture/api-integration.md
  # 只有在活跃时才加载
  # - ../frontend-app2/docs/architecture/api-integration.md
```

### 2. 智能依赖检测

启用自动依赖检测功能：

```yaml
# 在 core-config.yaml 中添加
crossProjectValidation:
  enabled: true
  autoDetectDependencies: true
  validateApiContracts: true
  checkDataConsistency: true
  reportBreakingChanges: true
```

### 3. 性能优化

对于大型项目，可以优化文档加载：

```yaml
# 使用分片文档减少加载时间
devLoadAlwaysFiles:
  # 只加载核心文档
  - ../backend/docs/architecture/api-summary.md
  - ../shared/docs/api-standards.md
  
  # 需要时再加载详细文档
  # ../backend/docs/architecture/api-specs.md
```

## 故障排除

### 常见问题1：开发代理无法找到跨项目文档

**症状**：开发代理提示无法加载相关项目文档。

**解决方案**：
1. 检查文件路径是否正确
2. 确认相对路径的基准目录
3. 验证文档文件是否存在

```bash
# 检查路径配置
cat .bmad-core/core-config.yaml | grep devLoadAlwaysFiles

# 验证文件存在
ls -la ../backend/docs/architecture/
```

### 常见问题2：API 接口验证失败

**症状**：开发代理报告 API 接口不匹配。

**解决方案**：
1. 更新 API 文档
2. 同步前后端接口定义
3. 检查数据类型一致性

```bash
# 更新 API 文档
@architect
*document-project

# 重新验证
@dev
*develop-story
```

### 常见问题3：性能问题

**症状**：开发代理加载文档缓慢。

**解决方案**：
1. 减少 `devLoadAlwaysFiles` 中的文件数量
2. 使用文档分片
3. 只加载必要的文档

```yaml
# 优化配置
devLoadAlwaysFiles:
  # 核心文档
  - ../shared/docs/api-standards.md
  - ../backend/docs/architecture/api-summary.md
  
  # 移除不常用的文档
  # - ../backend/docs/architecture/database-schema.md
```

## 最佳实践总结

### 1. 配置管理
- 使用工作区级配置统一管理跨项目依赖
- 定期更新 `devLoadAlwaysFiles` 以反映项目变化
- 保持文档的准确性和时效性

### 2. 开发流程
- 始终创建跨端 story 来管理全栈变更
- 利用开发代理的自动验证能力
- 保持前后端变更的同步性

### 3. 质量保证
- 定期进行技术债务评估
- 保持文档和代码的同步
- 使用自动化测试确保跨端一致性

### 4. 团队协作
- 建立统一的跨项目开发规范
- 定期同步各项目的开发进度
- 使用统一的 API 设计和数据格式

### 5. 性能优化
- 合理配置文档加载策略
- 使用文档分片提高性能
- 定期清理不必要的文档引用

## 实施建议

1. **从小开始**：先选择一个小的前端项目试点
2. **逐步推广**：验证流程后再推广到其他项目
3. **持续优化**：根据实际使用情况调整配置
4. **团队培训**：确保团队成员理解跨端开发流程
5. **文档维护**：定期更新文档以保持准确性

通过遵循这些最佳实践，您可以有效地使用 BMAD 方法进行多根工作区的全栈开发，提高开发效率并确保代码质量。