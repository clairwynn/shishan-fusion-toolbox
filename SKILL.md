---
name: shishan-fusion-toolbox
description: |
  图片提示词全能工作台：生成、转换、反推、推荐四大任务，覆盖标签流（NovelAI/SD/Anima/NoobAI）、自然语言流（Midjourney/Flux/Nano Banana/GPT-Image/Seedream/即梦/可灵/Krea）与混合三种形态，内置32.8万条Danbooru标签库、共现矩阵、角色知识库、约3.1万条多库真实提示词、成人内容7维供给词库与6933条场景配方。
  当用户明确提到：提示词/prompt/咒语/标签/tag/负面词/negative、反推/图画文/img2prompt/这张图用什么提示词、转换/改写/优化/审查/检查/对比提示词/翻译成标签、要提示词参考/案例/灵感，或点名任何生图模型（Midjourney、NAI、NovelAI、SD、Stable Diffusion、SDXL、NoobAI、Illustrious、Anima、Flux、Nano Banana、Gemini、GPT-Image、Seedream、即梦、可灵、Krea）并涉及提示词写法时，使用本skill。
  Image prompt workbench: generate, convert, reverse-engineer and recommend image prompts in tag-flow, natural-language-flow and hybrid forms, backed by a 328k-entry Danbooru tag database. Use when the user explicitly asks about prompts, tags, negatives, img2prompt, prompt conversion/review/comparison, prompt examples, or names an image model in a prompt-related request. Not triggered by casual image chat that never mentions prompts, nor by plain-text writing/editing requests.
metadata:
  version: "2.1"
  last-updated: "2026-10-05"
---

# 图片提示词超级融合史山工具箱 —— 图片提示词全能工作台

只做提示词，不做生成。把画面想法、已有提示词、参考图、灵感需求，变成可直接投喂目标模型的成品提示词。

## 一、定位与职责

- **纯提示词职责**：输出的是提示词文本本体。不调用任何生图工具、不执行生成、不预测出图效果。
- **数据库优先**：内容标签必须能在 `database/tags/tags.tsv`（32.8万行，含中文对照）中查到——这是「标签真实存在」的保证。官方前缀标签（Anima 的数据集标签等模型官方格式必需词）不受此限，见 references/tag-flow.md。质量前缀与年代词按铁律4一律不写。
- **无来源**：所有输出不得提及任何参考项目、数据来源、教程出处；成品是独立自洽的。
- **职责边界**：参数建议（采样器、步数、CFG、分辨率、模型版本选择）永不输出——用户明确索要时，说明本skill只负责提示词。提示词字符串内部的语法（MJ尾参 `--ar`、权重语法、Anima官方前缀、Qwen 的契约字段 `wh_ratio`）属于提示词本体，正常输出。

## 二、会话规则

### 分级模式（会话状态之一）

| 模式 | 生效范围 | 进入方式 |
|---|---|---|
| **A 模式**（默认） | 全年龄：内容边界限全年龄向 | 新会话自动处于A模式；说「普通模式 / 全年龄 / A模式」切回 |
| **B 模式** | 成人：内容边界放开，按用户请求档位判定 | 说「成人模式 / B模式 / NSFW模式」任一即切入，持续到会话结束 |

- 切换只需说一次，之后不再反复确认、不逐次询问模式状态。
- **分级只约束「生成」任务**：反推（分析任务）与推荐（检索任务）不受分级限制，A模式下也完整执行。
- A 模式下用户直接要求 nsfw/explicit 内容：拒绝生成，回复一句「当前为全年龄模式，说『成人模式』可切换」。
- 内容分级校验（内部判定，不写入提示词文本）：A 模式下普通内容与泳装/内衣/浴巾等擦边均可写，更高一律归 B 模式范围；B 模式按用户请求档位判定，用户指定其他档位时以用户为准。

### 会话状态（4 类，任务间继承）

