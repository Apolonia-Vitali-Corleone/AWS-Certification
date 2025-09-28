# AWS Auto Scaling

自动伸缩

# AWS CloudFormation

IaC

从手工托拽建资源——〉写代码描述来进行配置资源

# AWS CloudTrail

日志追踪

谁在什么时间干了什么事

# Amazon CloudWatch

性能检测平台。

除了性能之外，也能查application日志，查cloud resource



**CloudWatch 提供 Billing 计费指标**（命名空间 `AWS/Billing`，如 `EstimatedCharges`）。

你可以在 **us-east-1** 区域对这些指标创建 **CloudWatch Alarm**，并通过 **SNS** 发送通知（邮件/短信/Webhook 等），当**估算费用**超过阈值就告警。

这正满足“达到特定成本阈值即通知”的需求。

报警本身不发送邮件/短信；通常是**把告警发布到 SNS**再由 SNS 发送。



# AWS Compute Optimizer

一款只能推荐工具，分析资源利用率

只给建议

# AWS Config

资源现在长什么样子，是否合规

# AWS Control Tower

多账户最佳实践面板

# AWS Health Dashboard

健康状态面板

**AWS Health Dashboard**（含 Personal Health Dashboard）只报告**AWS 侧的事件**——服务中断、维护、配额快满等，**不检查你账号的安全组配置**，所以发现不了“某端口对 0.0.0.0/0 放通”这类错误。



提供**全局 AWS 服务状态**与**事件更新**，并且官方就支持**RSS 订阅**（每个区域/服务都有 RSS 源）。



# AWS License Manager

软件许可证管理器

# AWS Systems Manager

统一运维工具

运维套件（自动化、补丁、参数、Fleet Manager）

## AWS Systems Manager Parameter Store

既要存“配置数据”又要存“密码”，Parameter Store 一站式满足：普通配置用 **String**，敏感信息用 **SecureString（KMS 加密）**。

**性价比最高**：Standard 层**按调用计费、无每条密文月租**；而 **Secrets Manager** 对每个 secret **按月收费**（并按调用计费），适合需要**自动轮换/高级审计**等场景，但成本更高。

自带分层路径、版本管理、IAM 细粒度权限，直接被 EC2/Lambda/容器读取，集中管理很方便。

# AWS Management Console

AWS网页UI控制台

# AWS Organizations

更底层；AWS Control Tower基于此

多账号治理与 **SCP**；可配合创建**组织级**的 Access Analyzer

因为 **AWS Organizations 只做账号级治理**（多账号管理、合并计费、组织单元、SCP护栏等），**不会去解析具体资源策略**来判断“这个 S3 bucket/ IAM role 是否被外部主体共享”。

# AWS Service Catalog

内部自建应用商店

你们**自家的 IaC 模板/产品**（CloudFormation/SAM/CDK 产物）；也可发布“已批准的 Marketplace 产品”

# Service Quotas

服务器配额管理



# AWS Trusted Advisor

顾问检查工具；广泛体检

# AWS Well-Architected Tool

架构评估



# AWS Resource Explorer

只是**全局搜资源**/浏览清单，**不治理、不发布模板**。

# AWS Chatbot 

它的用途是把 **CloudWatch / Security Hub / CodeBuild** 等通知推到 **Slack 或 Amazon Chime**，并在聊天里执行部分 **AWS CLI/SDK** 命令做运维协作；它**不提供官方常见问答内容**

# Amazon Data Lifecycle Manager 

# Amazon Elastic Transcoder 

# AWS Launch Wizard

**技术向部署向导/工具**（如 SAP、SQL Server、HANA），帮你**估算与一键部署**到最佳实践架构，但不是人来做迁移。

# AWS Customer Carbon Footprint Tool

环保

# AWS Managed Services（AMS）

**托管运维服务**（监控、补丁、事件、变更等“日常运营”），可在迁移后代运维；不是专门的迁移项目团队。

AMS 是“托管运营”服务，AWS 官方团队+自动化为你**代管日常运维**，适合“已上云、要在规模化下更高效且更安全地运营”的公司

# AWS Professional Services（ProServe）

**付费咨询与交付团队**（架构师/PM/迁移专家），按 AWS 最佳实践**亲自下场做项目**。题干要“全球专家团队”→ **选它**。

# AWS Free Tier

**AWS Free Tier（免费用量）**＝给新手/轻量使用者的一组**免费额度**，超出后按正常价计费。主要分三类：

1. **12 个月免费**（自账号创建起算）
    例：小规格 EC2、RDS、S3 等的部分用量。适合上手练习与小测。
2. **Always Free**（长期有效）
    例：AWS Lambda 每月一定量的请求与计算、DynamoDB 基础用量、API Gateway/CloudWatch 的部分配额等。
3. **短期试用（Trials）**
    某些服务提供 **N 天/次**的临时免费试用配额（随服务不同而不同）。.

# AWS Local Zones

AWS 在某些城市就近建的小型“边缘分区”（仍属 AWS 机房，不在你家机房）。用来把算力放到**靠近用户/媒体工作站**的城市，拿 **单/低两位毫秒**延迟；不是把 AWS 搬到你机房，所以不是“把 AWS 扩展到 on-prem”。



# Amazon Elastic Block Store (Amazon EBS) Snapshots

EBS 卷的增量**时间点备份**，可复制到**跨 Region/账号**，用于恢复/新卷。

# AWS Elastic Disaster Recovery (DRS)

持续复制（block-level）到目标 Region/账号，一键切换/回切（原 CloudEndure）。
