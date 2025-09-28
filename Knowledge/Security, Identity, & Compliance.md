# 1-Resource Access Manager

`AWS Resource Access Manager (AWS RAM) `

cross-account sharing

# 2-Cognito

Amazon Cognito

APP 终端用户注册和登录

# 3-Secrets Manager 

# 4-GuardDuty

threat detection, findings

monitor AWS accounts, workloads, Amazon S3 buckets

# 5-Amazon Inspector 

漏洞扫描

vulnerabilities, CVE

# 6-Amazon Macie 

S3敏感数据识别

保密功能

PII discovery, S3

# IAM Identity Center





Identity Center 负责 SSO 与权限分配，本质上**不是**用来直接发凭证的服务。

**IAM Identity Center** 提供的是 **SSO/访问分配**（人到账号/角色的映射）。它**内部会调用 STS** 发放短期凭证，但它不是“给开发者直接颁发临时凭证的 API”，而是用于登录门户、CLI SSO 工作流与权限分配的管理层。

**可同时管“自家 AWS 账户 + 第三方 SaaS”**：Identity Center 充当 **IdP（Identity Provider，身份提供方）/ SSO（Single Sign-On，单点登录）中枢**，用 **SAML 2.0 / OIDC** 给上百种第三方应用发登录令牌（如 Microsoft 365、Salesforce、Slack、GitHub 等），并提供**用户门户**统一入口。

# 8-Certificate Manager

`AWS Certificate Manager (ACM)`

# 9-Key Management Service

`AWS Key Management Service (AWS KMS)`

**KMS keys**：用来**加解密**数据，不是身份凭证。

# 10-CloudHSM

硬件密钥模块，做加解密/密钥托管；

# 11-Directory Service

# 12-AWS Firewall Manager

# 13-AWS Artifact

compliance reports

合规内容下载处理

# 14-Detective

investigation

调查

# 15-AWS Signer

# 16-Security Lake

# 17-WAF & Shield

WAF

- web防火墙


- L7 Web规则

Shield

- 抗DDoS

# 18-Amazon Verified Permissions

# 19-AWS Audit Manager

evidence collection

证据自动收集

做框架化**合规评估与取证编排**；可以当“总控台”，但要看**轮换细节**仍需用 **Credential Report** 这类原始证据。

# 20-Security Hub CSPM

# IAM

`AWS Identity and Access Management (IAM) `

多个User在一个Group

- User——长期静态的凭证，也需要轮换哦
- Role——短期动态的凭证

注意

- EC2使用ROLE



只管**AWS 资源的 API 级权限**（用户/角色/策略），**不做用户门户，也不对第三方 SaaS 发 SSO**。

## IAM Access Analyzer

查资源是否对外可访问的分析，不报告密码/密钥轮换。

## IAM Credential Report

因为它专门给你一张**账户内所有 IAM 用户的凭证清单（CSV）**，包含：

- `password_enabled / password_last_changed / password_last_used`
- `access_key_1_active / access_key_1_last_rotated / last_used`（以及 key2 同样字段）
  正好用于**审计密码与访问密钥的轮换/使用情况**（合规需要的细节一键可得）。



# 22-Security Hub

总控

findings, aggregation, posture

# 23-AWS Private Certificate Authority

# 24-AWS Payment Cryptography

# 25-AWS Security Incident Response

# ---

# AWS Security Token Service(AWS STS)

**Role = 权限身份（不能直接用来签名请求）**

**STS = 把 Role/身份兑换成“临时可用的密钥”**

**Instance Profile = 仅限 EC2 的挂载方式，背后还是 STS 在发临时证书**

**STS**（Security Token Service）是**颁发临时凭证的核心 API 服务**：`AssumeRole`、`AssumeRoleWithSAML`、`GetSessionToken` 等，返回 **AccessKeyId + SecretAccessKey + SessionToken**，适用于用户/角色、跨账号、联合身份等**程序化获取临时凭证**的场景。

# ---

# Amazon Cloud Directory

# AWS Network Firewall

网络防火墙

VPC内L3-L7有状态防火墙

# SSH Public Keys

登 **EC2** 的 SSH 用，不能调用 AWS API。



# IAM Role

**跨账号访问**的标准做法是：在**目标账号**创建一个 **IAM Role**，其 **Trust Policy** 允许**源账号的用户/角色**执行 **STS:AssumeRole**，获得**临时凭证**去访问目标资源（按该 Role 的权限策略）。

这样既满足“当前没有权限”的前提，又能最小授权、可审计、可撤销。

# IAM Instance Profiles

只适用于 **EC2**（或 ECS on EC2）把 **Role** 附给实例的“壳”。底层依然是 **实例通过 STS 自动换取临时凭证**；它不是通用的“签发凭证”服务。

**“跑在 EC2 上” = Instance Profile（但本质还是 STS）**。

