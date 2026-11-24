# 推荐工作流（多库检索）

从六个真实提示词库（合计 30,581 条）检索并推荐现成提示词。定位：用户要**参考、案例、灵感**时使用；用户要「照这个改」时，选中案例后转入转换工作流（见 convert.md）。

## 库路由（先选库，再检索）

| 用户需求 | 首选库 | 次选 |
|---|---|---|
| GPT-Image / Nano Banana / Gemini 系 | `gpt-image-cases.json`（485条，13大类，中文标题+styles/scenes 标签） | `awesome-api-cases.json`（686条，7类，含 {argument} 占位变量） |
| 垂直题材（学术图表/纹身/水墨/电影参考/时尚编辑/改图指令/技术插画/建筑室内/数据可视化/像素/美术/等距） | `gpt-image-gallery.json`（66条，12 差异化主题册，质量最高） | gpt-image-cases.json |
| 中文模型（即梦/可灵/Seedream）或用户要中文 | `zh-library/`（5,430条中文） | `gpt4o-selected.json`（1,050条中文精选） |
| 通用/其他模型（MJ/Flux/SD 系参考） | `library/`（22,864条英文，11分类） | gpt-image-cases.json |

路由冲突时：题材垂直度优先于模型匹配；用户点名了库来源信号（"GPT-Image 风格的案例"）按点名走。

## library/ 的 11 分类

| 分类 | 内容 |
|---|---|
| social-media-post | 社交媒体配图（最大类） |
| product-marketing | 产品营销图 |
| profile-avatar | 头像 |
| game-asset | 游戏资产 |
| comic-storyboard | 漫画分镜 |
| infographic-edu-visual | 信息图/教育可视化 |
| ecommerce-main-image | 电商主图 |
| poster-flyer | 海报传单 |
| app-web-design | App/Web 设计图 |
| youtube-thumbnail | 视频封面 |
| others | 其他 |

## 工作流

1. **选库与确定类目**：按库路由表选库；在所选库内按需求关键词（主题/风格/构图/分类）筛候选。拿不准时问一句，或用用户描述中的信号词匹配。需求跨分类时主分类为主、次分类补 1-2 条，主次按用户描述中的用途词判定。
2. **检索**：读对应分类 JSON/文件，检索方法见 database/MANIFEST.md。JSON 内每条含 prompt 正文与元信息；新三库的 `styles`/`scenes` 字段可作二次筛选维度。**跨分类检索时必须按 `content` 去重**：`library/` 存在跨分类重复行（22,864 行 → 唯一内容 14,886，同一 prompt 可同时属于多个分类），不去重会把同一条重复推荐给用户。
3. **推荐输出：纯 prompt 列表**——默认 3-5 条（用户指定数量则按指定），每条放独立代码块。不加包装分析、不写推荐理由长文（用户问起某条为什么合适再解释一句）。
4. **先荐后改**：不主动给"改写版"——先把库里原样 prompt 给用户挑；用户选中某条后要求调整时，转入 convert.md 工作流（此时忠实原 prompt 语义，只按用户要求动）。新库条目含 {argument name="x" default="y"} 占位变量：推荐时保留原样并说明可替换项。
5. **不过滤**：推荐是检索任务，不受分级模式约束；库里有什么荐什么。

## 边界

- 不在推荐阶段自创/混合 prompt——用户要原创生成时不走本工作流（走生成工作流 A）。
- 库中 prompt 是真实案例（活基线）：生成任务对不熟悉题材对标信息完整度时，也可检索同分类案例作参照（只作内部对标，不直接展示）。
- 库文件较大（单文件最大 10 万行级），用检索命令定位，不通读灌入。