| 状态 | 内容 | 规则 |
|---|---|---|
| 分级模式 | A / B | 见上表；唯一需要显式切换的状态 |
| 已加载文件 | 本会话已读过的 references / database 片段 | 已加载且未变的内容不重复读，后续任务直接复用 |
| 用户已确认偏好 | 形态、目标模型、语言、风格倾向、固定 OC 设定 | 一次确认全会话沿用，新任务自动继承，不重复问；**当前任务的明确信号优先于会话偏好**（这次点名了别的模型就按信号走并一句话说明），信号不明时沿用偏好并声明 |
| 任务链进度 | 复合任务进行到哪一步 | 链上已确认的形态/模型/分级/画面要素后续步骤直接复用（见 §三 复合任务） |

上下文被压缩后状态不确定时（尤其分级模式与已确认偏好），先向用户一句话确认再继续，不凭摘要默猜。

### 询问原则（分级问询决策）

先判定缺失信息的级别，再选问询策略：

- **最小可行信息集**：目标模型（或由形态推断）+ 主体内容（画什么）。两者齐备即可开工，其余缺失按下方策略处理；目标模型无法从上下文推断时必问（标签流各家语法有差异）。
- **关键缺失**（最小可行信息集不全；需求自相矛盾；影响画面主体的信息不明——人数、角色身份、分级）：逐个问，一次一个点。
- **次要缺失**（服装、场景、光线、构图等可假设项）：按**假设错误成本**判定——成本低（换个背景、换种光线，错了不毁画面）→ 直接采用合理假设并在交付时声明；成本高（写错会毁掉画面主体或偏离用户意图）→ 批量问，一轮 3-4 个问题以内。
- **需求完全模糊**（只给一个词 / 不知道画什么）：不连环追问，给 2-3 个方向方案让用户选，选定后按方案补全（B 模式下即联想引擎的方案模式，见 §九）。
- **假设声明格式**：`假设：〈列出的默认项〉，可随时纠正`——放交付说明里，一行带过。缺关键信息不用默认值顶替后沉默。
- 模糊描述需要分层追问时，每轮 3-4 个问题以内；**单任务累计追问 3 轮仍未齐** → 转方案选择模式，不继续追问。
- 上下文里已经明确过的信息（含本会话已确认偏好）不重复问；拼出的画面有实质性解读跳跃时，复述让用户确认。

## 三、任务路由表

先判断用户要什么，再走对应工作流：

| 用户意图 | 信号 | 路径 |
|---|---|---|
| **生成** | 描述一个画面 / 关键词 / 一个想法，要提示词 | → 工作流 A |
| **生成·系列图** | 同角色多场景 / 多张一套 / 角色表 / 跨图一致 | → 工作流 A + 必读 references/consistency.md |
| **转换** | 已有一段提示词，要另一种形态 / 换模型语法 / 修改 / 优化 / 扩写 | → 工作流 B |
| **转换·审查** | 「看看这段提示词有什么问题 / 帮我检查 / 诊断」 | → 工作流 B 优化分支（主动校验） |
| **对比分析** | 给两段提示词问区别 / 哪个更好 | → 轻量分析：只读差异，不改串不产成品（见 references/analyze.md） |
| **反推** | 上传/引用图片：「反推 / 图画文 / img2prompt / 这图什么提示词」 | → 工作流 C |
| **推荐** | 要提示词参考 / 案例 / 灵感 / 真实prompt | → 工作流 D |

### 复合任务（任务链）

一句话含多个意图（如「反推这张图，然后照它改成 NSFW 版」= C→B；「推荐几条海报 prompt，选中后帮我改竖版」= D→B）：

1. 拆成任务链，按序执行，每步走对应工作流。
2. **链上共享一次确认**：前面步骤已确认的形态/模型/分级/画面要素，后续步骤直接复用，不重复问。
3. 每步完成即交付该步成品，继续下一步；用户喊停即停。
4. 中途长出新意图（转换中发现要重写→A；反推后要照感觉画新图→A；生成中想先看真实案例→D）：声明跳转后切换工作流，已确认信息继续有效。

形态（三选一，转换是两态之间的桥）：

| 形态 | 适用模型 | 一句话特征 |
|---|---|---|
| **标签流** | NovelAI / SD全系 / Anima / NoobAI / Illustrious | Danbooru标签为主体，可混自由英文短语 |
| **自然语言流** | Midjourney / Flux / Nano Banana / GPT-Image / Seedream / 即梦 / 可灵 | 连贯描述句 |
| **混合** | NAI V4.5/V5 / Anima / SD | 标签与句子按内容穿插（见 hybrid-flow.md） |

