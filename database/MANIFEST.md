# 数据库总索引（MANIFEST）

本文件是 `database/` 全部数据文件的定位与查询说明。查询前先把目标文件的**绝对路径**解析出来（从 skill 加载时给出的 base directory 推导），之后所有检索都用绝对路径。大文件一律用检索工具定位，不通读、不整库灌入上下文。

## tags/ —— 标签词库

| 文件 | 体量 | 内容 | 查询方法 |
|---|---|---|---|
| `tags.tsv` | 12MB / 328,023行 | **主标签库**。TAB三列 `标签名 / 中文名 / 类别码`（0=general, 1=artist, 3=copyright系列, 4=character, 5=meta），按名称字母序，UTF-8 无表头。写标签流的唯一内容标签源。**标签名是下划线形态**（`ass_ripple`、`school_uniform`） | `grep -P "\t\Q长发\E\t" "<ABS>"`（中→tag精确）；`grep -P "\t.*银" "<ABS>" \| head -20`（中文模糊）；`grep -P "^\Qschool_uniform\E\t" "<ABS>"`（tag→中）；含元字符必须 `\Q...\E` 包住。完整模式见 references/tag-flow.md §库查询 |
| `tag-aliases.csv` | 1.5MB / 32,260行 | CSV `tag,category,count,alias`（含表头；11,809 行 alias 为空）：含中日韩别名与 Danbooru 收录量。tags.tsv 的补充（别名反查）。**alias 列内含逗号，用真 CSV 解析，不要按逗号硬切** | `grep -P "^\Q1girl\E," "<ABS>"` |
| `tag-definitions.json` | 991KB / 7,660条 | **对象数组** `[{"tag": "...", "description": "..."}, ...]`，tag → 英文一句话释义（如 `{"tag": "1girl", "description": "An image containing one female character."}`）。写标签时确认语义用 | `grep -A1 '"tag": "1girl"' "<ABS>"` 或 rg 检索。**注意**：本文件是数组形态，`grep -o "\"1girl\": \"[^\"]*\""` 这类扁平映射写法**命中 0**，不要用 |
| `tags-wdv3.json` | 16MB / 140,990个tag | 独立词库，带 wdv3 验证标记。顶层为 `{metadata, validation_tags[10,857], tags{140,990 个键}}`。与主库互补（主库查不到时第二来源） | 检索：`grep -n '"tag名"' "<ABS>"`（一键一行，命中即该 tag 行） |
| `tags-wdv3-index.json` | 2.4MB / **284个分块** | tags-wdv3.json 的**完整**分块索引，按 subcategory 分组、组内字母序、每块 500 tag；缺 category 的 54 个 tag 归入 `uncategorized_N` 分组（不并入 general，避免掩盖分类缺失）。**覆盖率 100%**：`set(索引tag) == set(主文件tags键)`（140,990 / 140,990），缺失 0、多余 0。结构：`[{id, subcategory, tags:[...]}, ...]`。2026-10-06 重建——**旧版仅 395 块 / 30,914 tag（覆盖 21.9%），丢失 110,076 个 tag，不可作为检索入口** |
| `cooccurrence.csv` | 52MB / **1,904,237数据行 + 1行表头** | `tag_a,tag_b,count` 全量共现对。**三条使用要点**：① **单向存储**——每个无序对只存一次（不存反向行，全表 0 镜像 0 重复），查反向须换位（`grep -P ",\Q目标tag\E," `）；**行序为 count 全局降序（非字母序）**，`head`/`head -30` 取到的就是最高频伙伴；② **count 为整数**（数据源浮点已归一化），**存在 min=200 的阈值截断**（低于 200 的对已被丢弃——2026-10-09 由 100 提至 200 以瘦身，高频对保留完整，低频对可用基线快照找回）；③ **418 个 tag 不在 tags.tsv 主库**（累计 37,527 次引用，见 `cooccurrence-outside-tags.txt`），可经 tags-wdv3.json / tag-aliases.csv 回退查得。grep 示例：`grep -P "^\Qsolo\E," "<ABS>" \| head -30`（正向伙伴）；`grep -P ",\Q目标tag\E," "<ABS>" \| head -30`（反向） |
| `character.txt` | 224KB / 12,171行 | 角色 tag 清单，每行一个。**形态：空格形态（下划线形态 0 条）**——如 `pecorine (summer) (princess connect!)`、`seele vollerei (stygian nymph)`。与 tags.tsv 的下划线形态不同，查主库时需先把空格换成下划线（归一化后 96.1% 可命中）。检索：`grep -in "关键词" "<ABS>"` |
| `copyright.txt` | 64KB / 3,439行 | 系列/作品 tag 清单。**形态：空格形态（下划线形态 0 条）**——如 `kamen rider dcd`、`idolmaster 2`。查主库需先做空格→下划线归一（归一后 96.5% 可命中）。检索：同上 |
| `quality.txt` | 0.3KB / 28行 | 质量词清单。**本 skill 默认不写质量词，此清单仅供识别**。**与主库重合度极低：28 词中仅 1 词能命中 tags.tsv**（来自独立来源，分类口径不同），不可当作 tags.tsv 的质量词子集使用 |

