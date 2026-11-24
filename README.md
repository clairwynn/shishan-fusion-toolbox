# 图片提示词超级融合史山工具箱

`shishan-fusion-toolbox` — 一个只负责写提示词的 skill。不负责其它的功能.

这个是我自己做出来自己使用的skil融合了大量的数据与功能，是个超级史山，喜欢吃史的，可以试试，目前还有大量的bug我懒得修了，就将着吃吧

## 目录结构

```
shishan-fusion-toolbox/
├── SKILL.md              主入口：定位、任务路由、四大工作流、输出契约、铁律、按需加载表
├── README.md
├── LICENSE
├── DISCLAIMER.md         免责声明与数据来源说明（完整条款）
├── references/           方法论文档 25 份
│   ├── tag-flow.md       标签流语法、库查询 grep 模式与回退链
│   ├── nl-flow.md        自然语言流结构、句式模板、中英词库
│   ├── hybrid-flow.md    混合形态写法
│   ├── convert.md        形态互转、权重换算、修改哲学
│   ├── analyze.md        两段提示词对比
│   ├── reverse.md        反推分析框架与媒介边界
│   ├── recommend.md      库检索与「先荐后改」
│   ├── models.md         各模型专有规则；多人机制与组装顺序的唯一权威
│   ├── negative.md       负面提示词
│   ├── consistency.md    跨图一致性与角色锁定
│   ├── ideation.md       构思深化：记忆点、环境、服装、构图
│   └── nsfw/             B 模式资料：core、prose-method、prose-patterns、
│                         lexicon×7、themes、tags-techniques、association、codex-guide
└── database/             953 个数据文件
    ├── MANIFEST.md       数据文件定位与查询方法
    ├── tags/             标签库：tags.tsv（32.8 万行，中英对照）+ 共现矩阵 + 索引
    ├── characters/       角色库：771 个文件，按作品 / 索引 / 汇总三种视图
    ├── prompts/          真实提示词库：33 个文件，多库 + 中文库
    └── nsfw/             成人向词库、范本与场景配方
```

## 安装

1. 把整个目录放进运行时的 skill 目录（Claude Code、Doubao 等支持 `SKILL.md` 的运行时皆可），目录名保持 `shishan-fusion-toolbox`。
2. 只依赖文件读取与文本检索（`grep`）。没有检索工具时，标签流任务会降级为「只写高频基础标签」，并在交付时声明未经库验证。
3. 触发方式：提到提示词、prompt、咒语、标签、负面词、反推、img2prompt、提示词转换/审查/对比，或点名任一图像模型并涉及写法时自动进入。

## 工作方式

- **按需加载**：SKILL.md 的加载表规定每个任务该读哪几份文档，不整库塞进上下文，也不递归通读。
- **数据库优先**：写出的内容标签必须能在 `database/tags/tags.tsv` 里查到，这是「标签真实存在」的保证；模型官方前缀标签豁免。
- **分级模式**：默认 A 模式（全年龄）。说「成人模式 / B 模式 / NSFW 模式」切入 B 模式，之后持续有效，不反复确认。分级只约束生成任务，反推与推荐不受限。
- **输出契约**：成品放代码块，块外说明用中文、简短；负面提示词默认不给，要了才按需定制。

## 数据规模

| 数据 | 规模 |
|---|---|
| 标签库 `tags.tsv` | 32.8 万行，含中文对照 |
| 标签共现矩阵 | 51.7 MB |
| 角色库 | 771 个文件，按作品分卷 |
| 真实提示词库 | 约 3.1 万条，多库合并 + 中文库 |
| 场景配方 | 6933 条，跨模型适配 |
| 成人向供给词库 | 7 个维度（anatomy / acts / clothing / expression / fluids / props / viewpoint） |
| 全仓 | 979 个文件，约 162 MB |

## 许可与免责

作者：温知澄（[clairwynn](https://github.com/clairwynn)）

- 代码与文档：MIT，见 [LICENSE](LICENSE)。
- **数据来源**：仓库内所有数据与资料均为作者从互联网公开渠道收集整理而成。因数据量大、来源庞杂且经多次合并清洗，无法逐条标注每项数据的具体来源与参考项目；原始数据权利归各自权利人所有，商业分发前请自行核实来源授权。
- 内容分级：仓库内含成人向参考资料（`references/nsfw/`、`database/nsfw/`），仅限成年人使用。skill 默认运行在 A 模式，不会主动产出此类内容；B 模式需用户显式切换。
- 免责：本项目按「现状」提供，不附带任何明示或暗示担保。使用本 skill 产出的提示词所引发的任何后果（包括但不限于平台内容审核、模型使用条款、第三方权利纠纷），由使用者自行承担。
- 侵权移除：权利人可通过[仓库 Issue](https://github.com/clairwynn/shishan-fusion-toolbox/issues) 或作者主页联系，核实后将移除相关内容。

**完整条款请阅读 [DISCLAIMER.md](DISCLAIMER.md)**（数据来源说明、许可范围界定、内容分级与未成年人保护、免责条款、侵权处理渠道）。