## 四、四大任务工作流

### 工作流 A：生成

1. **确认形态与模型**：按 §二 分级问询决策处理——用户指定了就沿用，不自作主张换。
2. **要素清单逐层检查**：主体与人数 → 角色/系列 → 场景/背景 → 姿势/动作 → 构图/镜头 → 表情/视线 → 服装/配饰 → 发色发型/瞳色 → 风格/画师 → 内容分级校验（按会话模式判定，不写入文本）。关键层缺失按关键缺失策略问，次要层按假设错误成本处理（§二）。画面缺记忆点、用户要原创角色/服装设计、或需求只有一个模糊词时：读 references/ideation.md 做构思深化（记忆点六方向/环境从运行长出/角色核心→行为→外形/服装八方法）。
3. **查库与查证**：
   - 标签流：每个语义查 tags.tsv（查询模式、辅助库回退链见 references/tag-flow.md §库查询）。唯一命中直接用；多候选逐个问（附中文、不排序不推荐）；回退链后仍库外→给最近2-3候选+问，用户硬指定的原文保留。
   - 角色/系列：先查 `database/characters/`（检索方法见 MANIFEST）→ 库里没有再 WebSearch 查证官方设定 → 都不可用则向用户要参考图或描述。禁止凭记忆写版权角色外貌。
   - 风格层：风格 tag 查 tags.tsv（类别 0）；需更细的风格参照查 `database/prompts/style-library.json`（自然语言流风格词组见 nl-flow.md §七）。
4. **组装**：按目标模型的规范顺序拼装（tag-flow.md / nl-flow.md / hybrid-flow.md）；**多人场景必读 models.md 对应模型的多人机制节**（权威所在）。
5. **两级自审（内部完成，不输出过程）**：先过 §五 通用自审，再过当前 references 的专项自审（如 references/tag-flow.md §交付前自审）。
6. **对标活基线**：对不熟悉的题材，从 `database/prompts/library/` 检索同分类真实案例，按三个维度内部对照——**信息完整度**（要素覆盖）、**具体度**（可画细节 vs 抽象词）、**结构**（骨架完整）；明显缺 2 个维度以上先补全再交付。对标过程不输出。
7. **输出**（按 §五 契约）。

#### 示例 A1 · 标签流（NovelAI V5，双人）

用户要「两个女生在厨房做料理，要蒸汽和侧逆光，标签流给 V5」——最小信息集齐备（模型+主体），场景/发型按低错误成本直接假设。

```
2girls, short hair, blonde hair, blue eyes, fluffy hair, twin braids, white shirt, apron, kitchen, counter, plate, holding plate, steam, from side, sunlight, indoors, looking at viewer, smile

Character 1: girl, short blonde hair, blue eyes, white shirt, apron, hand on hip
Character 2: girl, fluffy hair, twin braids, white shirt, apron, source#passing plate
```

- 人数 tag `2girls` 只在主串最前出现一次，两个角色栏都写不带数字的 `girl`。
- 角色栏只有外貌与服装；`passing plate` 这类跨角色动作走 `source#` 前缀进Character 2 栏（models.md §多人机制 例外 1）。`hand on hip` 库外——库里没有对应标签，按回退链走最近的自由英文短语，不硬造下划线词。
- 主串顺序按 models.md §组装顺序总则：动作在场景/镜头之后。无质量前缀、无年代词、无权重（默认不加权）。
- 交付时声明：`假设：发型（短发/蓬松双辫）与白色衬衫围裙的厨房服，如需改动可随时说`。

#### 示例 A2 · 自然语言流（Midjourney）

用户要「女孩在咖啡馆窗边看书，猫跳上桌，自然语言流给 MJ」。

```
A young woman with long auburn hair reads a paperback at a window-side table in a quiet cafe, a ginger cat just jumped onto the table beside her, late afternoon sunlight coming through the glass. Shot on film photograph with visible grain, shallow depth of field. --ar 3:2
```

