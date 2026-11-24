# 标签流成人技巧全集（NovelAI / SD / Anima 等标签流模型）

本文件是标签流 NSFW 的完整技法库。核心创作哲学：**不描述行为本身，而是描述行为的容器、痕迹、前置状态和后续状态。** 用精确的位置词、分屏结构、source/target 语法替代模糊的"正在做什么"——生成更稳定，画面更具叙事性。

> **权重写法（本文件通用铁律）**：下文出现的 `{tag}`、`[[tag]]`、`{{{tag}}}` 一律是**识读旧配方的读法**（`{}`≈×1.05/层、`[]`≈×0.95/层）。**产出成品时一律用数值语法**（NAI `1.2::tag::`、SD 系 `(tag:1.3)`），见 models.md §权重语法 与 tag-flow.md §权重语法体系。

> **门控提示**：本文件的 NTR、胁迫与权力、偷窥/被注视、宠物调教等受限技法域，与 [themes.md](themes.md) 的 Never-Auto-Select 清单同级——**只有用户显式点名该主题时才展开使用**，不得从模糊的成人需求里自动选用。

> 大文件按需分段读：`grep -n "^### " "<本文件绝对路径>"` 列出全部技法域标题与行号（基础技法 + 装扮/人设/视角域 + 异性/多人域 + 体位/非直接域），按需读对应域，不通读全文件。

## 组装层级（成人画面的四块十一层）

成人画面的 tag 顺序是权力层级：**路由块在内容块之前**——人数没钉住，内容词越完美越歪。按本 skill 统一裁决适配后的层级（质量词/年代词按铁律不写）：

| 块 | 层 | 内容 |
|---|---|---|
| **路由块** | 1-2 | 人数（`1girl, solo` / `1girl, 1boy`）→ 画师位（用户点名才写） |
| **主体块** | 3-4 | 角色词 → 角色细节（发色发型瞳色 + 体型锚点 `mature female, curvy, petite`——体型锚点属于身体不是年龄） |
| **内容块** | 5-8 | 裸露状态（`nude, topless, bottomless`）→ 身体细节（大小/形态/乳头）→ 身体物理态（`wet, sweat, blush, shiny skin`）→ 覆盖变体（`panties aside, shirt lift`） |
| **框架块** | 9-11 | 表情+反应（核心模式+眼态+嘴态，见 lexicon/expression）→ 构图（机位/景别/focus，见 lexicon/viewpoint）→ 环境+打码（场景/光源/uncensored） |

**内容块内部次序**：裸露→解剖→物理态→覆盖变体（`nude, large breasts, perky nipples, aroused, blush` ✓；`perky nipples, blush, nude` ✗——状态词跑到了主体词前面）。

**层级与隐性权重的关系**：位置即权重（tags-techniques 权重逻辑）——灵魂元素仍放最前，十一层是"同类不散块"的组织律，不是机械填表。

## 解剖防御协议（成人画面特有崩坏的三层防御）

成人场景的解剖崩坏率高于普通画面（手融合、指倍增、胸与躯干粘连、双人肢体融合），防御分三层：

1. **正向层**：每图必含 1 个 silhouette 词（lexicon/anatomy §体型轮廓）+ 关键部位修饰词——身体细节写在正向，不指望负面词救。
2. **负向层**：成年防御块**必进负面**（B 模式默认附加，见 [../negative.md](../negative.md) §成年防御块）：`child, loli, shota, underage, young teen, kid, infant, minor, immature body` + 解剖通用块（`bad anatomy, bad hands, extra fingers, fused fingers, missing fingers, deformed, extra limbs`）。
3. **用户端层**：面部/手部修复、高清修复去噪属于出图端工具——一句话提示用户可用修复工具处理残留崩坏，不展开参数建议（§一职责边界）。

**双人接触防融合**：接触点必须有主人（models.md 多人机制）+ 重叠肢体用机位分离（俯视宽景+裁肢减负，见多人域技法）+ 串味三件套。


## 铁律

1. **器官暴露即标注，性行为写完整**：动作 tag + 双方器官，缺一个都不完整。
2. **男性默认隐形**：disembodied penis / invisible man 代替 1boy；叙事必须有男性身体时才 faceless male。光谱：`1boy → faceless male → disembodied penis → invisible man → solo focus`。
3. **半遮半掩胜过全裸**：torn clothes / panties aside / see-through 的戏剧性高于 nude。
4. **场景重交互轻背景**：如果重点是人物，环境 2-3 词够了。
5. **prompt 复杂度与稳定性成反比**：最稳定 = 1 角色 + 1 姿势 + 1 套服装 + 1 场景。越复杂越不稳定，复杂姿势需要足够多 tag 锚定每个动作。

## 六种创作意识

1. **摄影意识**：视角/光线/景深是画面骨架。
2. **情绪意识**：先选情绪阶段，再选对应 tag 组合（见情绪梯度表）。
3. **物理意识**：hanging breasts 因为趴着、ass ripple 因为被撞、spread toes 因为紧张——每个 tag 都要有物理因果。
4. **叙事意识**：静态物体的叙事密度远超动词——used condom、tally（正字计数）、torn pantyhose 自己会讲故事。
5. **化学反应意识**：tag 组合协同（见组合库）。
6. **控制意识**：灵魂元素锁死，细节留白；画面完备优先。

## 情绪五级梯度表 + 羞耻

路径：害羞 → 发情 → 被压倒 → 高潮 → 崩溃。先定位阶段，再取组合。

| 梯度 | tag 组合 |
|---|---|
| 害羞 | blush, nose blush, embarrassed, flying sweatdrop |
| 发情 | heavy breathing, steaming body, heart, sweat, spoken heart |
| 被压倒 | tears, drooling, trembling, clenched teeth |
| 高潮 | ahegao, rolling eyes, tongue out, heart-shaped pupils, female orgasm |
| 崩溃 | empty eyes, fucked silly, expressionless, broken |
| 羞耻 | @_@, wavy mouth, !, embarrassed, full-face blush |

## 万能尾缀套装（三套）

- **发情氛围**：`steaming body, heavy breathing, heart, sweat, blush, shiny skin`
- **高潮失神**：`torogao/ahegao, rolling eyes, twitching, trembling, female ejaculation, heart, sound effects`
- **被发现羞耻**：`@_@, wavy mouth, !, embarrassed, full-face blush, surprised, flying sweatdrop`

## 化学反应组合库

| 效果 | tag 组合 |
|---|---|
| 冲击力 | ass ripple + speed lines + motion blur |
| 弥漫情欲 | steaming body + heavy breathing + heart + sweat + spoken heart |
| 皮肤质感 | shiny skin + oiled skin + steaming body + wet skin |
| 透明感 | see-through + shiny clothes + fine fabric emphasis |
| 无意识感 | sleeping + expressionless + zzz + closed eyes |
| 内外同展 | stomach bulge + cross-section |
| 导演裁切 | head out of frame + close-up + [部位] focus |
| 湿透感 | wet clothes + see-through + clinging clothes + rain/water |

## 运动感辨析

| tag | 表达的动能 | 适用场景 |
|---|---|---|
| speed lines | 快速重复运动 | 激烈抽插 |
| motion blur | 整体动态模糊 | 高速运动 |
| ass ripple | 撞击点波纹扩散 | 后入冲击 |
| trembling | 不自主颤抖 | 高潮/恐惧 |
| motion lines | 通用运动轨迹 | 任何动态 |
| twitching | 痉挛抽搐 | 高潮余韵 |
| spasm | 强烈痉挛 | 强制高潮 |

## 施受定向

- `target#anal fisting` = 指定承受者；`source#grabbing` = 指定施加者；`mutual#hand in another's panties` = 双方互相。**双人场景默认使用**（这是动作入角色栏的唯一合法通道，见 models.md §多人机制 例外 1）。
- source#/target# 不只标记谁做什么，还标记谁知道什么（阴谋拥抱：施加者写 smirk + glowing eyes，承受者只写 from behind——信息差即叙事）。

## 非直觉技法

