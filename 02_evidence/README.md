# 02_evidence：索引、衍生材料与可复核证据

这一层是整个研究库的核心。目标是把“海量图片/视频/帖子”变成 AI 可以快速检索、同时又能回到原件验证的结构化证据。

## 四个主数据集

- `source_register.jsonl`：**来源主表**。每行一个外部来源或一次独立采集对象。
- `asset_manifest.jsonl`：**文件主表**。每行一个仓库内文件，连接到 `source_id`。
- `observations.jsonl`：**证据主表**。每行一个原子化、可定位、可复核事实。
- `social_reception.jsonl`：**社媒评价样本表**。用于记录样本选择、主题、态度和互动量，避免只摘录极端评论。

`source_register.csv` 保留为旧版/人类查看出口，但后续 AI 写入以 JSONL 为准。

## derived：给 AI 的多媒体中间层

原视频、图片、音频通常不适合每次重复读取。将以下衍生文件放入 `derived/`：

- `transcripts/`：视频、音频、访谈逐字稿与时间码。
- `ocr/`：UI、截图、网页截图的 OCR 文本。
- `keyframes/`：长视频关键帧及时间码索引。
- `web_text/`：网页正文的可检索文本和访问元数据。
- `translations/`：必要的翻译，必须保留原文与目标语言。

所有 derived 文件仍需写入 `asset_manifest.jsonl`，并设置 `content_role=derived` 与 `derived_from_asset_id`。

## 专门 JSON

现有 `frame_measurements.json`、`ui_facts.json`、`rules_matrix.json`、`hiring_signals.json` 可以继续保留，适合精确测量或专题结构。但它们不应成为孤立事实岛：新增记录应同步包含或映射到 `evidence_id`。

## observation 的最小要求

一条好的 evidence 只表达一个意思，并尽可能包含：

`evidence_id + source_id + asset_id + evidence_type + topic_tags + statement + locator + confidence + verification_status`

分析和报告优先引用 `evidence_id`，而不是直接引用文件名。