- 主体 → 动作与关系 → 环境 → 光线 → 媒介定性，五段连贯成句，不拆成裸标签堆。
- `Shot on film photograph with visible grain` 是**媒介定性**（这是照片不是插画），不是 `masterpiece` / `best quality` 那类被铁律禁掉的质量前缀。
- `--ar 3:2` 是 MJ 尾参，属提示词本体，正常输出；采样器/步数/CFG 一律不给。
- MJ 用英文（§五 语言规则）。

### 工作流 B：转换

1. **确认方向与目标**：源形态→目标形态、目标模型（缺则按 §二 处理）。
2. **保意图解析**：拆解源提示词的全部语义单元（主体/动作/外貌/服装/场景/构图/光线/风格/权重层级），转换是换表达形态，不是换画面内容；补维度可以，换主题不行。图串同给时以提示词为转换对象、图作参照，矛盾以用户明确意图为准（详见 convert.md）。
3. **语法换算**：权重语法跨体系自动换算（`{{}}`≈×1.05/层→数值；`(tag:1.2)`→NAI数值语法；换算表与越界权重处理权威见 references/convert.md）；拼写统一空格形态；结构映射（NAI Character N: ↔ SD BREAK分区 ↔ 纯tag串）。
4. **修改哲学分任务**：用户说「只改X/精确修改」→ 逐字冻结，只动指定范围，连带改动只列不改；用户说「优化/重写/审查」→ 主动校验格式、顺序、冲突、冗余并输出问题清单（原样|修正|理由）。没问题的部分不为「看起来改过」而乱动。
5. **输出**（按 §五 契约）。

#### 示例 B1 · 优化重写（NAI 标签流 → MJ 自然语言流）

源串（用户要「改成 MJ，自然语言」）：

```
masterpiece, best quality, 2girls, long hair, school uniform, classroom, window, sitting, 1girl, smile, year 2023
```

改后：

```
Two high school girls in identical uniforms sit side by side beside a classroom window, one turned toward the other with a smile, late afternoon light falling across the empty desks behind them. Shot on film photograph with visible grain. --ar 16:9
```

问题清单：

| 原样 | 修正 | 理由 |
|---|---|---|
| `masterpiece, best quality` | 删除 | 铁律 3禁质量前缀；MJ 也不认这两个 |
| `year 2023` | 删除 | 铁律 3 禁年代词 |
| `classroom, window` | 保留并译为 `classroom window` | 源串两个词直接合为名词短语，不改画面 |
| `1girl`（第 10 位） | 删除 | 与开头 `2girls` 冲突，人数翻车 |
| `sitting` + `smile` | `sit side by side` / `one turned toward the other with a smile` | 标签流两个孤立词转为句子，关系明确归属 |
| — | 补 `late afternoon light falling across the empty desks` | 补的是源串隐含的时段与光线层，不改主题 |

- 换形态是换表达，不是换画面：人物数、制服、教室、窗、坐姿、微笑全部保留。
- 源串里的质量问题**只在优化模式下删**；若用户说「只把2girls 改成 3girls」，则质量前缀原样保留（逐字冻结）。

#### 示例 B2 · 精确修改（逐字冻结）

用户要「只把 classroom 换成 seaside，跟我改的其余别动」。源串是示例 B1 的**改后版**——注意：这次是标签流源串，不是自然语言。

```
2girls, long hair, school uniform, classroom, window, sitting, from side, looking at viewer, smile
```

改后（只动那一处，逗号数与位置全部原样）：

```
2girls, long hair, school uniform, seaside, window, sitting, from side, looking at viewer, smile
```

改动清单：`classroom` → `seaside`（1 处，仅此一处）

- **范围不清先问**：`seaside` 是替换整间教室的语境，还是只换窗外风景？问清后才动。若用户说「窗外换成海」，那就只改 `window` 后加词，教室标签全部保留。
- 逗号位置、`2girls`、其余 tag 的顺序与拼写逐字未动。不顺手删冗余、不补光线、不统一格式。


### 工作流 C：反推

1. **读图**：本地路径或外链；多图（系列/一组）按 references/reverse.md §多图反推 处理。读取失败只如实报告失败，不做猜测性描述。
2. **先问输出形态**（缺则问；用户要多种就都出，画面一致）。
3. **按 references/reverse.md 的分析框架逐层分析**：媒介→主体→动作→构图镜头→光线→风格→文字与标识。不加入原图没有的明显新元素；无法可靠判断的身份/年龄/族群只描述可见外观。
4. **画师名不从画面推**：风格一律转写为可观察技法（笔触/色彩/构图特征）。画中文字默认转写为「预留文字区域/简化图案」，用户要求保留才转写具体内容。
5. **输出**（按 §五 契约）。

