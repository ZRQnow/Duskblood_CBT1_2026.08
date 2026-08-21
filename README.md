# Duskblood CBT1 行业研究库

本仓库保存《The Duskbloods》CBT1 / Global Network Test 的研究素材、结构化标签与分析报告。目录按素材类型划分，不再区分 `sources_raw` 与 `evidence`；事实链通过根目录的 JSON / JSONL 文件维护。

## 目录

```text
.
├── images/       # 图片、截图、动图；大文件由 Git LFS 管理
├── videos/       # 视频素材（当前仅保留入库说明，未新增视频）
├── interviews/   # 采访、翻译与访谈文本
├── analysis/     # 分析报告及可复用的详细分析提示词
├── *.json/jsonl  # 来源、素材、证据、分类、测试边界和论点标签
├── PROJECT_INDEX.json
└── AGENTS.md
```

## 证据链

`source_id → asset_id → evidence_id → claim_id`

- `source_register.jsonl`：外部来源主表。
- `asset_manifest.jsonl`：仓库文件主表，记录路径、哈希、尺寸、语言和标签。
- `observations.jsonl`：可定位、可复核的直接观察。
- `claims.json`：由证据支持或反驳的分析主张。
- `analysis_index.json`：现有分析报告索引。
- `analysis/PROMPT.md`：游戏产品与行业分析的完整工作提示词。

## 入库流程

1. 按格式把素材放入 `images/`、`videos/` 或 `interviews/`。
2. 在 `source_register.jsonl` 登记来源并分配 `source_id`。
3. 在 `asset_manifest.jsonl` 登记文件路径、SHA-256、大小、类型与处理状态，分配 `asset_id`。
4. 将能够直接复核的事实逐条写入 `observations.jsonl`，引用 `source_id`、`asset_id` 和准确定位。
5. 将解释、比较、产品判断和市场判断写入 `analysis/`；关键判断引用 `EVD-*`。
6. 需要形成跨报告主张时更新 `claims.json`，同时保留反证、信心与版本边界。

## 基本规则

- 不用文件名代替内容核验，不把推断写成事实。
- 不确定值写 `null`；保留冲突证据和样本限制。
- CBT1 结论只适用于已记录的测试版本、平台、地区和时段。
- 图片、视频、音频继续通过 Git LFS 管理；路径变化时同步更新 `asset_manifest.jsonl`。
- 未核实测试协议、版权、隐私或传播权限前，不把素材标记为可公开传播。

详细机器读取与写入规范见 `AGENTS.md`。
