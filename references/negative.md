# 负面提示词方法论

**默认不给**：负面提示词留给用户自己控制；用户要时按本文件定制。它不是许愿池——只解决「模型确实会犯、且明确知道要排除」的错误。

## 第一原则：具象化

抽象否定对模型几乎无效（它描述的是「不存在的东西」）。能写进正文的排除，优先写进正文：

| 差 | 好 |
|---|---|
| `no man-made structures` | 正文写 `荒芜的景观，没有建筑和道路` |
| `不要文字` | 正文写 `纯视觉画面，画面内没有任何可读文字` |
| 「不要悲伤」 | 直接写开心的样子，别用否定 |

风格需求用正面描述定义（「不要卡通」不如「写实摄影」）；一致性靠不变量声明与参考，负面词锁不住身份；主体意图直接写目标状态，不否定。

## 按需定制流程

1. **分层检查风险**，逐类挑「这张图真的会犯」的项：

| 类别 | 检查项 |
|---|---|
| 错误媒介 | 与目标媒介冲突的特征（写实图出 CG 感；插画出摄影景深） |
| 结构缺陷 | 畸形手、多指/少指、脸部崩坏、五官错位、穿模、肢体粘连 |
| 内容错误 | 多余人物、多余肢体、缺主体、元素悬浮 |
| 光影错误 | 过曝/欠曝、光源矛盾、无阴影 |
| 画质缺陷 | 低分辨率、噪点、伪影、过度锐化、塑料感、色带 |
| 材质错误 | 错误反射、材质混淆、湿感错误 |
| 文字标识 | Logo、车牌、水印、乱码错字（画面要文字时删除此类） |
| 构图错误 | 错误裁切、主体被切、失衡 |

2. **通用池**（按需取用，不全抄）：

```
low resolution, blurry, jpeg artifacts, oversharpened, over-smoothed,
deformed hands, extra fingers, missing fingers, fused fingers,
asymmetric face, distorted facial features, cross-eyed,
extra limbs, missing limbs, floating objects, disconnected parts,
bad anatomy, disproportional, unnatural pose,
overexposed, underexposed, flat lighting, contradictory shadows,
plastic skin, waxy texture, wrong reflections, material confusion,
readable text, watermark, signature, logo, garbled characters,
cluttered background, distracting elements, bad composition, awkward crop
```

3. **按媒介追加**：摄影→`3d render, cgi, cartoon, illustration, anime`；写实3D→`real photograph, anime, cel shading`；二次元→`photorealistic, real photo, noisy texture`；产品渲染→`lifestyle snapshot, cluttered scene`；扁平矢量→`photorealistic, complex 3d volume`。
4. **按主体追加**：人物→`malformed ears, bad teeth, uneven eyes`；动物→`extra paws, wrong fur direction, human-like pose`；建筑→`impossible geometry, warped perspective`。
5. **场景化微调示例**：风景/静物→加 `1girl, 1boy`（防人物乱入）；拒绝写实感→加 `photorealistic, realistic`；画面要出现 logo/徽记→删 `logo` 项；要留白构图→删 `negative space` 项。

## 数量与形态

### 三个数字互不相干，别混用

本文件出现三个「负面词条数」，它们服务于不同场景，**不是同一个上限**：

| 数字 | 是什么 | 何时用 |
|---|---|---|
| **8–15 条** | **本skill 的交付契约**——本 skill 定制并交付给用户的成品负面词条数 | 用户说「给我负面提示词」时，按此交付 |
| **17 项** | **NAI 官方 UC 基础串**的条数 | 用户自己要往 NAI 的 UC 栏粘贴时，作为整串参考池原样给出 |
| **9 项** | **B 模式成年防御块**的条数 | 成人画面的强制前缀，见下节 |

- 用户要「成品负面词」→ 按 8–15 条交付，用分层结构拼装（见下）。
- 用户要「NAI 的 UC 栏填什么」→ 给官方 17 项基础串，按 §各模型参考基础池 的规则删冲突项。
- 两者都要时分别说明，不要混成一条列表。

### 交付时的分层结构

```
成年防御块（仅 B 模式，9 项，逐词不删）
  → 解剖通用块（3–6 项，从 §通用池 按这张图会犯的错误挑）
    → 本图定制项（0–6 项，按题材/媒介/主体追加）
```

- **超 15 条时**：先删解剖通用块里的低概率项，**成年防御块不删**（它是成年底线，不是画质调整）。
- **不足 8 条时**：不硬凑——具象化排除写进正文（见 §第一原则），正文能解决的就不占负面词位。
- **每条必须有针对性**：能说出「为什么这条对这张图重要」。不通过信号：与正面描述矛盾（模型收到冲突指令随机取舍）、与用户主题无关、纯粹凑数。

## 各模型参考基础池（用户要时的起点，仍按需增删）

- **通用标签流**：`worst quality, low quality, bad anatomy, bad hands, extra fingers, missing fingers, watermark, signature, jpeg artifacts`
- **NAI（UC 栏完整基础串，17项）**：`lowres, artistic error, film grain, scan artifacts, worst quality, bad quality, jpeg artifacts, very displeasing, chromatic aberration, dithering, halftone, screentone, multiple views, logo, too many watermarks, negative space, blank page`——要 SFW 时最前加 `nsfw`；冲突项只删不换；多人图删 `extra characters` 且不从单人模板抄加权排除段；本图不想要的具体元素写主串最后负权重行，不进 UC。
- **Anima**：`worst quality, low quality, artist name, blurry, jpeg artifacts, chromatic aberration`；Turbo/Base 版追加 `score_1, score_2, score_3`（官方负向组成）。
- **自然语言流模型**：多数不吃负面词——排除项写进正文（具象化）。
- **多人图专条**：`extra characters` 只在单人图语境出现；三人图带它会和 `3girls` 打架。

## B 模式负面词（成人画面专节）

### 成年防御块（B 模式默认附加）

成人请求的负面词**最前面**挂成年防御块（解剖防御协议负向层，见 tags-techniques.md）：
```
child, loli, shota, underage, young teen, kid, infant, minor, immature body
```

- 这是成年底线的提示词级防线：防御的是**生成结果漂向未成年形态**，不改变 core.md 的输入端底线（未成年指向输入直接丢弃）。
- NAI 用户挂 UC 栏；SD 系挂负面框；逐词保留不删减，也不翻译成中文。
- 之后才接解剖通用块与本图定制项。

### 预设组合（style-negative-presets.csv）

`database/nsfw/presets/style-negative-presets.csv`（142 行）是风格与负面预设库，五列：`name, prompt, negative_prompt, description, category`。

- **BASE 系列预设**：质量基线与反向排除（反 3D、反 furry、反写实等 negative-only 堆叠预设）——用户要"排除某画风"时优先检索。
- **组合规则在 description 字段**：每条预设的 description 写明 Combos（可与哪些预设叠加）与 Conflicts（与哪些互斥）——拼装前必读，不做无声明组合。
- 按需拼装流程：按需求检索 CSV（`grep -i "关键词" "<ABS>/style-negative-presets.csv"`）→ 读命中行的 description 组合规则 → 取用其 negative_prompt 内容 → 与成年防御块、本图定制项合并 → 逐条过矛盾检查（§自检）。
- 检索命令与文件定位见 database/MANIFEST.md。

## 自检

- 每条负面词与正面描述零矛盾（逐条对照，删冲突项）。
- 画面需要的文字/颜色/人物没有被自己的负面词压掉。
- 交付条数落在 8—15（成年防御块不计入，见 §数量与形态）；每条说得出去除理由。