## characters/ —— 角色知识库（771个md，6.4MB，约13.6万行）

原样保留六个子目录：

| 子目录 | 内容 |
|---|---|
| `00_overview/` | 库总览与已知问题说明（4个文件）：`knowledge_base_overview.md`（库总览与全库字段口径）/ `data_sources.md`（数据来源）/ `known_data_issues.md`（已知问题）/ `limitations.md`（局限性） |
| `01_guides/` | 使用指南 |
| `02_characters/` | **角色档案主体**：`index/` 44个分片索引（英文名/中文名/作品/来源行）；`by_work/` 432个作品文件（单文件≤318行）；`pooled/` 54个分片（**按「作品英文名」首字母分桶，非角色名首字母**——按角色名首字母找会进错桶） |
| `03_danbooru_tags/` | 标签表：`by_category/` 185个（general/character/copyright/meta 分类表格）+ `popularity_index/` 39个热度分片（热度仅收录量，非权重/推荐） |
| `04_nai_manual/` | NAI 手册9张：sheet_01使用说明 / 02介质感 / 03光影结构 / 04特殊人物特征 / 05画师串策略 / 06线稿决策 / 07色彩签名 / 08通用人设TAG / 09日语形状TAG |
| `05_reference/` | 字段说明与来源追溯（3个文件）：`field_dictionary.md`（字段字典）/ `category_reference.md`（类别参考）/ `source_traceability.md`（来源追溯） |

**角色检索流程**：① `grep -rn -i -F -- "角色名" "<ABS>/02_characters/index"` 定位分片与作品（**必须带 `-F`**：47.8% 的角色名含 `(` 如 `eve_(elsword)`，去掉 `-F` 或改用 `grep -E` 会静默零命中）→ ② 已知作品读 `by_work/` 对应文件，未知读 `pooled/` **作品首字母**分片 → ③ 只读该角色条目（从其二级标题到下一个角色标题前），不顺带读同页其他角色 → ④ 多个同名候选先按作品区分，仍不明确才问用户；外貌标注"来源中未提供"时不猜补。**注**：`index/` 行只含 英文名/中文名/作品/源行号，**不含文件路径**，且其"作品(EN)"字段（如 `honkai:_star_rail`）与 `by_work/` 目录名（`honkai_star_rail`）标点形态不同，需按归一化对照。

**标签表检索**：选 `03_danbooru_tags/by_category/` 下对应类别，用完整 canonical 值精确检索，只取目标行。canonical 原值保留（不要假设一定含下划线或批量替换）；`=_=`、`^_^` 等符号标签保持原样。

## prompts/ —— 真实提示词库（62MB）

