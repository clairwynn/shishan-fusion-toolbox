# 混合形态写法（标签 + 自然语言穿插）

混合形态：Danbooru 标签与自然语言句子出现在**同一个提示词**里，按内容穿插、各司其职。适用于 NovelAI V4.5/V5、Anima、SD 系——这些模型同时训练了标签与字幕，两种表达都认识。纯标签流与纯自然语言流之外的第三形态；当画面需要"稳定属性 + 复杂互动"时是默认最优解。

## 分工原则（什么用 tag，什么用句子）

| 用 tag 承担 | 用句子承担 |
|---|---|
| 稳定视觉属性：发色/瞳色/发型/体型 | 动作与互动：`she pulls off one glove with her teeth while a high heel dangles from her toes` |
| 服装类型与配饰 | 空间关系：`the cat lies at the girl's feet` |
| 姿势锚点（standing, sitting, kneeling） | 构图指令：`leave 2/3 of the space blank`、`something close to the camera for a greater depth of field` |
| 构图/镜头术语（cowboy shot, from side） | 概念融合：`ink-wash qipao with holographic chiffon` |
| 场景名词（classroom, beach） | 物理与因果：接触点、受力、液体路径等 tag 写不清的关系 |

**判断口诀**：tag 做不到的（关系、方向、比例、因果、融合概念）用句子；句子写不稳的（身份属性、可枚举状态）用 tag。骨架用 tag，血肉用句子。

这些表达方式是示例不是词库——按当前题材创造新组合。

## 穿插方式（无固定先后，按内容组织）

混合形态**没有固定的"句先还是 tag 先"规则**，按画面内容自然组织，但两点通用：

1. **靠前的成分影响力更大**：最想突出的内容（灵魂元素、核心动作）尽量放前。
2. **内部一致**：一个提示词内选一种组织逻辑贯彻到底，不要前半段句先 tag 后、后半段又反过来。

三种可选组织策略（用户指定了就按用户的；没指定按画面选）：

- **策略A·句子开场**：先用一句自然语言交代画面与核心动作，随后 tag 沿视线路径锚定属性。适合动作性、叙事性强的画面。
  ```
  A samurai girl braces one foot against a wave-washed rock and draws her katana halfway from its sheath,
  1girl, solo, asymmetrical heavy brocade kimono top, wide-leg hakama, holding a half-drawn katana,
  looking intensely sideways, traditional japanese woodblock print style, flat bold highly saturated colors, ...
  ```
- **策略B·tag块+句子块分区**：主体锚/镜头/姿势用词组聚簇，关系/场景/光影用句子段落。适合层次复杂的稳定画面。
- **策略C·视线路径交替**：从第一视觉焦点开始，走到哪写到哪——遇到可枚举属性落 tag，遇到关系/因果落句子。适合多主体、强互动画面。

## 权重与句子的关系

- 权重语法（数值 `1.2::...::`、SD 括号）作用于 **tag 与 tag 包**；语义相关的 tag 组可打包加权，告诉模型"这些是一体的"。
- **句子不使用权重语法**——强调句子内容靠措辞精度与前置位置，不靠加权。
- 默认全部不加权（见 tag-flow.md §权重语法体系（按模型速查））；确需加权时核心概念 1.3+、支撑 1.1、大部分原样。**这两个档位是通用起点，不适用于全部模型**——Anima 的有效阈值高得多（1.5 起步，1.1–1.3 无效），在 Anima 下按 models.md §Anima 的区间走，不要照搬 1.3/1.1。

## 引号规则（重要）

- 叙事句子**直接写，不加引号**；引号在提示词里专指"要画进画面的文字"（`the words "OPEN" on the neon sign`）。
- 叙事段不要整段包进引号——那会被模型当成画面文字渲染。

## 平台适配

| 平台 | 混合规则 |
|---|---|
| **NovelAI V4.5/V5** | 三形态皆可，模型不在乎某一块是 tag 还是句子；多人场景的句子进各自 Character N: 段；引号法画文字 |
| **Anima** | 三种写法合法；混合时 artist 标签放在 NL 部分之前；写 NL 时**先点名角色再描述外观**（角色/系列名标准大写，如 `Hatsune Miku`）；多角色场景尤其要点名 |
| **SD / SDXL / NoobAI** | tag 为主体 + 按需混自由英文短语与短句；权重括号体系按 tag-flow.md；区域分割用 BREAK，句子进所属区域段 |

## 与其他形态的一致性

混合形态与纯标签、纯自然语言指向**同一个画面**时，内容必须一致——只是表达体系不同。用户同时要多种形态时，混合与另两种形态的画面要素、风格、构图不得互相矛盾。

## 交付前自审（内部完成）

1. 句子承担的信息不可被 tag 替代（空间关系/互动/构图指令/概念融合确实需要句子）。
2. tag 承担的稳定属性没有写成长句（发色、服装类型这些用 tag，别展开成从句）。
3. 同一信息没有在 tag 和句子里重复表达两次（`long hair` + `her long hair flows...` 二选一，除非句子有新增信息）。
4. 引号只用于画中文字；无质量前缀；权重符合默认不加权原则。
5. 靠前位置放了灵魂元素；组织策略内部一致。
