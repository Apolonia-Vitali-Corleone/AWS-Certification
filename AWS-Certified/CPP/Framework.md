# AWS CAF（Cloud Adoption Framework）

**Business Perspectives（业务视角）：**

1. **Business Perspective** - 专注于确保云投资能够加速数字化转型并实现业务成果
2. **People Perspective** - 支持组织文化演进，帮助员工适应云环境下的新工作方式
3. **Governance Perspective** - 专注于协调IT战略与业务战略，最大化业务价值并最小化风险

**Technical Perspectives（技术视角）：**

4. **Platform Perspective** - 专注于加速云原生解决方案的交付 
5. **Security Perspective** - 确保组织满足安全和合规目标 
6. **Operations Perspective** - 确保云服务的交付能够满足业务需求

## Business Perspective

## People Perspective

## Governance Perspective



## Platform Perspective

**Data engineering → Platform**（数据工程属平台基座能力）

**CI/CD → Platform**（持续集成与交付是平台工程/DevOps 能力）



## Security Perspective

**Incident response（安全事件响应）**——处理与安全相关的事件与入侵。[AWS Documentation](https://docs.aws.amazon.com/whitepapers/latest/aws-caf-security-perspective/incident-response.html?utm_source=chatgpt.com)

**Infrastructure protection（基础设施防护）**——保护网络与计算资源免受未授权访问与漏洞威胁。

**Infrastructure protection → Security**（基础设施防护属安全能力：IAM/网络/主机等）



## Operations Perspective

**Observability**、**Availability and continuity** 也都归在 **Operations** 视角

 **“Incident and problem management（事件与问题管理）” 属于 \*Operations（运营）\* 视角**

**Performance and capacity management → Operations**（运行容量/性能管控是运维能力）

**Change and release management → Operations**（变更与发布管理是运维流程能力）

# CAF KEY WORDS

**Business（业务）**：谈**战略与价值**、商业案例、预算与收益。
 *keywords*: business case/value, strategy, portfolio, ROI, funding, KPIs

**People（人员）**：谈**人和组织**：角色分工、技能培训、变更管理、云素养。
 *keywords*: roles, org change, training, **cloud fluency**, talent, culture

**Governance（治理）**：谈**规章与把关**：政策、合规、风险、财务治理、采购。
 *keywords*: policy/standards, risk, compliance, **FinOps/Cloud financial mgmt**, sourcing

**Platform（平台）**：谈**技术底座**：着陆区、网络、计算、存储、数据库、自动化 IaC。
 *keywords*: landing zone, VPC/network, compute/storage/db, CI/CD, IaC

**Security（安全）**：谈**保护与控制**：身份、数据保护、检测与响应。
 *keywords*: IAM, data protection/KMS, detective controls, threat/vuln, incident response

**Operations（运维）**：谈**Day-2 运行**：监控告警、变更发布、事件/问题管理、SRE、自动化。
 *keywords*: monitoring/observability, incident/problem, change/release, runbooks, automation

# Cloud Transformation Journey

CAF 的旅程有 **4 个推荐阶段**：

1. **Envision**：明确商业愿景与期望业务成果，确定云采用的价值假设与成功指标。
2. **Align**：对齐高层/业务/IT，做能力差距评估，制定路线图与投资组合（people、process、technology）。
3. **Launch**：选定试点用例，落地基础（landing zone、安全、运营），验证价值。
4. **Scale**：把成功模式规模化，扩展到更多业务单元与工作负载，持续治理与优化。

# AWS Well-Architect Framework

用于**已在云上的工作负载**做架构体检（6大支柱）

**六大支柱（6 Pillars）**：

1. **Operational Excellence（运维卓越）**：run-books、自动化、演练、可观测。
2. **Security（安全）**：最小权限、分层防御、数据保护、可追溯。
3. **Reliability（可靠性）**：故障域、冗余、自动恢复、变更管理。
   - **Elasticity = 自动伸缩 + 自愈能力**：能**自动增加/减少/替换**资源来应对故障与负载变化（如 ASG 替换不健康实例、Serverless 扩缩容）。这种“可恢复 + 维持可用”的效果，最贴近题干的“系统在遇到运行问题仍能保持功能”。在 Well-Architected 语境里，这属于**可靠性/弹性（resiliency）**的体现；若有 “Resiliency/Reliability” 选项应选它，但没有时 **Elasticity** 是最相近的概念。
4. **Performance Efficiency（性能效率）**：选型与弹性、基准测试。
   - 资源与性能效率。
5. **Cost Optimization（成本优化）**：按需、观察/分摊、优化使用率。
6. **Sustainability（可持续性）**：能耗/碳足迹感知、效率改进。
