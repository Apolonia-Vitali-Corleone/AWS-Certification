# AWS Budgets

# AWS Cost and Usage Reports

# AWS Cost Explorer

可视化分析账单（已经发生的账单）

provide rightsizing recommendations for Amazon EC2 resource at no additional cost

# AWS Marketplace

# AWS Billing Conductor

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