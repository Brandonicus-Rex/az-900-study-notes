# Domain 2: Describe Azure architecture and services (35–40%)

## Core architectural components

- **Region:** a geographic area containing one or more datacenters connected by a low-latency network. Some services are only available in certain regions.
- **Region pair:** two regions in the same geography, usually at least 300 miles apart. Used for replication and disaster recovery; planned updates roll out to one region of a pair at a time, and one region per pair is prioritized for recovery during an outage. Some newer regions have no pair.
- **Sovereign regions:** isolated instances of Azure for compliance or legal reasons (e.g., **Azure Government** for U.S. government, **Azure China** operated by 21Vianet).
- **Availability zone:** a physically separate datacenter (or group of datacenters) within a region, with independent power, cooling and networking. Regions that support zones have at least **three**.
  - **Zonal services:** pinned to a specific zone (e.g., VMs, managed disks).
  - **Zone-redundant services:** replicated across zones automatically (e.g., zone-redundant storage, SQL Database).
- **Resource hierarchy (top to bottom):**

| Level | Purpose |
|-------|---------|
| **Management groups** | Group subscriptions to apply policy and access at scale. Up to six levels deep (not counting root and subscription level) |
| **Subscriptions** | Unit of billing and access control. Use separate ones for environments, departments or billing boundaries |
| **Resource groups** | Logical containers for resources that share a lifecycle. A resource belongs to only one group; groups can't be nested |
| **Resources** | Individual services: VMs, storage accounts, databases, etc. |

- Deleting a resource group **deletes everything in it**.
- Settings applied at a higher level (policy, RBAC) are **inherited** by everything below.

> **Exam tip:** Availability zones protect against a **datacenter** failure. Region pairs protect against a **whole region** failing.

## Compute and networking

### Compute

| Service | What it is | Use when |
|---------|-----------|----------|
| **Virtual Machines** | IaaS: full control of the OS | Lift-and-shift, custom software, full control |
| **VM Scale Sets** | Group of identical, load-balanced VMs that scale automatically | Many identical VMs that scale with demand |
| **Availability sets** | Spread VMs across **fault domains** (separate power and network) and **update domains** (rebooted separately during maintenance) | Protect against hardware failure and planned maintenance within one datacenter |
| **Azure Virtual Desktop** | Desktop and app virtualization in the cloud, including multi-session Windows 10/11 | Remote desktops for users on any device |
| **Containers** (Container Instances, Container Apps, AKS) | Lightweight, portable app packages with no OS to manage | Microservices, fast startup. ACI = simplest; AKS = orchestration at scale |
| **Azure Functions** | Serverless, event-driven code | Short tasks triggered by events (HTTP, timers, queues) |
| **App Service** | PaaS for hosting web apps, APIs and mobile back ends | Web apps without managing servers |

### Networking

- **Virtual network (VNet):** a private network in Azure. Provides isolation, internet access, communication between Azure resources and with on-prem, routing and filtering.
  - **Public endpoints** are reachable from the internet; **private endpoints** use a private IP from your VNet.
  - **VNet peering** connects VNets directly over Microsoft's backbone (no public internet). Works across regions (global peering).
- **VPN Gateway:** encrypted connection to on-prem over the **public internet**. Types: site-to-site, point-to-site, network-to-network.
- **ExpressRoute:** **private** connection to Microsoft's cloud through a connectivity provider. **Does not go over the public internet.** More reliable, faster and lower latency.
- **Azure DNS:** hosts DNS domains on Azure's infrastructure. Supports private DNS zones and alias records. You can't buy domain names through it.

> **Exam tip:** Encrypted over the internet = **VPN Gateway**. Private, doesn't use the internet = **ExpressRoute**.

## Storage

- **Storage account:** a unique namespace for your data, reachable from anywhere over HTTP/HTTPS. The name must be globally unique.
- **Redundancy options:**

| Option | Copies | Protects against |
|--------|--------|------------------|
| **LRS** (locally redundant) | 3 copies in one datacenter | Disk or server failure |
| **ZRS** (zone-redundant) | 3 copies across 3 availability zones in one region | Datacenter failure |
| **GRS** (geo-redundant) | LRS in the primary region + LRS in a secondary region | Regional outage |
| **GZRS** (geo-zone-redundant) | ZRS in the primary region + LRS in a secondary region | Datacenter **and** regional outage |
| **RA-GRS / RA-GZRS** | Same as GRS/GZRS, plus **read access** to the secondary region | Lets you read data during a regional outage |

- **Storage services:**
  - **Blob:** unstructured object storage (images, video, backups).
  - **Files:** managed file shares using SMB or NFS; mountable like a network drive.
  - **Queue:** messages between app components.
  - **Table:** NoSQL key/attribute store.
  - **Disks:** block storage for VMs.
