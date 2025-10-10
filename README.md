# Code Workflow Assistant Plugin

一个增强开发体验的 Claude Code 插件，提供自定义命令和代理来优化代码工作流程。

## 📋 概述

此插件为 Claude Code 提供了两个主要功能：
- **API 文档自动生成** (`/apidoc`) - 智能解析接口代码并生成规范的 Markdown API 文档
- **智能提交消息** (`/commit`) - 基于代码变更生成标准化的 git 提交消息

## 🚀 安装

1. 确保已安装 Claude Code
2. 将插件目录放置在您的 Claude Code 插件目录中
3. 重启 Claude Code 以加载插件

## 📖 功能特性

### API 文档生成 (`/apidoc`)

自动解析接口代码并生成标准化的 Markdown API 文档。

**使用方法:**
```
/apidoc [code-path ...]（支持 @file 引用多个文件）
```

**功能特点:**
- 智能识别接口模块和分组
- 自动分析请求参数和响应结构
- 生成规范的 Markdown 格式文档
- 支持公开和鉴权接口分类
- 统一的响应格式和错误处理

**输出示例:**
```markdown
# 产品名称 模块名称 API 文档

# 一、概述

本API文档描述了产品名称产品后台服务提供的模块名称接口...

# 二、API 接口

## 1. 公开API（无需鉴权）

### 1.1 接口名称

- **API:** `GET /api/v1/module/public/endpoint`
- **描述:** 接口功能描述
- **鉴权:** 否
```

### 智能提交消息 (`/commit`)

基于代码变更自动生成标准化的 git 提交消息。

**使用方法:**
```
/commit [code-path ...]（支持 @file 引用多个文件）
```

**功能特点:**
- 遵循 Conventional Commits 规范
- 支持多种变更类型（feat, fix, docs, style 等）
- 自动识别变更范围和影响
- 使用表情符号增强可读性
- 支持多类型变更的组合提交

**支持的类型:**
- ✨ `feat` - 新功能
- 🐛 `fix` - 错误修复
- 📝 `docs` - 文档更新
- 💄 `style` - 代码格式化
- ♻️ `refactor` - 代码重构
- ⚡️ `perf` - 性能优化
- ✅ `test` - 测试相关
- 📦 `build` - 构建系统
- 👷 `ci` - CI 配置
- 🔧 `chore` - 其他变更
- 🌐 `i18n` - 国际化

**输出示例:**
```
✨ feat(auth): add user login functionality

- implement JWT token authentication
- add user login endpoint with email/password validation
- include token refresh mechanism
```

## 📁 项目结构

```
codeplugins/
├── .claude-plugin/
│   └── plugin.json          # 插件配置文件
├── agents/                  # 自定义代理目录（预留）
├── commands/                # 自定义命令目录
│   ├── apidoc.md           # API 文档生成命令
│   └── commit.md           # 智能提交消息命令
└── hooks/                  # 自定义钩子目录（预留）
```

## ⚙️ 配置

插件配置位于 `.claude-plugin/plugin.json`：

```json
{
  "name": "code-workflow-assistant",
  "description": "代码工作流助手插件，提供自定义命令和代理来增强开发体验",
  "version": "1.0.0",
  "author": {
    "name": "Developer",
    "email": "dev@example.com"
  },
  "license": "MIT",
  "keywords": ["claude-code", "plugin", "workflow", "development"],
  "engines": {
    "claude-code": ">=1.0.0"
  }
}
```

## 🛠️ 开发

### 添加新命令

1. 在 `commands/` 目录下创建新的 Markdown 文件
2. 按照 Claude Code 命令格式编写命令定义
3. 重启 Claude Code 以加载新命令

### 添加新代理

1. 在 `agents/` 目录下添加代理配置文件
2. 实现代理逻辑和接口
3. 在插件配置中注册新代理

### 添加钩子

1. 在 `hooks/` 目录下创建钩子脚本
2. 配置钩子触发条件和处理逻辑
3. 测试钩子功能

## 📄 许可证

本项目采用 MIT 许可证 - 查看 [LICENSE](LICENSE) 文件了解详情。

## 🤝 贡献

欢迎提交 Issues 和 Pull Requests 来改进此插件！

## 📞 支持

如有问题或建议，请通过以下方式联系：
- 提交 GitHub Issue
- 发送邮件至 dev@example.com

---

**Made with ❤️ for developers**