- **负权重擦除**：`-2::arm support::` 主动压制元素，在正面 prompt 内局部生效，比负面词更精准。
- **层级裁切**：`head out of frame` 轻裁 → `{{{head out of frame}}}` 强裁 → `[[[[[head out of frame]]]]]` 彻底消除（以上为旧配方读法）。**产出换算成数值**：强裁 `1.15::head out of frame::`、彻底消除改用负权重 `-2::head out of frame::`（见 models.md §权重语法）。
- **透视截面系统**：`x-ray, cross-section, uterus at viewer` + 插入动作 + `stomach bulge`（外部凸起同展）。
- **受精画面**：`fertilization, sperm cell, ovum` 在 cross-section 基础上画受精过程。
- **差分/多视图**：`instant loss, 2koma, before and after, 2views` 同画布状态对比；抱枕正反面 = `dakimakura (medium), split screen` + 正面描述 | 背面描述。
- **直播伪截图**：`fake screenshot, chat log, danmaku comments, battery indicator, viewfinder` + `livestream`。
- **脚部动能语言**：`dorsiflexion`（脚尖上翘=紧张/用力）、`plantar flexion`（下压=放松/优雅）、`toe scrunch`（蜷缩=高潮/痛苦）。
- **文字道具叙事**：`body writing, tally` = 身体上的使用记录；`price list on wall` = 场景羞辱信息。
- **衣物无人暗示**：`no humans` + 被污染的衣物（cum-filled boot / cum on hat / discarded clothes）——用痕迹代替行为。
- **拟态物替身**：`fumo (doll)` 比泛化 doll 质感好；`alternate face` 在娃娃上渲染目标角色。

## 场景与拘束

- **感觉遮断**：上半身日常 + 下半身被侵犯的矛盾张力。必须配表情矛盾（expressionless / looking at phone），绝不用 ahegao。行为越日常、下半身越激烈，张力越大。
- **场景作为拘束**：`stuck in wall / through wall / glory wall`（壁尻）、`in trash can, upside-down, folded`、`in washing machine, stuck`。核心结构：stuck/through/in [容器] + 身体部位分拆（upper body / lower body / head out of frame）。
- **感官剥夺分层**：每个感官通道单独一个 tag——`black ball gag`（口）+ `black blindfold`（眼）+ `earplugs`（耳）+ `arms immobilized` + `legs immobilized`。不能偷懒只写 blindfold, gagged。
- **捆绑权重分层**："绑的姿势"和"绑的结构"分开权重。倒吊三角锁定：`upside-down` 单独加权（旧配方读作 `{{{upside-down}}}`，产出写 `1.15::upside-down::`） + `top-down bottom-up` + `face to viewer`。
- **双人捆绑连接件**：`linked collar` / `linked gag`（共享口球）/ `bound together` / `shared object insertion, double dildo`。
- **触手需要空间容器**：先抛拓扑容器（`tentacle pit` / `flesh wall` / `inside creature`）再加行为；`tentacle background` = 整个背景全是触手。
- **史莱姆透明体**：外层透明是容器 tag（`see-through body` / `translucent skin`），内部可见内容单独提权重；用 `penis in body` 而非 vaginal 以保住透明感。
- **stealth sex**：告诉模型"周围有人但性行为在发生"，比单写 public 精准。
- **日常容器替换**：日常动作 + 性暗示内容物（cum in beer mug / cum toothpaste + brushing teeth）——模型接受"行为框架"因为动作本身正常。
- **逃离叙事三层**：服装残缺（torn pantyhose / lost one shoe）+ 步态（staggering / crawling / weak）+ 地面遗留（used condoms on ground）。

## 服装功能性降级梯度

比 torn clothes 更精确的层次（保留部分服装的张力比全裸高）：

- `strap slip` / `areola slip` = 刚好露出
- `panties aside` = 拨开但未脱
- `panties around one leg` = 仅一条腿挂着

## 角色类型锚定

### 伪娘 vs futa（精确区分）

- 伪娘锚定：`otoko no ko, small penis, foreskin`（男性基底+女装）。伪娘用 `dildo riding, anal object insertion`，不用 futanari，否则模型向女性漂移。
- futa 锚定：`futanari, pussy, fat mons`（女性基底+阴茎）；`full-packaged futanari` = 同时有阴茎+阴囊+阴道；`futa with female / futa with futa / futa on male` 指定搭档；`futasub` = 扶她作为受方。
- 伪娘场景状态：`erection under panties, small penis`（标准被动开场）；`chastity cage, ejaculation, @_@`（被锁强制高潮叙事）；`penis bow`（缎带系缚的礼物隐喻）；`trembling legs` 比 trembling 更有画面感。

### NTR 的道具叙事

不直接描述关系，用道具构建第三者存在感：`phone showing "husband calling"` / `incoming call`、`wedding ring on finger`、`condom belt` / `condom thigh strap`、`queen of spades symbol` / `spade tattoo`。苦主不做视觉主体：`pov`（第一人称苦主视角）/ `blurry foreground pov hand` / `human chair`。

### 人外角色反差

兽性特征越强，人类情绪越要写软：`dragon horns, dragon tail, fang` + `embarrassed, nose blush, holding towel`——杀伤力生物特征 + 软糯局促情绪 = 最大张力。

### 魅魔堕落三级

- 初级：`demon horns, tail, wings`
- 中级：`dark persona, corruption, glowing tattoo, heart-shaped pupils`
- 完全堕落：`glowing eyes, claw bra, glowing nails, pubic tattoo`

### 精灵差异化

- 圣洁：`pointy ears, circlet, forest, translucent skin`
- 黑暗：`dark elf, dark skin, tanlines`
- 野生：`body freckles, glowing markings on cheeks, black nails, black lips`

### 史莱姆娘

`liquid hair`（比 slime hair 准确）+ `see-through body`；`blue slime on legs` = 只有腿部残留，暗示形态不稳定。

### 色情改造公式

基础职业服 + 暴露化改造 + 色情道具：
- `nurse cap, slingshot swimsuit, holding syringe` = 色情护士
- `police hat, crop top, micro shorts, no panties` = 色情警察
- `maid headdress, naked apron, nude` = 裸体女仆

公式化思维可套用任何职业。

### 冷门精确 tag

`crotch plate`（骨盆装甲板）、`fine fabric emphasis`（面料质感强调）、`twitching penis`（高潮临界）、`flaccid penis`（未勃起）、`^^^`（抽搐/失控象形符号）。

## 权重逻辑（成人题材专用）

- **不是"重要就加权"，而是"模型不容易自己做到的才加权"**：复杂姿势、非常规视角、特殊概念 → 加权；breasts, nipples, blush 这些模型本来就懂的 → 不加权。
- **串越长，关键元素越容易被稀释**——长串里关键元素权重层数更高。
- **组合打包权重**：一组语义相关的 tag 打包成一个权重单元，告诉模型"这些是一体的"。旧配方读作 `{ahegao, rolling eyes, orgasm, fucked silly}`、`{{{steaming body, heavy breathing, female orgasm, sweat, blush, saliva}}}`；**产出用数值语法**：`1.2::ahegao, rolling eyes, orgasm, fucked silly::`。
- **灵魂元素最前**：想清楚"这张图的灵魂是什么"，那就是第一个 tag。

## 环境叙事

不只写 indoors——具体到 `bar counter, slot machine` / `train interior, crowd` / `stone wall, dungeon, chain`。但重点在人物时环境 2-3 词够。

---

# 增量技法：装扮/人设/组件/视角域

以下技法从法典配方库深度提炼，是上方基础技法的扩充。括号内为相对 database/nsfw/codex/ 的出处文件。


### 一、服装状态与穿法语言

- **reverse 骨架系统**：反向穿戴不是删正装而是"换骨架"——先立 reverse 主件，再叠附属件，最后负权重擦掉原部件。代表性写法：`reverse bunnysuit, reverse outfit, frontless outfit, shrug (clothing), pasties` + `-1::rabbit ear::` / `-2::maid::` / `-1::hakama::`（outfits/bunny.md、outfits/occupational.md）
- **naked 单件公式**：任何单件日常物前加 naked 即成"仅此一件"的裸装骨架，比 nude+服装组合稳定得多。代表性写法：`naked apron / naked coat / naked cape / naked kimono / naked ribbon / naked scarf / naked suit / naked bandage`（outfits/casual-alteration.md、outfits/nude-covering.md）
- **内层声明词**：多层穿搭必须声明"谁在谁里面"，模型才按层渲染。代表性写法：`bodystocking under clothes / swimsuit under clothes / leotard under clothes / panties under pantyhose`（outfits/rubber.md、outfits/misc.md）
- **透明度四档**：translucent（半透）→ see-through（明显透）→ transparent（全透）→ see-through silhouette（逆光只透轮廓）；拉满可写三档连用。代表性写法：`completely colorless and translucent leotard` / `see-through silhouette, backlighting`（outfits/corset.md、outfits/sleepwear.md）
- **胶衣开门件**：紧身胶衣的暴露=开洞+拉链两族：开洞用 cutout 词族逐部位枚举，拉链用 full-length zipper+unzipped 表"进行中"。代表性写法：`center opening, navel cutout, underboob cutout, full-length zipper, unzipped`（outfits/rubber.md）
- **异质材质族**：PVC/塑料/全息/虹彩是透明的高级替代材质，自带未来感。代表性写法：`clear plastic clothes, pvc outfit, holographic clothing, iridescent leotard`（outfits/rubber.md、outfits/bunny.md）
- **同义词并联保险**：稀有概念用 2-3 个同义 tag 并联塞进同一权重提高触发率。代表性写法：`1.71::transparent dress,pvc dress,see-through dress::`（outfits/casual-alteration.md）
- **湿润状态链**：湿身要写到"湿了哪件衣物"并补发丝与体温，fine fabric emphasis 专司湿布贴肉。代表性写法：`wet shirt, wet clothes, wet hair, water drop, steaming body, fine fabric emphasis`（girl-series/alt-daily.md 湿身系列）
- **遮点布帘家族**：挂帘式遮点是"半遮"的标准结构，加 aside/lift 即成可掀状态。代表性写法：`breast curtain, pelvic curtain, pelvic curtain lift, short pelvic curtain`（outfits/dancer.md、outfits/casual-alteration.md）
- **不对称残缺感**：单边错位暗示"刚被弄乱"，比 torn clothes 更日常。代表性写法：`asymmetrical legwear, single thighhigh, single glove, mismatched bikini, single pantsleg, single bare shoulder`（outfits/race-queen.md、misc/cosplay.md）
- **impossible 合法化**：`impossible clothes/bodysuit/underwear` 是"现实中不存在的剪裁"的声明词，与 revealing clothes 成对防画风崩。代表性写法：`impossible clothes, revealing clothes, impossible bodysuit`（outfits/corset.md、outfits/rubber.md）
- **穿帮事故族**：意外暴露自成一类，配惊讶符号表情。代表性写法：`wardrobe malfunction, accidental exposure, strap break, button popping, bursting breasts` + `!, !?, @_@`（girl-series/alt-daily.md）

