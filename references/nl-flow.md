# 自然语言流完整规范（Midjourney / Flux / Nano Banana / GPT-Image / Seedream / 即梦 / 可灵 / Krea）

> 本文件负责自然语言流的全部写法；模型专有差异见 models.md；混合形态见 hybrid-flow.md。
> 大文件按需分段读：`grep -n "^## " "<本文件绝对路径>"` 列节行号；日常造句只需 §二骨架 + §三模板 + §八模型偏好，§六词库仅在词穷时查。

自然语言流用连贯描述句写画面：一句承担一层信息，整段读起来"能念给人听"。画面完备优先，句数与总长度不设上限，该多就多。

## 一、总则

### 定位与分工

- **基本单元是句子，不是词串**。每个句子只做一件事：立主体、写动作、给场景、定镜头、上光线、收风格。写成逗号并列的词组堆，就退化成了劣质标签流。
- **一个凝固瞬间**：描述的是一张静止画面里的一刻。动作写成瞬间的姿态与周围环境的即时反应（衣摆扬起的弧度、溅起的水花），不写成有先后顺序的过程叙事。
- 与标签流的分工：

| | 标签流 | 自然语言流 |
|---|---|---|
| 目标模型 | NovelAI / SD全系 / Anima / NoobAI / Illustrious | Midjourney / Flux / Nano Banana / GPT-Image / Seedream / 即梦 / 可灵 / Krea |
| 基本单元 | Danbooru 标签 + 自由短语 | 完整描述句 |
| 擅长表达 | 稳定视觉属性、角色特征、二次元语感 | 动作与互动、空间关系、构图指令、概念融合、真实摄影语感 |

- **同一画面、两套措辞**：用户同时要两种形态时，内容指向同一画面，但措辞体系独立——自然语言流里不出现裸标签堆，标签流里不出现整句。

### 事实层——不编造

- 只描述能看到、能推断、能负责的内容。焦距、光圈、机身、镜头型号仅当用户给出元数据或画面证据足够明确时才写，否则转写为视觉效果：

| 不写 | 改写成 |
|---|---|
| `85mm f/1.4` | 中长焦压缩感、浅景深、背景柔和虚化 |
| `Shot on Sony A7R V` | 高解析度相机质感、自然透视、皮肤纹理保留 |
| `8K`（当作画面属性） | 只作期望生成质量表述，不声称是画面真实参数 |

- 品牌 / IP / 角色名 / 地点：内部分析时可以理解，成品默认不依赖具体名称，转写为外形、配色、服装、轮廓、材质、设计语言。
- 看不清的物体、身份、文字内容不补全；看不清就写「模糊标识」「简化图案」。
- 自检：正文里每一个具体数字和专有名词，都能指出依据吗？指不出来的删掉。

### 媒介边界

先判定媒介，再动笔。媒介定性写进收尾句，并排除最容易混淆的媒介特征：

| 媒介 | 必须排除的混淆项 |
|---|---|
| 摄影 | 3D 渲染感、插画感、过度磨皮 |
| 写实 3D | 真人摄影感、二次元、厚涂 |
| 半写实 3D | 纯二维插画感 |
| 二次元插画 | 写实摄影、复杂 3D 体积 |
| 厚涂插画 | 摄影感、矢量扁平感 |
| 扁平矢量 | 写实摄影、真实材质 |
| 产品渲染 | 生活随拍感、杂乱背景 |
| UI / 平面设计 | 摄影景深、无意义装饰 |
| 混合媒介 | 点明主导媒介，不让模型自由发挥 |

- 媒介判定不明时，选一个最接近用户意图的，并在交付说明里注明「按 X 处理」。
- 自检：把提示词给一个不知道上下文的人看，他能说出这是摄影还是插画吗？

### 边界规则

- **负面词默认不给**；用户要求时按 negative.md 处理。
- **生成参数不进正文**：采样器、步数、CFG、分辨率、seed 一概不写。MJ 尾参（`--ar`、`--niji`、`--stylize`）属于提示词内语法，正常使用；其他模型要表达画幅，用一句构图语言（`a wide 16:9 horizontal composition`）或留给出图端设置。
- **质量前缀一律不写**：masterpiece、best quality、8k、超高画质等泛质量词不进正文。质量感通过具体视觉细节承载——皮肤毛孔纹理、织物织纹、可控的光比、干净的反射。

