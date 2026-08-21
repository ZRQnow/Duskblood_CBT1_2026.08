# 01_sources_raw：原始素材存档

这里保存未经改写、裁剪、转码或分析的原始材料。原件的职责是“留下可回看的研究现场”，而不是直接承担结论。

## 推荐分类

- `_inbox/`：新收到、尚未完成登记和分类的素材。
- `official/`：官网、官方社媒、公告、预告、开发者材料。
- `gameplay/`：原始实机、直播、VOD、录屏。
- `screenshots/`：原生静态截图；从视频抽取的关键帧进入 `02_evidence/derived/`。
- `interviews/`：开发者、媒体、玩家/测试者访谈原件。
- `social/`：X、Reddit、Discord、论坛短帖、评论、讨论串快照等。
- `press_media/`：媒体新闻、preview、评测和专题文章。
- `recruiting/`：招聘与团队/技术方向材料。
- `technical/`：版本信息、连接报错、服务器/性能、网络测试相关材料。
- `community/`：社区整理帖、长期讨论、二手汇总材料。

## 入库规则

1. 新素材可以先进入 `_inbox/`，但完成正式入库前必须分配 `source_id`。
2. `02_evidence/source_register.jsonl` 是来源主表；旧 `source_register.csv` 只作为可选的人类查看导出，不作为唯一真源。
3. 每个实际保存文件必须登记到 `asset_manifest.jsonl` 并获得 `asset_id`。
4. 文件名推荐：`YYYYMMDD_source-id_short-topic_序号.ext`。
5. 同一个网页的 HTML、截图、附件可共享一个 `source_id`，但每个文件有独立 `asset_id`。
6. 不覆盖原件；来源更新时新增版本并记录 `supersedes_source_id` 或 `derived_from_asset_id`。
7. 测试协议、转载权限、隐私状态不明确时，先标为 restricted/unknown。

本目录不放 OCR、逐字稿、关键帧、翻译、摘要或分析。这些衍生材料进入 `02_evidence/derived/`。
