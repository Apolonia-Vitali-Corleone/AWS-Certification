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

# Amazon S3 Glacier

冷备份；审计归档

# Amazon S3 Analytics

Storage Class Analysis

分析桶里对象的**访问模式**，帮你判断哪些数据很少被访问、**适合转到 IA 类**（S3 Standard-IA / One Zone-IA），以便你**制定 Lifecycle 迁移规则**来省钱。

# AWS S3 Inventory Report



# Amazon S3 File Gateway



# AWS Storage Gateway

本地到云存储之间的桥梁

back up without changing its existing backup workflow

# Amazon FSx for Lustre

FSx的变体，专为高性能计算（HPC）优化

# Amazon S3 Express One Zeon

关键词：single-digit millisecond latency