## 二、统一结构骨架

本节八段是 **models.md §组装顺序总则 六段通则的自然语言流展开版**；遇到冲突以总则为准。推荐顺序（八段）：

| 段 | 信息层 | 职责 | 常用落位 |
|---|---|---|---|
| 1 | 主体与关键特征 | 一句话立住「谁/什么」：身份、数量、最抓眼的 2—3 个特征 | 首句，锚点主场 |
| 2 | 动作与互动 | 凝固瞬间正在发生的事；谁对谁、对物做什么；肢体与道具关系 | 第 1—2 句 |
| 3 | 外貌细节 | 发型发色、五官特征、表情视线、年龄感与肤色 | 主体确定后立即跟 |
| 4 | 服装与材质 | 服装轮廓与层次；关键材质与质感（湿、哑光、透明、织物纹理） | 外貌之后 |
| 5 | 场景与氛围 | 地点、时间、天气、环境实体；情绪由场景元素承载 | 中段 |
| 6 | 构图与镜头 | 景别、机位、透视、景深；主体位置与占比；前景/中景/背景 | 光线之前 |
| 7 | 光线与色彩 | 光源方向与软硬、光比；主色—辅助色—点缀色、冷暖与饱和 | 收尾前 |
| 8 | 风格与媒介收尾 | 媒介定性 + 风格词组 + 后期质感；必要时一句反向划清媒介边界 | 末句 |

骨架的英文形态：

```
A [风格定性] [主体] [动作/姿态], [外貌细节].
[服装与材质句].
[场景与氛围句], [前景/背景空间关系].
[构图与镜头句].
[光线与色彩句].
[风格与媒介收尾句].
```

中文同构：主体与关键特征 → 动作与互动 → 外貌 → 服装材质 → 场景氛围 → 构图镜头 → 光线色彩 → 风格媒介。

### 锚点前置原则

- 写前从 12 维（§五）里挑出 **3—5 个最影响相似度的要素**，写进提示词**前 1/3**。首句就是锚点主场，不是铺垫。
- 锚点优先级（从高到低挑）：
  1. 独特构图 / 画面结构
  2. 主体轮廓、姿态、比例
  3. 特殊镜头关系（视角、透视、遮挡）
  4. 标志性光线
  5. 关键材质
  6. 背景几何
  7. 色彩关系
  8. 空间层次
  9. 由具体元素构成的情绪
- 验收标准：**删掉后半段，画面还成立**——说明锚点放对了位置。
- 反模式：八个段每段都写一点、平均用力 → 模型注意力被稀释，命中率反而下降。**宁可五个维度写透，不要十二个维度写平。**

### 顺序的容错性

- 八段是**推荐顺序，不是硬门禁**。各模型对不同位置的敏感度不同：多数模型对开头的权重最高；Flux / GPT-Image 系对全文空间关系的解析更均匀；MJ 对前几个意象最敏感。**硬规则只有一条：锚点永远前置**（总则六段的第一段身份不可后移）。其余段落在多数模型上互换不致命，但要遵守两条软规则：
  - 同类信息保持相邻（构图与镜头相邻、光线与色彩相邻），不把同一层拆到首尾两处。
  - 每个维度的信息一次性写完，不回头补述——回头补述等于稀释。

### 句法纪律

- 具体名词与动词优先，形容词必须落到可画的特征上。
- 一句一层信息，不贪多；长句可以，但长在细节密度上，不长在从句套从句上。
- 方位与空间关系写明确：谁在左、谁在右、什么最靠近镜头、背景里有什么。
- 抽象词不裸奔（落地方法见 §八）。

## 三、句式模板库

模板是脚手架，不是填空题：按需取用、删掉不相关的层，段的顺序遵循 §二 的八段骨架。

### 通用模板

```
A [风格定性] [主体] [动作/姿态], [外貌细节].
[服装与材质句].
[场景与氛围句], [前景/背景空间关系].
[构图与镜头句].
[光线与色彩句].
[风格与媒介收尾句].
```

- 前两句必须含全部锚点；后面各段按需展开。
- 人数写进首句（`a lone figure`、`two women`）；多人时每人给一句身份锚点与位置（`on the left` / `on the right`），互动写明谁对谁做什么，不写「两个人」就完事。