### 二、色情改造公式的域内变体

- **身份锚策略**：职业改造只保留一个"身份最小锚"（帽徽/头饰），其余全换色情件，模型靠锚点认职业。代表性写法：`nurse cap, slingshot swimsuit` / `maid headdress + 色情件` / `police hat + 色情件`（outfits/occupational.md）
- **谱系交叉法**：任一职业 × 逆兔/兔女郎即可重组出新装，交叉时只换身份锚、兔女郎件保持不动。代表性写法：逆兔女仆 / 逆兔护士 / 逆兔赛车女郎 / 水手服逆兔（outfits/bunny.md、outfits/occupational.md）
- **中式侧开律**：旗袍/汉服的暴露开关是"侧"不是"前"：very short hanfu + side slit/sideless/side-tie + 分离袖，兜底件是 dudou。代表性写法：`see-through chinese hanfu, side-tie, detached sleeves, dudou`（misc/cosplay.md）
- **神符号转移**：修女/圣女改造把十字架留在身上但挪到色情位，神性与色情同框。代表性写法：`cross pasties, cross necklace, cross earrings, breast curtain`（outfits/fantasy-alteration.md）
- **异域三件套**：harem outfit+mouth veil+双 curtain 是舞娘/埃及/阿拉伯万能骨架，金饰链化做"chain only clothes"。代表性写法：`harem outfit, mouth veil, breast curtain, pelvic curtain, waist chain, leg chain`（outfits/dancer.md、outfits/fantasy-alteration.md）
- **宅职业三步化**：魔法少女/爱豆/赛车女郎只需"leotard 化+高跟长靴化+开洞化"三步。代表性写法：`magical girl, highleg leotard, showgirl skirt, thigh boots, cleavage cutout`（outfits/magical-girl.md、outfits/race-queen.md）
- **物种印花短路径**：cow/cat/pig 印花套件是"改造成牲畜"的最短路径：印花件+兽耳+铃铛+假尾。代表性写法：`cow print bikini, cow ears, neck bell, anal tail`（outfits/misc.md、misc/cosplay.md）
- **巫女成对改**：miko 服是白 kimono+红 hakama 的成对结构，破坏时两件一起改，符咒（ofuda）遮点是日系特供遮点物。代表性写法：`short kimono, hakama skirt, ofuda on nipples`（outfits/fantasy-alteration.md）

### 三、视角与构图语言

- **特写三视角叠加**：裙底/臀/足特写通用骨架=from below+ass focus+foreshortening，fisheye 强畸变、dutch angle 斜置、top-down bottom-up 专司趴床。代表性写法：`from below, from behind, ass focus, foreshortening, fisheye`（viewpoint/skirt.md、viewpoint/feet.md）
- **遮挡即构图**：裙底/偷窥视角永远让前景物当画框，反射面可做第二画框。代表性写法：`staircase, escalator, under desk, through legs, behind umbrella, puddles, reflections, reflected upskirt`（viewpoint/skirt.md）
- **身体自框**：用自身肢体做取景洞口。代表性写法：`looking through legs, looking through own legs, head between own thighs, bent over, arm support`（viewpoint/misc.md）
- **足底四要素**：foot focus+foreshortening+soles+脚趾动作；气味用 steam/smell/scent lines 具象化；鞋的状态（dangle/removed/unworn）决定羞耻等级。代表性写法：`foot focus, foreshortening, soles, spread toes, shoe dangle, unworn shoes`（viewpoint/feet.md）
- **承托物系统**：胸部特写让胸被环境"接住"比悬空稳定。代表性写法：`breast rest, breast press, breasts on desk/tray/book/glass, leaning on exercise ball`（viewpoint/breast.md）
- **下乳仰视件**：低头弯腰+仰拍机位是下乳/侧乳专用，漏点只写单点 slip 不写全裸。代表性写法：`from below, underboob focus, close-up, head out of frame, areola slip`（viewpoint/breast.md）
- **背面骨相词**：背面域的性感点靠骨相而非皮肤，配 looking back 保眼神连接。代表性写法：`from behind, looking back, bare back, shoulder blades, median furrow, backboob`（viewpoint/back.md）
- **下半身独立成画**：lower body+head out of frame+feet out of frame 裁掉上半身做纯部位构图。代表性写法：`lower body, head out of frame, legs only, foot focus`（viewpoint/legs.md）
- **镜像分身**：镜子用于"镜内裸/镜外穿"对比与自拍二次构图。代表性写法：`mirror, reflection, different reflection, reflection focus`（viewpoint/misc.md、girl-series/hidden-showing.md）
- **景别词族**：cowboy shot 是全域默认景别与兜底保险；其余景别/机位词按需声明。代表性写法：`cowboy shot / wide shot, medium shot, close-up, zoom layer, straight-on, three quarter view, profile, tachi-e`（全域高频、viewpoint/misc.md）
- **光位氛围开关**：光位词与主题绑定：backlighting 配剪影透明，underlighting 配仰视与恐怖，dappled sunlight 配户外，godlighting 配舞台/教堂。代表性写法：`backlighting, see-through silhouette / underlighting, from below / godlighting, stage`（viewpoint、girl-series/seduction.md）
- **POV 词族**：观演关系由 pov 决定——pov（你是男）/female pov（她的视角）/pov hands（男手入画）/pov crotch（男部位入画）/pov doorway（开门见客）/pov across table。代表性写法：`pov, pov hands, pov crotch, pov doorway`（persona/outfits.md、components/male.md）
- **器材透视**：把"看穿"装进设备成为画面主体，配 `?` confused 表偷拍感。代表性写法：`x-ray glasses, x-ray smartphone, pov, school uniform, ?`（components/male.md）

### 四、自拍·直播·录像

- **自拍基本件**：selfie+holding phone+looking at lens+outstretched arm（伸出去的手臂），俯拍比例用 from above+focus on chest and feet 自述。代表性写法：`selfie, holding phone, outstretched arm, from above`（girl-series/hidden-showing.md）
- **自拍匿名脸**：遮脸不遮身是自拍域的固定张力结构，遮具任意。代表性写法：`covering own eyes, phone covering one eye, mouth mask, mask pull, one finger selfie challenge (meme)`（girl-series/hidden-showing.md）
- **镜前自拍件**：mirror selfie 必须带 reflection/holding phone，镜头-镜面双关系才成立。代表性写法：`mirror selfie, holding phone, reflection focus`（girl-series/hidden-showing.md）
- **录像与直播件**：录像=video camera+tripod+recording+viewfinder；直播=livestream+chat log+danmaku comments+live host+viewer count+fake phone screenshot UI。代表性写法：`recording, viewfinder / livestream, chat log, fake screenshot`（outfits/lingerie.md、girl-series/hidden-showing.md）
- **封面伪件与取证**：id card/name tag/price tag 给自拍者"盖章"；杂志封面套件做刊物质感。代表性写法：`id card on face, holding id card / doujin cover, magazine cover, content rating`（girl-series/misc.md、girl-series/exhibitionism.md）

### 五、自慰场景语法

