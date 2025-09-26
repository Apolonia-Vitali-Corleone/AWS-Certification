# AWS Migration Hub

不执行迁移

# AWS Application Migration Service

`AWS Application Migration Service (MGN)`

MGN 做的是**整机/块级复制**，把本地物理机或虚机原样“搬到 EC2”（lift-and-shift），不是把**文件**迁到 S3/EFS/FSx。

把本地服务器直接全部搬运到EC2上

# Application Discovery Service

做**资产与依赖发现**（清点服务器、进程、网络依赖），把数据送到 Migration Hub 供**迁移分组/波次规划**用；**不负责生成完整的云上成本估算/商业案例**。若要成本，需要把数据再喂给 ME 或手动进 Pricing Calculator。

`ME:Migration Hub`



只做**发现/清点**：采集本地服务器的清单、依赖与性能数据，然后**把数据喂给 Migration Hub**。它不负责“规划与跟踪”。

# Database Migration Service

`AWS Database Migration Service (AWS DMS) `

special for database migration, not for lots of files

# AWS Transfer Family



| 维度       | **AWS Transfer Family**                                      | **AWS Snow Family**                                          |
| ---------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 核心用途   | **在线**托管 SFTP/FTPS/FTP（托管端点）把文件进/出 **S3 或 EFS** | **离线大规模数据迁移** + **边缘计算**（在设备上跑 EC2/容器） |
| 典型场景   | 伙伴/客户用传统 *FTP/SFTP* 协议与你互传文件；要托管、身份认证、审计 | 带宽差/断网、窗口固定、**TB–PB 级**“首搬”；矿区、船上等边缘场 |
| 连接方式   | 互联网协议：SFTP/FTPS/FTP；身份可用 IAM、目录、AD、OIDC      | 物理设备：**Snowcone / Snowball（Storage/Compute）/ Snowmobile** 寄送 |
| 数据落地   | S3 或 EFS（在线实时可用）                                    | 回寄设备后导入 **S3**（或快照）；也可在设备本地先算后传      |
| 传输特性   | 在线、持续、托管高可用；无代码/低改造替代自建 SFTP 服务器    | 离线高速拷贝：NFS、**on-device S3 端点**、DataSync on Snow、OpsHub |
| 规模/速度  | 受网络带宽限制（可水平扩展端点）                             | 一次装载数十 TB～PB；Snowmobile 可达 **100 PB** 级           |
| 成本模型   | 按端点小时费 + 传输量/请求（落 S3/EFS 的常规费用）           | 设备/作业费 + 驻留天数 + 运输费 + 上云后存储费用             |
| 关键不做   | 不解决弱网/断网；不做物理搬运                                | 不是互联网上的 SFTP 托管服务                                 |
| 考点关键词 | “SFTP/FTPS/FTP 到 S3/EFS”“合作伙伴文件交换”“托管端点/身份审计” | “离线迁移”“TB–PB”“边缘/断网”“Snowcone/Snowball/Snowmobile”   |

`一句话记忆`

- **Transfer Family**：**在线协议网关**（SFTP/FTPS/FTP ↔️ S3/EFS）。
- **Snow Family**：**离线卡车/箱子把数据搬到云上 + 可在边缘先计算**。

`选择规则（超短）`

- 需要 **SFTP/FTPS/FTP** 对接 → **Transfer Family**。
- 网络不给力、数据量特别大、或在边缘现场作业 → **Snow Family**。

# AWS Snow Family

## Snowmobile

`10PB(petabytes) or more`

## Snowball



## Snowcone



下面给你一份**AWS Snow Family（离线迁移 + 边缘计算）系统化速记**（含关键英文名词，便于做题/查文档）。

`1. 家族成员（硬件）`

- **AWS Snowcone / Snowcone SSD**
  - 最小最轻（便携/电池包可选/恶劣环境）。
  - 用途：**小规模离线数据迁移**、极端边缘场景的**轻量计算**（EC2 小规格、容器 via AWS IoT Greengrass）。
  - 预装 **AWS OpsHub** 支持、可跑 **AWS DataSync agent**（把本地数据经局域网搬到设备，再回 AWS）。
- **AWS Snowball（Edge）**
  - 两类机型：
    - **Storage Optimized**（以大容量为主，内置 **S3 兼容端点 + NFS**，适合批量数据导入/导出）。
    - **Compute Optimized**（更多 vCPU/内存/本地 NVMe，支持 **EC2 实例**、**容器/Greengrass**、可做本地推理、预处理、分布式边缘集群）。
  - 可多台组成集群，适合**TB～PB 级离线迁移**与**边缘计算**二合一。
- **AWS Snowmobile**
  - 45 英尺集装箱卡车，**一次最多 ~100 PB** 级数据迁移（超大规模数据中心退役/全量归档时用）。

> 记忆：**Snowcone（小） → Snowball（中：存储/计算两型） → Snowmobile（超大）**

`2. 核心能力（两大类）`

1. **离线数据迁移（Offline Data Transfer）**
   - 典型流程：**下单 Job → 设备寄送 → 本地拷贝（NFS/S3 端点/DataSync/OpsHub）→ 寄回 → AWS 把数据导入 S3/创建快照**。
   - 适用：带宽受限、时间窗口固定、海量历史数据“首搬”。
   - 接口形态：
     - **S3-compatible on-device**（常见于 Snowball Storage Optimized）
     - **NFS**（NAS 直接挂载）
     - **DataSync agent**（自动化/断点续传/校验）
     - **OpsHub**（GUI 管理与拷贝）