**八段落地范例**（同一画面，段落顺序即信息顺序）：

```
Two high school girls in identical uniforms sit side by side beside a classroom window, one turned toward the other with a smile. Soft late afternoon light falls across the empty desks behind them, dust suspended in the beams. The room is quiet and empty, chairs pushed in at the rows, chalkboard still showing the last lesson's notes. Medium shot at eye level, both figures framed to the left of the window. Warm muted palette, film photograph with visible grain, shallow depth of field. --ar 16:9
```

- 第 1 句 = 主体与关键特征 + 动作互动（锚点全在这句，两个「制服相同」的身份锚点也在这句）
- 第 2 句 = 光线；第 3 句 = 场景氛围（`quiet and empty` 是氛围不是环境词堆砌）
- 第 4 句 = 构图镜头（`framed to the left of the window` 把人物与窗的空间关系钉住）
- 第 5 句 = 风格与媒介收尾（`film photograph with visible grain` 是媒介定性，**不是** `masterpiece`/`best quality` 那类被铁律禁掉的质量前缀）
- 八段不必写满：没有 Chalkboard 细节的画就别硬加，每段按需展开

### 人像

- 开头 `A portrait of ...` / `A close-up portrait of ...`，先把脸立住。
- 中段写神态与视线：`gazing calmly at the camera`、`a faint, unreadable smile`。
- 皮肤与年龄线索写实：`natural skin texture with visible pores`，不做磨皮式描述。
- 结尾收镜头与光：`shallow depth of field`、`soft window light from the left`。

### 风景

- 开头 `A sweeping view of ...` / `A vast landscape of ...`；画面主体可以是人烟、建筑或自然本身。
- 前中后三层各给一句：前景一个近距实体、中景主结构、背景退远的天际线或山影。
- 结尾交代时刻与天气：`at golden hour after rain, mist settling in the valley`。

### 产品 / 静物

- 开头 `A studio product shot of ...` / `A still life of ...`。
- 材质与表面细节是主角：`matte ceramic surface with fine speckles`、`condensation droplets on chilled glass`。
- 布光写清软硬与方向：`three-point softbox lighting`、`hard side light with controlled reflections`。
- 承载面与背景给足留白：`on a pale marble surface, neutral grey background, generous negative space`。
- 道具做减法：只留支撑卖点的道具，不写会抢识别度的杂物。

### 动作 / 叙事场景

- 先钉住凝固瞬间：`the instant she turns around`、`mid-leap, both feet off the ground`。
- 再写动势与环境的即时反应：`her coat flaring`、`papers scattering across the wet pavement`。
- 场景细节要支撑叙事而不是装饰：谁、在哪、何时、发生了什么，都要能从画面里读出来。
- 机位收尾带上运动感：`low-angle shot with slight motion blur at the edges`。

### 海报 / 图文设计

- 先声明成品形态与画幅：`a vertical 9:16 campaign poster`、`a minimalist exhibition poster`。
- 主视觉一句立住；排版层级写清：主标题、副标题、信息层各自的位置与占比。
- **画中文字用双引号原样写入**，拼写逐字准确：`the headline "夏日限定" in bold serif, placed at the top third`。文字要少而准，多余装饰性文字不写。
- 概念字体海报让文字当主视觉：`the title itself forms the main visual structure`。
- 配色克制、留白充足：`a restrained two-color palette with disciplined whitespace`。

### 角色工作表（多视图）

- 开头 `A character sheet of [角色], full-body front, three-quarter, side and back views on one sheet`。
- 身份锚点逐项锁：年龄段与体型、脸型五官、发型发色、服装轮廓、随身道具。
- 跨分格一致性写明：`the same character with identical face, hairstyle, body proportions, outfit and color scheme across all panels`。
- **分格展示的视觉联系**（多格不散的三件）：一张主锚图压阵 + 贯穿色统一（同一主色出现在每个分格）+ 实物载体串联（线索板、相册页、拍立得摊开——分格"贴"在一个可见物体上）；表情集合/换装表尤其需要载体。
- 纯色背景、均匀布光：`plain neutral background, even studio lighting, no environmental clutter`。
- 跨图一致性的完整手段见 consistency.md。

## 四、复杂度分级