- **道具烈度阶梯**：手指→振动棒（under clothes/in thighhigh）→遥控跳蛋（remote control vibrator+controller）→假几把（dildo riding/suction cup）→拉珠（pulling anal beads）→生活物替代（broom/staff/cane/cucumber/shower head/table-kun/pillow/giantess 建筑）——道具等级=场面烈度。代表性写法：`vibrator under clothes, remote control vibrator, dildo riding, pulling anal beads`（girl-series/masturbation.md）
- **隔衣自慰**：不脱是第一张力层，隔什么都行。代表性写法：`fingering through panties, masturbation under shirt, clothed masturbation, hand in clothes`（girl-series/masturbation.md）
- **被发现三角**：caught+开门手（pov hand open door）+惊愕表情，行为证据由物件补全。代表性写法：`caught, pov hand open door, @_@, panties around one leg, used tissue`（girl-series/masturbation.md）
- **事后痕迹链**：让"刚发生"由物件讲：汁液痕迹/湿床单/纸巾/地上道具/挂在腿上的内裤。代表性写法：`after masturbation, pussy juice stain, wet sheet, dildo on floor, panties around one leg`（girl-series/masturbation.md）
- **画中画媒介**：看片/看书自慰把媒介内容画进画面，屏幕即画框。代表性写法：`looking at computer screen, sex in computer screen, pornographic magazines, text:r18`（girl-series/masturbation.md）
- **高潮姿态锁**：自慰到潮喷用姿态组合锁定而非表情单点。代表性写法：`arched back, head back, female ejaculation, spread toes, trembling legs`（girl-series/masturbation.md）

### 六、露出场景语法

- **大衣开关结构**：露出域万能开场=外层大衣（naked coat/trench coat）+里层全裸或情色件+开合动词。代表性写法：`naked coat, open coat, opened by self, flashing, coat grab`（girl-series/exhibitionism.md）
- **公开度声明**："有人在"不靠行为 tag 靠人群词。代表性写法：`public indecency, public nudity, crowd, passerby, background character, faceless male`（girl-series/exhibitionism.md）
- **气质分岔**：同一套裸装换表情即换作品气质——冷脸狂气系 vs 害羞怂系。代表性写法：`middle finger, shaded face, jitome / shy, nervous smile, flying sweatdrops`（girl-series/exhibitionism.md）
- **偷窥机位库**：偷拍视角自带叙事，画面里放"拍摄设备"即可。代表性写法：`vending machine, streetlight, flashlight beam, from inside the locker, cellphone photo`（girl-series/exhibitionism.md、girl-series/alt-daily.md）
- **玩具出街步态**：行走+体内玩具=步态词+震颤词+痕迹词三件套。代表性写法：`dildo under dress, walking, knees together feet apart, trembling legs, pussy juice trail`（girl-series/exhibitionism.md）
- **正装突发高潮**：办公/上课/板书中突然高潮：失态符号+动作线+手扶固定物+视线逃离。代表性写法：`^^^, motion line for orgasm, trembling, hands on chalkboard, looking away`（girl-series/misc.md）

### 七、诱惑与侍寝语法

- **侧躺标准件**：侧躺诱惑固定五件，另一只手做小动作（绕指内裤/持套/拉绳）。代表性写法：`lying, on side, knee up, hand on own cheek, elbow rest, seductive smile, panties around one finger`（girl-series/seduction.md）
- **开门见客机位**：pov doorway+open door+from above looking down 三件固定，人物状态由穿着声明。代表性写法：`pov doorway, open door, from above, looking down, strap slip`（girl-series/seduction.md）
- **被子交互**：bed invitation+lifting covers 把被子变道具，红被压暖色氛围。代表性写法：`bed invitation, lifting covers, under covers, red covers`（girl-series/seduction.md）
- **嘴叼物语**：mouth hold 词族让嘴参与叙事，叼什么=什么意图。代表性写法：`condom in mouth, condom wrapper in mouth, clothes in mouth, hair tie in mouth, sash in mouth`（girl-series/seduction.md、girl-series/alt-daily.md）
- **引导抓胸**：把"谁的手"写死，男性只以 pov hands 存在。代表性写法：`guided breast grab, grabbing another's hand, pov hands, finger sucking`（girl-series/seduction.md）
- **乳沟容器化**：乳沟当托架放任意小物；身体倒饮=pouring onto self+液体名。代表性写法：`condom between breasts, card between breasts, can between breasts, pouring onto self, wine on body`（girl-series/seduction.md、outfits/dancer.md）
- **遮穴小物**：手持任意小物遮点即"欲遮还露"姿势件。代表性写法：`fan covering crotch, book on own crotch, holding sign covering breasts, condom box`（outfits/nude-covering.md、girl-series/seduction.md）
- **前置道具叙事**：将要发生=前置物（套/润滑液/替代器放在画面里）；已发生=used condom 计数。代表性写法：`holding condom, condom packet strip, lube bottle laid aside, artificial vagina`（persona/outfits.md）

### 八、人设与组件搭配

- **组件插槽正交**：体型/毛发/皮肤/痕迹是独立插槽，可与任何服装域正交组合。代表性写法：`mature female, plump, petite figure, excessive pubic hair, shiny skin, skindentation, bite mark, hickey`（components/female.md）
- **婊子化标准包**：妆容+穿环+黑桃+深肤色是跨文件反复出现的打包件，一次挂载整体变调。代表性写法：`heavy makeup, purple eyeshadow, purple lips, dark skin, queen of spades symbol, tongue piercing, navel piercing`（components/female.md、outfits/misc.md）
- **分离件文化**：shrug/detached collar/detached sleeves/bridal gauntlets/arm garter/wrist cuffs 让衣物碎片独立存在，身体核心裸露时"碎片"仍挂着——碎片越多越像"穿到位"。代表性写法：`shrug (clothing), detached collar, detached sleeves, bridal gauntlets, wrist cuffs`（outfits/bunny.md、outfits/occupational.md）
- **带状物最廉价**：thigh strap/garter straps/leg loop/o-ring 是成本最低的色情组件，朴素 outfit 加一条即变调。代表性写法：`thigh strap, garter straps, o-ring thigh strap, leg loop`（全域高频）
- **乳房形态学**：下垂分级 perky→pointy→sagging→hanging→long breasts；挤压关系 apart/squeezed together/unaligned；压迫 press/smother/rest。代表性写法：`sagging breasts, unaligned breasts, breasts squeezed together, breast smother`（viewpoint/breast.md、components/female.md）
- **男性最低存在量**：性爱场景=faceless male/muscular male+head out of frame+阴茎描述；调情场景只剩 bulge/erection under clothes/pov hand——男性 tag 数与场景烈度成反比。代表性写法：`faceless male, male head out of frame, huge penis / bulge, erection under clothes`（components/male.md、persona/outfits.md）
- **condom 生命周期**：未用=packet strip/wrapper；使用中=pointless condom；用完=used condom→容器化（belt/thigh strap/necklace/盒/鞋/桶）。代表性写法：`condom packet strip, pointless condom, used condom belt, used condoms in heart-shaped box`（outfits/misc.md、components/female.md）
- **双子镜像法**：双人=同套件异色+对称姿态；不对称双人=一人 smug 一人 shy。代表性写法：`black cat lingerie, white cat lingerie, symmetrical docking`（outfits/lingerie.md）
- **差分同角色法**：2koma 前后差分写同一角色：公共 tag 放外层、Character 1/2 各写状态，结构词声明分屏。代表性写法：`2koma, before and after, instant loss, 2views, split screen`（girl-series/misc.md）
- **伪娘/扶他的"藏"表达**：藏匿式表达让下体处于半公开状态；伪娘女性化用淡妆/饰品递进，男性底盘用 flat breasts/male focus 压住。代表性写法：`otoko no ko, male focus, flat breasts, light makeup / futanari, covered penis, bulge, penis under dress`（persona/femboy-design.md、persona/futa-design.md）
- **角色锚与皮肤系统**：`角色名 (cosplay)` 直取官方服，`official alternate costume` 换官方皮肤，`alternate color/hairstyle` 微调，`aged up, mature female` 覆盖年龄。代表性写法：`角色名 (cosplay), official alternate costume, aged up`（persona/canon-chars.md）
- **主题色双轨**：`xxx theme` 定大调、`xxx trim` 做细节呼应，成对使用色彩才整。代表性写法：`black theme, purple theme, white theme + gold trim, neon trim, blue trim`（outfits/misc.md、misc/cosplay.md）

### 九、权重与稳定性惯例

