# Wiki Schema

## Domain
中国历史与世界历史知识库 — 覆盖从古代文明到近现代的政治、军事、经济、文化、科技发展。
中西方历史并重，注重比较视角和跨文明联系。

## Conventions
- 文件名: 英文小写 + 连字符 (e.g., `qin-dynasty.md`, `world-war-ii.md`)
- 每页以 YAML frontmatter 开头
- 页面间用 `[[wikilinks]]` 链接 (每页至少 2 个出链)
- 更新页面时务必更新 `updated` 日期
- 每篇新页面必须添加到 `index.md` 对应分类下
- 每次操作必须追加到 `log.md`
- **溯源标记:** 综合 3+ 来源的页面, 在段落末尾添加 `^[raw/articles/xxx.md]`
- 语言: 页面内容用中文撰写, 人名/地名首次出现时括号标注英文

## Frontmatter
```yaml
---
title: 页面标题
created: YYYY-MM-DD
updated: YYYY-MM-DD
type: entity | concept | comparison | query | timeline | summary
tags: [from taxonomy below]
era: 具体年代范围 (e.g., "221-206 BCE", "14th century")
sources: [raw/articles/source-name.md]
confidence: high | medium | low
contested: true
contradictions: [other-page-slug]
---
```

## raw/ Frontmatter
```yaml
---
source_url: https://...
ingested: YYYY-MM-DD
sha256: <hex digest of body content below frontmatter>
---
```

## Tag Taxonomy
添加新 tag 前必须先更新此列表。

### 中国历史断代 (Chinese Periods)
- `pre-qin` — 先秦 (夏商周、春秋战国)
- `qin-han` — 秦汉
- `wei-jin` — 魏晋南北朝
- `sui-tang` — 隋唐
- `song-yuan` — 宋元
- `ming-qing` — 明清
- `republican-era` — 民国
- `prc-era` — 中华人民共和国

### 世界历史断代 (World Periods)
- `ancient` — 古代 (至 476 CE)
- `medieval` — 中世纪 (476-1492)
- `early-modern` — 近代早期 (1492-1789)
- `modern` — 近代 (1789-1945)
- `contemporary` — 现当代 (1945-至今)

### 地区 (Regions)
- `east-asia` — 东亚
- `southeast-asia` — 东南亚
- `south-asia` — 南亚
- `middle-east` — 中东
- `europe` — 欧洲
- `africa` — 非洲
- `americas` — 美洲
- `eurasia` — 欧亚大陆

### 主题领域 (Themes)
- `political` — 政治制度、政权更迭
- `military` — 军事、战争
- `economic` — 经济、贸易、丝绸之路
- `cultural` — 文化、思想、宗教
- `sci-tech` — 科技、发明
- `social` — 社会结构、人口
- `diplomacy` — 外交、国际关系
- `law` — 法律、制度

### 人物类型 (Figure Types)
- `emperor` — 帝王/君主
- `general` — 将领
- `statesman` — 政治家/改革家
- `philosopher` — 思想家/哲学家
- `scientist` — 科学家/发明家
- `artist` — 文学家/艺术家
- `explorer` — 探险家/航海家
- `revolutionary` — 革命者

### 事件类型 (Event Types)
- `war` — 战争/战役
- `revolution` — 革命/起义
- `reform` — 改革/变法
- `treaty` — 条约/协定
- `discovery` — 发现/发明
- `migration` — 人口迁徙
- `epidemic` — 瘟疫/疾病
- `disaster` — 自然灾害

### 元信息 (Meta)
- `comparison` — 对比分析 (中西对比、断代对比)
- `timeline` — 时间线
- `controversy` — 历史争议
- `historiography` — 史学史

## Page Thresholds
- **创建新页面** 当某实体/概念出现在 2+ 来源中 或 是一篇来源的核心
- **更新已有页面** 当新来源提到已覆盖的内容
- **不创建页面** 对一笔带过的提及或领域外内容
- **拆分页面** 当页面超过 ~200 行 — 拆为子主题
- **归档页面** 当内容已被完全取代 — 移至 `_archive/`

## Entity Pages
人物、朝代、国家、城市、战役、典籍的页面。包含:
- 概述 / 是什么
- 关键信息 (年代、地理位置、规模)
- 与其他实体的关系 ([[wikilinks]])
- 来源引用

## Concept Pages
制度、思想、运动、趋势的页面。包含:
- 定义 / 核心内容
- 发展脉络
- 中西方比较视角
- 历史影响与评价
- 相关概念 ([[wikilinks]])

## Comparison Pages
跨文明/跨时代的对比分析。包含:
- 比较对象和目的
- 对比维度 (表格优先)
- 结论或综合分析
- 来源

## Timeline Pages
特定主题/地区的时间线。格式:
```markdown
| 年份 | 事件 | 地区 | 备注 |
|------|------|------|------|
```

## Update Policy
当新信息与已有内容冲突时:
1. 检查日期 — 新来源通常优先
2. 如确有矛盾, 同时标注两方观点及日期来源
3. 在 frontmatter 标记 `contradictions: [page-name]`
4. Lint 报告中标出, 等待人工审核