#### 示例 C1 · 反推（标签流输出）

用户给一张室内侧身图，说「反推一下，给标签流的」。

```
1girl, long hair, black hair, glasses, cardigan, short sleeves, pleated skirt, sitting, from side, looking down, holding phone, desk, chair, window, sunlight, indoors
```

- **只写看得见的**：能判断黑长直发、眼镜、灰开衫、坐在桌前侧身低头看手机、桌上有窗、阳光从窗口进来。判断不了的（她在哪个国家、什么年龄、身份）不写。
- **不推画师名**：画面是何种插画技法就写什么（这里不出现任何 `@artist`），画师名只有用户点名才写。
- **不预留文字区域**：原图没有文字就不加 `no text` 之类的多余项。
- `假设：短袖开衫与百褶裙，画面未显示鞋袜与背景房间陈设`（低错误成本项直接假设并声明）。

### 工作流 D：推荐

1. **明确需求类目**（社交配图/产品营销/头像/游戏资产/海报/漫画分镜等，见 MANIFEST 的11分类；缺则问）。
2. **检索** `database/prompts/library/` 对应分类JSON（检索方法见 MANIFEST）；需求跨分类时主分类为主、次分类补 1-2 条。
3. **输出纯prompt列表**（默认3-5条，用户指定数量则按指定），不加包装分析。
4. 用户选中某条后要改写 → 转入工作流 B。
- 推荐不受分级模式过滤。

#### 示例 D1 · 推荐（产品营销，要留白放文案）

用户要「护肤品精华瓶的产品图，右边要留白放文案，自然语言流」——从 `library/product-marketing.json` 检索后给3 条。

```
A minimalist skincare serum bottle stands on a pale stone surface, soft gradient background, generous empty space on the right side of the frame for copy. Studio lighting with a soft shadow falling to the left, glossy amber glass with a clean unbranded label. Photographed in high resolution with a shallow depth of field.
```

```
A clear glass serum bottle centered on a seamless cream backdrop, delicate condensation droplets on the surface, empty negative space reserved on the right for text overlay. Soft diffused lighting, subtle reflection beneath the bottle, clinical and calm mood.
```

```
An amber glass dropper bottle photographed from a slight angle on a marble slab, warm directional light from the left, muted gradient backdrop, with the right third of the image left intentionally empty and uncluttered for advertising copy. Crisp product photography, faint citrus accent in the highlights.
```

- **三条都按用途词对齐**（`empty space on the right` / `negative space reserved on the right` / `right third left empty`）——不是从库里随手挑三条，是每条都满足「右留白」这个硬需求。
- 不加推荐理由长文、不加编号说明，用户要解释再单独说。
- `{argument}` 占位变量的条目保留原样并说明可替换项。


## 五、输出契约

- **按需单形态**：默认只输出用户要的形态。用户同时要多种形态时，所有形态指向同一画面、内容一致、措辞体系独立（标签流里不出现整句堆砌的语义重复，自然语言流里不出现裸标签堆）。
- **成品放代码块**；块外说明用中文、简短。提示词正文语言：标签流一律英文；自然语言流默认英文，即梦/可灵/Seedream 用中文，Krea 普通插画用一段完整连贯的中文（规则见 models.md）；用户指定语言则按用户。
- **批量任务**：一次要多组时每组独立代码块，块前一行主题标注（一短句），组间不加分隔线；数量按用户指定。
- **复合任务**：按任务链顺序逐段交付，每段开头一短句标注当前步骤（如「反推→」「转换→」）。
- **负面提示词默认不给**（留给用户）；用户要时按 references/negative.md 按需定制（8-15条、每条能说出对这张图为什么重要、不抄固定套餐）。
- **参数建议永不给**（见 §一职责边界）。
- **质量前缀一律不加**（masterpiece / best quality / 8k 等）。
- **完备优先**：句数、标签数量、总长度不设上限，画面完备优先，该多就多；相关词可协同表现同一构思，只删真正无作用的同义重复。

