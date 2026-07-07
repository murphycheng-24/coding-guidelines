# Engineering Discipline — LLM 编码纪律指南

[![MIT License](https://img.shields.io/badge/license-MIT-blue)](LICENSE)
[![Rules](https://img.shields.io/badge/rules-10-brightgreen)](CLAUDE.md)
[![Tools](https://img.shields.io/badge/tools-Claude%20%7C%20Cursor%20%7C%20Codex%20%7C%20WorkBuddy-orange)](https://github.com/murphycheng-24/coding-guidelines)
[![GitHub stars](https://img.shields.io/github/stars/murphycheng-24/coding-guidelines?style=social)](https://github.com/murphycheng-24/coding-guidelines/stargazers)
[![Last Commit](https://img.shields.io/github/last-commit/murphycheng-24/coding-guidelines)](https://github.com/murphycheng-24/coding-guidelines/commits)

一个 `CLAUDE.md` 文件，包含 10 条工程纪律规则 — **基于 [Karpathy 4 条行为准则](https://x.com/karpathy)的增强版**。工具无关 — 适用于 **Claude Code**、**Codex**、**Cursor**、**WorkBuddy** 及任何 LLM 编码助手。

[English](./README.md) | 简体中文

## 为什么需要它

Karpathy 原版的 4 条规则（编码前思考、简洁优先、精准修改、目标驱动执行）是一个很好的起点。这个增强版将其扩展为 **10 条规则** — 新增了验证、调试、依赖管理、沟通和自我审计 — 不仅教模型如何写代码，还教它如何**自我验证**。

> *"这些不是建议。这些是规则。遵循它们，你产出的代码不需要重写。"*
> — Andrej Karpathy

## 10 条规则一览

| # | 规则 | 防止什么 |
|---|------|---------|
| 1 | **先读再写** | 与代码库格格不入的"外星"代码 |
| 2 | **编码前思考** | 默默假设、隐藏权衡 |
| 3 | **简洁** | 过度工程、过早抽象 |
| 4 | **精准修改** | 不必要的 diff 噪音、风格漂移 |
| 5 | **验证** | 看似能跑但实际有问题的代码 |
| 6 | **目标驱动执行** | 模糊任务、不清晰的成功标准 |
| 7 | **调试** | 瞎猜而非系统化排查 |
| 8 | **依赖** | 臃肿的包清单、不必要的依赖 |
| 9 | **沟通** | 不清晰的提交信息、未标记的隐患 |
| 10 | **常见失败模式** | 厨房水槽、错误抽象、失控重构等 |

## 四个阶段

```
┌─────────────────────────────────────────────┐
│  飞行前    →  浮出假设                       │
│             →  陈述计划                       │
│               (规则 2, 规则 6)               │
├─────────────────────────────────────────────┤
│  飞行中    →  规则 1-4 用于编写              │
│             →  规则 8 用于依赖               │
├─────────────────────────────────────────────┤
│  飞行后    →  规则 5 (验证)                  │
│             →  规则 7 (调试时)               │
│             →  规则 9 (沟通)                 │
├─────────────────────────────────────────────┤
│  自我审计  →  规则 10 失败模式               │
│             →  宣布完成前检查                 │
└─────────────────────────────────────────────┘
```

## Before & After 示例

### 示例 1：搜索功能（不遵守规则 vs 遵守规则）

**用户请求**：*"给用户列表加一个搜索功能"*

**不遵守规则的 LLM**：
- 创建一个新的 `SearchService` 类，3 层抽象
- 添加 `lodash`、`fuse.js`、`rxjs` 作为依赖
- 重构现有的 `UserList` 组件以使用新服务
- 改动 8 个文件，400+ 行 diff
- ✅ 搜索能用... 但 PR 审查是噩梦

**遵守规则的 LLM**：

| 规则 | 改变了什么 |
|------|-----------|
| **规则 2**（编码前思考） | LLM 陈述：*"我会在现有的 UserList 上加一个过滤函数。不需要新依赖。"* |
| **规则 3**（简洁） | 使用现有的 `useState` + `filter()` — 15 行，不是 400 行 |
| **规则 4**（精准修改） | 只改 `UserList.tsx` — 不顺手重构别的 |
| **规则 8**（依赖） | 零新增依赖 |
| **规则 5**（验证） | 在宣布完成前运行现有测试套件 |

**结果**：1 个文件改动，15 行新增，0 新依赖，干净的 PR。

### 示例 2：Bug 修复

**不遵守规则**：LLM 猜测修复，加 `try/catch` 压制报错，标记"已修复"。

**遵守规则**：
1. **规则 7**（调试）— 先复现错误：*"当 `user.profile` 为 null 时崩溃"*
2. **规则 5**（验证）— 写一个能复现 bug 的测试，然后修复让测试通过
3. **规则 4**（精准修改）— 只改空值检查，不重构整个函数
4. **规则 9**（沟通）— 提交信息：*"修复 user.profile 为 undefined 时的空指针"*

---

## 安装

### 方式 A：Claude Code 插件（推荐）

在 Claude Code 中，首先添加插件市场：

```
/plugin marketplace add murphycheng-24/coding-guidelines
```

然后安装插件：

```
/plugin install engineering-discipline@coding-guidelines
```

这会将指南安装为 Claude Code 插件，使其在你所有项目中可用。

### 方式 B：CLAUDE.md（按项目）

新项目：
```bash
curl -o CLAUDE.md https://raw.githubusercontent.com/murphycheng-24/coding-guidelines/main/CLAUDE.md
```

已有项目（追加）：
```bash
echo "" >> CLAUDE.md
curl https://raw.githubusercontent.com/murphycheng-24/coding-guidelines/main/CLAUDE.md >> CLAUDE.md
```

### 方式 C：Cursor

将 [`.cursor/rules/engineering-discipline.mdc`](.cursor/rules/engineering-discipline.mdc) 复制到你项目的 `.cursor/rules/` 目录。详见 **[CURSOR.md](CURSOR.md)**。

## 在其他工具中使用

这些规则是**工具无关的**：

| 工具 | 使用方式 |
|------|---------|
| **Claude Code** | 将 `CLAUDE.md` 放在项目根目录 |
| **Cursor** | 使用 `.cursor/rules/engineering-discipline.mdc` |
| **Codex (OpenAI)** | 包含在系统提示或项目级指令中 |
| **WorkBuddy** | 技能自动将规则加载到上下文 |

这些规则之所以有效，是因为它们约束的是**通用的 LLM 失败模式** — 默默假设、过度工程、风格漂移、范围蔓延 — 这些都不是特定工具的问题。

## 如何判断它在起作用

如果你看到以下情况，说明这些指南正在发挥作用：

- **diff 中不必要的改动更少** — 只有请求的改动出现
- **因过度复杂而导致的重写更少** — 代码第一次就写得简洁
- **澄清问题在实现之前提出** — 而不是在犯错之后
- **bug 修复通过重现测试验证** — 而非心存侥幸
- **干净、精简的 PR** — 没有顺带的重构或"改进"
- **具体的提交信息** — "修复用户查找中的空指针" 而非 "修复 bug"

## 定制

这些指南设计用于与项目特定指令合并。将它们添加到你现有的 `CLAUDE.md` 或创建一个新的。

对于项目特定规则，添加如下章节：

```markdown
## 项目特定指南

- 使用 TypeScript 严格模式
- 所有 API 端点必须有测试
- 遵循 `src/utils/errors.ts` 中现有的错误处理模式
```

## 仓库结构

```
.
├── .claude-plugin/
│   └── plugin.json                     # Claude Code 插件配置
├── .cursor/
│   └── rules/
│       └── engineering-discipline.mdc  # Cursor IDE 规则
├── skills/
│   └── engineering-discipline/
│       └── SKILL.md                    # 可复用技能定义
├── CLAUDE.md                           # 核心指南（10 条规则）
├── CURSOR.md                           # Cursor 使用指南
├── CONTRIBUTING.md                     # 贡献指南
├── CHANGELOG.md                        # 版本变更记录
├── README.md                           # 英文 README
├── README.zh.md                        # 本文件（中文 README）
├── LICENSE                             # MIT 许可证
└── .gitignore
```

## 权衡说明

这些指南倾向于**谨慎而非速度**。对于琐碎的任务（简单的拼写错误修复、显而易见的一行修改），请自行判断 — 并非每个改动都需要完整的严谨流程。

目标是减少非琐碎工作中代价高昂的错误，而不是拖慢简单任务。

## 许可

MIT © [murphycheng-24](https://github.com/murphycheng-24)
