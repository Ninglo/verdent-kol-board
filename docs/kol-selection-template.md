# Verdent KOL Selection Template / Verdent KOL 筛选模板

> 适用场景：按国家 / 语言 / campaign brief 筛选 KOL，并输出给团队讨论的网页名单。核心原则是：**先用结构填满正选，再用同类型替补兜底；宁缺毋滥，不用大号掩盖受众不匹配。**

## 1. 先确定投放结构

每次先把名额拆成可执行的 slot，而不是先看谁粉丝大。

示例：德国 6 月每周 10 个：

| Slot | 占比 | 数量 | 说明 |
|---|---:|---:|---|
| 前端 / 设计 / Ship pretty | 20% | 2 | 可以短视频为主，重点看视觉、工具发现、非工程师可理解 |
| AI Coding YouTube / Builder | 30% | 3 | 长视频，重点看 Claude Code / agent / build app / SaaS / product builder |
| AI Coding 短视频 / Builder | 30% | 3 | 短视频，重点看近期热度、语言、代码/工具演示 |
| 先锋新闻 / AI trend | 20% | 2 | 长短可以都有，但如果短视频没有好候选，标注暂不投 |

> 如果某个 slot 找不到合格候选，保留“暂不投/待讨论”空位，不要强行用不相关大号补齐。

## 2. 候选分层

输出名单必须分三层：

1. **Primary / 正选**：默认先联系，用来填满名额。
2. **Backup / 替补**：无档期、不合作、报价过高时，按同 slot 替换。
3. **Rejected / 已剔除**：保留重要误选样本和剔除原因，避免后续又按粉丝量误选。

## 3. 短视频筛选规则

短视频不能只看粉丝量。建议按以下优先级：

1. **语言必须匹配**：德国项目优先德语标题 / 德语口播 / 德国受众；明显俄语、西语、英语泛内容要谨慎。
2. **最近表现优先**：看最近 3–6 条，而不是历史均播或单个爆款。
3. **播放 / 粉丝比**：小号如果最近每条 2K–5K 且粉丝只有 2K–10K，可能比 300K 粉但近期低播更值得试。
4. **内容相似度**：必须接近 builder / AI coding / tool workflow / frontend design，不要用 IT 安全、泛生活、教育鸡汤、AI 饮食等偏离账号。
5. **宁缺毋滥**：新闻短视频或某类短视频找不到好人，就写“暂不投”，再和团队讨论是否改成长视频或重新搜索。

## 4. 长视频筛选规则

长视频更看重内容深度和受众质量：

- 近期是否发过 Claude Code / Codex / AI Agent / build app / vibe coding / SaaS / automation。
- 频道简介是否明确覆盖 founder、product builder、developer、PM、SMB owner。
- 单条视频是否有真实观看，而不是只靠历史订阅。
- 是否适合 brief 里的叙事：Build faster / earn sooner / ship pretty / AI cofounder。

## 5. 多语言标题处理

为了避免误判语言和内容方向，每个视频建议保留：

```json
{
  "title": "原始标题",
  "title_en": "English translation for quick review",
  "views": 12345,
  "when": "2026-05-26",
  "duration": "62s",
  "thumb": "...",
  "url": "..."
}
```

要求：

- 原标题必须保留，不能只放翻译。
- 英文翻译服务于快速判断内容，不要求文学化，准确即可。
- 如果出现俄语 / 西里尔文字 / 非目标语言，要在推荐理由或剔除原因里明确指出。

## 6. 每个 KOL 的推荐字段

推荐网页或 JSON 至少包含：

```json
{
  "name": "KOL name",
  "handle": "@handle",
  "platform": "YouTube | TikTok | Instagram | Shorts",
  "region": "DE",
  "followers": 10000,
  "avg_views": 5000,
  "campaign": "AI Coding / TikTok Builder",
  "status": "primary | backup | rejected",
  "slot_role": "正选 | 替补 | 剔除 | 空位",
  "contact_status": "待确认档期 | 暂不联系",
  "why": "推荐或剔除原因，必须包含语言、近期表现、受众匹配判断",
  "videos": []
}
```

## 7. 推荐理由写法

推荐理由不要泛泛说“粉丝多、AI 相关”，要包含三件事：

1. **语言 / 地区**：例如“德语/德国”。
2. **近期内容证据**：例如“最近两条 25K/21K”。
3. **受众匹配**：例如“Cursor/Claude/AI agent 工具，适合 builder 工具切片”。

示例：

> 德语；近期 Cursor/Claude/AI 成本与 agent 工具内容，单条 Cursor 8K，适合 builder 工具切片。

剔除理由也要明确：

> 剔除：近期内容明显俄语/西里尔文字，不符合德语 KOL 预期。

## 8. 网页交付模板