先判断用户要什么，再决定输出形态；不要把所有输入都强行套进复杂模板。

| 级别 | 形态 | 信息量 | 适用场景 |
|---|---|---|---|
| L1 极简 | 单句 | 4—6 个信息点 | 快速试稿、社媒配图、用户只要一句 |
| L2 标准 | 一段 3—6 句 | 八段全走、每段一句 | 日常生成的默认形态 |
| L3 详细 | 一到两段 6—10 句 | 八段写透 + 材质/空间/情绪全部具体 | 商业交付、高质量需求 |
| L4 穷举 | 连续 450—700 字自然语言 | 12 维逐项落地，空间关系全部显式 | 反推重构、高还原需求、关键生产资产 |

- **L1 极简**：`[主体与关键特征]，[核心风格]，[场景或构图]，[光影或氛围]`。锚点就是这一句的全部——挑最抓画面的 3—4 个要素压进一句话。
- **L2 标准（默认）**：按 §二 八段骨架走，一段连贯的话。每段允许合并（光线与色彩并一句、构图与镜头并一句）。
- **L3 详细**：在 L2 基础上加密度——材质给到质感记忆点、空间给到三层遮挡关系、情绪给到具体视觉来源；锚点仍在前 1/3。
- **L4 穷举**：每个维度都有明确落句；前景、中景、背景的遮挡、尺度、空气透视全部写清；色彩写到主色、辅助色、点缀色与光比的层级。信息多但不能平铺——锚点密度依然要高于其余部分。
- 用户明确说「只要一句 / 简单点」→ 只出 L1，不附加结构。用户没说 → 默认 L2，重要任务升 L3。
- 任何级别都遵守：锚点前置、无抽象词裸奔、无标签堆。

## 五、12 维检查框架

写前当清单挑维度，写后当补全清单查遗漏。按需取用，不机械塞满；每条末尾标注其在八段骨架中的落位。

**与 SKILL.md 要素清单的关系**：12 维是生成工作流「要素清单」（SKILL.md 工作流 A）在自然语言流的特化视图——主体/动作对应其主体与姿势动作层，环境对应场景层，构图/镜头对应构图镜头层，光线/色彩/材质/空间/情绪/后期是 NL 流的表达强项维度，风格对应风格画师层。层次划分以 SKILL.md 要素清单为权威基座，此处分维度细化。

**第 0 步 · 用途判定**：广告素材 / 游戏美宣 KV / 社媒内容图 / 产品商拍 / 人像写真 / 电影剧照 / 插画海报 / 3D 角色美宣 / 电商主图 / 建筑室内 / 食物摄影 / 动物摄影 / 风景城市 / 平面设计。用途决定该强调叙事、商业展示、人物表现、产品结构、空间设计还是视觉传播，也决定复杂度级别。

