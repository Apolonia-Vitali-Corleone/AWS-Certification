# Kinesis Video Streams

# MediaConvert

# MediaLive

# MediaPackage

# MediaStore

# MediaTailor

# Elemental Appliances & Software

# Elastic Transcoder

将于 **2025-11-13** 终止服务

**AWS Elastic Transcoder 是什么？干什么用？**

- **它是**：AWS 早期的**托管转码服务**（Managed Transcoding Service），把存到 **S3（Amazon Simple Storage Service，简单存储服务）** 的视频/音频**批量转成**不同**格式/码率/分辨率**，以便在各种设备上播放。
- **怎么用**：创建 **Pipeline（管线）** → 以 **Job（作业）** 指定输入 S3 对象与**Preset（预设参数）** → 输出多个版本到 S3；可发 **SNS（Amazon Simple Notification Service，简单通知服务）** 回调。
- **能做**：H.264/MP4、HLS（HTTP Live Streaming，HTTP 实时流）打包、WebM、音频转码、生成缩略图/水印、字幕传递等。
- **典型场景**：离线 **VOD（Video on Demand，点播）** 资产批量转多清晰度与容器格式。

**和现在主推的服务对比**

- **AWS Elemental MediaConvert**（文件式转码，现行主力）：功能更全（HEVC/H.265、4K/HDR、专业编解码、DRM、复杂打包、广播级特性），更适合**新项目**。
- **Elastic Transcoder**：较**简单/便宜**、功能有限，**多年不再新增特性**；官方一般**建议新工作负载选 MediaConvert**。
- **直播（Live）**：用 **AWS Elemental MediaLive + MediaPackage**，不是 Elastic Transcoder。

**一眼记住**

- **老牌点播转码** → Elastic Transcoder（简单、基础）。
- **新建/专业需求** → MediaConvert。
- **直播** → MediaLive/MediaPackage。





# Amazon Interactive Video Service

# AWS Deadline Cloud

# MediaConnect