# AWS Artifact

compliance reports

合规内容下载处理

# AWS Audit Manager 

evidence collection

证据自动收集

做框架化**合规评估与取证编排**；可以当“总控台”，但要看**轮换细节**仍需用 **Credential Report** 这类原始证据。

# AWS Certificate Manager (ACM) 

# AWS CloudHSM 

# Amazon Cognito

APP 终端用户注册和登录

# Amazon Detective

investigation

调查

# AWS Directory Service

# AWS Firewall Manager

# Amazon GuardDuty

threat detection, findings

monitor AWS accounts, workloads, Amazon S3 buckets

# AWS Identity and Access Management (IAM) 

多个User在一个Group

- User——长期静态的凭证
- Role——短期动态的凭证

注意

- EC2使用ROLE

# AWS IAM Identity Center

# IAM Access Analyzer

查资源是否对外可访问的分析，不报告密码/密钥轮换。

# IAM Credential Report

因为它专门给你一张**账户内所有 IAM 用户的凭证清单（CSV）**，包含：

- `password_enabled / password_last_changed / password_last_used`
- `access_key_1_active / access_key_1_last_rotated / last_used`（以及 key2 同样字段）
   正好用于**审计密码与访问密钥的轮换/使用情况**（合规需要的细节一键可得）。

# Amazon Inspector 

漏洞扫描

vulnerabilities, CVE

# AWS Key Management Service (AWS KMS)

**KMS keys**：用来**加解密**数据，不是身份凭证。

# Amazon Macie 

S3敏感数据识别

保密功能

PII discovery, S3

# AWS Resource Access Manager (AWS RAM) 

cross-account sharing

# AWS Secrets Manager 

# AWS Security Hub

总控

findings, aggregation, posture

# AWS Shield

抗DDoS

# AWS WAF

web防火墙

L7 Web规则

# Amazon Cloud Directory

# AWS Network Firewall

网络防火墙

VPC内L3-L7有状态防火墙

# SSH Public Keys

登 **EC2** 的 SSH 用，不能调用 AWS API。