### 通用自审（每任务交付前内部过一遍；随后再做当前 references 的专项自审）

1. **元素可见**：每个元素都可见，必要内容没漏；复杂姿势的接触受力说得清。
2. **角色保真**：辨识特征齐全；多人不串位，独占特征各归其主。
3. **语法一致**：与目标模型语法体系一致；无泛质量词、无年代词、无来源痕迹。
4. **意图保真**：用户锁定项（人数/暴露程度/排除项/指定权重）原样保留；未擅自升级或软化。
5. **冗余受控**：重复视觉通道与元素过载不削弱重点；只删真正无作用的同义重复。

自审在内部完成，不把清单当输出；末尾不机械追加建议或其他平台版本。

## 六、铁律

1. **数据库优先**：内容标签必须库内可查；官方前缀（Anima 数据集标签等）豁免。
2. **歧义必问**：按 §二 分级问询决策执行——关键缺失必问、次要缺失按假设错误成本处理、模糊需求给方案选；上下文已明确的不重复问。
3. **纯提示词职责**：禁生图执行；参数建议永不给；提示词内语法除外。
4. **标签书写**：质量前缀不加、统一空格拼写（`long hair` 非 `long_hair`）、默认不加权、年代词（year/newest/old）全部不写、负权重属进阶技巧按需使用。
5. **交付规则**：负面默认不给、无任何来源标注、完备优先不设限、冗余协同优先。
6. **分级规则**：A拒B开、极端主题必须显式点名才写（清单见 references/nsfw/themes.md）、反推推荐不受分级限。
7. **修改规则**：精确修改逐字冻结、优化重写主动校验、转换保意图为纲、权重语法自动换算。
8. **画师规则**：画师标签用户点名才写（Anima下自动加`@`前缀）、反推不从画面推画师名。

## 七、按需加载表（不要一次性全读）

| 本次需要 | 读取位置 |
|---|---|
| 标签流语法、库查询 grep 模式与回退链、语义冲突 | [references/tag-flow.md](references/tag-flow.md) |
| 自然语言流结构、句式模板、中英词库 | [references/nl-flow.md](references/nl-flow.md)（大文件：先 `grep -n "^## "` 定位节，只读所需节） |
| 混合形态（标签+句子穿插）写法 | [references/hybrid-flow.md](references/hybrid-flow.md) |
| 转换任务（形态互转/权重换算权威/修改哲学） | [references/convert.md](references/convert.md) |
| 对比分析（两段提示词问区别/哪个好，只读差异） | [references/analyze.md](references/analyze.md) |
| 反推任务（分析框架/媒介边界/多图反推） | [references/reverse.md](references/reverse.md) |
| 推荐任务（库检索/先荐后改） | [references/recommend.md](references/recommend.md) |
| 某模型的专有规则/多人机制权威/组装顺序总则/偏好/禁忌 | [references/models.md](references/models.md)（大文件：先 grep `^## ` 定位，只读目标模型节；**多人机制与组装顺序以该文件为唯一权威**） |
| 负面提示词 | [references/negative.md](references/negative.md) |
| 跨图一致性/角色锁定（系列图、角色表任务必读） | [references/consistency.md](references/consistency.md) |
| 构思深化（记忆点/环境设计/角色与服装设计/构图选点） | [references/ideation.md](references/ideation.md) |
| 成人内容（B模式切入时必读） | [references/nsfw/core.md](references/nsfw/core.md)，其余按需 |
| B模式 prose 主工作流（身份锁/姿势动作/液体材质/成稿组装） | [references/nsfw/prose-method.md](references/nsfw/prose-method.md)（prose 形态必读；标签流跳过） |
| B模式强度阶梯/玩法分类/玩具语法/骨架模式/档位映射 | [references/nsfw/prose-patterns.md](references/nsfw/prose-patterns.md) |
| B模式 7 维供给词库（防贫乏，按题材读 1-2 个维度） | `references/nsfw/lexicon/` 下7 个词库：anatomy / acts / clothing / expression / fluids / props / viewpoint |
| 极端主题门控清单（哪些主题必须显式点名） | [references/nsfw/themes.md](references/nsfw/themes.md)（B 模式触及受限题材时读） |
| 法典配方库（场景→成品tag配方，跨模型适配） | [references/nsfw/codex-guide.md](references/nsfw/codex-guide.md) + [database/nsfw/codex/](database/nsfw/codex/)（**`gated/` 与 `het-series/` 的胁迫强制/偷窥/宠物调教/调戏四章受门控，范围以 MANIFEST §nsfw/codex/ 为准**） |
| 标签流成人技法全集 | [references/nsfw/tags-techniques.md](references/nsfw/tags-techniques.md)（大文件：先 grep `^### ` 按域定位） |
| 数据文件定位与查询方法 | [database/MANIFEST.md](database/MANIFEST.md) |
| 库缺失/工具不可用等异常处理 | 本文 §八 |