1. **主体**：人物 / 产品 / 动物 / 食物 / 建筑 / 风景 / 城市场景 / 交通工具 / 植物花卉 / IP 潮玩 / 平面视觉 / 多主体混合。只分析与该主体类型相关的专项——没有人就不写表情视线手脚，没有产品就不写包装卖点，没有动物就不写毛发眼神。→ 第 1 段。
2. **动作**：主体正在做什么；姿态、肢体走向、与道具和环境的互动；瞬间的受力与动势。→ 第 2 段。
3. **环境**：室内外、地点类型、时间、季节、天气；环境实体清单（至少 3 个撑起空间）。→ 第 5 段。
4. **构图**：画幅横竖；主体位置与占比；中心 / 三分法 / 对称 / 对角线 / 框架式 / 散点；横线、竖线、斜线、三角形、S 形、放射线结构；视觉重心与动线；元素的大小、遮挡、重复、平衡、层级。→ 第 6 段。
5. **镜头**：平视 / 俯视 / 仰视 / 顶视 / 鸟瞰；特写 / 半身 / 中景 / 全身 / 远景；广角感 / 自然透视 / 空间压缩；近大远小与透视汇聚；透过玻璃、窗、门缝、树叶观看；倾斜机位与运动感。→ 第 6 段。
6. **光线**：主光方向；硬光 / 柔光 / 逆光 / 侧光 / 顶光 / 环境光；自然光 / 棚拍三点布光 / 窗光 / 霓虹 / 体积光；轮廓光、补光、局部高光、阴影落点；光比与冷暖；光线如何塑造体积、材质、空间、情绪。→ 第 7 段。
7. **色彩**：主色 / 辅助色 / 点缀色；冷暖倾向；饱和度、明度、对比度；单色 / 互补 / 邻近 / 冷暖对比；色彩如何引导视线、分离主体、构成情绪。→ 第 7 段。
8. **材质**：皮肤、毛发、布料、皮革、金属、玻璃、陶瓷、木材、石材、水面、液体、冰、雾、烟、花瓣、露珠、屏幕、食物表皮。写出反光、粗糙、湿润、透明半透明、磨砂、柔软、硬质、颗粒、褶皱、油光、霜感；识别最重要的**质感记忆点**写透。→ 第 4 段。
9. **空间**：背景清晰度与虚化程度；前景虚化；主体与背景分离；光斑、雾气、烟雾、渐变阴影、树影、反射；前中背景之间的遮挡、尺度、空气透视；背景承担信息还是氛围。→ 第 5、6 段。
10. **情绪**：整体情绪**及其具体视觉来源**——写「孤寂」就说清是广角空旷构图 + 冷调低饱和 + 单一微小主体。抽象词不落地等于没写。→ 第 5 段。
11. **风格**：媒介定性 + 风格词组（词组库见 §七）+ 排除混淆媒介。→ 第 8 段。
12. **后期**：颗粒 / 辉光 / 柔焦 / 运动模糊 / 胶片感 / 色差 / 镜头眩光；商业精修 / 电影调色 / 产品精修；清晰度与细节密度以具体质感表述，不写泛质量词。→ 第 8 段。

**补全技巧**：写完后按 1→12 快速过一遍，问「这一维用户会不会默认期待？」——会而没写，补一句；不会，跳过。画面糊成一团、注意力分散时反向操作：砍维度，留 5 个写透。

## 六、中英词汇银行

**用法**：词穷或需要中英对照时查这里。按需取 3—5 个精准词织进句子，不要整段照抄——**精准 > 华丽 > 数量**，一个「光比 4:1 的硬质侧光」胜过五个「电影感 高级 氛围 大片」。

### 风格 / 媒介

| 中文 | English |
|---|---|
| 电影感写实 | Cinematic Realism |
| 商业广告质感 | Commercial Advertising Look |
| 复古胶片 | Vintage Film |
| 赛博朋克 | Cyberpunk |
| 蒸汽朋克 | Steampunk |
| 水墨国风 | Chinese Ink Painting |
| 敦煌壁画 | Dunhuang Mural |
| 暗黑哥特 | Dark Gothic |
| 超现实主义 | Surrealism |
| 极简主义 | Minimalism |
| 波普艺术 | Pop Art |
| 厚涂油画 | Impasto Oil Painting |
| 二次元赛璐璐 | Anime Cel Shading |
| 3D 写实渲染 | Photorealistic 3D Render |
| 像素艺术 | Pixel Art |
| 黏土定格 | Claymation |
| 纸艺拼贴 | Paper Collage |

### 色彩

| 中文 | English |
|---|---|
| 霓虹冷色调 | Neon Cool Tones |
| 金红暖色调 | Gold-Red Warm Tones |
| 莫兰迪灰调 | Morandi Muted Tones |
| 马卡龙粉彩 | Pastel Macaron Colors |
| 黑白高对比 | High-Contrast Black & White |
| 赛博紫蓝 | Cyber Purple-Blue |
| 森系绿调 | Forest Green Tones |
| 日落橘粉 | Sunset Orange-Pink |
| 深海蓝绿 | Deep Ocean Teal |
| 复古棕褐 | Vintage Sepia |
| 双色调 | Duotone |
| 低饱和高级灰 | Desaturated Muted Grey |

写色彩用三段式：主色 → 辅助色 → 点缀色，并说明冷暖与饱和度倾向。

### 光影

