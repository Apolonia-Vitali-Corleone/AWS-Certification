# AWS Application Discovery Service

把本地服务器直接全部搬运到EC2上

# AWS Application Migration Service 

# AWS Database Migration Service (AWS DMS) 

# Migration Evaluator 

# AWS Migration Hub

不执行迁移

# AWS Schema Conversion Tool (AWS SCT) 

# AWS Snow Family 

# AWS Migration Hub Refactor Spaces 

# AWS Transfer Family

# AWS DataSync

托管的数据迁移/同步服务，支持 NFS/SMB、对象存储 ⇄ S3/EFS/FSx 等；**传输中使用 TLS 加密**，并通过**校验和/元数据比对**做**端到端完整性验证**，专门解决“把文件/对象安全、可验证地搬到 AWS”的需求。

支持以 **SMB 端点**做文件双向迁移/同步。

# AWS MAP（Migration Acceleration Program）

三阶段：

- **Assess** → **Mobilize** → **Migrate & Modernize**。

# Repurchase

放弃原系统，直接买现成 SaaS 产品替代。

将自研/自管 CRM/ERP/BI 等，改用 **SaaS**（如 Salesforce、Workday、Atlassian Cloud、QuickSight 等）。

# Replatform

不改业务逻辑，只换更省心的平台/托管服务。

自建 MySQL → **Amazon RDS**；自建对象存储 → **S3**；自管队列 → **SQS/SNS**；Tomcat → **Elastic Beanstalk** / **ECS/EKS**。

# Rehost

基本不改应用，直接把机器从本地搬到云上。

AWS Application Migration Service (MGN) 把物理/VM 复制成 **EC2**；块存储上 **EBS**；网络按原样建 **VPC**。

# Refactor

改代码/架构，拆单体为微服务，深度用云原生。

**Lambda / API Gateway / Step Functions / SQS / SNS / DynamoDB / Aurora / ElastiCache / EventBridge / EKS** 等。

# Retire

停止使用并下线某应用/组件，保留必要数据后**关停并回收资源**。

功能被 SaaS/新系统取代、使用率极低、维护成本高、已到生命周期末期。