| 文件/目录 | 体量 | 内容 |
|---|---|---|
| `library/` | 12个JSON / 45MB | **主推荐库**：22,864行 / 唯一 id 15,188 / 唯一内容 14,886（同一 content 可跨分类出现在多行；**条数是行数口径**，去重见 §使用约定），11分类（social-media-post 9,791 / product-marketing 5,735 / profile-avatar 2,128 / poster-flyer 1,032 / game-asset 726 / comic-storyboard 702 / infographic-edu-visual 606 / ecommerce-main-image 577 / app-web-design 242 / youtube-thumbnail 226 / others 1,099），另有 `manifest.json`（分类索引：slug/title/file/count + `totalPrompts` / `uniquePrompts` / `uniqueContents`）。JSON 为**一行一条**格式，每条含 `id / content(英文prompt正文，可含 {argument name="x" default="y"} 占位变量) / title` |
| `gpt-image-cases.json` | 约1MB / 485条 | GPT-Image 系案例库（awesome-gpt-image-2 精选，13大类，中文标题，`styles`/`scenes` 标签数组，`source` 署名） |
| `awesome-api-cases.json` | 约1.2MB / 686条 | GPT-Image 案例库第二源（7类：poster/portrait/ui/comparison/ad-creative/ecommerce/character；含 {argument} 占位变量，与 library 同构） |
| `gpt-image-gallery.json` | 约75KB / 66条 | **差异化主题册精选**（12册：research-paper-figures 学术图表 / tattoo-design 纹身 / ink-and-chinese 水墨 / cinematic-film-references 电影参考 / fashion-editorial 时尚编辑 / edit-endpoint-showcase 改图指令 / technical-illustration / architecture-and-interior / data-visualization / pixel-art / fine-art-painting / isometric），Curated 质量最高 |
| `gpt4o-selected.json` | 2.3MB / 1,050条 | 精选提示词：`items[]{id, slug, title(中文), source{name,url}, model, images(仅文件名引用), **prompts(正文，字符串数组)**, examples, notes, originFile, description, tags, coverImage}`。**注意：本文件无 `content` 字段**——正文在 `prompts` 数组内，按 `content` 检索会零命中，检索须用 `prompts` 字段名 |
| `zh-library/` | 11.6MB / 5,430条 | 中文提示词库：`prompts.part1-3.json`（各 1,810 条；`id/title(中文)/category/image/likes/themes/styles/prompt(含{}占位变量)`）+ `list.part1-3.json`（索引）+ `categories.json`（79 个分类名→`{count, major}` 的扁平映射，**无 `total` 键**）+ `meta.json`（**`total:5430` 的权威口径在此**）+ `pinyin.json`；`prompts-twitter.json` 为空数组`[]`、`twitter_manifest.json` 仅为占位 `{"files":[]}` |
| `style-library.json` | 33KB | 风格库结构化数据（风格分类/中英标签对照），nl-flow.md 风格词组库的数据源 |
| `style-cases.json` | 1.2MB | 风格案例集 |
| `twitter/` | 4个JSON | 推特抓取提示词与筛选报告（curation_report_2026-06-02/07/08.json + ingested_tweets.json） |

**检索方法**：先按 recommend.md §库路由选库 → `library/` 读 `library/manifest.json` 确定分类文件；新三库（gpt-image-cases / awesome-api-cases / gpt-image-gallery）与 gpt4o-selected、zh-library 用 `grep -n -iF "关键词" "<ABS>"` 行级定位（**全部 JSON 已归一为「一条一行」格式**，命中行即完整条目；zh-library 亦已逐条分行，2026-10-09 修复）。**注意**：本环境无 `rg`（ripgrep），文档一律以 `grep` 表述；`grep -F`（固定串）优先，含元字符的关键词务必用 `-F`。条目行较长（library 多数 ~1–12KB），终端会整行回吐，可用 `| cut -c1-300` 截断预览。**占位变量**：文档写法 `{argument name="x" default="y"}` 是解析后的形态，**原始字节中引号被 JSON 转义为 `\"`**，按文档字面 `grep -F '{argument name="'` 会零命中——检索占位条目请用 `grep -nF '{argument name=\\"'`（或先 `json.load` 再判字符串）。推荐时保留原样或按用户需求替换 default 值并说明。

## nsfw/ —— 成人内容数据（8.6MB，含 codex/；不含 codex 约 5.8MB）

