# Engineering Workflow and Code Review Skill

一个面向 Codex 的工程化工作流 skill，适用于代码审查、功能开发、重构、迁移和验证。

## 它解决的问题

- 只看 README 或说明文件，不追踪真实调用链
- 只改局部文件，不检查上下游影响
- 复杂任务不查资料，直接凭经验实现
- 把逻辑堆进单文件或大函数
- 测试通过后就把功能说成完整成功

## 核心流程

1. 判断当前任务属于代码审查还是代码实现
2. 根据模式读取项目结构、调用链和相关模块
3. 新技术、复杂算法、架构设计或方案不明确时，检索 GitHub、论文和官方文档
4. 修改前先输出分析、模块边界、计划和验证标准
5. 等待用户明确审阅通过后再修改代码
6. 按职责拆分模块，按 checkpoint 逐步实现
7. 区分静态检查、测试、运行时验证、数据检查和闭环证据
8. 只对已经获得的证据做结论

## 文件结构

```text
engineering-code-review/
├── SKILL.md
├── agents/openai.yaml
└── references/
    ├── implementation-mode.md
    └── review-mode.md
```

## 使用

将整个目录放入个人 skill 目录，或放入项目的 `.agents/skills/`：

```text
<project>/.agents/skills/engineering-code-review/
```

然后在任务中使用：

```text
使用 engineering-code-review 审查这个功能，先分析调用链和模块边界，暂时不要修改代码。
```

## 适用场景

代码审查、科研工程、机器人项目、算法实现、包结构迁移、复杂功能开发和分阶段验证。