- **正负主题色**：配色用 `n::xxx theme::` 正权统一，禁用色用负权抹除，连裙摆都能负权删掉。代表性写法：`1.1::white theme::, -2::white clothes::, -3::dress, skirts hemline::`（outfits/swimwear.md、outfits/casual-alteration.md）
- **极端权重集中制**：一条串里 2.0+/3.0+ 超高权重只给"这张图是什么"的一两个词（主件/主色/主姿态），其余 0.8-1.4 微调。代表性写法：`4.02::extremely high platform footwear::, 2.69::black latex trench coat::`（outfits/casual-alteration.md）
- **画风弱权挂前部**：画风/画师 tag 用 0.6-1.05 弱正权放串头，既定调又不抢主体。代表性写法：`0.9::artist:xxx::` 或 `0.77::画风tag::`（outfits/casual-alteration.md、persona/canon-chars.md）
- **长串三核心保全**：上限不是硬门槛，超长串（100+ tag）仍可出——关键是角色/服装/姿态三核心前置完整，复杂度损失主要发生在"第二个角色/第二套服装"上。代表性写法：长串时 `1girl, solo, 服装主体, 姿态` 放前 20 位（persona/nonhuman-design.md）

### 十、域内独有招式

- **人体彩绘伪服装**：bodypaint 直接"画出一套衣服"，主题图案+作画过程件增强可信度。代表性写法：`bodypaint, painted clothes, bodypainted swimsuit, holding marker pen, spilled paint`（outfits/body-drawing.md）
- **纹身即进度条**：淫纹→发光淫纹→全身纹身→计数纹身，纹身密度=堕落/使用进度。代表性写法：`womb tattoo, glowing tattoo, full-body tattoo, abortion mark`（outfits/body-drawing.md、outfits/corruption.md）
- **裸体遮盖道具库**：convenient censoring+covering breasts/crotch+身边任意物，遮盖物与职业绑定即成梗。代表性写法：`convenient censoring, covering crotch, money on pussy / sword covered body / hongbao`（outfits/nude-covering.md）
- **unworn 反向时空锚**：`unworn [X]` 让"没穿的衣物"出现在画面任何位置，与 folded clothes/clothes on floor 一起构成脱衣叙事的时空证据。代表性写法：`unworn clothes on bed, unworn shoes on floor, clothes on floor, folded clothes`（outfits/nude-covering.md、girl-series/alt-daily.md）
- **恶堕三改件**：恶堕=皮肤色+瞳形+发光三轴同改，服装层换紫黑主题+霓虹描边+破损。代表性写法：`corruption, dark persona, heart-shaped pupils, no pupils, glowing tattoo, dark skin, neon trim, cracked skin`（outfits/corruption.md）
- **机械替换点位**：机娘色情=人体位逐一换机械词，透明躯体配发光核心。代表性写法：`mechanical cervix, crotch plate, mechanical uterus, head-mounted display, covered eyes, barcode tattoo, see-through body, glowing core`（misc/machinery.md、outfits/misc.md）
- **机械拘束桩**：实验室系拘束词汇——"装置"替代"绳索"成为高科技拘束语言。代表性写法：`stationary restraints, medical restraints, stasis tank, sex machine, milking machine, machine tube in ears`（misc/machinery.md）
- **打码词与数据删除**：censoring 词汇系统自成一组，赛博遮点用故障弹窗。代表性写法：`mosaic censoring, bar censoring, uncensored, identity censor, glitch censor, error message, blue screen of death`（components/male.md、outfits/nude-covering.md）
- **呈上仪式**：holding tray+[物 on tray]+"跪呈/挂牌"组合=服务型身份宣言。代表性写法：`holding tray, dildo on tray, shoes on plate, price tag`（outfits/occupational.md、misc/machinery.md）
- **玻璃按压系**：贴玻璃+部位 on glass，雾面玻璃做"半透视"第二层。代表性写法：`against glass, breasts on glass, ass on glass, frosted glass, steamed glass, condensation`（girl-series/alt-daily.md、viewpoint/misc.md）
- **姿态词汇表**：淫态姿势有专用词且极稳定，比动作描述短语可靠。代表性写法：`knees together feet apart, bowlegged pose, m legs, wariza, yokozuwari, seiza, pigeon-toed, watson cross, horse stance`（全域高频）
- **文案挂载点**：文字可挂载在身体/衣物/道具任意表面，位置=用途声明。代表性写法：`text:"use me" on stomach, body writing, text on ass, clothing cutout + text, tally`（outfits/body-drawing.md、girl-series/seduction.md、components/female.md）


---



# 增量技法：异性系列/多人系列域

以下技法从法典配方库深度提炼。括号内为相对 database/nsfw/codex/ 的出处文件。

> 提炼自 het-series 与 group-series 配方库，只收基础技法全集与装扮/视角域消化稿未覆盖的增量。

### 一、调戏与偷窥场景构造

- **衣物拉扯动词族**：每件衣物对应一个"进行中"动词，拉扯动作本身就是袭扰事件的最低烈度起点，比静态半脱更有事件感。代表性写法：`panty pull, skirt pull, bra lift, shirt lift, shorts pull, pants pull, clothes pull`（teasing.md）
- **日常掩护分工式**：女方 Character 行内只写日常活动与专注词，男方 Character 行内用 `source#` 前缀挂侵害动作（动作入栏的合法通道，见 models.md §多人机制 例外 1），"表面正常"由分栏结构承载而非表情词。代表性写法：`Character 1: holding book, looking at book, reading / Character 2: source#grabbing from behind, hand under clothes`（teasing.md）
- **公共设施锚定姿势**：电车/摩天轮/收银台等站立场景必须写"手抓的固定件"，否则站姿漂移。代表性写法：`train interior, holding hand grip, girl all hands holding hand grip / ferris wheel interior / checkout counter`（teasing.md）
- **随身遗弃物标记进行中**：场景里放"刚被放下"的道具即可宣告行为正在发生。代表性写法：`microphone laid aside, beer can laid aside`（teasing.md）
- **强迫对视小动作**：捏下巴、掰脸是调戏域的"目光控制器"，配 pov hand 即成第一人称机位。代表性写法：`hand on another's chin, cheek squash, face squeeze, pov hand`（teasing.md、coercion.md）
- **偷窥三向反应谱**：被看到者的反应决定作品气质，惊愕/恼怒/掩护三族按需取一，不混用。代表性写法：`!, @_@ / anger vein, v-shaped eyebrows, scowl / covering breasts, covering privates, hiding face`（voyeurism.md）
- **猫眼与帘子机位**：从遮挡物后取景自带偷拍叙事，门镜用 fisheye 强化畸变。代表性写法：`pov peephole, fisheye, vignetting / curtain grab, opening curtains, pov`（voyeurism.md、multi.md）
- **蒸汽天然遮点**：浴室场景蒸汽既是氛围也是遮点，湿度写足即可免打码词。代表性写法：`steam, mist, hot, fog, wet body, wet hair, soap bubbles, hair censor`（voyeurism.md）
- **痒觉调教子域**：挠痒是拘束调教的非侵入分支，用大笑+眼泪+挣扎替换色情表情。代表性写法：`tickling armpits, tickling feet, feathers, laughing, tearing up, bound`（teasing.md）

### 二、胁迫与权力表达

- **小巷壁咚环境包**：kabedon 不单独成立，配齐巷内杂物环境词才出"压迫现场"。代表性写法：`alley, brick wall, graffiti, trash can, industrial pipe, against wall, kabedon, dutch angle`（coercion.md）
- **单手压双手**：力量差用手位表达，"just one hand"是关键字眼。代表性写法：`source#just one hand holding girl's wrists, wrists pinned against wall, arms raised`（coercion.md）
- **体型差权重放大**：压迫感不足时给体型差单独加高权重，放在受方行内。代表性写法：`4::short female, petite, small body::, 1.2::back against wall::`（coercion.md）
- **把柄道具威胁**：不画裸照本身，用"手持照片"一个 tag 声明胁迫关系。代表性写法：`2::holding girl's nude photo::, cellphone, recording`（coercion.md）
- **持械恐惧构图**：凶器+受方恐惧表情+拘束暗示三件同框，第一人称只给持械手。代表性写法：`pov hand holding sex toy, huge dildo, @_@, flying sweatdrops, chain, shackles`（coercion.md）
- **面部强制操控**：掰嘴/扯舌/捏脸是胁迫域面部词族，配 forced smile 即"强颜欢笑"。代表性写法：`finger in another's mouth, mouth pull, tongue pull, forced smile, recording`（coercion.md）
- **绑架两格差分模板**：第一格写日常行走，第二格写冲突动作，2koma 承载时间线。代表性写法：`2koma, instant loss / Character 1: walking, expressionless / Character 2: cover mouth with towel, hug from behind`（coercion.md）
- **拍卖台叙事**：贩卖场景=舞台+价格牌+挂牌+牵绳，围观用 multiple others。代表性写法：`auction, stage, price tag, sign around neck, slave, kneeling, viewer holding leash`（misc.md）

### 三、宠物调教语法

