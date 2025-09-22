# CodeCommit

# CodeBuild

构建

# CodeDeploy

**部署编排**：把应用发布到 **EC2/本地、ECS、Lambda**；支持**滚动/蓝绿/金丝雀**、健康检查与自动回滚。
 *常与 CodePipeline 串联做 CI/CD。*

# CodePipeline

持续交付流水线

# Cloud9

Web IDE for writing code;

You can open a terminal there, but it’s not the service meant to manage all AWS resources.

# CloudShell

browser-based, pre-authenticated service

# X-Ray

分布式追踪Tool

跟踪请求，发现性能瓶颈

# AWS FIS

# Infrastructure Composer

# AWS App Studio

# AWS AppConfig

# CodeArtifact

# Amazon CodeCatalyst

# Amazon Q developer

Including Amazon CodeWhisperer

# ---

# AWS CLI

命令行工具

**AWS CLI:** Command-line tool (terminal), not a web interface.

# AWS SDK

`AWS Software Development Kit`

allows developers to access AWS services from application code

**AWS SDK:** Programming libraries for code to call AWS APIs, not an interface.

# AWS CDK

`AWS Cloud Development Kit(AWS CDK)`

因为 **AWS CDK** 本质上是一个“开发框架（framework）”，用主流编程语言写代码来**定义云资源**，然后**自动合成为 CloudFormation 模板并由 CloudFormation 去部署**。

**AWS SDK**：在你的**应用程序运行期**调用各个 AWS 服务 API 的**客户端库**。

**AWS CDK**：用熟悉的编程语言来**定义与部署云基础设施**（IaC），最终**合成为  ** **CloudFormation** 再创建资源。

两者现在都**在**，且都在持续更新

# ---







# AWS CodeStar

一键**搭项目脚手架**（repo+CI/CD+示例应用+权限+看板）的**项目级**入口。

CodeStar 常帮你同时创建 CodeCommit/GitHub、CodeBuild、**CodePipeline**、CodeDeploy 等；而 CodePipeline 只管阶段与动作的编排。

想**快速落地一个可跑的样例/脚手架**（含仓库、流水线、部署位）→ 选 **CodeStar**。

已有仓库与构建，需**自定义/多阶段/跨账户**的 CI/CD 流程 → 选 **CodePipeline**。



# AWS Application Composer

可视化拖拽**无服务器架构**（API GW、Lambda、SQS、DynamoDB…），一键生成 **IaC 模板**（SAM/CFN/CDK）。
 *不是运行时/流水线，只负责设计+导出模板。*

# AWS CodeArtifact

托管**包仓库**（npm/PyPI/Maven/NuGet），可做上游代理缓存与权限管控。
 *不存容器镜像（镜像用 ECR）。*



# Amazon CodeGuru

**智能代码审查 + 性能剖析**套件：

- Reviewer：PR/仓库的静态建议（Bug/安全/最佳实践）。
- Profiler：生产环境**热点/CPU/内存**分析与节省建议。
   *以 Java/Python 最常见。*





# AWS Device Farm



