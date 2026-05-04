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
├── docs/
│   ├── context-engineering.md
│   ├── mcp-vs-skill.md
│   └── vibe-coding-risk-level.md
├── skills/
│   ├── bug-fix/SKILL.md
│   ├── code-review/SKILL.md
│   ├── refactor/SKILL.md
│   └── release-check/SKILL.md
├── checklists/
│   ├── before-coding.md
│   ├── before-commit.md
│   ├── high-risk-change.md
│   └── pr-review.md
└── templates/
    ├── claude-basic.md
    ├── agents-basic.md
    └── skill-template.md
```

第一版先聚焦四类资产：

- `CLAUDE.md`：给 Claude Code 使用的项目级行为规则；
- `AGENTS.md`：给 Codex、Cursor、其他 coding agents 使用的通用规则；
- `skills/`：面向具体任务的 Agent 工作流；
- `checklists/`：给人类和 Agent 共用的检查清单。

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

### 方式一：直接复制模板

把 `CLAUDE.md` 或 `AGENTS.md` 复制到你的项目根目录。

然后根据你的项目特点补充：

- 技术栈；
- 构建命令；
- 测试命令；
- 代码风格；
- 高风险模块；
- 发布要求。

---

### 方式二：按任务加载 Skill

如果你正在修 bug，可以使用：

```text
skills/bug-fix/SKILL.md
```

如果你正在做 Code Review，可以使用：

```text
skills/code-review/SKILL.md
```

如果你正在发布版本，可以使用：

```text
skills/release-check/SKILL.md
```

---

### 方式三：把检查清单放进团队流程

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

## Roadmap

- [ ] 完善基础 `CLAUDE.md` 和 `AGENTS.md` 模板
- [ ] 增加更多任务型 Skills
- [ ] 增加真实 diff review 案例
- [ ] 增加企业级 AI Coding 风险分级
- [ ] 增加 MCP 工具接入规范
- [ ] 增加 AI Coding 成熟度模型
- [ ] 增加中文公众号文章版本

---

## License

MIT