- **身份核+物种插件**：项圈牵绳是身份核，耳朵/尾巴/手套/铃铛是可换装的物种插件。代表性写法：`animal collar, leash, viewer holding leash + fake animal ears, anal tail, paw gloves, neck bell`（pet-play.md）
- **人形姿势动物化**：用动物姿势词替换人类姿势词，尾巴动态词补生动度。代表性写法：`all fours, crawling, paw pose, tail wagging, kneeling`（pet-play.md）
- **牵绳端即持有者视角**：牵绳词决定谁是主人，from above+pov 完成"低头看狗"构图。代表性写法：`viewer holding leash, leash pull, leashing pov, from above, pov`（pet-play.md）
- **食盆喂食仪式**：盆+内容物+进食姿态+监视者手位四件构成完整喂食叙事。代表性写法：`pet bowl, cum in bowl, licking cum, face in bowl, source#foot on another's head`（pet-play.md）
- **骑乘式体罚**：骑背打屁股是独立构图单元，鞭痕负责讲历史。代表性写法：`riding, ride on girl's back, grabbing another's hair, spanking, slap mark`（pet-play.md）

### 四、性交场景叙事结构

- **阶段换挡词**：前-中-后各有一套专用词不可混用——imminent 系是预备、动词+器官是进行、after/cum 系是结束。代表性写法：`imminent penetration, imminent vaginal → sex, deep penetration, vaginal → cum in pussy, after sex`（sex-scenes.md、afterglow.md）
- **无露剪影位**：性行为可用剪影合法化，backlighting 系保住轮廓叙事。代表性写法：`silhouette, backlighting, see-through silhouette, from side, night`（sex-scenes.md）
- **环境支点姿势**：公共家具当姿势承托物，"抵着/靠着"词让站立位稳定。代表性写法：`against tree, against window, hands on window, leaning on piano, swivel chair`（sex-scenes.md、locations.md）
- **半浸水分层**：水中场景写"水面线"，上下半身分属两种渲染逻辑。代表性写法：`partially submerged, upper body out of water, see-through water surface, perspective water surface`（sex-scenes.md）
- **抱举位专名族**：悬空性交有专用姿势名，配抬人词锚定力量关系。代表性写法：`suspended congress, reverse suspended congress, carrying person, leg grab, full nelson`（sex-scenes.md、multi.md）

### 五、事后（afterglow）证据系统

- **精液位置梯度**：cum 的位置语序精确表达"灌了多少、结束多久"，由内到外层层溢出。代表性写法：`cum in pussy, cumdrip, cum overflow, cum pool, cum string, cum on body`（afterglow.md）
- **刚结束时间戳**：体表蒸汽+汗+床单湿痕宣告"刚刚"，配颤搐词补余韵。代表性写法：`steaming body, very sweaty, partially wet sheet, stained sheets, trembling, twitching, spasm`（afterglow.md）
- **一次性用品静物组**：避孕套+纸巾+包装袋是事后场景默认静物，数量词制造"多次"暗示。代表性写法：`used condom, multiple condoms, condom wrapper, used tissue`（afterglow.md）
- **体液容器化**：事后域把精液接入任意器皿，容器即展示叙事。代表性写法：`cum drip into cup, cum filled with cup, holding cum bottle, cum in lantern`（afterglow.md）
- **事后日常反差**：无反应日常动作+在场精液痕迹=心理状态叙事。代表性写法：`playing games, expressionless, cum in pussy, cumdrip / brushing teeth, hickey, empty eyes`（afterglow.md）
- **事后邀请姿态**：分穴展示+比v+文字是"自愿延续"的收尾变奏。代表性写法：`spreading own pussy, double v, text:"please use me", heart hands`（afterglow.md）
- **结算现场叙事**：钱币散落+肢体展示把事后变成交易现场，不用价格牌。代表性写法：`money on body, banknotes, cash, spread legs, empty eyes`（afterglow.md、misc.md）

### 六、场地场景库

- **场地固定三件套**：每个高频场地自带"场所词+专属道具+光效"固定包，缺一失真。代表性写法：`love hotel: pink theme, red heart shaped pillows, pink light / karaoke box: disco ball, microphone, neon light`（locations.md、misc.md）
- **欲望场景默认光**：夜间情色用彩色点光统一色调，粉紫是默认欲望色。代表性写法：`pink light, purple light, neon lights, rim light, dark background`（misc.md、teasing.md）
- **封闭容器的张力源**：电梯/车厢的封闭性靠"故障或人流"制造张力，光用应急灯。代表性写法：`elevator interior, power outage, emergency light / train interior, crowded`（locations.md、teasing.md）
- **亵渎感来自圣物在场**：教堂/神社/婚礼场景保留专属圣物，行为与圣物同框即亵渎。代表性写法：`gothic architecture, stained glass, veil / in church, kneeling`（sex-scenes.md、shared-service.md）
- **室内杂乱度=时间流逝**：散落生活物做"长时间停留"的进度条。代表性写法：`messy room, instant noodles, cans, trash bag, stained sheets`（afterglow.md、misc.md）

### 七、多人分场纪律（Character 字段）

- **外层公共、行内私有**：人数/镜头/场景/光照放外层串，**角色栏只写该角色的外貌与服装**；动作按 models.md §多人机制的两条硬边界例外处理——跨角色动作挂`source#`/`target#` 前缀进各自角色栏，主交互之外的角色动作进她自己的栏；其余动作留外层主串并用句子写清归属。代表性写法：外层 `2girls, from side, indoors` + 行内 `Character 1: girl, ... / Character 2: boy, ...`（全域惯例；裁决权威见 models.md §多人机制【权威】）
- **关系动词必须挂靠**：每个跨角色动作都用 source#/target# 双向声明，无挂靠动词会被随机分配给错误角色。代表性写法：`source#fingering / target#fingering`、`source#sitting on person, target#sitting on person`（yuri.md、multi.md）
- **一主多攻分区律**：N 个攻击者各守一个身体部位，每个 Character 只写一个动作动词。代表性写法：`sit on the right + lick ear / sit on the left + french kiss / kneeling between legs + cunnilingus`（yuri.md、coercion.md）
- **俯视宽景+裁肢减负**：三人以上默认 from above+full body，脚部统一裁掉降低崩坏面。代表性写法：`from above, dutch angle, feet out of frame`（multi.md、shared-service.md）
- **颜色即角色码**：两人同装时用单轴异色区分（黑白丝/红白旗袍），色写进各自行内。代表性写法：`white pantyhose / black pantyhose`、`red china dress / white china dress`（shared-service.md、multi.md）
- **旁观者要给状态**：不出手的第三人必须写情绪或自慰词，空置 Character 会变成第二主角。代表性写法：`watching nude, in heat, hand between own legs, grinning`（multi.md、sex-scenes.md）

### 八、协作侍奉与多人站位

- **cooperative 前缀**：两人协作动作用 cooperative+行为词宣告，配双人比心补默契感。代表性写法：`cooperative fellatio, cooperative paizuri, cooperative footjob, cooperative handjob, teamwork (sexual), heart hands duo`（shared-service.md）
- **服务位分区句式**：侍奉场景按身体部位分派站位，每人 Character 写"方位+动作"。代表性写法：`sit on the man's right, lick man's ear / sitting on the man's left, kissing / kneeling between the man's thighs`（multi.md）
- **贴靠接口词族**：两人身体贴合用 docking 词族，对称/错位两档，错位档适配身高差。代表性写法：`symmetrical docking, asymmetrical docking, breasts press, side-by-side`（shared-service.md、yuri.md）
- **双飞站位词典**：2girls1boy 的高频站位各有专名，选位即选构图。代表性写法：`girl sandwich + breast press / human stacking + lying on person / reverse spitroast + cunnilingus / cowgirl position + sitting on face / suspended congress + carrying / boy sandwich + double penetration`（multi.md、sex-scenes.md）
- **共享玩具博弈化**：双人共享物可写成竞技，拔河/掰腕把性行为变比赛。代表性写法：`anal beads-to-anal beads, sex toy pull / arm wrestling, remote control vibrator, vibrator in thigh strap, holding remote control`（yuri.md）
- **百合身体接口词**：百合域专用接触词，ass-to-ass 系统贯穿磨豆腐到双头龙。代表性写法：`tribadism, pussy to pussy, ass to ass, pussy sandwich, leg lock, sitting on face`（yuri.md）
- **多人邀请语**：事后展示用"任选"短语+分穴动作变成集体邀请。代表性写法：`take your pick, spread pussy, hands on own ass, looking back`（multi.md、afterglow.md）

### 九、权重惯例与域内独有招式

