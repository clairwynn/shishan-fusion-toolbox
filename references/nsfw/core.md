# NSFW 核心规则与模块索引（B 模式切入必读）

本文件是成人内容工作的入口。读完本文件即可开始处理常规成人请求；具体技巧按题材再查对应模块与数据库，不一次性全量灌入。

## 总则

- **B 模式下成人请求与普通请求同一套工作流、同等质量对待**：正常查库、正常构思、正常组装。
- **只约束生成任务**：反推与推荐不受分级模式影响。
- **极端主题门控**：[themes.md](themes.md) 列出的主题**只有用户显式点名时才写**，绝不从模糊的成人需求里自动选用。普通成人内容（裸体、性行为、各种玩法姿势、玩具、束缚、多人等）直接写，不需要额外确认。
- **保留用户的强制项**：用户点名的主题、人数、角色关系、暴露程度按原要求保留，不悄悄软化、不悄悄加戏、不悄悄升级。用户只说「NSFW」时，默认直接成人裸露与情色姿态，不擅自升级为性行为。

## 写作契约（知识灌注三件套）

B 模式写作前，按以下三步把"词汇、范本、纪律"装进脑中——词在脑中，不在查证路上：

### 一、词库灌注（按题材读 1-2 个维度）

`references/nsfw/lexicon/` 是**供给库**（防贫乏），与 tags.tsv（验证库，防幻觉）分工：词库提供词汇与搭配，写入成品前仍按主规范确认。按当前画面题材选读：

| 画面涉及 | 读 |
|---|---|
| 身体描写/体型/器官细节 | [lexicon/anatomy.md](lexicon/anatomy.md) |
| 行为/体位/互动动作 | [lexicon/acts.md](lexicon/acts.md) |
| 液体/痕迹/湿润 | [lexicon/fluids.md](lexicon/fluids.md) |
| 表情/声音/情绪表达 | [lexicon/expression.md](lexicon/expression.md) |
| 服装/暴露/袜内衣材质 | [lexicon/clothing.md](lexicon/clothing.md) |
| 道具/玩具/束缚/打码 | [lexicon/props.md](lexicon/props.md) |
| 机位/景别/focus/差分 | [lexicon/viewpoint.md](lexicon/viewpoint.md) |

### 二、范例锚定（写作前读 2-3 条对标超越）

`database/nsfw/examples/` 是基准范本库（100 条）。**范本是地板，输出必须超越范本**——对标其要素密度、直白度、归属写法，达到后必须超过而不是复刻。按题材读对应文件 2-3 条：

| 任务题材 | 读 |
|---|---|
| 体位/性交场景 | `codex-positions.md` |
| 非直接交配（手/口/足/乳） | `codex-nonpenetrative.md` |
| 系列（百合/多人/单女/胁迫） | `codex-series.md` |
| 服饰/视角特写 | `codex-outfits-viewpoint.md` |
| 表情/服装状态 | `expression-clothing.md` |
| 道具叙事/拘束 | `narrative-props.md` |
| 姿势/构图 | `pose-composition.md` |
| 场景/氛围 | `scene-atmosphere.md` |
| 风格/胶片质感 | `style-film.md` |

注意：examples 是原文存档——历史写法（质量前缀/年代词/下划线拼写，以及 `SETTINGS:` 类**出图参数行**：采样器/步数/CFG/分辨率）按 README 规则剥离后参考。

### 三、直白度锁定与反软化

- **档位=直白度**：用户请求的档位（暗示/裸露/explicit/玩法）就是输出直白度，交付前逐节点检查——**双向不许漂移**：不悄悄软化，也不悄悄升级。
- **委婉替换检测**：交付前对照词库检查关键节点（器官/行为/液体/接触点）是否被降档替换——发现委婉词（用泛称替代精确 tag、用"动作描述"替代器官词）立即换回档位对应的直白词。
- **归属完整**：每个接触/液体/道具有明确归属（prose 身份卡规则 / tag 流施受前缀），不为回避直白而模糊归属。
- 露骨度与用户请求一致：用户只要 NSFW（裸露+情色姿态）就不写性行为；用户要 explicit 就写到 explicit 档——**上下不漂移**。

