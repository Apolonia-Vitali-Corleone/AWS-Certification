# AWS Auto Scaling

自动伸缩

# AWS CloudFormation

IaC

从手工托拽建资源——〉写代码描述来进行配置资源

# AWS CloudTrail

日志追踪

谁在什么时间干了什么事

# Amazon CloudWatch

性能检测平台

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

# AWS License Manager

软件许可证管理器

# AWS Management Console

AWS网页UI控制台

# AWS Organizations

更底层；AWS Control Tower基于此

多账号治理与 **SCP**；可配合创建**组织级**的 Access Analyzer，

# AWS Service Catalog

内部自建应用商店

你们**自家的 IaC 模板/产品**（CloudFormation/SAM/CDK 产物）；也可发布“已批准的 Marketplace 产品”

# Service Quotas

服务器配额管理

# AWS Systems Manager

统一运维工具

运维套件（自动化、补丁、参数、Fleet Manager）

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

# AWS Professional Services（ProServe）

**付费咨询与交付团队**（架构师/PM/迁移专家），按 AWS 最佳实践**亲自下场做项目**。题干要“全球专家团队”→ **选它**。

# AWS Free Tier

**AWS Free Tier（免费用量）**＝给新手/轻量使用者的一组**免费额度**，超出后按正常价计费。主要分三类：

1. **12 个月免费**（自账号创建起算）
    例：小规格 EC2、RDS、S3 等的部分用量。适合上手练习与小测。
2. **Always Free**（长期有效）
    例：AWS Lambda 每月一定量的请求与计算、DynamoDB 基础用量、API Gateway/CloudWatch 的部分配额等。
3. **短期试用（Trials）**
    某些服务提供 **N 天/次**的临时免费试用配额（随服务不同而不同）。