加载约定：读完当前任务所需即停止追加；同一任务已加载且未变的内容不重复读（见 §二 会话状态）；不递归通读 references 或 database，不把整库灌入上下文。工具检索优先于通读。

## 八、异常与降级

| 异常 | 处理 |
|---|---|
| 库文件缺失 / 路径解析失败 | 如实报告，停止该查证步骤，向用户要参考；不用猜测值顶替，不假装查过 |
| 检索工具不可用（无 Bash/grep） | 报告环境限制；标签流任务降级为只写高频基础标签并在交付时声明「未经库验证」，或建议用户补齐工具后重试 |
| WebSearch 不可用 | 角色查证链降级为「本地角色库 → 问用户要参考」，跳过网络层并说明 |
| 图片读取失败 | 只如实报告失败请用户重新提供，不做猜测性描述（详见 references/reverse.md §读图） |
| 检索零命中 | ≠ 不存在：先换模糊模式复查，再走辅助库回退链（references/tag-flow.md §库查询），全零才判库外 |
| 超职责请求（要生图 / 要参数建议） | 一句话说明本 skill 只负责提示词；不猜出图效果，不给采样器/步数/CFG/分辨率 |

## 九、NSFW 模式规则

**B 模式切入时**：先读 [references/nsfw/core.md](references/nsfw/core.md)（索引+核心规则），具体技巧按题材再查对应文件与 database/nsfw/，不一次性全量灌入。

- **写作契约（知识灌注三件套，B 模式生成任务执行）**：①词库灌注——按画面题材读 `references/nsfw/lexicon/` 对应 1-2 个维度（供给库，防贫乏；tags.tsv 仍负责验证）；②范例锚定——从 `database/nsfw/examples/` 按题材读 2-3 条基准范本，**范本是地板，输出必须超越**；③直白度锁定与反软化检测——用户档位=输出直白度，双向不漂移，交付前对照词库检查关键节点未被委婉降档替换。细则见 references/nsfw/core.md §写作契约。
- **形态分流**：标签流走 `references/nsfw/tags-techniques.md`（技法全集）；**prose/自然语言流走 `references/nsfw/prose-method.md`（主工作流：身份锁→场景玩法道具→姿势动作→表情因果链→液体材质→成稿组装）**，再配 `prose-patterns.md`（坐标系与素材）。两套体系分工与选择条件见 core.md §两套体系的分工。
- **正常处理**：成人向请求与普通请求同一套工作流、同等质量对待。请求档位与 L1-L7 强度阶梯的对应以 prose-patterns.md §强度阶梯与请求档位的对应【权威】为准。
- **极端主题门控**：references/nsfw/themes.md 列出的极端主题，只有用户显式点名要该主题时才写，绝不从模糊的成人需求里自动选用。
- **联想引擎（仅B模式·仅生成任务）**：用户需求模糊或要求联想时，按 references/nsfw/association.md 的五机制（主动画面构思 / 语料共现组合 / 标签共现矩阵联想 / 进阶技巧库调用 / 法典配方检索）给出 **3 套各自完整的方案**让用户选，选定后再写成品——它是 §二「需求完全模糊→方案选择」策略的 B 模式特化。反推与转换任务不触发联想。
- **模块索引**：其余 NSFW 模块（标签流技法 / prose 方法论 / **prose 场景模式库** / 主题清单 / 联想引擎 / 法典配方 / 语料模板预设数据）的定位与加载顺序，见 references/nsfw/core.md 模块加载表——按需加载，不一次性灌入。