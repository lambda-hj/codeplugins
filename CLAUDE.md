# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 项目概述

这是一个 Claude Code 插件项目，提供自定义命令和代理来增强开发体验。插件名称为 `pilot`，主要通过两个命令优化代码工作流程：
- `/commit` - 智能生成标准化的 git 提交消息
- `/apidoc` - 自动解析接口代码并生成规范的 Markdown API 文档

## 项目结构

```
codeplugins/
├── .claude-plugin/
│   ├── plugin.json          # 插件配置文件（必须保持与 marketplace.json 中的一致）
│   └── marketplace.json     # 本地 Marketplace 定义
├── agents/                  # 自定义代理目录
│   ├── prompt-engineer.md   # 提示工程专家代理
│   └── review-code.md       # 代码质量 pragmatist 代理
├── commands/                # 自定义命令目录
│   ├── commit.md           # 智能提交消息命令
│   └── apidoc.md           # API 文档生成命令
└── hooks/                  # 自定义钩子目录（当前为空）
```

## 核心功能

### 智能提交消息 (/commit)

- **功能**: 基于代码变更生成遵循 Conventional Commits 规范的提交消息
- **支持类型**: feat, fix, docs, style, refactor, perf, test, build, ci, chore, i18n
- **格式**: 使用表情符号增强可读性，中文说明，英文主题
- **使用**: `/commit [file-path ...]` （支持 @file 引用多个文件）

### API 文档生成 (/apidoc)

- **功能**: 智能解析接口代码并生成标准化的 Markdown API 文档
- **输出格式**: 统一的 RESTful API 文档格式，包含公开和鉴权接口分类
- **目标文件**: `docs/api.md`
- **使用**: `/apidoc [api-path ...]` （支持多个 API 路径）

## 代理系统

### prompt-engineer
- **专长**: 高级提示工程技术和 LLM 优化
- **应用**: 构建 AI 功能、改进代理性能、制作系统提示
- **特点**: 掌握思维链、宪法 AI、生产提示策略

### code-quality-pragmatist
- **专长**: 识别过度工程化和不必要的复杂性
- **应用**: 代码审查、架构决策、确保代码简洁实用
- **重点**: 简单性优于理论最佳实践

## MCP 服务器配置

项目配置了多个 MCP 服务器，但在本地设置中已禁用：
- context7 - 文档检索
- chrome-devtools - 浏览器自动化
- sequential-thinking - 顺序推理
- mobile - 移动端支持
- filesystem - 文件系统访问
- fetch - 网络请求

## 插件管理

### 安装
插件通过本地 marketplace 方式安装，配置文件位于：
- `~/.claude/plugins/marketplaces/code-workflow-plugins/`

### 配置文件
- `plugin.json`: 插件元数据，必须与 marketplace.json 中的名称一致
- `marketplace.json`: Marketplace 定义，包含插件列表和源路径

### 常见问题
- **插件名称不一致**: 确保 plugin.json 和 marketplace.json 中的 name 字段相同
- **manifest 无效**: 避免使用不识别的字段（如 engines）
- **插件找不到**: 检查路径配置和 marketplace 设置

## 开发指南

### 添加新命令
1. 在 `commands/` 目录创建新的 Markdown 文件
2. 按照 Claude Code 命令格式编写定义
3. 在 `plugin.json` 中注册命令路径
4. 重启 Claude Code 加载新命令

### 添加新代理
1. 在 `agents/` 目录添加代理配置文件
2. 实现代理逻辑和接口
3. 在相关配置中注册代理（如需要）

### 命令格式规范
- 使用 YAML front matter 定义元数据
- `description`: 命令描述
- `argument-hint`: 参数提示（可选）
- 主体部分包含命令逻辑和指令

## 版本控制

- **Git 仓库**: `git@github.com:lambda-hj/codeplugins.git`
- **主分支**: `main`
- **提交规范**: 使用 Conventional Commits 格式
- **许可证**: MIT

## 故障排除

### 插件加载失败
1. 检查 `plugin.json` 语法正确性
2. 验证与 `marketplace.json` 中名称一致性
3. 确认文件路径配置正确
4. 重启 Claude Code

### 命令不可用
1. 确认命令文件存在于 `commands/` 目录
2. 检查 `plugin.json` 中是否正确注册
3. 验证命令文件格式符合规范

### MCP 服务器问题
1. 检查 `.mcp.json` 配置正确性
2. 查看本地设置中的服务器状态
3. 确认网络连接和依赖可用性