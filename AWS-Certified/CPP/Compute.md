# AWS Fargate

容器化“任务/服务”（Web、Worker、批处理）

**容器**运行（ECS/EKS 的无服务器计算层）

无服务器容器运行时，**看不到也不能管理底层主机**

# AWS Lambda

**函数**运行（事件驱动 FaaS）

事件触发函数（API、S3、队列、定时）

**Lambda 单次调用上限是 15 分钟**，不适合长时间批处理。



# AWS Batch

**AWS Batch = 任务排队机 + 自动开关一群临时服务器**；
 你只把“要干的活（脚本/容器）”丢进去，Batch 会按队列自动**拉起/回收**算力并**重试失败**。
 **EC2** 则是你自己先准备好服务器，再自己排队、扩缩容、容错。

3 个开关（记住就会用）

- **Compute Environment**：用什么算力（EC2/Fargate，On-Demand/Spot，最多开到多少 vCPU）。
- **Job Queue**：活儿排队的地方，先来先干/按优先级。
- **Job Definition**：怎么干（用哪个 Docker 镜像、命令、vCPU/内存、超时/重试）。

`一眼例子`

> **有 10,000 张图片要加水印，每张处理 1 分钟，能被中断后重试。**

- **用 EC2：**
   你得：估算要几台机 → 建 ASG → 写 SQS 消费与扩缩容逻辑 → 处理失败重试 → 干完别忘了关机。
- **用 Batch：**
   做一个打好水印的 **Docker 镜像** → 注册成 **Job Definition** → 提交 **array job(1..10000)** →
   Batch 自动：按负载**开一批（可用 Spot 省钱）**→ 分发任务 → 失败**重试** → 干完**缩到 0**。

`什么时候选谁（考试/实战速记）`

- **Batch**：成千上万 **无状态、可重试、离线**任务（仿真/转码/ETL）；**峰来开、峰去关**；**吃 Spot**。
- **EC2**：**长期在线**服务或你要**完全掌控服务器**（自管队列与伸缩）。

> 背口诀：**“有活就开工，没活就散场——选 Batch；一直营业——选 EC2。”**

# EC2

supported by Saving Plans

## EC2 Instance

**Convertible Reserved Instances（可转换预留实例）是什么意思？**

- **本质**：一种 EC2 的**计费承诺**（1 年或 3 年）。你承诺长期使用，换取较大折扣。

- **“可转换”**：在有效期内你可以把现有 RI **兑换**成其它配置，典型可改：

  - **实例家族/代数**（如 m5 ↔ r7）
  - **实例大小**（2xlarge ↔ 4xlarge 等，按归一化单位折算）
  - **操作系统**（Linux ↔ Windows）
  - **租赁类型**（Shared ↔ Dedicated）
  - **支付方式**（All/Partial/No Upfront）

  > 交换时要求新组合的**价值（按官方小时价）≥ 原 RI 价值**。**不能跨 Region**。

- **折扣**：**比 Standard RI（标准预留）小**，但换来上述灵活性。

- **容量**：和 Standard 一样，做 **Zonal RI** 才会保留容量；**Regional RI** 只是价格折扣。

- **适用**：需要长期运行，但**未来可能更换实例家族/系统**等不确定的场景。

- **不适用**：规格很确定且稳定 → 选 **Standard RI** 折扣更高；
  不想签约 → **On-Demand**；
  能容忍中断、追求最低价 → **Spot**（可能被回收）。

## AMIs

`Amazon Machine Images (AMIs)`

实例模板（系统盘快照 + 启动配置），可 **跨 Region/账号复制**，一键重建 EC2。

## EBS

`Elastic Block Store (Amazon EBS) `

块存储；只能EC2使用；只能一个实例挂载

## Instance store

本地盘（Instance store）快又近，但**掉电就忘**；EBS/EFS/S3 是**服务级持久化**。

# EC2 Image Builder

# AWS Elastic Beanstalk

托管应用平台（PaaS）

底层可控

托管应用托管平台 PaaS

可托管应用，也支持 Docker，但**需要你自备 Dockerfile/镜像**或 Dockerrun；不会像 App Runner 那样从源码自动制镜像并持续部署。

**Spring Boot 商城后端**
 把 jar 上传到 EB 的 **Java 平台** → EB 自动建好 ALB、ASG、EC2，设置健康检查；你只关心版本发布与环境变量（DB_URL、REDIS_URL）。

