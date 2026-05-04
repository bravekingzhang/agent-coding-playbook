# Agent Coding Playbook

AI Coding Agent 越来越强。

但真正的问题不是它不会写代码。

真正的问题是：

- 它容易猜需求；
- 它容易扩大修改范围；
- 它容易过度设计；
- 它容易改无关代码；
- 它容易在没有验证的情况下宣布完成。

这个项目想做一件事：

> 把工程师脑子里的工程判断，沉淀成 Agent 能执行的规则、Skill、检查清单和工作流。

这里不是 Prompt 收藏夹。

这里是 AI Coding 的工程实践手册。

---

## 一句话定位

**让 AI 不只是会写代码，而是按一个靠谱工程师的方式写代码。**

英文定位：

> Turn engineering judgment into instructions that coding agents can follow.

---

## 为什么需要这个项目？

很多人第一次使用 AI Coding Agent 时，都会经历一个很爽的阶段。

你说一句：

> 帮我把这个 bug 修一下。

Agent 开始读代码、改文件、生成 diff、写总结。

看起来很聪明。

但时间久了，你会发现几个非常真实的问题：

1. 它会在需求不清楚时自己补全假设；
2. 它会为了一个小 bug 顺手重构一片代码；
3. 它会写出看起来“很工程化”，但实际过度设计的实现；
4. 它会把无关文件一起格式化；
5. 它会说“已完成”，但没有跑测试、没有跑 typecheck、也没有证明真的完成。

所以 AI Coding 的核心不是让模型多写代码。

更重要的是：

> 怎么让 Agent 不乱写代码。

---

## 这个仓库包含什么？

```text
agent-coding-playbook/
├── README.md
├── CLAUDE.md
├── AGENTS.md
├── LICENSE
├── docs/
│   ├── ai-coding-maturity-model.md
│   ├── context-engineering.md
│   ├── mcp-tooling-guidelines.md
│   ├── mcp-vs-skill.md
│   └── vibe-coding-risk-level.md
├── skills/
│   ├── acp-bug-fix/SKILL.md
│   ├── acp-code-review/SKILL.md
│   ├── acp-refactor/SKILL.md
│   ├── acp-release-check/SKILL.md
│   └── acp-test-first/SKILL.md
├── checklists/
│   ├── before-coding.md
│   ├── before-commit.md
│   ├── high-risk-change.md
│   └── pr-review.md
├── examples/
│   ├── bad-prompts.md
│   └── good-prompts.md
└── templates/
    ├── agents-basic.md
    ├── claude-basic.md
    └── skill-template.md
```

当前版本聚焦六类资产：

- `CLAUDE.md`：给 Claude Code 使用的项目级行为规则；
- `AGENTS.md`：给 Codex、Cursor、其他 coding agents 使用的通用规则；
- `skills/`：面向具体任务的 Agent 工作流；
- `checklists/`：给人类和 Agent 共用的检查清单；
- `docs/`：AI Coding 工程化方法说明；
- `examples/`：好坏任务描述示例。

---

## 核心原则

### 1. Think Before Coding

写代码之前，先想清楚。

Agent 需要先说明：

- 它理解的需求是什么；
- 哪些文件或模块可能相关；
- 它做了哪些假设；
- 哪些地方存在歧义或风险。

如果需求不清楚，就不要假装清楚。

---

### 2. Simplicity First

优先选择最简单、最直接、最小可行的实现。

不要为了一个小问题引入：

- 新框架；
- 新抽象；
- 新配置层；
- 新通用工具；
- 未来可能用得上的扩展点。

能用 50 行解决的问题，不要写成 200 行。

---

### 3. Surgical Changes Only

像外科手术一样改代码。

只改必须改的地方。

每一行 diff 都应该能回答这个问题：

> 这一行为什么和当前需求有关？

如果回答不上来，就不应该改。

---

### 4. Goal-Driven Execution

不要只告诉 Agent “做什么”。

要告诉它：

> 做到什么才算完成。

好的完成标准包括：

- 测试通过；
- typecheck 通过；
- lint 通过；
- build 成功；
- bug 复现用例不再失败；
- 公共 API 行为没有意外变化。

没有验证，不要宣布完成。

---

### 5. Context Discipline

上下文不是越多越好。

Agent 不应该把整个仓库、所有文档、所有历史信息都塞进一次会话。

更好的做法是：

- 常驻规则保持简短；
- 任务型知识用 Skill 按需加载；
- 源码文件按需读取；
- 大任务拆成多个小 session；
- 会话变脏时及时 handoff。

---

### 6. Human Review Awareness

Agent 的总结不是事实。

真正的事实是 diff、测试结果和运行结果。

对于高风险改动，必须人工 Review。

高风险范围包括：

- 登录；
- 权限；
- 支付；
- 数据迁移；
- 安全；
- 隐私；
- 线上发布；
- 公共 API；
- 大规模重构。

