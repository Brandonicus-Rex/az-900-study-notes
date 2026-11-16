# Domain 3: Describe Azure management and governance (30–35%)

## Cost management

- **Factors that affect cost:**
  - **Resource type:** settings, size and tier change the price.
  - **Consumption:** pay-as-you-go, or commit in advance for discounts (**Reservations**: 1 or 3 years).
  - **Maintenance:** clean up unused resources (e.g., disks and IPs left behind after deleting a VM).
  - **Geography:** prices vary by region.
  - **Network traffic:** inbound (ingress) data is usually free; **outbound (egress) is charged**, and prices vary by billing zone.
  - **Subscription type:** some include free usage allowances.
  - **Azure Marketplace:** third-party solutions can include vendor fees.
- **Ways to save:** Reservations, **Azure Hybrid Benefit** (reuse existing Windows Server and SQL Server licenses), spot VMs, autoscaling, right-sizing, shutting down unused resources.
- **Pricing Calculator:** estimates the cost of **new** Azure resources before you deploy them.
- **TCO Calculator:** compares the cost of running **on-premises** infrastructure with running it in Azure.
- **Microsoft Cost Management:** analyze actual spending, set **budgets** and **alerts**, and view recommendations.
  - **Budget alerts:** spending passes a threshold.
  - **Credit alerts:** Azure credits are running low.
  - **Department spending quota alerts:** an Enterprise Agreement department reaches its quota.
- **Tags:** name/value pairs on resources (e.g., `CostCenter: IT`). Used for cost reporting, ownership, environment and automation. **Tags are not inherited** from resource groups by default (Azure Policy can enforce inheritance).

> **Exam tip:** Estimating a **new** deployment = **Pricing Calculator**. Comparing **on-prem vs Azure** = **TCO Calculator**. Tracking **actual** spending = **Cost Management**.

## Governance and compliance

- **Microsoft Purview:** a family of data governance, risk and compliance solutions. Gives a unified view of data across on-prem, multi-cloud and SaaS; helps classify sensitive data and manage compliance.
- **Azure Policy:** creates, assigns and manages rules for resource configurations. Evaluates resources and flags non-compliance, and can **block** non-compliant deployments or **auto-remediate** some.
  - **Initiative:** a group of related policies managed together.
  - Policies can be assigned at management group, subscription or resource group level and are inherited.
  - Example: "Only allow VMs in East US," or "Require a tag on all resources."
- **Resource locks:** prevent accidental deletion or modification. Locks apply even to Owners.
  - **Delete (CanNotDelete):** can read and modify, but can't delete.
  - **ReadOnly:** can only read; no changes or deletions.
  - To delete or change a locked resource, **remove the lock first**. Locks are inherited by child resources.
- **Service Trust Portal:** Microsoft's public site for audit reports, compliance documentation and security practices.

> **Exam tip:** **Policy** controls **what** resources can be created and how they're configured. **RBAC** controls **who** can do things. **Locks** prevent changes no matter who you are.

## Managing and deploying resources

| Tool | What it is |
|------|-----------|
| **Azure portal** | Web-based GUI for managing resources |
| **Azure Cloud Shell** | Browser-based shell with Azure CLI and Azure PowerShell preinstalled; no local install needed |
| **Azure CLI** | Cross-platform command-line tool using Bash-style commands (`az vm create`) |
| **Azure PowerShell** | PowerShell cmdlets for Azure (`New-AzVM`) |
| **Azure Arc** | Extends Azure management to on-prem, edge and multi-cloud resources (servers, Kubernetes, data services) |
| **Azure Resource Manager (ARM)** | Deployment and management layer for Azure. **Every** request from the portal, CLI, PowerShell or API goes through ARM |
| **ARM templates** | JSON files that define infrastructure declaratively (infrastructure as code) |
| **Bicep** | Simpler language that compiles to ARM templates |

- **Infrastructure as code (IaC):** define and deploy infrastructure with code instead of manual steps. The benefits are repeatability and consistency.
- **ARM template benefits:** **declarative** (describe *what* you want, not how), **repeatable**, **orchestrated** (deploys resources in the right order and in parallel where possible), **modular**, and **extensible** (can run scripts).

> **Exam tip:** All management tools (portal, CLI, PowerShell, REST) talk to **Azure Resource Manager**. ARM is what enforces RBAC, locks and tags.

## Monitoring tools

| Tool | What it does |
|------|-------------|
| **Azure Advisor** | Personalized recommendations in five categories: **reliability, security, performance, operational excellence, cost** |
| **Azure Service Health** | Health of Azure services that affect **you**. Three parts: **Azure Status** (global status), **Service Health** (your services and regions), **Resource Health** (your individual resources) |
| **Azure Monitor** | Collects, analyzes and acts on metrics and logs from Azure, on-prem and other clouds |
| **Log Analytics** | Part of Azure Monitor: query logs with Kusto Query Language (KQL) |
| **Azure Monitor alerts** | Notify you or trigger actions when a metric or log condition is met; uses **action groups** |
| **Application Insights** | Part of Azure Monitor: performance monitoring for web apps (requests, failures, response times, dependencies) |

> **Exam tip:** "Is Azure down in my region?" → **Service Health**. "How can I save money or improve security?" → **Advisor**. "Collect metrics and logs, set alerts" → **Monitor**.

## Key terms

| Term | Definition |
|------|-----------|
| Pricing Calculator | Estimates the cost of new Azure resources |
| TCO Calculator | Compares on-prem costs with Azure |
| Cost Management | Analyzes actual spending; budgets and alerts |
| Reservations | 1- or 3-year commitments for discounts |
| Azure Hybrid Benefit | Reuse existing Windows Server/SQL licenses in Azure |
| Tags | Name/value metadata on resources |
| Microsoft Purview | Data governance, risk and compliance solutions |
| Azure Policy / initiative | Rules for resource configuration / group of policies |
| Resource lock | Delete or ReadOnly protection against accidental changes |
| Azure Resource Manager | Deployment and management service behind all Azure tools |
| ARM template / Bicep | Declarative IaC in JSON / simpler language that compiles to ARM |
| Azure Arc | Manage non-Azure resources from Azure |
| Azure Advisor | Recommendations across five categories |
| Service Health | Status of Azure services affecting you |
| Azure Monitor / Log Analytics / Application Insights | Metrics and logs / KQL queries / app performance |

## Questions to review

1. Which tool estimates the cost of migrating your on-premises datacenter to Azure?
2. Is inbound or outbound data transfer typically charged?
3. You apply a tag to a resource group. Do the resources inside it automatically get the tag?
4. Which lock type allows changes but prevents deletion?
5. A user with the Owner role tries to delete a resource with a Delete lock. What happens?
6. You want to stop anyone from creating VMs outside East US. Which service do you use?
7. What service handles every request from the portal, CLI and PowerShell?
8. What are the five Azure Advisor recommendation categories?

<details>
<summary>Show answers</summary>

1. **TCO Calculator.**
2. **Outbound (egress)** is charged; inbound is usually free.
3. **No.** Tags aren't inherited by default (Azure Policy can enforce it).
4. **Delete (CanNotDelete).**
5. **The deletion fails.** Locks apply to everyone; the lock must be removed first.
6. **Azure Policy.**
7. **Azure Resource Manager (ARM).**
8. **Reliability, security, performance, operational excellence, cost.**

</details>