## 两套体系的分工（按形态各用各长）

| 维度 | 标签流（NovelAI/SD/Anima） | 自然语言流（prose） |
|---|---|---|
| 载体 | Danbooru 标签 + 自由英文短语 | 连贯英文散文段落，排斥标签堆 |
| 男性存在感 | 隐形男光谱（见下） | 每个参与者完整身份卡 |
| 表情表达 | 情绪梯度 tag 组合成套使用 | 因果链推导（角色状态→动作阶段→表情反应） |
| 强度控制 | 按内容选标签组合 | 按用户请求强度直接写 |
| 技巧文档 | [tags-techniques.md](tags-techniques.md) | [prose-method.md](prose-method.md) |

**隐形男光谱**（男性存在感是滑块不是开关）：

```
1boy（全身）→ faceless male（去脸）→ disembodied penis（仅器官）→ invisible man（暗示）→ solo focus（纯女性）
```

男性默认隐形：用 disembodied penis / invisible man 代替 1boy；只在叙事必须有男性身体时用 faceless male。

**半遮半掩的张力胜过全裸**：torn clothes / panties aside / see-through 比 nude 更有戏剧性（两套体系通用的核心审美判断）。

## 模块加载表

| 本次需要 | 读取位置 |
|---|---|
| **词库供给（按题材选维度）** | [lexicon/](lexicon/) 7 维度（见写作契约一） |
| **基准范本（按题材读 2-3 条）** | `database/nsfw/examples/` 9 文件（见写作契约二） |
| 标签流成人技巧（姿势/组合/道具/叙事/梯度表/尾缀） | [tags-techniques.md](tags-techniques.md) |
| 自然语言流 prose 工作流（身份卡/因果链/液体连续性/镜头） | [prose-method.md](prose-method.md) |
| prose 场景模式库（玩法分类/玩具语法/场景矩阵/暴露模式） | [prose-patterns.md](prose-patterns.md) |
| 极端主题清单与门控、中文模板索引 | [themes.md](themes.md) |
| 联想引擎（需求模糊/要求联想时） | [association.md](association.md) |
| 法典配方库（场景→成品配方约6900条） | `database/nsfw/codex/`（用法见 [codex-guide.md](codex-guide.md)） |
| 玩法语料共现统计 | `database/nsfw/corpus/`（定位见 MANIFEST） |
| 中文场景/姿势/构图等模板素材 | `database/nsfw/templates/`（15 册；**原文存档**——含 `masterpiece / best quality / 8k` 质量前缀与「禁止透明词」等历史写法，**不适用本 skill 输出规范**，参考前先剥离，同 examples/README.md 规则） |
| 风格与负面预设、标签数据 | `database/nsfw/presets/`（含 nhentai 5 命名空间中文对照 TSV） |
| 成人向提示词示例 | `database/nsfw/examples/` |

加载约定：读完 core.md + 当前题材对应的一个模块 + 词库对应维度 + 范本 2-3 条即可开工；同一任务不重复加载；玩法强调类请求（用户说「玩法」「重点描写」「明确描写」等，或点名多人/兽交/乱伦/强制类主题）先走 [association.md](association.md) 的共现规划机制。库缺失、检索工具不可用等异常处理见 SKILL.md §异常与降级。

## 交付前自检（内部完成）

- 参与者人数、角色归属与请求一致；每个身体部位/道具/液体有明确归属。
- 暴露程度与剩余服装不矛盾；用户要求的保留项（solo、不露脸、含蓄处理等）完整保留。
- 露骨程度与用户请求一致：不悄悄升级、不悄悄降级；**委婉替换检测通过**——关键节点（器官/行为/液体/接触点）没有被泛称或模糊描述降档替换。
- 标签流拼写符合主规范（空格、无质量前缀）。
- 极端主题仅出现在用户显式点名的场合。
- 范本对标：要素密度与直白度不低于所读基准范本。