- **关系动词优先加权**：多人域"模型做不到"的部分集中在关系动词上，权重给到 1.4-2.0，位次高于表情环境。代表性写法：`2.0::sitting on person::, 1.71::sex from behind::, 1.5::target#pull another's panties::`（teasing.md、multi.md）
- **外层轻权、行内重权**：镜头环境用 1.05-1.16 微权放外层，Character 行内核心姿势 1.3+ 重权，形成两层权重结构。代表性写法：外层 `1.16::from side::` / 行内 `1.6::sitting on another's back::`（yuri.md、multi.md）
- **描述性短语直接入串**：复杂关系允许整个英语短语作单个 tag 进权重，比硬凑单词串稳定。代表性写法：`1.05::short female, petite, small body:: / 2::the boy between 2girls::`（coercion.md、teasing.md）
- **多人防散架负权**：多人串默认负权 multiple views/chibi，防止人群被拆成分屏或Q版。代表性写法：`-2::multiple views::, -2::chibi, doll::`（misc.md、yuri.md）
- **尺寸对比量尺叙事**：巨大器官用"参照物+反应"呈现，量尺/刻度让尺寸可读。代表性写法：`penis awe, looking at penis, penis on stomach, penis measuring, holding ruler, length markings`（misc.md、shared-service.md）
- **共感装置远程叙事**：分屏两端用同一器官连接，使用侧与受感侧各占一格各写状态。代表性写法：`telepathic sex, shared sense / split screen, penis in artificial vagina, invisible penetration, stomach bulge`（misc.md）
- **嵌套道具插入**：器物可"穿在"身体上再被使用，双层插入写 insertion 套 insertion。代表性写法：`artificial vagina in pussy, vaginal artificial vagina insertion, cum in artificial vagina`（misc.md、afterglow.md）


# 增量技法：体位/非直接交配域

以下技法从法典配方库深度提炼。括号内为相对 database/nsfw/codex/ 的出处文件。

从 codex/positions/ 与 codex/nonpenetrative/ 两域配方归纳，只收现有技法参考未覆盖的增量。

### 传教士与正上位
- **四件式体位骨架**：人数+躺姿+体位词+行为词是任何正上位串的固定底盘，抓握点与床品作变体层。代表性写法：`lying,on back,on bed,missionary,sex,spread legs,sheet grab,leg grab`（missionary.md）
- **提腿烈度梯度**：女方腿部动词按强度递进成一条轴，选档即换场面烈度。代表性写法：`leg grab → legs lift → folded → legs up → hugging own legs → leg lock,crossed ankles → piledriver (sex)`（missionary.md、breeding.md）
- **插入系第一人称机位**：男方视角固定三件+俯角，penis 特写由 pov crotch 承载。代表性写法：`pov,pov crotch,from above,just the tip,looking at penis`（missionary.md）
- **相机旋转三件**：正面镜头+倾斜+倒置组合出"头朝下的俯视脸"机位。代表性写法：`front view,dutch angle,upside-down`（missionary.md）
- **惊慌预备叙事**：尺寸威慑写"注视+惊吓符号+身体后缩"，不写心理词。代表性写法：`looking at penis,penis awe,wide-eyed,!?,spoken interrobang,leaning back`（missionary.md、train.md）

### 站立与悬空
- **悬挂双词对**：正面抱起与背后抱起是两个专词，不可混用。代表性写法：`suspended congress / reverse suspended congress`（standing.md、train.md）
- **悬空证明链**：托举类用"离地+下垂+脚部动词"证明体重存在。代表性写法：`hanging legs,feet off ground,feet doesn't touch ground,dangling arms,hanging arms`（standing.md、rear.md）
- **腿锁缠绕组**：被抱方用"腿绕腰+臂绕颈"固定成一体。代表性写法：`leg lock,legs wrapped around waist,legs locked around waist,arms around neck`（standing.md）
- **压墙压迫件**：墙系站位=贴墙+压迫点+反剪双臂+脸被按。代表性写法：`against wall,pressed against wall,arms behind back,face on wall,cheek press`（standing.md、rear.md）
- **摔跤锁具**：双臂后扳+抬腿是独立锁词，与 reverse suspended congress 连用出火车便当。代表性写法：`full nelson,reverse suspended congress,carrying person,leg grab`（train.md、misc.md）
- **体重覆压语言**：压住感用"覆压+贴紧"词组而非暴力词。代表性写法：`lying on person,back-to-chest,closely attached,boy on top`（rear.md、missionary.md）

### 坐位
- **骑坐双词对**：正面骑与背面骑各有专属词对，混写两边都不像。代表性写法：`upright straddle,sitting on lap / reverse upright straddle,reverse cowgirl position`（sitting.md）
- **膝上手部锚**：坐位的亲疏由"手上小动作"区分。代表性写法：`head pat,chin grabbing,hand on another's head,hug from behind`（sitting.md）
- **日常载体坐姿**：日常物件同时充当座椅与遮掩。代表性写法：`playing computer game,holding controller,sitting on person,stealth sex`（sitting.md）
- **弱露暗示件**：坐位可用暗示词组替代直白行为。代表性写法：`implied sex,cum string,clothed female nude male`（sitting.md）

### 后入
- **三姿势层**：后入按身体支撑面分三档，tag 组互不通用。代表性写法：`all fours / prone bone,on stomach / standing,bent over`（rear.md）
- **脸埋双件**：趴床后入的脸部处理固定两件，加咬物则更狠。代表性写法：`face in pillow,pillow grab,sheet bite`（rear.md、breeding.md）
- **抓握点权力刻度**：抓哪里决定支配等级，从手腕到角一路递进。代表性写法：`arm grab → holding another's wrist → arm held back → grabbing another's hair → head grab → headlock → grabbing another's horns`（rear.md、missionary.md）
- **伸手求救画眼**：挣扎不写动词，画一只伸向观众的手。代表性写法：`outstretched hand,reaching,reaching towards viewer,looking at viewer`（rear.md）
- **隔街透视偷窥**：从室外隔窗看屋内=方位词+透视设备词+隐秘词。代表性写法：`from outside,from below,x-ray,stealth sex`（rear.md）
- **侧躺勺式套件**：侧背后位有专名，抬腿与抚胸是固定配件。代表性写法：`spooning,lying on side,leg lift,grabbing another's breast`（rear.md）

### 种付
- **mating press 锁定套装**：种付位固定六件锁具，脚踝交叉是最强信号。代表性写法：`mating press,leg lock,crossed ankles,legs around waist,mutual hug,arms around neck`（breeding.md）
- **极限折叠白描句**：超出词库的柔体折叠直接写英文描述。代表性写法：`legs pressed past shoulders,feet almost touching back of head,u-shaped body,pancake breasts`（breeding.md）
- **受孕特写负权**：中出+受精可视化会招怪异子宫大特写，负权关闭。代表性写法：`fertilization,sperm cell,ovum` + `-2::impregnation close up::`（breeding.md、sitting.md）
- **挑衅败北双格**：第一格挑衅表情、第二格体位失态，权力反转由分格完成。代表性写法：`2koma,instant loss,split screen` + `mesugaki,smug,+++` → `folded,@_@,trembling`（breeding.md）
- **cleanup 中间态**：口交转正戏有专词衔接。代表性写法：`cleanup fellatio,kissing penis`（breeding.md）

### 骑乘
- **三核心+半蹲变体**：女上位固定三件，半蹲有独立词。代表性写法：`cowgirl position,girl on top,straddling` / `squatting cowgirl position`（cowgirl.md）
- **主导表情组**：女上位必须挂强势表情词，否则漂回被动。代表性写法：`assertive female,smug,naughty face,looking down`（cowgirl.md）
- **顶腹抚摸叙事**：插入深度用"摸自己被顶起的肚子"讲出。代表性写法：`stomach bulge,hand on own stomach`（cowgirl.md）
- **裙摆遮盖骑乘**：遮住结合部比全露稳定。代表性写法：`covered penetration,miniskirt,deep penetration`（cowgirl.md）
- **男方仰视机位**：被骑视角固定三件+女方面向镜头。代表性写法：`pov,from below,lying on bed,girl on top,facing viewer`（cowgirl.md）
- **引导插入词组**：女导男用"握手+对准+将入"。代表性写法：`penis grab,holding penis,guided penetration,just the tip,imminent vaginal`（cowgirl.md）

