# AWS Batch

**AWS Batch = 任务排队机 + 自动开关一群临时服务器**；
 你只把“要干的活（脚本/容器）”丢进去，Batch 会按队列自动**拉起/回收**算力并**重试失败**。
 **EC2** 则是你自己先准备好服务器，再自己排队、扩缩容、容错。

3 个开关（记住就会用）

- **Compute Environment**：用什么算力（EC2/Fargate，On-Demand/Spot，最多开到多少 vCPU）。
- **Job Queue**：活儿排队的地方，先来先干/按优先级。
- **Job Definition**：怎么干（用哪个 Docker 镜像、命令、vCPU/内存、超时/重试）。

### 一眼例子

> **有 10,000 张图片要加水印，每张处理 1 分钟，能被中断后重试。**

- **用 EC2：**
   你得：估算要几台机 → 建 ASG → 写 SQS 消费与扩缩容逻辑 → 处理失败重试 → 干完别忘了关机。
- **用 Batch：**
   做一个打好水印的 **Docker 镜像** → 注册成 **Job Definition** → 提交 **array job(1..10000)** →
   Batch 自动：按负载**开一批（可用 Spot 省钱）**→ 分发任务 → 失败**重试** → 干完**缩到 0**。

### 什么时候选谁（考试/实战速记）

- **Batch**：成千上万 **无状态、可重试、离线**任务（仿真/转码/ETL）；**峰来开、峰去关**；**吃 Spot**。
- **EC2**：**长期在线**服务或你要**完全掌控服务器**（自管队列与伸缩）。

> 背口诀：**“有活就开工，没活就散场——选 Batch；一直营业——选 EC2。”**

# Amazon EC2

supported by Saving Plans

# EC2 INSTANCE



# AWS Elastic Beanstalk

托管应用平台（PaaS）

底层可控

托管应用托管平台 PaaS

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

# AWS Copilot 

CLI工具

# AWS Wavelength

5G移动边缘计算