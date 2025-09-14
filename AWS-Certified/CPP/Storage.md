# AWS Backup

备份服务；不提供存储；提供“策略+调度”

automate data protection

# Amazon Elastic Block Store (Amazon EBS) 

块存储；只能EC2使用；只能一个实例挂载

# Amazon Elastic File System (Amazon EFS)

通用NFS文件系统

多机共享，多个EC2同时挂载自动扩缩

EFS=NFS 

# AWS Elastic Disaster Recovery

灾备迁移

# Amazon FSx

FSx=特定文件系统

# Amazon FSx File Gateway

让本地负载访问在AWS中的Windows文件共享

# Amazon FSx for Windows File Server

托管的 Windows 文件服务，通过 SMB 暴露共享给 EC2/本地。

# Amazon S3

对象存储；直接API访问

## Amazon S3 Glacier

冷备份；审计归档

## Amazon S3 Analytics

Storage Class Analysis

分析桶里对象的**访问模式**，帮你判断哪些数据很少被访问、**适合转到 IA 类**（S3 Standard-IA / One Zone-IA），以便你**制定 Lifecycle 迁移规则**来省钱。

## Amazon S3 File Gateway

在本地以 **SMB/NFS 文件共享** 方式挂载，**把文件映射为 S3 对象**；本地透明缓存、后台并行传输与带宽管理，适合归档/备份、数据湖、ML 数据集等。

## Amazon S3 Inventory Report

Amazon S3 的 **数据管理与报告工具**（Management & Analytics 功能家族）。

定期（每日或每周）生成 CSV/ORC/Parquet 格式的清单文件，列出 bucket 中对象的**元数据**（比如存储类、加密状态、标签、版本 ID 等）。

常用于合规审计、大规模对象跟踪、验证加密或生命周期策略。

## Amazon S3 Versioning

因为它专门用来防 **误删/误覆盖**：

- 开启后，**覆盖会生成新版本，旧版本仍可回滚**；
- “删除”只是打一个 **Delete Marker**，**可恢复**到之前版本；
- 还可配合 **MFA Delete** 增强删除保护（可选）。

## Amazon S3 Lifecycle Rules

**做**分层/过期**管理，可能反而把对象**自动删掉，不防误删/误覆盖。

## Amazon S3 Bucket Policies

管**谁能访问**；若授权用户误操作，策略并不能保留旧版本。

## Amazon S3 Server-side Encryption

只管**保密性**（加密存储），**不能**防止被覆盖或删除。

# AWS Storage Gateway

本地到云存储之间的桥梁

back up without changing its existing backup workflow

# Amazon FSx for Lustre

FSx的变体，专为高性能计算（HPC）优化

# Amazon S3 Express One Zeon

关键词：single-digit millisecond latency

