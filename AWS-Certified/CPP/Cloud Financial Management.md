# AWS Marketplace

第三方厂商在 AWS 公共商店发布

# AWS Billing Conductor

做**内部分账/结算与自定义价目**的对账与分摊，不产出迁移商业案例。

# Billing and Cost Management

# ---

# ---

# AWS Budgets

# AWS Cost and Usage Reports

不给可视化预测，只给原始数据

# AWS Cost Explorer

可视化分析账单（已经发生的账单）

provide rightsizing recommendations for Amazon EC2 resource at no additional cost



既可以分析过去、可视化历史花费，还可以给出未来成本预测



# AWS Pricing Calculator

**事前估算** AWS 费用，用来规划新/迁移/扩容方案，按区域与配置生成月度/年度成本估算，并可分组查看明细、包含折扣与承诺（如 RI/Savings Plans）的影响。既可通过公开站点使用，也可在 Billing & Cost Management 控制台里的 “Pricing Calculator” 入口使用。

# Cost Allocation Tags

中文翻译：成本分担标签

**定义**：给 AWS 资源加上用于**费用归属**的标签键值（如 `Project=OrderEZ`、`Dept=Marketing`），让账单按这些维度拆分统计。

- **定义**：给 AWS 资源加上用于**费用归属**的标签键值（如 `Project=OrderEZ`、`Dept=Marketing`），让账单按这些维度拆分统计。
- **为什么用它（来自图里的 4 点）**
  1. **细粒度追踪**：把元数据贴到资源上，能按部门/项目等多层级精细跟踪成本。
  2. **自定义分类**：可按你的组织结构与项目命名规则自定义标签。
  3. **详细报表**：**一致地**应用后，标签会出现在成本报表里，便于对不同部门/项目的花费做深入分析。
  4. **与成本工具联动**：可无缝用于 **AWS Cost Explorer**、**AWS Budgets** 等做综合分析与预测。

**实务提示（高频考点）**

- 在 **Billing → Cost allocation tags** 中**启用**要计费的标签，否则不会出现在账单维度里。
- 统一键名与取值（如 `CostCenter/Project/Owner/Env`），全账号一致地给资源打标。
- 搭配 **Cost Explorer / CUR / Budgets** 做按项目/部门的分摊、预算预警与报告。

# AWS Billing Console

**查看账单与成本报表的控制台，**展示现状**，不做迁移评估/商业案例。