| 中文 | English |
|---|---|
| 黄金时刻光 | Golden Hour Light |
| 蓝调时刻 | Blue Hour |
| 影棚三点布光 | Studio Three-Point Lighting |
| 柔光箱 | Softbox Light |
| 硬质侧光 | Hard Side Light |
| 逆光剪影 | Backlight Silhouette |
| 轮廓光 / 边缘光 | Rim Light |
| 体积光束 | Volumetric Light Beams |
| 丁达尔效应 | Tyndall Effect Rays |
| 霓虹灯光 | Neon Lighting |
| 窗光 | Window Light |
| 月光冷光 | Moonlight Cold Glow |
| 篝火暖光 | Campfire Warm Glow |
| 荧光生物光 | Bioluminescent Glow |
| 伦勃朗光 | Rembrandt Lighting |
| 明暗对比法 | Chiaroscuro |
| 屏幕光反打 | Screen Glow Fill |
| 漫射柔光 | Diffused Soft Light |

### 镜头 / 构图

| 中文 | English |
|---|---|
| 特写 / 近景 | Close-up |
| 半身 / 中景 | Medium Shot |
| 全身 / 远景 | Full Shot / Wide Shot |
| 极低机位仰拍 | Extreme Low Angle |
| 俯拍 / 顶视 | High Angle / Top-Down |
| 鸟瞰 | Bird's-eye View |
| 平视 | Eye-level |
| 荷兰角 | Dutch Angle |
| 三分法 | Rule of Thirds |
| 中心构图 | Center Composition |
| 对称构图 | Symmetrical Composition |
| 框架式构图 | Framing Composition |
| 引导线 | Leading Lines |
| 浅景深 | Shallow Depth of Field |
| 深焦 | Deep Focus |
| 广角感 | Wide-angle Feel |
| 空间压缩感 | Lens Compression |
| 微距 | Macro |
| 前景遮挡 | Foreground Occlusion |
| 负空间留白 | Negative Space |

### 材质 / 质感

| 中文 | English |
|---|---|
| 次表面散射 | Subsurface Scattering |
| 景泰蓝珐琅 | Cloisonné Enamel |
| 磨砂玻璃 | Frosted Glass |
| 拉丝金属 | Brushed Metal |
| 阳极氧化铝 | Anodized Aluminum |
| 做旧皮革 | Weathered Leather |
| 粗麻布 | Burlap |
| 丝绒 | Velvet |
| 陶瓷釉面 | Glazed Ceramic |
| 混凝土 | Raw Concrete |
| 水磨石 | Terrazzo |
| 湿润表面 | Wet Surface |
| 凝露水珠 | Condensation Droplets |
| 皮肤毛孔纹理 | Skin Pores Texture |
| 胶片颗粒 | Film Grain |

### 情绪 / 氛围

| 中文 | English |
|---|---|
| 宁静 | Serene |
| 压抑 | Oppressive |
| 史诗感 | Epic |
| 孤寂 | Solitary |
| 温暖 | Cozy |
| 疏离 | Detached |
| 张力 | Tense |
| 神圣 | Sacred |
| 荒诞 | Absurd |
| 怀旧 | Nostalgic |
| 未来感 | Futuristic |
| 梦幻 | Dreamlike |

**硬约束**：情绪词必须配具体视觉来源。写「孤寂」时要说清是广角空旷构图 + 冷调低饱和 + 单一微小主体。

### 角色与服装

| 类别 | 中文 → English |
|---|---|
| 角色 | 赛博少女 Cyberpunk Girl ｜ 机甲战士 Mecha Warrior ｜ 古风仙子 Ancient Fantasy Fairy ｜ 精灵弓手 Elf Archer ｜ 星际探索者 Interstellar Explorer ｜ 末日幸存者 Post-Apocalypse Survivor |
| 发型 | 长直黑发 Long Straight Black Hair ｜ 双马尾 Twin Tails ｜ 银白短发 Silver-White Short Hair ｜ 丸子头 Bun ｜ 半扎发 Half-Up Half-Down ｜ 辫发 Braided Hair |
| 表情 | 冷漠淡然 Cold and Indifferent ｜ 温柔微笑 Gentle Smile ｜ 霸气凛然 Domineering Presence ｜ 忧郁沉思 Melancholic Contemplation ｜ 俏皮可爱 Playful ｜ 坚定执着 Determined |
| 服装 | 汉服 Hanfu ｜ 和服 Kimono ｜ 商务西装 Business Suit ｜ 晚礼服 Evening Gown ｜ 机能风 Techwear ｜ 学院风 Preppy ｜ 工装 Workwear |