2. **边缘计算（Edge Compute at the Edge）**
   - 在设备上直接运行 **EC2 实例**、**容器/Greengrass**、本地 **对象/块/文件**存储，进行**就地推理/过滤/聚合**，再回传结果。
   - 适用：断网/弱网、低时延、受物理/法规限制必须本地处理的数据场景。
   - 可与 **EKS Anywhere、IoT、AI 推理框架**等结合（按项目需要）。

`3. 管理与工具（配套）`

- **AWS OpsHub for Snow Family**：GUI 一体化管理（激活/解锁、监控、数据拷贝、启动 EC2、创建桶/NFS 等）。
- **AWS DataSync（on Snow）**：把 NAS/文件服务器数据**高效拷入设备**，或设备回 AWS 后**自动上云**。
- **Snowball Client / CLI**：命令行导入导出（适合自动化管道）。
- **AWS Key Management Service (KMS)**：**端到端加密**（设备上数据全加密，密钥不落地）。
- **Chain-of-custody & 物流追踪**：篡改防护、封条/机身检测、运单追踪（企业合规友好）。

`4. 常见接口方式（怎么“接线”）`

- **NFS**：把设备当 NAS 挂载，直接拷贝文件。
- **S3 兼容端点（on-device S3 endpoint）**：应用用 S3 API 写入“设备上的对象存储”。
- **DataSync**：图形化/脚本化任务，传输/校验/带宽控制/重试更省心。
- **本地块/对象/文件**：在边缘计算场景为 EC2/容器提供数据盘或对象接口。

`5. 选型原则（面试/考试拿分版）`

- **数据量**：
  - **< 十 TB、极端便携** → Snowcone / Snowcone SSD
  - **几十～上百 TB/数 PB** → Snowball（Storage Optimized 为主）
  - **几十 PB～百 PB 级** → Snowmobile
- **有没有边缘算力**：
  - 要在现场跑模型/预处理/断网自治 → 选 **Compute Optimized**（Snowball），或轻量场景用 **Snowcone**。
- **接口偏好**：
  - 现有备份/NAS → **NFS**；应用已会 S3 → **S3 端点**；要自动化/校验/批量任务 → **DataSync on Snow**。
- **网络条件**：
  - 带宽差/断网 → Snow（离线）优于在线迁移（如纯 DataSync over WAN）。
- **时间窗口**：
  - 短时间必须“搬完” → Snow 设备批量并行拷贝 + 物流回传最快。

`6. 安全与合规要点`

- **硬件防篡改 + 全盘加密（AES-256）+ KMS 托管密钥**；解锁需 **manifest + unlock code** 双要素。
- **设备丢失/被盗**：无密钥不可读；后台可**远程擦除与禁用**。
- **数据完整性校验**：传输前后校验（manifest/哈希），导入 S3 后可比对。
- **链路**：全流程可审计追踪，满足企业与法规对链路管控的要求。

`7. 计费构成（理解即可）`

- **每台/每作业（per device/job）服务费**
- **在站点的日费（per-day fee）**
- **运输与关税**（根据地区）
- **上云后存储/请求费用**（落到 S3/快照等后按常规计费）

`8. 常见误区`

- **“要搬很多数据就用 DataSync”**：DataSync 适合**在线**持续/周期同步；**首搬海量**且带宽受限时，**Snow 家族效率更高**。
- **“Snow 只能迁移不能算”**：Snowball/ Snowcone 都能**跑 EC2/容器/Greengrass**，是真·边缘计算设备。
- **“Snowball 没有 S3 接口”**：**Storage Optimized** 提供 **S3 兼容端点**，很多应用可零改造写入。

------

要不要我给你做一张**一页对比表（设备→容量等级→接口→是否可计算→典型场景→如何接线）**放到 Canvas，便于打印/背题？

# DataSync

托管的数据迁移/同步服务，支持 NFS/SMB、对象存储 ⇄ S3/EFS/FSx 等；**传输中使用 TLS 加密**，并通过**校验和/元数据比对**做**端到端完整性验证**，专门解决“把文件/对象安全、可验证地搬到 AWS”的需求。

支持以 **SMB 端点**做文件双向迁移/同步。



DataSync 不仅能“持续同步”，也能做“一次性的大批量迁移”。



# AWS Transform

# AWS Mainframe Modernization

# Amazon Elastic VMware Service

# ---

# Migration Evaluator

https://console.tsologic.com/signin

# ---



# AWS Schema Conversion Tool (AWS SCT) 

# AWS Migration Hub Refactor Spaces 







# AWS MAP（Migration Acceleration Program）

三阶段：

- **Assess** → **Mobilize** → **Migrate & Modernize**。



# RExx Family

## Repurchase

放弃原系统，直接买现成 SaaS 产品替代。

将自研/自管 CRM/ERP/BI 等，改用 **SaaS**（如 Salesforce、Workday、Atlassian Cloud、QuickSight 等）。



## Replatform

不改业务逻辑，只换更省心的平台/托管服务。

自建 MySQL → **Amazon RDS**；自建对象存储 → **S3**；自管队列 → **SQS/SNS**；Tomcat → **Elastic Beanstalk** / **ECS/EKS**。



## Rehost

基本不改应用，直接把机器从本地搬到云上。

AWS Application Migration Service (MGN) 把物理/VM 复制成 **EC2**；块存储上 **EBS**；网络按原样建 **VPC**。



## Refactor

改代码/架构，拆单体为微服务，深度用云原生。

**Lambda / API Gateway / Step Functions / SQS / SNS / DynamoDB / Aurora / ElastiCache / EventBridge / EKS** 等。



## Retire

停止使用并下线某应用/组件，保留必要数据后**关停并回收资源**。

功能被 SaaS/新系统取代、使用率极低、维护成本高、已到生命周期末期。