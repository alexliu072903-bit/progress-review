# Progress Review · 进展评测

**[English](README.md) | 中文**

一个仅在 AirJelly 内运行的 skill：只使用当前用户的 AirJelly profile、memory 与已记录事件，把一段时间内可被 Context 支持的工作整理成两份对照视图——一条时间线、一条项目线，每条都标上「负责等级」与「结果状态」。

它只有一个硬要求：**数据源是封闭的**——不得用 workspace、Git、网页、外部文档、其他 MCP 或当前对话补证。同一份 AirJelly Context snapshot、同一评测对象与同一时间窗口，应得到相同的分类与输出结构。

## 它做什么

给定一个人的 AirJelly Context，产出两份对照视图（自包含 HTML）：

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

## 数据来源

唯一允许的数据来源是 AirJelly 已保存的 profile、memory、event，以及当前 session 注入的 `airjelly_context`。

事件可以来自飞书、ChatGPT、Claude、Chrome 等原始应用，但必须已经进入 AirJelly memory；Skill 不会重新访问这些应用补证。AirJelly Context 不足时只标记缺口，不读取本地仓库、GitHub、网页或用户临时提供的材料。当前环境无法访问 AirJelly Context 时，Skill 不生成评测。

## 安装

把 `progress-review/` 文件夹放进 AirJelly 的 skills 目录：

- AirJelly：`~/Library/Application Support/AirJelly/skills/progress-review/`

## 使用

```text
帮我做一份进展评测，窗口是过去 3 个月。
```

## 最小输入

评测对象、时间窗口、输出用途和公开边界。成果事实全部从 AirJelly Context 读取；缺失时标记证据缺口，不要求用户补材料，也不回退到其他来源。

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
| 1.1.0 | 2026-10-04 | 改为 AirJelly-only：封闭数据源、禁止外部补证、Context 不可用时 fail closed。 |
| 1.0.0 | 2026-10-04 | 首个版本：封闭双轴词表、两条线输出、固定模板、QA。 |