| 目录/文件 | 内容 |
|---|---|
| `corpus/upper.tsv` / `lower.tsv` | 玩法/主题语料统计，**3 列** `行号<TAB><TAB>文本`（第 2 列**基本**为空，但其中 upper 8 行 / lower 39 行含章节号，非恒空——取正文恒用 `cut -f3`）。upper 12,761行 / lower 9,830行，正文自首章起、前言/目录/编者内容与来源痕迹行已剔除。联想引擎机制二的共现规划数据源 |
| `corpus/filtered-candidates.tsv` | **5 列带表头** `source / row / paragraph / categories / title`（8,161 行含表头 = 8,160 数据行；`source` ∈ upper/lower）。**`row` 字段语义不明、无法用于定位源文件**（值域 upper 100–12,859 超出 upper.tsv 的 12,761 行；`paragraph` 值为源文件首列的段落编号）。检索请按 `title` / `categories` 走，不要按 `row` 定位 |
| `corpus/cooccurrence.json` | 玩法共现表：`{generatedFrom, totalCandidates, interpretation, categoryCounts, countingNote, pairs[]}`，`pairs` 161 条、含 `a/b/count/pBGivenA/pAGivenB/lift` 六字段、单向存储。**2026-10-06 已与 filtered-candidates.tsv 对齐**：`totalCandidates: 8,160`（＝tsv 实测数据行）、22 个 `categoryCounts` 全部等于 tsv 实测（多标签重复计数，求和大于行数属正常，见 `countingNote`）。**注**：`categoryCounts` 为多标签计数，同一行可属多类 |
| `templates/00-范例.md` … `14-人格卡片.md` + `README.md` | 中文模板15册：00范例 / 01场景主题 / 02景别构图 / 03裸露液体 / 04服装专项 / 05光影氛围 / 06姿势动作 / 07表情眼神 / 08风格胶片 / 09妆容专项 / 10发型饰品 / 11瑕疵细节 / 12纹身标记 / 13道具宠物 / 14人格卡片。检索：`grep -rn "关键词" "<ABS>/templates/"` 命中后读对应小节。**原文存档**：内含 `masterpiece, best quality, 8k` 等质量前缀等历史写法，**不适用本 skill 输出规范**，参考前先剥离（同 examples/README.md 规则） |
| `presets/style-negative-presets.csv` | 142行风格与负面预设（CSV：name, prompt, negative_prompt, description, category；含 BASE 系列反3D/反furry等堆叠预设）——用户要负面词或风格预设时的素材；组合规则（Combos/Conflicts）见 negative.md §B 模式负面词 |
| `presets/nhentai-*.tsv` | 5个TSV：nhentai.net 五命名空间英文→中文对照（数据行 tags 964 / parodies 3,092 / characters 9,934 / artists 13,675 / groups 11,800，**每个文件另有 3 行 `#` 注释头**；列 `英文tag\t命名空间\t收录量\t中文(空=未翻译)`；中文覆盖：tags 221 / parodies 1,379 / characters 1,909，artists/groups 无中文）。B 模式查成人作品系列/角色中文名用；快照 2022-08，代码 Apache-2.0、译名 CC BY-SA 3.0（数据来源注记，输出仍遵守无来源铁律） |
| `presets/nhentai-tags.json` | 历史合并文件（id→中文名，138KB / 5,061 条，键为纯数字 ID）——**与上方 5 个 TSV 互补，不构成替代关系**：TSV 的 221 个中文名是本文件 5,061 个中文名的**真子集**（TSV 独有=0）。用法：`TSV` 查「英文tag→中文名」（含命名空间与收录量），本文件查中文名全集。**注意：本文件键为数字 ID，无法用 Danbooru tag 名检索** |
| `examples/` | 成人向提示词示例 9 文件 100 条（5 文件来自模板分册 60 条 + 4 文件 codex-*.md 法典精选 40 条；另有 README.md；**原文存档**——使用规则见该目录 README.md：历史写法不代表本 skill 输出规范，参考前先剥离质量前缀/年代词/下划线拼写/**出图参数行**） |

## nsfw/codex/ —— 法典配方库（约2.8MB，101文件，6,933条成品配方）

"场景 → 成品 tag 配方"实例库，**NAI 数值基准语法**（`1.2::tag::`、`Character N:` 字段、【】占位符=角色/画风待填处）。完整用法、跨模型适配、门控说明见 `references/nsfw/codex-guide.md`。

**门控**：`gated/` 23 文件受 `themes.md` 门控。另注意 **`het-series/` 并非全部通用**——其中的胁迫强制（coercion）、偷窥（voyeurism）、宠物调教（pet-play）、调戏（teasing）等章与 `gated/` 同级受限，**仅用户显式点名该主题时才展开**，不得从模糊的成人需求里自动选用。

| 子目录 | 文件数 | 内容 |
|---|---|---|
| `positions/` | 8 | 体位：正身位/站立位/坐身位/后入/火车便当/种付位/骑乘位/杂项 |
| `nonpenetrative/` | 6 | 足交/口交/素股/手交/乳交/其他 |
| `het-series/` | 8 | 异性系列：调戏猥亵/胁迫强制/宠物调教/偷窥/性交场景/事后/场地/杂项（**受限章见上方门控说明**） |
| `group-series/` | 3 | 百合/协作侍奉/双飞多飞 |
| `girl-series/` | 6 | 单女系列：隐秘展示/自慰/诱惑/露出/另类日常/杂项 |
| `outfits/` | 16 | 泳装/内衣/睡衣/改造系列/人体绘制/兔女郎/胶衣/舞娘/魔法少女/恶堕等 |
| `components/` | 2 | 男性/女性组件 |
| `viewpoint/` | 6 | 视角强调：胸腹/裙底/足底/腿背/杂项 |
| `special/` | 3 | 伪娘/futa/攻守反转（NTR 在 gated/） |
| `extreme/` | 2 | 过激玩法/RBQ |
| `bondage/` | 8 | 捆绑拘束：姿势/用具/位置/监禁/凌辱/节日等 |
| `persona/` | 6 | 人设配方：服饰/角色锚定/扶她/伪娘/人外设计 |
| `misc/` | 4 | cosplay/机械/杂项涩涩/社区串收录（含原书文末三个附录章节，无独立标题边界故合并） |
| `gated/` | 23 | **受 themes.md 门控**：睡奸/催眠/NTR/群交/兽交（总览+狗虫马等5文件）/异种6文件（触手史莱姆兽人哥布林等）/r18g重口8文件（杀害/截肢/刑罚/排泄物/血肉内脏等）——**仅用户显式点名时检索使用** |

**入库处理说明**：未成年指向条目已在入库时物理排除（成年底线，检索不应命中）；`{{}}`/`[[]]` 已归一化为数值权重。**2026-10-06 二次清洗实测**：① `charN:` 归一——codex 半角 1 处、corpus 半角 24 处 + 全角 `charN：` 3,411 处，合计 **3,436 处**已改为 `Character N:`（原值 `char1:girl,aheigao` 这类冒号后紧贴 tag 的形态最易漏配）；② 拼写错误修正 **272 处**：`m legs`→`legs` 255 处（用负向前瞻 `(?<![A-Za-z_])`，未误伤 `slim legs` / `small legs`）、`micro biniki`→`micro bikini` 6、`embrrassed`→`embarrassed` 4、`betweem`→`between` 2、`frillled`→`frilled` 2、`bressts`→`breasts` 2、`cleft of venis`→`cleft of venus` 1。**仍未处理**：`{{}}` 层叠权重括号 codex 10 处 / corpus 15,840 处——正形需逐处判断嵌套层数对应的强度，**不自动改**（见下方「待人工确认」）。历史写法不代表输出规范——质量前缀/年代词等按本 skill 铁律处理。

**不可见字符归一化（2026-10-06）**：全库已清除三类不可见字符——不换行空格 `U+00A0`→普通空格（89,956 处）、零宽空格 `U+200B`（370 处）、内嵌 `U+FEFF`（8 处），共 93 文件。**codex 标签串里的 NBSP 是重点**：修好之后 `ass ripple` 这类标签才能正常走「空格→下划线」归一化并在 `tags.tsv` 中查到（铁律1）。全角空格 `U+3000` 属正文排版（ASCII-art 对齐、日文正文），**未改动**。**零宽连接符分类处置（2026-10-06 二次清洗）**：`U+200D`（ZWJ）实测 18 处**全部是 emoji 家族序列**（👩‍💼 / 🧑‍🔧 / 🧑‍🍳 / ❤️‍🔥 / 🏳️‍⚧ / 🏳️‍🌈 等），是 emoji 的必需组成，**全部保留**；`U+200C`（ZWNJ）实测 3 处为**零宽连接符污染**（`golden embroidery‌,` / `intestine‌ bulge,`），会导致 tag 查库失败，**已全部删除**。

**查询示例**：

```bash
# 按中文场景标题检索
grep -rn "骑乘" "<ABS>/codex/positions/cowgirl.md" | head
# 按英文tag反查使用它的配方文件
grep -rln "asphyxiation" "<ABS>/codex/" --include="*.md"
# 目录级场景检索
grep -rln "温泉" "<ABS>/codex/girl-series/" "<ABS>/codex/misc/"
```

## 共现表使用注意（tags/cooccurrence.csv）

- **单向存储**：每个无序对只存一次（严格字典序），不存在 `a,b` 与 `b,a` 双向记录。查反向伙伴须换位检索。
- **count 为整数**：数据源浮点值已归一化；**存在 min=200 的阈值截断**（低于 200 的对已被丢弃——2026-10-09 由 100 提至 200 瘦身，不是「没有关联」而是「关联较弱未收录」，低频对可用基线快照找回）。
- **418 个库外 tag**：共现对中有 418 个 tag 不在 tags.tsv 主库（累计 37,527 次引用，清单见 `cooccurrence-outside-tags.txt`）。可经 `tags-wdv3.json` / `tag-aliases.csv` 按回退链查得。**联想结果命中库外 tag 时，按 tag-flow.md §库查询 的回退链走辅助库，不要直接判定为不存在。**

## tags-wdv3.json 的已知局限

- **无中文字段**：本文件不含任何中文名字段，**无法与 tags.tsv 的中文名做一致性校验**。查中文名一律以 tags.tsv 为准。
- **291 个类别冲突**：同一 tag 在两库的category 不一致（如 `7-eleven` tsv=3copyright / wdv3=general；`acrylic_paint_(medium)` tsv=5meta / wdv3=general）。**查类别以 tags.tsv 为准**，本文件仅作第二来源补充。
- **54 个 tag 无 category 字段**。

## tags.tsv ↔ tags-wdv3.json 的覆盖差

两库**互补而非包含**，检索时按回退链互查：

| 方向 | 数量 | 说明 |
|---|---|---|
| 两库交集 | 137,754 | 语义一致，可互为验证 |
|仅 tags.tsv（主库独有） | **190,269（58.0%）** | wdv3 未收录；主库更全，以主库为准 |
| 仅 tags-wdv3 | 3,236 | 主库未收录；主库查不到时按回退链查此库 |
| tag-definitions.json 独有 | 2 | 均为畸形条目（`\m/`、`\||/`）；其记载的 `byleth_(fire_emblem)`、`black_blindfold` 实测已在 wdv3 中（不在 tags.tsv），属「wdv3 独有」 |

## 使用约定

- 所有内容标签以 `tags/tags.tsv` 为主库（下划线形态）；辅助库（别名/释义/wdv3）按需补充。查库时若手头是空格形态（本 skill 的**输出**规范），先把空格换成下划线再查主库。
- 文件体量差异巨大：先检索定位、再精读命中片段；禁止把任何大文件整读进上下文。
- 检索零命中 ≠ 不存在：换模糊模式复查后再下结论（见 tag-flow.md §库查询）。
- **计数口径**：`prompts/library/` 的每个分类 `count` 与 `totalPrompts` 都是**行数**（同一 content 可跨分类出现在多行）。真实唯一素材量以 `manifest.json` 的 `uniquePrompts`(15,188) / `uniqueContents`(14,886) 为准；跨分类检索时按 `content` 去重后再推荐。**注意：`uniqueContents` 的实测值为 14,886，manifest.json 内记载的 14,890 是陈旧值（P6-6 已同步修正）**。
- **不可见字符**：数据已于 2026-10-06 归一化（NBSP / ZWSP / 内嵌 BOM 已清除）。新入库数据如再次引入，按同一规则处理后再入库。
