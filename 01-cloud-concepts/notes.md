# Domain 1: Describe cloud concepts (25–30%)

## Cloud computing

- **Cloud computing** means delivering computing services (compute, storage, networking, databases, analytics) over the internet, paid for as you use them.
- **Shared responsibility model:** responsibility is split between the cloud provider and the customer, and the split depends on the service type.
  - **Customer, always:** your information and data, devices (mobile and PCs), and accounts and identities.
  - **Provider, always:** physical datacenter, physical network and physical hosts.
  - **Varies by service type:** OS, network controls, applications, and identity and directory infrastructure.
- **Cloud models:**

| Model | What it is | Key point |
|-------|-----------|-----------|
| Public | Built, controlled and maintained by a third-party provider; anyone can buy services | No CapEx, quick to provision, less control over hardware |
| Private | Cloud used by a single organization, on-prem or hosted | Full control, but you buy and maintain the hardware |
| Hybrid | Public and private connected together | Flexibility; keep sensitive or legacy workloads private and burst to public |
| Multi-cloud | Using more than one public cloud provider | Managed across environments, e.g. with **Azure Arc** |

- **Azure Arc** manages resources outside Azure (on-prem, other clouds) as if they were in Azure.
- **Azure VMware Solution** runs VMware workloads natively in Azure.
- **Consumption-based model:** no upfront cost, no infrastructure to buy, pay for what you use, and stop paying when you stop using it.
- **CapEx vs OpEx:**
  - **CapEx (capital expenditure):** upfront spending on physical infrastructure, deducted over time.
  - **OpEx (operational expenditure):** spending on services or products as you go. **Cloud is OpEx.**
- **Serverless:** the provider manages the servers; you deploy code and pay only when it runs (e.g., Azure Functions).

> **Exam tip:** The customer is **always** responsible for data, devices, accounts and identities, even in SaaS.

## Benefits of cloud services

| Benefit | Meaning |
|---------|---------|
| **High availability** | Resources stay available despite failures; backed by SLAs (e.g., 99.9%, 99.99%) |
| **Scalability** | Adjust resources to meet demand. **Vertical** = scale up/down (more CPU/RAM). **Horizontal** = scale out/in (more instances) |
| **Elasticity** | Scaling that happens automatically as demand changes |
| **Reliability** | Ability to recover from failures; decentralized design across regions |
| **Predictability** | **Performance:** autoscale, load balancing. **Cost:** forecast with the Pricing Calculator and TCO Calculator |
| **Security** | Choose your control level (IaaS = most control); provider handles physical security and patching in PaaS/SaaS |
| **Governance** | Templates and policies keep deployments compliant; auditing flags non-compliant resources |
| **Manageability** | **Of** the cloud: autoscaling, monitoring, templates. **In** the cloud: portal, CLI, APIs, PowerShell |

- **SLA uptime cheat sheet:** 99.9% ≈ 43.8 min downtime/month; 99.99% ≈ 4.38 min/month; 99.999% ≈ 26 sec/month.

> **Exam tip:** "Automatically adds resources when demand rises" = **elasticity**. "Can add resources to meet demand" = **scalability**. Watch the word *automatically*.

## Cloud service types

| | IaaS | PaaS | SaaS |
|---|------|------|------|
| **You manage** | OS, middleware, runtime, apps, data | Apps and data | Just your data, devices, accounts |
| **Provider manages** | Physical hardware, network, virtualization | Plus OS, middleware, runtime | Everything else |
| **Control** | Most | Medium | Least |
| **Examples** | Azure VMs, virtual networks | Azure App Service, Azure SQL Database, Azure Functions | Microsoft 365, Outlook, Dynamics 365 |
| **Use cases** | Lift-and-shift migration, test/dev | Developing apps without managing infrastructure | Email, messaging, productivity |

> **Exam tip:** "Lift-and-shift" or "full control of the OS" points to **IaaS**. "Focus on code, not infrastructure" points to **PaaS**. "Ready-to-use software" points to **SaaS**.

## Key terms

| Term | Definition |
|------|-----------|
| Shared responsibility model | Division of security and management duties between provider and customer |
| Public / private / hybrid cloud | Third-party shared / single-organization / combination of both |
| Multi-cloud | Using multiple public cloud providers |
| Consumption-based model | Pay only for resources used; no upfront cost |
| CapEx / OpEx | Upfront infrastructure spend / ongoing pay-as-you-go spend |
| Serverless | Provider manages servers; code runs on demand |
| SLA | Service-level agreement: the provider's uptime commitment |
| Vertical / horizontal scaling | Bigger resources / more instances |
| Elasticity | Automatic scaling based on demand |
| IaaS / PaaS / SaaS | Infrastructure / platform / software as a service |

## Questions to review

1. Under the shared responsibility model, who is responsible for protecting user accounts in a SaaS application?
2. A company wants to keep sensitive data on-premises but use Azure for extra capacity during peak periods. Which cloud model is this?
3. Which spending model does cloud computing use: CapEx or OpEx?
4. An app automatically adds VM instances when traffic spikes. Which cloud benefit does this describe?
5. Adding more RAM to an existing VM is an example of which type of scaling?
6. Which service type gives you the most control over the operating system?
7. Azure App Service is an example of which service type?
8. Which tool lets you manage on-premises servers and resources in other clouds from Azure?

<details>
<summary>Show answers</summary>

1. The **customer**. Accounts and identities are always the customer's responsibility.
2. **Hybrid cloud.**
3. **OpEx.**
4. **Elasticity** (automatic scaling).
5. **Vertical** scaling (scaling up).
6. **IaaS.**
7. **PaaS.**
8. **Azure Arc.**

</details>
