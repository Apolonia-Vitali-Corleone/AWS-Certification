下面把 **VPC 的主要组件**按用途分组列出来，并给出“是什么/何时用/和谁区别”的要点（覆盖你提到的 *VPC Flow Logs*、*Route Table* 等）：

# 基础网络构件

- **VPC / CIDR（IPv4/IPv6）**：你私有网络的边界与网段。
- **Subnet（子网：Public / Private）**：可用区内的网段切分；是否“公有”取决于其路由表是否指向 IGW。
- **Route Table（路由表：子网关联 / 边界关联）**：决定去往目的网段的下一跳；除了常见的“子网路由表”，还有**网关路由表**可关联到 IGW/VGW 来控制入口/出口流量路径。([AWS Documentation](https://docs.aws.amazon.com/vpc/latest/userguide/route-table-options.html?utm_source=chatgpt.com))
- 
- **NAT Gateway（NATGW：Public / Private 两种）**：让私有子网实例**仅出站**访问外部（IPv4），外部不能反向连入；**Public NATGW**出网经 IGW，**Private NATGW**用于经 TGW/VGW 出网到别的 VPC/本地。([AWS Documentation](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-nat-gateway.html?utm_source=chatgpt.com))
- **Egress-only Internet Gateway（EIGW）**：**仅 IPv6** 的出站公网访问（不做 NAT），入站不予接受；IPv4 出站用 NATGW。([AWS Documentation](https://docs.aws.amazon.com/vpc/latest/userguide/egress-only-internet-gateway.html?utm_source=chatgpt.com))
- **DHCP Option Set**：为 VPC 内主机分发 DNS 域名、NTP 等网络参数。([AWS Documentation](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_DHCP_Options.html?utm_source=chatgpt.com))
- **ENI（Elastic Network Interface）**：可附着到 EC2 的虚拟网卡（含私网 IP、SG 等属性），可在同一 AZ 的实例之间迁移。([AWS Documentation](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-eni.html?utm_source=chatgpt.com))

# 访问控制（内外两层“防火墙”）

- **Security Group（安全组）**：**实例级**、**有状态**，按五元组规则放行/拒绝进出站。
- **Network ACL（NACL）**：**子网级**、**无状态**，按规则顺序评估。
   → 速记：**SG=实例/有状态**；**NACL=子网/无状态**。([AWS Documentation](https://docs.aws.amazon.com/whitepapers/latest/aws-best-practices-ddos-resiliency/security-groups-and-network-acls-bp5.html?utm_source=chatgpt.com))

# 私网访问 AWS 服务（VPC Endpoints）

- 
- **Interface Endpoint（PrivateLink）**：在你 VPC 内创建 **ENI 端点**，私线访问大量 AWS/SaaS 服务。([AWS Documentation](https://docs.aws.amazon.com/vpc/latest/privatelink/create-interface-endpoint.html?utm_source=chatgpt.com))
- **Gateway Load Balancer Endpoint（GWLBe）**：通过 GWLB 把流量引到检验/安全设备（NLB/GWLB 背后服务）。([AWS Documentation](https://docs.aws.amazon.com/vpc/latest/privatelink/gateway-load-balancer-endpoints.html?utm_source=chatgpt.com))

# 互联互通（VPC↔VPC / 本地 / DX）

- **AWS Transit Gateway（TGW）**：区域级三层转发“枢纽”，把多 VPC、本地 VPN 汇聚成**星型**拓扑。([AWS Documentation](https://docs.aws.amazon.com/vpc/latest/tgw/what-is-transit-gateway.html?utm_source=chatgpt.com))
- **Site-to-Site VPN**：本地到 VPC 的 IPSec 隧道，AWS 侧叫 **Virtual Private Gateway（VGW）**，你侧叫 **Customer Gateway（CGW）**。([AWS Documentation](https://docs.aws.amazon.com/vpn/latest/s2svpn/VPC_VPN.html?utm_source=chatgpt.com))
- **Direct Connect & DX Gateway**：专线接入及其跨区/多 VPC 聚合网关，常与 TGW/VGW 组合。([AWS Documentation](https://docs.aws.amazon.com/directconnect/latest/UserGuide/direct-connect-gateways-intro.html?utm_source=chatgpt.com))
- **Carrier Gateway（Wavelength 专用）**：在 5G 边缘区把 Wavelength 子网连到运营商网络（类 IGW 的 NAT 行为）。*仅当用到 Wavelength 时才会见到*。([AWS Documentation](https://docs.aws.amazon.com/wavelength/latest/developerguide/carrier-gateways.html?utm_source=chatgpt.com))

# 名称解析（DNS）

- **Route 53 Resolver（VPC 内置解析）** + **Inbound/Outbound Endpoints & 规则**：在混合环境里把本地与 VPC 的 DNS 互通（本地→VPC 用 Inbound，VPC→本地 用 Outbound + 规则）。([AWS Documentation](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/resolver.html?utm_source=chatgpt.com))

# 可观测与排障

- 
- **Traffic Mirroring**：复制 **报文内容**（ENI 级别的进/出包）到分析/安全设备（NLB/GWLB 目标），做深度包检与故障定位。([AWS Documentation](https://docs.aws.amazon.com/vpc/latest/mirroring/what-is-traffic-mirroring.html?utm_source=chatgpt.com))
- **Reachability Analyzer**：静态配置分析，验证“源→目的”是否可达，并给出逐跳路径/阻断点。([AWS Documentation](https://docs.aws.amazon.com/vpc/latest/reachability/what-is-reachability-analyzer.html?utm_source=chatgpt.com))
- **Network Access Analyzer**：基于规则找出**潜在的越权访问路径**（合规审计用）。([AWS Workshops](https://workshops.aws/categories/VPC Network Access Analyzer?utm_source=chatgpt.com))

# 配置复用与抽象

- **Prefix Lists（前缀列表）**：把一组 CIDR 做成对象在**路由表/安全组**复用；分 **AWS-managed** 与 **Customer-managed** 两类。([AWS Documentation](https://docs.aws.amazon.com/vpc/latest/userguide/working-with-aws-managed-prefix-lists.html?utm_source=chatgpt.com))

------

## 易混淆对比（1 行速记）

- **IGW vs NATGW vs EIGW**：IGW=公网双向；NATGW=私网实例**仅出站 IPv4**；EIGW=**仅 IPv6 出站**。([AWS Documentation](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Internet_Gateway.html?utm_source=chatgpt.com))
- **Endpoint 三兄弟**：Gateway（S3/DDB 专用，走路由表，**非**PrivateLink）；Interface（PrivateLink，建 ENI，最常见）；GWLBe（经 GWLB 送检流量）。([AWS Documentation](https://docs.aws.amazon.com/vpc/latest/privatelink/gateway-endpoints.html?utm_source=chatgpt.com))
- **SG vs NACL**：SG=**实例/有状态**；NACL=**子网/无状态**（有序评估）。([AWS Documentation](https://docs.aws.amazon.com/whitepapers/latest/aws-best-practices-ddos-resiliency/security-groups-and-network-acls-bp5.html?utm_source=chatgpt.com))
- **Peering vs TGW**：Peering 点到点，适合少量互通；TGW 枢纽型，适合多 VPC/多站点规模化。([AWS Documentation](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-peering.html?utm_source=chatgpt.com))
- **VPN(VGW/CGW) vs Direct Connect**：VPN=公网加密隧道（易开通），DX=专线（低抖动/大带宽），可与 TGW/VGW 组合及用 **DX Gateway** 聚合多 VPC。([AWS Documentation](https://docs.aws.amazon.com/vpn/latest/s2svpn/VPC_VPN.html?utm_source=chatgpt.com))
- **Flow Logs vs Traffic Mirroring vs Reachability Analyzer**：Flow Logs=**元数据日志**；Mirroring=**全包内容**；Reachability=**静态路径分析**。([AWS Documentation](https://docs.aws.amazon.com/vpc/latest/userguide/flow-logs.html?utm_source=chatgpt.com))

> 说明：上面多数是 **Amazon VPC 的功能/子资源**；像 **AWS Network Firewall、VPC Lattice** 属于相邻服务，不算“VPC 核心组件”。

如果你愿意，我可以按“考试/面试速记卡”的格式，把每个组件再压成 1～2 行要点（触发条件 + 常见坑 + 与谁对比）供背诵。

# VPC Peering

两 VPC 之间点对点私网路由，**不经公网**，支持跨账号/跨区。拓扑多了会成“网状”。([AWS Documentation](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-peering.html?utm_source=chatgpt.com))

点对点，不经过AWS Transit Gateway，不需要“路由”

# Internet Gateway（IGW）

让子网可直连公网；默认 VPC 才自带，其它需手动创建与附加并在路由表指向。([AWS Documentation](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Internet_Gateway.html?utm_source=chatgpt.com))

# AWS Transit Gateway

多VPC之间，像一个路由一样

# Gateway Endpoint

S3/DynamoDB 专用；路由表指向网关，无需 IGW/NAT。**不使用 PrivateLink**。([AWS Documentation](https://docs.aws.amazon.com/vpc/latest/privatelink/gateway-endpoints.html?utm_source=chatgpt.com))

# VPC Flow Logs

记录 **ENI/VPC/Subnet** 粒度的**流量元数据**（五元组、accept/reject 等），可送 CloudWatch Logs / S3 / Firehose；S3 默认**5 分钟**聚合投递一批文件。([AWS Documentation](https://docs.aws.amazon.com/vpc/latest/userguide/flow-logs.html?utm_source=chatgpt.com))

inbound and outbound traffic in Amazon VPC