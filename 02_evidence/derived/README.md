# derived：AI 可读衍生材料

这里保存由原始素材生成、但不替代原件的中间产物。

推荐子目录：`transcripts/`、`ocr/`、`keyframes/`、`web_text/`、`translations/`。

命名建议：`asset-id__derived-type__v01.ext`。每个衍生文件必须在 `asset_manifest.jsonl` 中记录 `derived_from_asset_id`、处理方法、处理时间和语言。

逐字稿应保留说话人和时间码；OCR 应保留来源图片 `asset_id`；关键帧必须保留视频时间码。不要把模型自动生成的画面解释当成已确认事实，解释仍需经过 observation 层确认。
