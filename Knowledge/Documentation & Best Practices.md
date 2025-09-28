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



# AWS Architecture Center

是做什么的？

- **定位**：不是云服务，而是**官方架构资料库/最佳实践门户**。
- **你能在这里找到**：
  1. 参考架构图和部署蓝图（Web 三层、Serverless、电商、数据湖、DR 等）；
  2. 解决方案模式与设计指南（高可用、伸缩、成本优化、安全基线）；
  3. 行业场景合集（金融、游戏、媒体、制造等）；
  4. Well-Architected 相关内容、白皮书、图标库、架构图模板、示例代码与教程链接。
- **什么时候用**：
  - 备考/学习：快速对照“官方推荐怎么搭”；
  - 方案评审：找**可复用**的参考设计与权衡点；
  - 落地实施：复制架构图/清单，按指南配置组件并核对最佳实践。
- **和具体服务的关系**：
  - 它不提供计算/存储功能；而是告诉你**这些服务如何拼装**成一套可靠、可扩展、可控成本的架构。
- **备考提示（CCP/SAA）**：遇到题干问“到哪里找官方参考架构/最佳实践”，答案通常是 **AWS Architecture Center**（而不是单个服务页面）。



你说得对，这些词很容易混。给你一套“**一句话 + 何时关心 + 怎么验 + AWS 例子**”速记，帮你把边界拉清。

# 核心定义（最短版）

- **Scalability（可扩展性）**：设计层面，系统在**增加资源**时能**线性提升容量/吞吐**的能力（横向更佳）。
- **Elasticity（弹性）**：运行层面，系统能**自动**随负载**增减资源**，峰值不崩、低谷不浪费。
- **Reliability（可靠性）**：系统能**持续按预期工作**的概率/稳定度（少宕机、少错误）。
- **Resiliency（韧性/弹性恢复力）**：遇到**故障**还能**继续服务或快速恢复**（容错、自愈、冗余、灾备）。
- **Consistency（一致性）**：数据视图的**正确性与时效**（强一致/最终一致；读写是否看到同一状态）。

# 关注点 & 常见指标

- **Scalability** → 线性扩展比、吞吐随节点数增长曲线、热点是否消除。
- **Elasticity** → 扩/缩容触发与**收敛时间**、过/欠配率、单位请求成本。
- **Reliability** → **SLA（服务等级协议）/SLO（服务水平目标）**、MTBF（平均无故障时间）、错误率。
- **Resiliency** → **RTO（恢复时间目标）/RPO（恢复点目标）**、故障注入演练结果、故障域隔离。
- **Consistency** → 复制延迟、陈旧读比例、事务隔离级别、幂等保障。

# 典型设计/服务对应（AWS）

- **Scalability**：无状态微服务、分片；**Amazon Aurora 读副本**、**Amazon DynamoDB 分区**。
- **Elasticity**：**EC2 Auto Scaling（自动伸缩）**、**DynamoDB Auto Scaling**、**AWS Lambda 并发**、**Aurora Serverless**。
- **Reliability**：**多可用区（Multi-AZ）**部署、健康检查与重试、**S3 11 个 9 的耐久性**。
- **Resiliency**：**跨区/跨区域**架构、断路器/回退、**Route 53 健康路由**、**Backup/DR（灾难恢复）**演练。
- **Consistency**：**DynamoDB 强一致读/最终一致读**选项、**RDS 只读副本（异步→可能旧）**、**S3 强一致**。

# 容易混的边界

- **Scalability vs Elasticity**：前者是**可否扩**（结构能力），后者是**何时/如何自动扩**（运行策略）。
- **Reliability vs Resiliency**：前者看**长期稳定**，后者看**出故障时的生存/恢复**。
- **Consistency**独立于上面四个，是**数据语义**问题；强一致通常牺牲一些**延迟/可用性**。

# 选择题速决口诀

- 问“**自动随流量增减**” → **Elasticity**。
- 问“**加机器能否更顶量**” → **Scalability**。
- 问“**持续稳定达标**” → **Reliability**。
- 问“**故障仍能用/快恢复**” → **Resiliency**。
- 问“**读到是不是最新**” → **Consistency**。

# 一眼判断示例

- “黑五突增 10× 流量，系统自动扩容 2 分钟稳定” → **Elasticity**（背后要求 **Scalability**）。
- “某可用区故障，业务无感切换，RTO≈0” → **Resiliency**。
- “一年 99.99% 可用，错误率 <0.1%” → **Reliability**。
- “把服务从 3 节点扩到 9 节点，吞吐近 3×” → **Scalability**。
- “读到旧数据 200ms 内收敛为最新” → **（最终）Consistency**。

# 面试/考试小陷阱

- “remain functional when encountering **operational problems**” 更像 **Resiliency** 而不是 Elasticity。
- “低延迟+边缘分发” 是 **CloudFront**；“谁调用了什么 API（应用程序编程接口）**”是 \**CloudTrail\**；“应用与资源监控/日志**”是 **CloudWatch**。

如果你愿意，我可以把这 5 个词做成一页“对照清单（含示例与指标）”方便你打印随身看。