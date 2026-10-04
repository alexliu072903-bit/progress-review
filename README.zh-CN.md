# Progress Review · 进展评测

**[English](README.md) | 中文**

一个给 AI coding Agent（AirJelly、Claude Code、Codex 等）用的 skill：把一个人真实做过的事，整理成两份对照视图——一条时间线、一条项目线，每条都标上「负责等级」与「结果状态」。

它只有一个硬要求：**产出是确定的**——把这个 skill 发给任何同事，用任何 Agent 跑同一个人，结果都一样。

## 它做什么

给定一个人的 memory 或 context，产出两份对照视图（自包含 HTML）：

- **时间线**——按时间排序，看轨迹。
- **项目线**——按主题聚类，看权重。
- **四类显式清单**——做了 / 没做、有影响 / 无影响、闭环 / 未闭环。

每条内容标两个维度：

- **负责等级**——主导 / 负责 / 推动 / 影响 / 参与
- **结果状态**——已交付 / 已产生影响 / 在研发 / 待验证 / 未闭环 / 已停止-归档

标准是「**有效性叙事**」：让一个陌生读者快速看到你负责了什么、改变了什么、有没有可核验的证据。

## 结构

```text
SKILL.md                                     主流程：用途、命名边界、确定性、两条线、输出
references/taxonomy.md                       封闭词表：负责等级与结果状态，含 tie-breaker
references/evidence.md                       事实 / 判断 / 假设；什么算完成
references/qa.md                             出厂前一致性检查
assets/team-progress-review.template.html    固定输出模板
```

## 为什么产出是一致的

1. **封闭词表**——只能取枚举值，不得自创标签。
2. **可判定规则**——每个值有定义与 tie-breaker。
3. **证据强制**——每条带来源与日期；无证据不升级。
4. **固定排序**——时间线升序，项目线按确定度。
5. **固定模板**——Section、类名、图例一致。
6. **出厂 QA**——含跨次运行的一致性检查。

## 安装

把 `progress-review/` 文件夹放进你 Agent 的 skills 目录：

- AirJelly：`~/Library/Application Support/AirJelly/skills/progress-review/`
- Claude Code：`~/.claude/skills/progress-review/`
- Codex：`~/.codex/skills/progress-review/`

## 使用

```text
帮我做一份进展评测，窗口是过去 3 个月。
```

## 最小输入

一个人的 memory 或 context。缺失时，skill 会索取最小材料：一句事实简介、≥2 个产出、每个产出 1 个可核验链接；对外版本再加联系方式。

## 边界

- 明面不得称「绩效评估」「技术评估」。
- 不编造数据、日期、头衔。
- 「合并不等于发布，有数据不等于已验证」。
- 涉密或公司内部内容不发布。

## License

MIT

## History

| 版本 | 日期 | 变更 |
| --- | --- | --- |
| 1.0.0 | 2026-10-04 | 首个版本：封闭双轴词表、两条线输出、固定模板、QA。 |