页面保持信息清晰，不要花哨：

- 顶部：项目名、比例、数据源、noindex 说明。
- Summary：正选总数、长视频数、短视频数、暂不投空位数。
- 正选列表：按 slot 顺序展示。
- 替补列表：按同 slot 兜底顺序展示。
- 已剔除列表：展示误选原因。
- 支持搜索：名称、handle、原标题、英文翻译、推荐理由。

## 9. 部署与隐私

如果部署到 GitHub Pages：

- 加 `robots.txt`：

```txt
User-agent: *
Disallow: /
```

- HTML 加：

```html
<meta name="robots" content="noindex,nofollow,noarchive,noimageindex">
<meta name="googlebot" content="noindex,nofollow,noarchive,noimageindex">
```

注意：GitHub Pages 仍是公开 URL，robots 只能减少搜索引擎收录，不能作为访问控制。

## 10. 可复用 Prompt

```text
请基于以下 campaign brief、国家/语言、候选 KOL 数据，输出一个 Verdent KOL 推荐网页数据集。

要求：
1. 先按我给的比例拆 slot，不要先按粉丝量排序。
2. 输出 Primary / Backup / Rejected 三层。
3. 短视频重点看目标语言、最近 3–6 条播放、内容与 builder/AI coding/frontend/news 的匹配度。
4. 长视频重点看内容深度、builder 受众、近期是否出现 Claude Code/Codex/AI Agent/build app/SaaS 等主题。
5. 所有非中文标题保留原标题，并补充 title_en 英文翻译。
6. 若某个 slot 没有足够好的人，输出一个“暂不投/待讨论”空位，不要强行补人。
7. 推荐理由必须包含：语言/地区、近期内容证据、受众匹配原因。
8. 剔除重要误选样本，并写清剔除原因。
9. 最终数据字段包括：name, handle, platform, avatar, followers, avg_views, campaign, status, slot_role, contact_status, why, videos。
```

## 11. Existing-contact dedupe workflow / 已联系 KOL 查重流程

本项目固定使用以下飞书多维表格作为“已联系 / 执行中 / 已发布”查重来源：

- Base: `https://cybercreate.feishu.cn/base/Tjvzb84ayacQEJsNxWgcLcxBndh?table=tblvyU3GKeS2TP2z&view=vewAukWAAu`
- Base token: `Tjvzb84ayacQEJsNxWgcLcxBndh`
- Table: `tblvyU3GKeS2TP2z` / `执行总表`
- Key fields:
  - `博主名称`
  - `Agency`
  - `执行状态`
  - `国家/地区`
  - `语言`

### 11.1 标准步骤

1. 先完成 KOL 筛选，得到我们“看得上”的 `primary` 名单。
2. 读取 `执行总表` 的字段结构，确认字段名没有变化。
3. 导出 `博主名称 / Agency / 执行状态 / 国家/地区 / 语言`。
4. 用 KOL 的 handle / profile URL 里的 `@handle` 与 `博主名称` 做归一化精确匹配。
5. 不使用宽松模糊匹配，避免误判，例如 `julia` 不等于 `Julian Ivanov`。
6. 输出两段文本：
   - `未命中：可给 Agency 新联系`
   - `已命中：交给已有 Agency 跟进`
7. 暂不投空位单独列出，不发给 Agency。

### 11.2 归一化匹配规则

- 全部转小写。
- 去掉开头 `@`。
- 从 YouTube / TikTok URL 中提取 `@handle`。
- 去掉非字母数字字符。
- 只做精确匹配，不做短子串匹配。

### 11.3 Agency handoff 文本模板

```markdown
## 未在执行总表命中：可整理给 Agency 新联系
- KOL Name — https://platform.com/@handle

## 已在执行总表命中：优先交给已有 Agency 跟进
- KOL Name — https://platform.com/@handle
  - Agency: AgencyName×N
  - 状态: 发布×N / 沟通中×N / 创作中×N
  - 命中记录数: N

## 暂不投 / 待讨论空位
- Slot Name — 暂不投原因
```

### 11.4 Reusable prompt add-on

```text
筛选完成后，请先用固定的飞书多维表格执行总表查重：
https://cybercreate.feishu.cn/base/Tjvzb84ayacQEJsNxWgcLcxBndh?table=tblvyU3GKeS2TP2z&view=vewAukWAAu

查重字段使用：博主名称、Agency、执行状态、国家/地区、语言。
匹配时用 KOL handle / profile URL @handle 与「博主名称」归一化精确匹配，不要做宽松模糊匹配。
输出两部分：
1. 未联系过：给 Agency 新联系，只包含名称和主页链接。
2. 已联系过：列名称、主页链接、命中的 Agency 和执行状态，交给已有 Agency 跟进。
暂不投空位单独列出。
```
