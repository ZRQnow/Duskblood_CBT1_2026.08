# AGENTS.md

本文件定义 AI Agent 在本仓库中的默认读取顺序、事实标准与写入规则。

## 默认读取顺序

1. `PROJECT_INDEX.json`
2. `test_context.json`、`taxonomy.json`、`reader_contract.json`
3. `source_register.jsonl`
4. `asset_manifest.jsonl`
5. 与任务相关的 `observations.jsonl`、`social_reception.jsonl` 和专门 JSON
6. `analysis_index.json` 与对应的 `analysis/*.md`
7. `claims.json`

## 事实层级

- **source**：外部来源或一次独立采集对象。
- **asset**：仓库中实际保存的文件。
- **evidence**：从 asset 中能够定位和复核的单一观察。
- **analysis**：对一个或多个 evidence 的解释、比较或推断。
- **claim**：可被证据支持、反驳或修订的报告主张。

严禁把 analysis 或 claim 反写成 evidence。

## 目录与写入规则

- 素材按媒介类型进入 `images/`、`videos/`、`interviews/`；不要另建 raw、evidence、draft、qc 或 final 流程目录。
- 标签、来源、证据和主张写入根目录 JSON / JSONL；分析报告只写入 `analysis/`。
- 新事实优先写 `observations.jsonl`，一行一个 JSON 对象。
- 每条 evidence 尽可能包含 `source_id`、`asset_id` 和 locator。
- 视频事实提供时间码；网页/文章提供 URL 与段落定位；图片提供 asset_id，必要时记录画面区域。
- 不能确认的信息写 `null`，不要使用 0、空字符串或猜测值代替。
- 同一事实只是换一种措辞时不重复创建 evidence；可补充 `corroborating_source_ids`。
- 预测、产品判断和市场判断只能进入 `analysis/` 或 `claims.json`。

## 多媒体处理

- 视频/音频：保留原文件，补 transcript 与关键事件时间码；需要精确动作时再做帧级测量。
- 图片：保留原图，结构化画面描述、OCR 与必要区域定位。
- 社媒：保存 URL、账号、日期、平台和互动量快照；正文以摘要和必要短引文为主。
- 访谈：保留来源、说话人、翻译状态；翻译或摘要必须声明其衍生关系。
- 网页：优先保存 URL、访问时间和可检索文本；必要时保留页面快照。

## 分析写作规则

每份 `analysis/*.md` 至少包含：研究问题、当前判断、证据、反证/冲突、样本与版本限制、行业比较、待验证问题。关键句引用 `EVD-*`，不要只写模糊的“据玩家反馈”。执行完整研究任务时遵循 `analysis/PROMPT.md`。

## 禁止事项

- 不因文件名或文件夹名直接推断内容。
- 不把 CBT1 数值和平衡结论外推为正式版确定结论。
- 不删除冲突证据来维护既有观点。
- 不在未核实测试协议、版权或隐私状态时把 restricted/unknown 素材标为 public。
- 不修改或删除已登记素材，除非用户明确授权且已校验迁移后的路径、大小与哈希。
