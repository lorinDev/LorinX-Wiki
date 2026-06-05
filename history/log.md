# Wiki Log

> 所有 wiki 操作的时序记录。只追加, 不修改。
> 格式: `## [YYYY-MM-DD] action | subject`
> Actions: ingest, update, query, lint, create, archive, delete
> 超过 500 条时轮转: 重命名为 log-YYYY.md, 新建 log.md

## [2026-06-03] create | Wiki initialized
- Domain: 中国历史与世界历史知识库
- 创建目录结构: SCHEMA.md, index.md, log.md
- 子目录: raw/{articles,papers,transcripts,assets}, entities, concepts, comparisons, queries, timelines, _archive
- Tag 体系: 中国断代(8) + 世界断代(5) + 地区(8) + 主题(8) + 人物类型(8) + 事件类型(8) + 元信息(4) = 49 tags
- 准备就绪, 待摄入首批来源

## [2026-06-03] ingest × 14 | 先秦专题全面填充
创建 14 个页面覆盖先秦时期:

**实体页 (8)**:
- xia-dynasty — 夏朝（二里头文化关联，真实性争议）
- shang-dynasty — 商朝（甲骨文、青铜器、殷墟）
- zhou-dynasty — 周朝（封建制、天命观、宗法制，西周→东周转折）
- spring-autumn-period — 春秋时期（五霸、成文法萌芽、孔子时代）
- warring-states-period — 战国时期（七雄、变法、长平之战、走向统一）
- confucius — 孔子（仁、礼、有教无类，儒家创始）
- laozi — 老子（道、无为、辩证思维，道家创始）
- sun-tzu — 孙子（《孙子兵法》十三篇，兵家鼻祖）

**概念页 (4)**:
- mandate-of-heaven — 天命观（以德配天、中西对比）
- zhou-feudal-system — 周代封建制（与欧洲 Feudalism 对比、瓦解过程）
- bronze-age-china — 中国青铜文明（礼器文化、技术成就、世界比较）
- hundred-schools-of-thought — 诸子百家（九流十家、四家核心思想对比）

**时间线 (1)**:
- pre-qin-timeline — 先秦大事年表（新石器时代至秦统一，含文化里程碑）

**元数据 (1)**:
- 更新 index.md 含完整先秦目录

## [2026-06-03] ingest × 8 | 春秋各国实体页 + 对比
创建 8 个新页面:

**诸侯国实体页 (7)**:
- state-qi — 齐国（姜太公封国 · 管仲改革 · 春秋首霸 · 稷下学宫 · 田氏代齐）
- state-jin — 晋国（姬姓 · 晋文公城濮之战 · 六卿制度 · 三家分晋标志春秋之终）
- state-chu — 楚国（亦夷亦夏 · 楚庄王问鼎中原 · 楚辞 · 疆域最广 · 吴起变法失败）
- state-qin — 秦国（西陲崛起 · 秦穆公霸西戎 · 商鞅变法最彻底 → 统一天下）
- state-lu — 鲁国（周公封国 · 周礼正宗 · 孔子故里 · 三桓专政 · 弱小而文化影响深远）
- state-wu — 吴国（阖闾用孙武/伍子胥 · 柏举之战破楚 · 夫差争霸 · 被越所灭）
- state-yue — 越国（勾践卧薪尝胆 · 文种灭吴九术 · 春秋最后霸主 · 昙花一现）

**对比页 (1)**:
- spring-autumn-states — 春秋各国综合对比（五霸 · 七国 · 改革深度 · 兴亡模式 · 历史规律）

更新 index.md 含完整索引目录

## [2026-06-03] ingest × 4 | 战国四公子
创建 4 个人物实体页:

- lord-mengchang — 孟尝君田文（齐 · 门客三千 · 鸡鸣狗盗 · 狡兔三窟 · 绝嗣无后）
- lord-xinling — 信陵君魏无忌（魏 · 窃符救赵 · 四公子最贤 · 五国合纵败秦 · 被猜忌抑郁而终）
- lord-pingyuan — 平原君赵胜（赵 · 毛遂自荐 · 长平之战争议 · 散家财守邯郸 · 善终）
- lord-chunshen — 春申君黄歇（楚 · 唯一非王族 · 扶立楚王 · 开发江东→上海"申" · 被李园斩首灭族）

更新 index.md 和图谱

## [2026-06-03] ingest × 3 | 韩赵魏三国
- state-han — 韩国（七雄最弱 · 劲弩产地 · 申不害术治 · 郑国渠 · 前230首灭）
- state-zhao — 赵国（胡服骑射 · 长平之战40万 · 廉颇蔺相如 · 李牧 · 前228灭）
更新 index.md 和图谱

## [2026-06-03] ingest × 14 | 春秋战国全面补完
**燕国 (1)**: state-yan — 荆轲刺秦 · 乐毅伐齐 · 黄金台 · 前222灭亡
**思想家 (4)**: mozi(兼爱非攻·科学) · mencius(性善论·仁政·民贵君轻) · zhuangzi(逍遥游·齐物论) · han-fei(法术势集大成·死于李斯)
**改革/军事家 (5)**: guan-zhong(盐铁专营·尊王攘夷) · shang-yang(徙木立信·作法自毙) · wu-qi(魏武卒·楚变法) · sun-bin(围魏救赵·减灶杀庞涓) · bai-qi(长平坑杀45万·人屠)
**文人 (1)**: qu-yuan(离骚·端午·香草美人)
**帝王 (1)**: qin-shi-huang(统一六国·郡县制·焚书坑儒)
**战役 (1)**: battle-of-changping(赵括纸上谈兵·白起坑杀45万)
**概念 (1)**: vertical-horizontal-alliance(合纵连横·苏秦张仪)

先秦专题总计 47 页

## [2026-06-03] ingest × 3 | 收尾：制度+战役
- commandery-county-system — 郡县制（vs封建制·春秋萌芽→秦确立·百代皆行秦政法）
- well-field-system — 井田制（井字九宫·公田私田·春秋瓦解·商鞅彻底废除）
- battle-of-maling — 马陵之战（减灶诱敌·庞涓死此树下·魏国衰落转折）

---

## [2026-06-03] ingest × 1 | 世界史开张
- goguryeo — 高句丽（朱蒙建国 · 好太王 · 丸都山城 · 隋炀帝三征惨败 · 唐太宗亲征未克 · 壁画世界遗产 · 中韩归属争议 · 705年）

世界史→东亚断代开张，跨出中国史