### 场景与环境

| 中文 | English |
|---|---|
| 雨夜霓虹街巷 | Rainy Neon Alley |
| 霓虹都市天际线 | Neon City Skyline |
| 古刹禅院 | Ancient Temple Courtyard |
| 赛博贫民窟 | Cyberpunk Slum |
| 星舰舰桥 | Starship Bridge |
| 荒原废墟 | Post-Apocalyptic Ruins |
| 竹林小径 | Bamboo Forest Path |
| 悬浮群岛 | Floating Islands |
| 极简白色影棚 | Minimal White Studio |
| 复古咖啡馆 | Retro Cafe Interior |

### 后期与画质

| 中文 | English |
|---|---|
| 电影调色 | Cinematic Color Grading |
| 青橙调 | Teal and Orange Grade |
| 胶片颗粒 | Film Grain |
| 柔焦 | Soft Focus |
| 辉光 | Bloom |
| 色差 | Chromatic Aberration |
| 镜头眩光 | Lens Flare |
| 运动模糊 | Motion Blur |
| 商业精修 | Commercial Retouch |
| 高细节密度 | High Detail Density |

`8K`、`超高细节` 只能作为期望生成质量描述，不能声称是画面真实参数。

### 构图与画面动词

把构图、光线、空间关系自然织进句子的动词：

| 中文 | English |
|---|---|
| 占据画面中央 | dominates the center of the frame |
| 锚定在左侧 | anchored on the left |
| 被……框住 | framed by ... |
| 退向远方 | receding into the distance |
| 虚化成光斑 | dissolving into soft bokeh |
| 被光照透 | backlit and translucent |
| 笼罩在……里 | bathed in ... |
| 掠过表面 | glancing across the surface |
| 融入背景 | blending into the background |
| 被裁在腰际 | cut off at the waist by the frame |

## 七、风格词组库

### 选择逻辑

1. 先按**用途**匹配类目：成品海报 / 商品图 / UI / 信息图 / 人像 / 角色 / 建筑 / 叙事场景 / 古风 / 出版物……
2. 再按**视觉词**匹配风格：写实 / 3D / 插画 / 古典 / 品牌 / 海报 / 界面……
3. 再按**语境**匹配场景：商业 / 教育 / 社媒 / 叙事 / 历史 / 创意……
4. 需求模糊时，给 2—3 个最强的风格方向让用户选，再写成品。

### 分类与核心词组

每类给出可直接嵌入句子的英文风格词组。**风格词不配构图等于没写**——选完词组，回头检查构图、配色、笔触是否落实。

**写实摄影**：`documentary photography`、`candid street photography`、`cinematic realism`、`commercial product photography`、`believable imperfections`、`natural skin texture`。要点：写清机位距离、光源、质感、背景与动作；纪实感靠可信的小瑕疵支撑；商业美妆之外避免磨皮塑料感。

**插画与艺术**：`anime illustration`、`watercolor illustration`、`Chinese ink wash painting`、`decorative flat illustration`、`visible brushstrokes`、`hand-painted texture`、`stylized proportions`。要点：风格词必须与构图、配色、笔触材质、情绪同句落实；使用参考图时先声明要保留的特征并锁定角色识别。

**3D 与潮玩**：`3D render`、`collectible figure`、`blind-box toy character`、`matte vinyl material`、`soft studio lighting`、`display base`、`subsurface scattering`。要点：锁脸部与服装锚点；指定材质、包装、底座、收藏比例；避免没有身份细节的通用玩具感。

**海报与排版**：`typography-driven poster`、`key visual`、`title as the main visual structure`、`clean layout with disciplined whitespace`、`bold sans-serif headline`、`ink double exposure`、`portrait silhouette blended with ink texture`。要点：锁定主体、标题、版式、配色、画幅；画中文字双引号原样写、逐字准确；要成品海报就不要拼贴展示板感；非必要不加文字。

**商品与电商**：`hero product shot`、`packaging visual`、`clean studio lighting`、`selling-point layout`、`minimal supporting props`。要点：主商品、卖点标签、辅助道具分层；道具不削弱商品识别；包装文字少而准。

**品牌与标志**：`logo design`、`brand identity board`、`application mockup`、`one palette and one typography logic across all panels`。要点：品牌名与文字准确；变体克制、配色统一；面板间共享同一套字体逻辑。

