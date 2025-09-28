# S3

Amazon Simple Storage Service

对象存储；直接API访问

## S3 Glacier

冷备份；审计归档



## S3 Glacier Deep Archive

**极冷归档，**取回慢且有取回费**，不适合“每天访问一部分”的需求。



## S3 Analytics

Storage Class Analysis

分析桶里对象的**访问模式**，帮你判断哪些数据很少被访问、**适合转到 IA 类**（S3 Standard-IA / One Zone-IA），以便你**制定 Lifecycle 迁移规则**来省钱。



## S3 File Gateway

在本地以 **SMB/NFS 文件共享** 方式挂载，**把文件映射为 S3 对象**；本地透明缓存、后台并行传输与带宽管理，适合归档/备份、数据湖、ML 数据集等。



## S3 Inventory Report

Amazon S3 的 **数据管理与报告工具**（Management & Analytics 功能家族）。

定期（每日或每周）生成 CSV/ORC/Parquet 格式的清单文件，列出 bucket 中对象的**元数据**（比如存储类、加密状态、标签、版本 ID 等）。

常用于合规审计、大规模对象跟踪、验证加密或生命周期策略。

做清单/报表，帮助审计与计费分析，本身不迁移/归档。





## S3 Versioning

因为它专门用来防 **误删/误覆盖**：

- 开启后，**覆盖会生成新版本，旧版本仍可回滚**；
- “删除”只是打一个 **Delete Marker**，**可恢复**到之前版本；
- 还可配合 **MFA Delete** 增强删除保护（可选）。



## S3 Lifecycle Rules

**做**分层/过期**管理，可能反而把对象**自动删掉，不防误删/误覆盖。

你要做的是**把不常访问的数据自动归档到更便宜的存储层**（如 Standard-IA、Glacier、Glacier Deep Archive），并可在到期时**自动删除**——这正是 **S3 Lifecycle** 规则的作用（基于前缀/标签，按天数自动 *Transition* / *Expiration*）。



## S3 Object Lock

WORM/合规保留与法律保留，和节省成本无直接关系。



## S3 Bucket Policies

管**谁能访问**；若授权用户误操作，策略并不能保留旧版本。

## S3 Server-side Encryption

只管**保密性**（加密存储），**不能**防止被覆盖或删除。



## S3 Transfer Acceleration

- **长距离传输提速**：把上传/下载先就近打到 CloudFront 全球边缘站点，再走 AWS 专用骨干到目标桶所在 Region，显著降低跨洲/跨国延迟与丢包影响。

- **安全**：全程使用 HTTPS/TLS（到边缘站点、再到 S3），满足“securely”的要求。

它让**客户端就近连到 CloudFront 边缘站点**，随后通过 **AWS 全球骨干网**把数据“加速隧道”传到目标 S3 区域，从而**降低端到端延迟、提高上传/下载速度**。



## S3 Intelligent-Tiering 

做**存储成本分层**，与传输速度无关。

一种 **自动分层** 的 S3 存储类型：根据**实际访问频率**，自动把对象放到最省钱的层里。

适合**访问模式未知或经常变化**的数据，你无需自己判断用 Standard/IA/Archive。

小提示：若“是否会被访问”难以预估，可用 **S3 Intelligent-Tiering**；而已知“老化后不常访问”的固定规律，用 **Lifecycle** 最合适。

Intelligent-Tiering 会**自动按最近访问频率在多个层级间搬移**（Frequent/IA/可选 Archive 层），**不需要你手工分类**。

**成本最优**：常读的数据留在 Frequent；变冷后自动进 IA/Archive 层拿更低单价。Frequent 与 IA **无取回费**，只收很低的**监控与自动化费用**（按对象计），整体对“冷热混合+不可预知”场景通常更省钱。



## S3 Express One Zeon

关键词：single-digit millisecond latency

## S3 ACLs

管权限控制；

## S3 Standard-IA

`S3 Standard-Infrequent Access`

多 AZ 冗余，价格高于 One Zone-IA；



## S3 One Zone-IA

`S3 One Zone-Infrequent Access`



## S3 Cross-Region Replication

S3 Cross-Region Replication, CRR

CRR 是**桶到桶的异地复制**，用于合规/容灾/就近读取的**后端副本同步**。它不改变**终端用户 → S3** 的传输路径，也**不会加速**用户到 S3 的上传/下载；甚至复制会带来额外费用与延迟。

# EFS

`Amazon Elastic File System (Amazon EFS)`

通用NFS文件系统

多机共享，多个EC2同时挂载自动扩缩

EFS=NFS 

# FSx

FSx=特定文件系统



## FSx File Gateway

让本地负载访问在AWS中的Windows文件共享

给 **FSx for Windows File Server** 提供 **SMB** 访问/缓存，**不支持 NFS**。



## FSx for Windows File Server

托管的 Windows 文件服务，通过 SMB 暴露共享给 EC2/本地。

## FSx for Lustre

FSx的变体，专为高性能计算（HPC）优化

# Storage Gateway

本地到云存储之间的桥梁

back up without changing its existing backup workflow

# AWS Backup

备份服务；不提供存储；提供“策略+调度”

automate data protection

# Recycle Bin

# AWS Elastic Disaster Recovery

灾备迁移

# ---

# ---















