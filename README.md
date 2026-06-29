# vibe-opportunity-hunter

> 一个 Claude Code skill，帮 vibe coder 在真实社区噪音里挖出**可在 1-2 周内做完 MVP** 的市场机会。

## 它解决什么

普通的"找 idea"会落入三个陷阱：

1. **AI 拼贴**——让模型凭训练数据想 idea，输出的都是过时的、抽象的"AI for X"
2. **听 KOL**——跟 KOL 喊的红利方向往往已经过窗口期，没有可验证的原始信号
3. **臆想需求**——自己觉得有需求，但没有用户在公开场合真的表达过

这个 skill 强制走"田野调研"路线：去用户在的地方（Reddit、HN、Product Hunt、IndieHackers、即刻、小红书、V2EX、App Store 差评、GitHub Issues），听他们用自己的话说出痛点，给每个机会附**真实可点击的 URL 引用** + 25 ★ 评分 + 1-2 周 MVP 路径 + 48 小时验证方案。

## 评测结果（iteration 1）

3 个 eval × (with_skill vs no_skill baseline) 量化对比：

| Eval | with_skill | baseline | Δ |
|---|---|---|---|
| `generic-zh-no-constraints` | **12/12 (100%)** | 5/12 (42%) | **+58pp** |
| `domain-focused-en` (AI coding tools) | **9/11 (82%)** | 4/11 (36%) | +46pp |
| `domain-focused-zh-lifestyle` | **10/13 (77%)** | 6/13 (46%) | +31pp |
| **平均** | **86.2%** | 41.4% | **+44.8pp** |

主要差距来自：信号源覆盖广度、引用真实性、25★ 评分结构、48h 验证方案、反模式回避。详见 [`evals/evals.json`](evals/evals.json)。

## 安装

```bash
git clone https://github.com/xionggq0205-sys/vibe-opportunity-hunter.git ~/.claude/skills/opportunity-hunter
```

或者下载 `SKILL.md` 放到 `~/.claude/skills/opportunity-hunter/SKILL.md`。

## 触发方式

在 Claude Code 里随意提及任何"找方向"意图，skill 会自动触发：

- "我想做个 side project 但不知道做啥"
- "最近有什么红利方向？"
- "帮我找个能赚钱的小工具"
- "what should I build next?"
- "最近大家在抱怨什么？"

也可以直接说 `/opportunity-hunter` 强制调用。

## 用法

skill 跑完后会给你一份结构化机会清单，每个机会含：

- **痛点描述** + 2-3 条用户原话（带 URL）
- **目标用户画像**
- **信号强度评分**（25 ★，5 维度：频次/新鲜度/强度/用户清晰度/替代方案空白）
- **MVP 范围建议**（具体技术栈 + 时间估计）
- **48 小时验证方案**（怎么用最快路径证伪/证实需求）

最后给你一个排序表 + 主动跟进钩子（问你要不要深挖某个方向）。

## 已知限制

- 小红书等反爬严格的平台，公开搜索引擎收录差，skill 可能拿到的是二手转载——遇到这种情况会**显式标注引用层级**，并建议你贴 5-10 条原帖 URL 重做一轮。
- 跨语言扫描默认开启，但中文 prompt 默认偏中文源、英文 prompt 默认偏英文源，可以在 prompt 里指定混合。
- 评分维度倾向"可证伪 + 1-2 周可落地"，所以会过滤掉 ML 训练、监管资质、强网络效应这类方向——这些是 vibe coder 的禁区。

## 反馈

issue / PR 欢迎。如果发现 skill 给出的某个机会引用是假的或失效的，请开 issue 提供证据，我会修。

## License

MIT
