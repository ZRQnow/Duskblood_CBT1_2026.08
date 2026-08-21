# AGENTS.md

本文件定义 AI Agent 在本仓库中的默认读取顺序、事实标准与写入规则。

## 默认读取顺序

1. `PROJECT_INDEX.json`
2. `00_brief/test_context.json`
3. `00_brief/taxonomy.json`
4. `00_brief/brief.md` 与 `00_brief/reader_contract.json`
5. `02_evidence/source_register.jsonl`
6. `02_evidence/asset_manifest.jsonl`
7. 与任务相关的 `02_evidence/observations.jsonl`、衍生文本和专门 JSON
8. 对应的 `03_analysis/*.md`
9. `04_narrative/argument_map.json`

除非用户明确要求，不要从 `05_drafts/` 或 `07_final/` 反向推断事实。

## 事实层级

- **source**：外部来源或一次独立采集对象。
- **asset**：仓库里实际保存的文件。
- **evidence**：从 asset 中能够定位和复核的单一观察。
- **analysis**：对一个或多个 evidence 的解释、比较或推断。
- **claim**：准备进入报告的可支持/可反驳主张。

严禁把 analysis 或 claim 反写成 evidence。

## 写入规则

- 新事实优先写 `observations.jsonl`，一行一个 JSON 对象。
- 每条 evidence 必须尽可能包含 `source_id`、`asset_id` 和 locator。
- 视频事实必须提供时间码；网页/文章必须提供 URL 与页面/段落定位；图片必须提供 asset_id，必要时记录画面区域。
- 不能确认的信息写 `null`，不要使用 0、空字符串或猜测值代替。
- `confidence` 只能描述证据可靠程度，不得用于掩盖缺失来源。
- 同一事实如果只是不同措辞，不重复创建 evidence；补充新的来源到 `corroborating_source_ids`。
- 任何预测、产品判断、市场判断只能进入 `03_analysis/` 或 `04_narrative/`。

## AI 处理多媒体的默认方式

- 视频/音频：生成 transcript + 关键事件时间码；需要精确动作时再做帧级测量。
- 图片：保留原图；衍生 OCR、画面描述和必要的区域定位。
- 社媒：保存 URL、作者/账号、时间、平台、互动量快照；正文以摘要和必要短引文为主，不用整篇复制代替原链接。
- 访谈：原始音视频与逐字稿分离；逐字稿保留说话人、时间码和翻译状态。
- 网页：优先保存 URL、访问时间和可检索文本；页面快照作为证据备份。

## 分析写作规则

每个 `03_analysis/*.md` 至少应包含：研究问题、当前判断、证据、反证/冲突、样本与版本限制、行业比较、待验证问题。关键句引用 `EVD-*`，不要只写模糊的“据玩家反馈”。

## 禁止事项

- 不因文件名或文件夹名直接推断内容。
- 不把 CBT1 的数值和平衡结论外推为正式版确定结论。
- 不删除冲突证据来维护既有观点。
- 不在未核实测试协议、版权或隐私状态时把 restricted 素材标成 public。
