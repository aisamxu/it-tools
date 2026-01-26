# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 项目概述

IT-Tools 是一个面向开发者的在线工具集合，使用 Vue 3 + TypeScript + Vite 构建。项目采用 pnpm 作为包管理器。

## 常用命令

```bash
# 安装依赖
pnpm install

# 开发模式
pnpm dev

# 构建生产版本
pnpm build

# 类型检查
pnpm typecheck

# 代码检查
pnpm lint

# 单元测试
pnpm test

# 运行单个测试文件
pnpm test src/tools/chmod-calculator/chmod-calculator.service.test.ts

# E2E 测试
pnpm test:e2e

# 创建新工具
pnpm run script:create:tool my-tool-name
```

## 代码架构

### 工具系统 (核心)

每个工具位于 `src/tools/<tool-name>/` 目录下，包含：
- `index.ts` - 使用 `defineTool()` 定义工具元数据（名称、路径、描述、图标、关键词）
- `<tool-name>.vue` - 工具的 Vue 组件
- `<tool-name>.service.ts` - 业务逻辑（可选）
- `<tool-name>.service.test.ts` - 单元测试
- `<tool-name>.e2e.spec.ts` - E2E 测试

工具注册流程：
1. 在 `src/tools/index.ts` 中导入工具
2. 将工具添加到 `toolsByCategory` 数组中对应的分类

### UI 组件库

自定义组件位于 `src/ui/` 目录，采用 `c-` 前缀命名（如 `c-button`、`c-input-text`、`c-card`）。组件通过 `unplugin-vue-components` 自动注册，无需手动导入。

### 国际化

- 全局翻译文件：`locales/*.yml`
- 工具可拥有独立翻译：`src/tools/<tool-name>/locales/`
- 使用 vue-i18n，通过 `translate()` 函数获取翻译

### 路径别名

`@` 别名指向 `src/` 目录，例如 `@/plugins/i18n.plugin`。

### 自动导入

通过 `unplugin-auto-import` 配置，以下 API 无需手动导入：
- Vue: `ref`, `computed`, `watch` 等
- Vue Router: `useRouter`, `useRoute`
- VueUse: `useDark`, `useClipboard` 等
- vue-i18n: `useI18n`
- naive-ui: `useDialog`, `useMessage` 等

## 工具分类

工具按以下分类组织：Crypto、Converter、Web、Images and videos、Development、Network、Math、Measurement、Text、Data