**Node.js（Express）API**
 选择 **Node.js 平台**，`npm start` 作为入口；高峰期 EB 自动横向扩容实例，闲时缩回去。

**Django + Gunicorn**
 用 **Python 平台**或打成 **Docker 镜像**；配置 `.ebextensions` 写 Nginx 反代、环境变量、静态文件收集。

**Go（Gin）服务**
 直接选 **Go 平台**或提供 **Dockerfile**；滚动发布无中断，失败自动回滚旧版本。

**队列消费者（Worker 环境）**
 EB 的 **Worker 环境**自带 **SQS** 轮询：推送订单消息到队列，Worker 实例自动拉取执行（图像处理、发邮件等）。

# Amazon Lightsail

pre-configured application stacks

# AWS Outposts 

on-premise AWS（本地AWS）

把AWS硬件与服务下沉到本地机房

# AWS App Runner

App Runner 是面向**Web 服务/API**的全托管平台，支持**从源码直出镜像并部署**：

- 连接 GitHub/CodeCommit（或直接接容器镜像）。
- 使用 **Cloud Native Buildpacks（经由 CodeBuild）自动构建容器镜像**，再一键部署。
- 自带 HTTPS、健康检查、自动伸缩与负载均衡，几乎无需运维。

# AWS Copilot 

CLI工具

# AWS Wavelength

5G移动边缘计算

# AWS Compute Optimizer

**自动给你“选型与降本”建议**（rightsizing）。它分析 CloudWatch 指标，判断资源是否过/欠配，并推荐更合适、通常更省钱的规格。

可以帮你判断EC2 instance的rightsize

# optimized

## 1) Compute optimized（计算优化）

- **Families**: **C7i / C7g(Graviton) / C7a(AMD) / C6i / C6g**, **Hpc7g / Hpc6a**（HPC 专用）
- **优化点**: 高 vCPU 比例、单核/整机算力强
- **常见场景**: 高并发 Web/API、批处理、视频转码、科学计算、HPC 作业

## 2) Memory optimized（内存优化）

- **Families**: **R7i / R7g / R7a / R6i / R6g**, **X2idn / X2iedn / X2iezn**, **High Memory (u-6tb1 ~ u-24tb1)**, **z1d（高频 + 大内存/本地 NVMe）**
- **优化点**: 高内存/CPU 比、极大内存容量、低延迟内存访问
- **常见场景**: 内存数据库（Redis/Memcached）、高性能缓存、实时大数据分析、内存密集型 Java/微服务、SAP HANA

## 3) Storage optimized（存储优化）

- **Families**: **I4i / I3 / I3en**（本地 NVMe，超高 IOPS/吞吐），**Im4gn / Is4gen**（Graviton + Nitro SSD），**D3 / D3en / H1**（大容量 HDD/吞吐）
- **优化点**: 本地直连 NVMe/大盘吞吐/高顺序读写
- **常见场景**: NoSQL（Cassandra/ScyllaDB）、搜索（Elasticsearch/OpenSearch）、数据仓库、日志/数据湖预处理、需要本地盘的分布式系统

## 4) Accelerated computing（加速计算）

- **GPU 训练/通用加速**: **P5 / P4d / P3**（NVIDIA 数据中心 GPU，深度学习训练、HPC）
- **GPU 图形/推理/媒体**: **G5 / G4dn**（渲染、虚拟工作站、部分推理/编解码）
- **视频转码**: **VT1**（专用芯片，低成本高路数转码）
- **ML 专用芯片**: **Trn1 / Trn1n (Trainium, 训练)**，**Inf2 / Inf1 (Inferentia, 推理)**
- **FPGA**: **F1**（可编程逻辑加速）
- **优化点**: 专用硬件（GPU/ASIC/FPGA）带来的吞吐、并行度
- **常见场景**: 深度学习训练与推理、渲染、视频转码、基因组学、定制硬件加速

## 5) General purpose（通用型，平衡型）

- **Families**: **M7i / M7g / M6i / M6g**（平衡 vCPU/内存/网络），**T4g / T3**（Burstable 突发性能，低成本）
- **优化点**: 资源均衡（或按需突发）
- **常见场景**: 大多数通用应用、微服务、中小型数据库、开发测试

> 备注：**Mac**（mac1/mac2）是运行 macOS 的专用实例，场景特殊；严格来说不属于上述“优化”分类。
