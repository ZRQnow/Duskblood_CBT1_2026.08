# Duskblood CBT1 行业研究库

本仓库用于整理 The Duskbloods CBT1 / Global Network Test 的原始素材、可复核证据、主题分析与最终研究产出。目标不是单纯“存文件”，而是建立一套可持续追加、可追溯、适合 AI Agent 读取的行业研究 base。

## 核心原则

1. **原始素材不改写**：图片、视频、网页快照、访谈、社媒帖子等原件进入 `01_sources_raw/`。
2. **来源、文件、事实、主张四层分离**：`source_id → asset_id → evidence_id → claim_id`。
3. **事实与分析分离**：观察到什么写入 `02_evidence/`；为什么重要、如何解释写入 `03_analysis/`。
4. **任何关键结论都可回溯**：分析至少引用 `evidence_id`，证据再回到具体素材与时间码/页面/截图位置。
5. **AI 先读索引，不盲扫仓库**：Agent 应先读 `AGENTS.md` 与 `PROJECT_INDEX.json`。
6. **保留测试版本边界**：CBT/网络测试观察不得直接等同于正式版结论。
7. **合规优先**：测试协议、转载权限、隐私或个人信息不明确时，先标记 restricted/unknown，不默认可公开传播。

## 目录结构

```text
Duskblood_CBT1_2026.08/
├── AGENTS.md                 # AI Agent 读取与更新规则
├── PROJECT_INDEX.json        # 机器可读项目索引
├── 00_brief/                 # 研究问题、测试背景、分类体系、读者约定
├── 01_sources_raw/           # 原始素材；按来源类型归档
│   ├── _inbox/               # 尚未完成登记的新素材
│   ├── official/             # 官方页面、公告、预告、开发者材料
│   ├── gameplay/             # 原始实机、直播/VOD、试玩录像
│   ├── screenshots/          # 原生截图；视频抽帧不放这里
│   ├── interviews/           # 开发者、媒体、玩家/测试者访谈
│   ├── social/               # 单条社媒帖子、评论、讨论串快照
│   ├── press_media/          # 新闻、评测、preview、媒体文章
│   ├── recruiting/           # 招聘与团队信号
│   ├── technical/            # 版本、网络、报错、服务器/性能相关材料
│   └── community/            # 社区整理、论坛长期讨论等辅助材料
├── 02_evidence/              # 来源台账、素材清单、衍生文本、结构化事实
│   ├── source_register.jsonl # 来源主表，机器读取的唯一真源
│   ├── asset_manifest.jsonl  # 仓库文件主表
│   ├── observations.jsonl    # 原子化事实/观察主表
│   ├── social_reception.jsonl# 社媒样本与评价编码
│   ├── derived/              # transcript/OCR/keyframe/web text 等衍生材料
│   └── schemas/              # JSON Schema
├── 03_analysis/              # 按研究主题形成分析，不新增无证据事实
├── 04_narrative/             # 论点地图、证据关系与成文提纲
├── 05_drafts/                # 工作草稿与修订稿
├── 06_qc/                    # 事实、证据链、合规、格式和发布检查
└── 07_final/                 # 通过 QC 的最终研究产物
```

## 快速入库流程

1. 新素材先放入 `01_sources_raw/_inbox/`，不要先凭印象分类。
2. 在 `02_evidence/source_register.jsonl` 新增 `source_id`。
3. 将实际文件移动到对应原始素材目录，并在 `asset_manifest.jsonl` 分配 `asset_id`。
4. 对视频/音频生成 transcript，对图片生成 OCR/描述，对长视频生成关键帧；衍生材料进入 `02_evidence/derived/`。
5. 把可复核、单一含义的事实拆成 `observations.jsonl` 中的 `evidence_id`。
6. 分析文件只引用 `evidence_id`；不得把“看起来像”“可能是”写成已确认事实。
7. 形成跨主题结论后更新 `04_narrative/argument_map.json`。
8. 发布前执行 `06_qc/qc_checklist.md`。

## ID 体系

- 来源：`SRC-类型-四位序号`，例如 `SRC-GMP-0001`
- 文件：`AST-六位序号`，例如 `AST-000001`
- 证据：`EVD-六位序号`，例如 `EVD-000001`
- 主张：`CLM-四位序号`，例如 `CLM-0001`

同一个外部来源可以对应多个 `asset_id`；同一个素材可以产生多个 `evidence_id`；一个 `claim_id` 可以由多个证据共同支持或反驳。

## 大文件

图片、视频、音频等二进制大文件继续通过 Git LFS 管理。对 AI 来说，原视频并不是首选读取对象：优先提供 transcript、关键帧索引、OCR 和结构化 observation，并保留回到原视频的时间码。
