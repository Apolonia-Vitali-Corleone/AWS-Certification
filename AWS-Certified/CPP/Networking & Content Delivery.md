# VPC 

Virtual Private Cloud

# CloudFront 

CDN服务

静态资源

# API Gateway

专门管理API的网管

不是LoadBlancer

# Direct Connect 

专用物理线路

需要ISP和colocation facility

# AWS App Mesh

# AWS Global Accelerator 

全球加速器

动态资源

# Route 53 

DNS服务

# AWS Data Transfer Terminal

# AWS Cloud Map

服务发现 

# Application Recovery Controller

# ----

# Network Access Control List

NACL 作用于子网级

NACL是无状态的，inbound和outbound都需要写规则。allow和deny都需要写规则。NACL **不会**评估所有规则，命中即停止。stateless，可显式 deny。



# Security Group

Security Group作用于实例级

Security Group是有状态的，只写允许规则（缺省即拒）。只支持**允许规则**，按**端口/协议/来源**精确放行。



# ---





# AWS PrivateLink 

专用的VPC终端，直接走AWS内部网络

# AWS Transit Gateway 

VPC之间的网络总线

# AWS VPN 

# AWS Site-to-Site VPN 

公司到云

# AWS Client VPN 

个人到云



# AWS Network Access Analyzer 

安全分析工具

# AWS Ground Station 

卫星服务

# Amazon VPC Lattice

比AWS Cloud Map更完整的服务发现