### 非直接交配通用语法
- **隔层公式**：任何行为加"隔着什么"即成新题材，液体落回隔层收尾。代表性写法：`footjob with legwear,sockjob,paizuri under clothes,penis over clothes` + `cum in gloves,cum on socks,cum under breasts`（footjob.md、handjob.md、paizuri.md）
- **penis on/between 接触谱系**：between 表夹合、on 表贴放，贴哪写哪。代表性写法：`penis on face,penis on navel,penis between thighs,penis between breasts,penis between buttocks`（全域）
- **after 状态族**：事后=after+行为词一枚，接痕迹与表情降级。代表性写法：`after fellatio,after paizuri,after sex` + `used condom,cumdrip`（全域）
- **承接双件**：接精必须"手型/容器"成对出现。代表性写法：`cupping hands,holding glass,cum in bucket`（oral.md、handjob.md）
- **第三者无知觉**：在场不知情者只给日常动作，信息差自己成立。代表性写法：`watching tv,drinking tea,holding strawberry cake`（oral.md）
- **多任务冷感**：边做别的边被做=冷感词+双手机制。代表性写法：`emotionless sex,bored,multitasking,holding phone,looking at phone`（rear.md、handjob.md）
- **口部象形符号**：含住状态用颜文字 tag 稳定触发。代表性写法：`:>=,:o,:q,o3o`（oral.md）
- **逐角色施受标注**：多人场景 source#/target# 按角色各写一遍，互斥动作不串人。代表性写法：`source#ankle grab,target#ball busting,mutual#ass-to-ass`（footjob.md、other.md）
- **视线方向语法**：视线词即心理定位——上视侍奉、下视支配、旁视羞耻。代表性写法：`looking up,looking down,looking away,sideways glance,eye contact`（全域）

### 足交
- **足交骨架与变体词**：核心两件+脚部特写；双足/反向/背后/隔衣各一词。代表性写法：`footjob,foot on penis,feet focus` / `two-footed footjob,reverse footjob,footjob from behind,footjob over clothes`（footjob.md）
- **足穴造穴**：并脚成穴有专词，"膝分脚合"是姿势件。代表性写法：`foot pussy,feet together,knees apart feet together,simulated footjob,presenting foot`（footjob.md）
- **踩踏词族**：碾压主题独立成组，配第一人称脚底机位。代表性写法：`stepped on,crotch stomping,ball busting,cbt,denki anma,stepping on viewer`（footjob.md）
- **女支配表情组**：踩踏/足交配"俯视+嫌恶+坏笑"。代表性写法：`femdom,looking down,disgust,evil grin,shaded face,smug`（footjob.md）
- **协助足交**：谁扶脚也写死。代表性写法：`guided footjob,holding another's foot,ankle grab`（footjob.md）

### 口交
- **深喉三件**：深度=喉部凸起+透视，侧视最稳。代表性写法：`deepthroat,throat bulge,x-ray`（oral.md）
- **逆向口交**：男上位口交有专词，配仰头与倒置。代表性写法：`reverse fellatio,irrumatio,head back,upside-down,male on top`（oral.md）
- **器官贴脸谱系**：从贴脸到遮眼到投影，烈度全靠位置词递进。代表性写法：`penis on face → penis over eyes → penis covering eyes → penis on head → penis shadow`（oral.md）
- **张嘴邀请件**：自己拉开嘴是主动邀请标准件。代表性写法：`oral invitation,fingers in own mouth,mouth pull,tongue out`（oral.md）
- **遮掩口交**：扇/纱/围巾遮嘴而行为照做。代表性写法：`covered fellatio,fellatio under mask,penis behind hand fan,scarf pull`（oral.md）
- **桌下信息差结构**：桌下桌上是两个世界，桌面物件当画框。代表性写法：`under table,stealth sex,hidden from view above table`（oral.md）
- **事后展示套装**：张嘴+伸舌+口部特写+溢出四件展示口中结果。代表性写法：`open mouth,tongue out,mouth focus,cum on tongue,cum overflow from mouth,gokkun`（oral.md）
- **侍奉位阶**：跪姿词定服务等级，配手型与视线。代表性写法：`kneeling,wariza,seiza,squatting,cupping hands,looking up`（oral.md）
- **呼气可视化**：事后余韵让吐气成雾上屏。代表性写法：`breathe out thick steam,screen fogging,sounds effect next to mouth`（oral.md）
- **唇印物证**：口红印标记"刚做完"，涂哪印哪。代表性写法：`lipstick mark on penis,smeared lipstick`（oral.md、footjob.md）

### 素股与手交
- **素股骨架+紧缝证据**：腿间行为固定两件，交叠脚踝证明夹紧。代表性写法：`thigh sex,penis between thighs,legs together,crossed ankle,cross feet`（intercrural.md）
- **浅接触变体词**：仅龟头/摩擦各有专名。代表性写法：`glansjob,frottage,grinding`（intercrural.md）
- **套物手交族**：手套/袜/内裤/袖子套上去即成新题材，射在其中收尾。代表性写法：`gloves on penis,single gloves,cum in gloves,penis under sleeves,sock on penis,white lace panty on penis`（handjob.md）
- **背后手交专名**：从背后握有专词，护理是其招牌变体。代表性写法：`reach-around,head on another's shoulder,breasts on another's back`（handjob.md）
- **握法变体**：双手/反向/只动龟头/榨取各一词。代表性写法：`two-handed handjob,reverse grip handjob,glansjob,milking handjob`（handjob.md）
- **榨精过程词**：软硬状态+液体词构成"被榨"叙事。代表性写法：`soft limp penis,prostate fluid leaking,projectile cum`（handjob.md、footjob.md）

### 乳交
- **三核心+专词变体**：挤压+夹合是骨架，站位/贫乳/免手/反向各一词。代表性写法：`paizuri,breasts squeezed together,penis between breasts` / `perpendicular paizuri,naizuri,handsfree paizuri,reverse paizuri`（paizuri.md）
- **贫乳专用通道**：贫乳必须换 naizuri 并配压平件。代表性写法：`naizuri,flat breasts,cooperative naizuri`（paizuri.md）
- **衣下乳交三路**：衣外/衣下/侧孔三种进入方式各有词，湿痕透布收尾。代表性写法：`paizuri under clothes,penis over clothes,penis under another's clothes,sideboob,cum in clothes`（paizuri.md、other.md）
- **乳交邀请件**：扒开乳沟+纽扣缝="请用"标准件。代表性写法：`paizuri invitation,spread cleavage,button gap,center opening,presenting breasts`（paizuri.md）
- **润滑前置件**：先给倒油/湿润过程件再乳交。代表性写法：`lubrication,wet breasts,oiled skin`（paizuri.md）

### 其他部位
- **臀缝交借词法**：股缝交专词不稳时借乳交词+臀部位词。代表性写法：`buttjob,penis on ass` + `1.28::ass squeezed together,paizuri::`（other.md）
- **小众部位交词表**：膝窝/腋/睾丸/尾各有专名，多数需透视辅助。代表性写法：`kneepit sex,armpit sex,balljob,tribadism,tailjob,tail around penis`（other.md）
- **乳头插入枚举句式**：统一句"[物] inserted into nipple"，物可无限替换。代表性写法：`nipple penetration` + `popsicle/syringe/sword/beads inserted into nipple`（other.md）
- **拳交深度锚**：用"抵达子宫"的透视件证明深度。代表性写法：`vaginal fisting,fist in uterus,uterus cross section,stomach bulge`（other.md）
- **隔衣射精双件**：射在衣物下=under clothes 词+湿斑词。代表性写法：`ejaculation under clothes,cum in clothes,cum stain,stained clothes`（other.md）
- **尾缠绕词组**：人外尾部行为=缠绕词+尾部位词。代表性写法：`tailjob,tail around penis,own tail between pussy,tail censor`（other.md）

### 权重与镜头惯例（本域）
- **人数打包权重**：人数词打包加权稳住多人结构。代表性写法：`1.28::1girl,1boy::,1.1::2girls::`（rear.md）
- **视角负权防漂移**：不要的机位与分屏直接负权擦除。代表性写法：`-2::pov::,-3::pov::,-1::multiple views::,-4::multiple views::`（全域）
- **拘束防断肢**：写捆绑性爱时负权排除"截肢"式误读。代表性写法：`-1::amputee::`（missionary.md）
- **高权白描构图句**：复杂机位用 2-3 权重的英文句子直接声明。代表性写法：`3::the viewer's perspective is from outside the room,peeking inside through a slightly open door::`（cowgirl.md）
- **微调权重档位序列**：本域常用 1.05→1.63 微调档，1.16/1.22 为默认双档。代表性写法：`1.05::…::,1.16::…::,1.22::…::,1.34::…::,1.63::…::`（全域）
- **弱权留用制**：怕抢戏的元素给 0.2-0.5 弱权而非删除。代表性写法：`0.2::faceless,covered face::,0.4::medium penis::,0.5::sweat::`（sitting.md、oral.md）
- **性别切换开关**：同一配方换搭档只动人数与性别头两词。代表性写法：`1boy,1girl ↔ 1.1::2 girls::,futa with female,futanari`（breeding.md）

更多主题与中文模板素材：`database/nsfw/templates/`（15 册，检索见 MANIFEST）；玩法组合规划见 [association.md](association.md)；极端主题门控见 [themes.md](themes.md)。