- **Blob access tiers:**

| Tier | Use for | Minimum storage period |
|------|---------|------------------------|
| **Hot** | Frequently accessed data | None |
| **Cool** | Infrequent access | 30 days |
| **Cold** | Rarely accessed, but needs fast retrieval | 90 days |
| **Archive** | Rarely accessed; retrieval takes hours | 180 days |

- **Moving data:**
  - **AzCopy:** command-line tool for copying blobs and files.
  - **Storage Explorer:** GUI app for managing storage.
  - **Azure File Sync:** syncs on-prem Windows file servers with Azure Files.
  - **Azure Migrate:** hub for migrating servers, databases and apps.
  - **Azure Data Box:** physical device for moving large amounts of data offline (more than 40 TB, or when bandwidth is limited).

> **Exam tip:** **Archive** is the cheapest tier for storage but the most expensive and slowest to retrieve from. Archive can only be set on individual blobs, not as an account default.

## Identity, access, and security

- **Microsoft Entra ID** (formerly Azure AD) is Azure's cloud identity and access management service. It provides authentication, SSO, app management and device management.
- **Microsoft Entra Domain Services:** managed domain services (domain join, Group Policy, LDAP, Kerberos/NTLM) without running domain controllers.
- **Authentication methods:**
  - **SSO:** sign in once and access many apps.
  - **MFA:** two or more of something you **know** (password), **have** (phone) or **are** (biometric).
  - **Passwordless:** Windows Hello for Business, Microsoft Authenticator, FIDO2 keys.
- **External identities:** **B2B collaboration** lets partners sign in with their own identities; **B2C** handles customer sign-in for apps you publish.
- **Conditional Access:** if-then policies based on signals (user, location, device, app, risk). Example: require MFA when signing in from an unknown location.
- **Azure RBAC:** assigns roles (e.g., Owner, Contributor, Reader) to users, groups or apps at a **scope** (management group, subscription, resource group, resource). Permissions are inherited downward.
- **Zero Trust:** "never trust, always verify." Principles: **verify explicitly**, **use least-privilege access**, **assume breach**.
- **Defense-in-depth layers (outer to inner):** physical security → identity and access → perimeter → network → compute → application → data.
- **Microsoft Defender for Cloud:** monitors security posture and protects workloads across Azure, on-prem and other clouds. Provides a secure score and recommendations.

> **Exam tip:** **Authentication** = proving who you are (AuthN). **Authorization** = what you're allowed to do (AuthZ). Entra ID handles authentication; RBAC handles authorization to Azure resources.

## Key terms

| Term | Definition |
|------|-----------|
| Region / region pair | Geographic area of datacenters / two linked regions for DR |
| Availability zone | Physically separate datacenter(s) within a region |
| Management group | Container for subscriptions to apply governance at scale |
| Subscription | Billing and access boundary |
| Resource group | Logical container for resources with a shared lifecycle |
| Availability set | Spreads VMs across fault and update domains |
| VNet peering | Private connection between VNets over the Microsoft backbone |
| VPN Gateway / ExpressRoute | Encrypted tunnel over the internet / private dedicated connection |
| LRS / ZRS / GRS / GZRS | Storage redundancy: local / zone / geo / geo-zone |
| Access tiers | Hot, cool, cold, archive: cost vs retrieval speed |
| Microsoft Entra ID | Cloud identity and access management |
| Conditional Access | Signal-based access policies |
| RBAC | Role-based access control at a scope |
| Zero Trust | Verify explicitly, least privilege, assume breach |

## Questions to review

1. What is the minimum number of availability zones in a region that supports them?
2. In what order does the Azure resource hierarchy go, from top to bottom?
3. Can a resource belong to more than one resource group?
4. You need a private connection to Azure that doesn't go over the public internet. Which service do you use?
5. Which storage redundancy option protects against both a datacenter failure and a regional outage?
6. Which blob tier is cheapest to store data in, and what's the catch?
7. Which feature can require MFA only when users sign in from outside the corporate network?
8. What are the three principles of Zero Trust?

<details>
<summary>Show answers</summary>

1. **Three.**
2. **Management groups → subscriptions → resource groups → resources.**
3. **No.** A resource belongs to exactly one resource group (but can be moved).
4. **ExpressRoute.**
5. **GZRS** (or RA-GZRS).
6. **Archive.** Retrieval takes hours and costs more, and data has a 180-day minimum.
7. **Conditional Access.**
8. **Verify explicitly, use least-privilege access, assume breach.**

</details>