**UI 与界面**：`app screen mockup`、`dashboard UI`、`status bar and tab layers`、`readable interface text`。要点：锁定平台、比例、层级和全部可见文字；避免平台描述过泛。

**信息图表**：`infographic`、`explainer diagram`、`labeled modules connected by arrows`、`short labels with generous spacing`。要点：先限制模块数量（3—5 个）再补视觉细节；用色块、箭头、图标和留白控制复杂度；不把长段正文塞进画面。

**建筑与空间**：`architectural visualization`、`interior render`、`isometric city map`、`material and lighting define the space`。要点：定视角、尺度、材质、光线、空间功能；概念图之外避免不合理透视；地图类锁定标签语言与相对位置。

**场景叙事**：`narrative scene`、`storyboard frame`、`environmental storytelling`、`details that support the story`。要点：写清谁、在哪、何时、冲突、情绪、机位；避免通用幻想背景；让故事线索在画面里可见。

**历史与古风**：`ancient Chinese scroll painting`、`dynasty costume`、`classical ink atmosphere`、`album-leaf format`、`poetic negative space`。要点：指定朝代、服饰制度、器物参考、版式与文化气质；明确长卷、册页或海报形式；避免朝代混搭与随机现代物件。

**文档与出版**：`editorial page layout`、`encyclopedic plate`、`technical manual page`、`typography hierarchy aligned to a grid`。要点：定义页面尺寸、分栏、图表系统与字体层级；字少而可读；图表与说明对齐页面网格。

## 八、模型句式偏好速览

各模型的完整专有规则、禁忌与官方格式见 models.md；此处只列影响造句的差异。

| 模型 | 语言 | 句式偏好 | 要点 |
|---|---|---|---|
| Midjourney | 英文 | 精炼、意象密集的一两句，删虚词 | 尾参属提示词内语法：`--ar 16:9`、`--niji 6`（二次元）、`--stylize`（风格化强度）；不写尾参之外的任何参数 |
| Flux / Nano Banana / GPT-Image | 英文 | 完整句子 + 显式空间关系 | 位置用 `on the left` / `behind her` / `in the foreground` 写明；吃长句与细节密度；不加尾参 |
| Seedream / 即梦 / 可灵 | 中文 | 与英文同构的八段中文句 | 方位同样写明（「画面左侧」「她身后」）；不加尾参 |
| Krea | 中文 | 一段完整连贯的中文（普通插画） | 细节规则见 models.md |

### 抽象词落地（所有模型通用）

「高级感」「电影感」「氛围感」「大片感」这类词不能裸写，必须用 2—3 个具体视觉元素解释：

- 高级感 → 低饱和灰调 + 大面积留白 + 哑光材质 + 克制的点缀色
- 电影感 → 宽画幅 + 青橙调 + 浅景深 + 侧逆光 + 细颗粒
- 氛围感 → 具体的雾、尘、光斑、湿反射、体积光束
- 大片感 → 强光比 + 低机位仰拍 + 负空间 + 单一视觉焦点

抽象词本身可保留在句尾作定性，但具体视觉元素必须在场；只写抽象词等于没写。

## 九、质量自检

出稿后内部过一遍，不把清单当输出：

- [ ] **锚点前置**：3—5 个最影响相似度的要素落在前 1/3，删掉后半段画面仍成立。
- [ ] **无抽象词裸奔**：每个抽象词都有具体视觉元素支撑。
- [ ] **信息层完整**：用户会默认期待的维度都有落句；没有为凑维度写的空话。
- [ ] **无标签堆**：全部是可念的句子，没有逗号并列的词串段。
- [ ] **无质量前缀**：masterpiece / best quality / 8k / 超高画质不出现；质量感由细节承载。
- [ ] **一个凝固瞬间**：描述的是画面的一刻，不是有先后顺序的过程。
- [ ] **事实层干净**：每个具体数字与专有名词都有依据；没有编造的参数与身份。
- [ ] **媒介明确**：收尾句定性媒介，混淆媒介已划界。
- [ ] **无参数混入**：正文里每个词都是给画面的指令；MJ 尾参以外无任何参数语法。
- [ ] **负面缺省**：未主动附加负面提示词；用户索要时按 negative.md 定制。