---

## 推荐使用方式

### 方式一：作为 Claude Code 插件安装（推荐）

这个仓库本身是一个 Claude Code 插件 + marketplace。安装后，Skill 会按需自动触发，并附带 `/acp-init` 一键初始化项目规则。

在 Claude Code 里执行**两步**：

```bash
# 1. 把本仓库注册为 marketplace（marketplace 名字叫 acp）
/plugin marketplace add bravekingzhang/agent-coding-playbook

# 2. 从 acp marketplace 安装 agent-coding-playbook 插件
/plugin install agent-coding-playbook@acp
```

> 注意：Claude Code 没有 `/plugin install user/repo` 这种一步式语法。必须先 `marketplace add`，再 `install <plugin>@<marketplace>`。

本地开发或离线安装：

```bash
git clone https://github.com/bravekingzhang/agent-coding-playbook.git ~/agent-coding-playbook
# 在 Claude Code 中
/plugin marketplace add ~/agent-coding-playbook
/plugin install agent-coding-playbook@acp
```

安装后可用：

- Skills（自动按需触发，全部带 `acp-` 命名空间避免冲突）：`acp-bug-fix`, `acp-code-review`, `acp-refactor`, `acp-release-check`, `acp-test-first`, `acp-feature-add`, `acp-investigate`, `acp-plan-task`
- Slash command：`/acp-init` —— 在当前项目根写入 `CLAUDE.md` 模板并尝试自动检测构建/测试命令

---

### 方式二：直接复制模板

### 方式二：直接复制模板

把 `CLAUDE.md` 或 `AGENTS.md` 复制到你的项目根目录。

然后根据你的项目特点补充：

- 技术栈；
- 构建命令；
- 测试命令；
- 代码风格；
- 高风险模块；
- 发布要求。

---

### 方式三：按任务加载 Skill

如果你正在修 bug，可以使用：

```text
skills/acp-bug-fix/SKILL.md
```

如果你正在做 Code Review，可以使用：

```text
skills/acp-code-review/SKILL.md
```

如果你正在发布版本，可以使用：

```text
skills/acp-release-check/SKILL.md
```

如果你希望先写测试再实现，可以使用：

```text
skills/acp-test-first/SKILL.md
```

---

### 方式四：把检查清单放进团队流程

例如 PR Review 时，可以使用：

```text
checklists/pr-review.md
```

发布前，可以使用：

```text
checklists/high-risk-change.md
```

---

## 适合谁？

这个项目适合：

- 正在使用 Claude Code / Codex / Cursor / Cline / Devin 等工具的开发者；
- 希望在团队内推广 AI Coding 的技术负责人；
- 想把团队工程经验沉淀为规则和 Skill 的架构师；
- 不满足于“AI 帮我写代码”，而是希望构建 AI Coding 工程体系的人。

---

## 这个项目不是什么？

它不是：

- Prompt 大全；
- 神奇咒语集合；
- 模型排行榜；
- 工具推荐列表；
- 让你完全不用看代码的自动驾驶系统。

它更像一本工作手册：

> 教你把工程经验写成 Agent 能遵守的规则。

---

## 一句话记住

> Prompt 是临场发挥，Playbook 才是团队资产。

或者更直接一点：

> 不要训练 AI 会写代码，要训练 AI 按工程规矩写代码。

---

## Current Status

The initial version includes:

- [x] Base `CLAUDE.md` rules
- [x] Base `AGENTS.md` rules
- [x] Bug fix skill
- [x] Code review skill
- [x] Refactor skill
- [x] Release check skill
- [x] Test-first skill
- [x] Feature-add skill
- [x] Investigate skill
- [x] Plan-task skill
- [x] Claude Code plugin manifest (`.claude-plugin/plugin.json`)
- [x] `/acp-init` slash command
- [x] Before-coding checklist
- [x] Before-commit checklist
- [x] PR review checklist
- [x] High-risk change checklist
- [x] Context engineering guide
- [x] MCP vs Skill guide
- [x] MCP tooling guidelines
- [x] Vibe coding risk model
- [x] AI Coding maturity model
- [x] Good and bad prompt examples
- [x] Basic templates for `CLAUDE.md`, `AGENTS.md`, and Skills

---

## Roadmap

Next planned improvements:

- [ ] Add real-world diff review examples
- [ ] Add PR template for AI-generated changes
- [ ] Add issue templates for bug fix, refactor, and release tasks
- [ ] Add enterprise adoption guide
- [ ] Add language-specific playbooks for TypeScript, Python, Android, and frontend projects
- [ ] Add MCP server design examples
- [ ] Add CI workflow examples for agent-friendly verification
- [ ] Add metrics guide for measuring AI coding effectiveness
- [ ] Add contribution guidelines

---

## License

MIT
