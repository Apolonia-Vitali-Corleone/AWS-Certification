# AWS Amplify

面向前端/全栈开发的**应用开发平台**与工具链（CLI/库/Hosting/后端生成）。

一键接入 **认证( Cognito )**、**存储(S3)**、**函数(Lambda)**、**API(REST 或 GraphQL)**、静态站点 **托管与CI/CD**、本地开发与环境管理。

Cognito、S3、API Gateway+Lambda、**AppSync**、DynamoDB、Secrets Manager

Web/移动端快速搭建登录、数据、文件、推送、托管的**成套应用**。

**覆盖端到端（前端+后端+托管）的开发体验；AppSync 只是它可以创建使用的一个后端选项**。

# AWS AppSync

托管的**GraphQL API 服务**（含实时订阅、细粒度鉴权、缓存、冲突解决）

  GraphQL Schema/Resolver、**实时(Subscriptions)**、多源聚合、细粒度授权（Cognito/IAM/OIDC/API Key）、Pipeline Resolver、Response Caching。

**DynamoDB**、Lambda、OpenSearch、Aurora Serverless (Data API)、HTTP、S3（签名URL）

给多个客户端/微服务提供**统一的 GraphQL 数据层**与实时更新。

  只负责**API 层（GraphQL）**；不管前端托管与整体应用脚手架。Amplify 的 GraphQL 后端默认就是用 **AppSync** 实现。

# Device Farm

# Amazon Location Service

# 选型速记

- 想要**一站式**“前端+托管+后端资源生成”，少折腾基础设施 → **Amplify**。
- 你已经有/想单独设计一层**GraphQL 网关**（聚合多数据源、实时订阅、细粒度鉴权） → **AppSync**。
- 两者常一起用：**Amplify 生成并驱动 AppSync** 的 GraphQL API，数据落 **DynamoDB**，登录走 **Cognito**，前端托管用 **Amplify Hosting**。



