# SC-900 Cram Sheet

**Microsoft Security, Compliance, and Identity Fundamentals.** Skills measured as of **July 28, 2026**. Built to be read the night before and skimmed again in the 30 minutes before you sit down.

## Exam facts

| Item | Value |
|---|---|
| Domains and weights | Concepts **10–15%** · Microsoft Entra **25–30%** · Security solutions **35–40%** · Compliance solutions **20–25%** |
| Time | **45 minutes** of exam time (about 65 minutes of seat time with instructions and agreements) |
| Passing score | **700** on a 1–1000 scale (scaled, not 70% of raw questions) |
| Question count | Microsoft's generic figure is **40–60**; expect roughly 40–50 |
| Item types | Multiple choice, **"select two/three"**, **Yes/No statement sets** (each statement scored on its own), **sentence completion** (dropdown), drag-and-drop matching, hot area, an occasional short case |
| Learn access during the exam | **No.** In-exam Microsoft Learn is for role-based exams only |
| Renewal | **None.** Fundamentals certifications do not expire |
| Retake | 24 hours after a first failed attempt |

**What the July 2026 update did.** It was a branding and wording refresh, not a restructuring: Microsoft Entra names everywhere, agent identities (Microsoft Entra Agent ID) added under identity types, Microsoft Defender XDR (never "Microsoft 365 Defender"), Defender Threat Intelligence, Security Copilot, the unified Purview portal, unified eDiscovery, and posture wording (Exposure Management). Old study material that says Azure AD, compliance center, or eDiscovery (Premium) is where people lose marks.

## How to attack the items

- **The exam tests product-to-need mapping.** Almost every scenario asks "which capability does this job". Learn the one-line purpose of each product and the two neighbours it is confused with.
- **Yes/No sets are the score killers.** Three statements, each scored separately. Read each statement as its own True/False question and look for absolutes ("always", "all", "cannot").
- **Watch the qualifier:** NOT, BEST, MOST, LEAST privilege, minimum license, "without creating a guest account", "no public IP".
- **License tiers are fair game:** Entra ID Free vs P1 vs P2 vs ID Governance; Defender for Office 365 Plan 1 vs Plan 2; Defender for Endpoint P1 vs P2; Audit Standard vs Premium; E3 vs E5.
- **Sentence completion items** are definitions. If a sentence says "run KQL logic on a schedule to create alerts", the blank is "analytics rules". Know the definitions precisely.
- Nothing in the exam requires portal clicks or PowerShell. Concepts, purposes, and boundaries only.

## Domain 1 · Concepts of security, compliance, and identity (10–15%)

### Shared responsibility model

| Responsibility | On-premises | IaaS | PaaS | SaaS |
|---|---|---|---|---|
| Information and data | Customer | Customer | Customer | Customer |
| Devices (mobile and PCs) | Customer | Customer | Customer | Customer |
| Accounts and identities | Customer | Customer | Customer | Customer |
| Identity and directory infrastructure | Customer | Customer | **Shared** | **Shared** |
| Applications | Customer | Customer | **Shared** | Microsoft |
| Network controls | Customer | Customer | **Shared** | Microsoft |
| Operating system | Customer | Customer | Microsoft | Microsoft |
| Physical hosts, network, datacenter | Customer | Microsoft | Microsoft | Microsoft |

> **Trap.** Three things never move to the provider: **data, endpoints, identities and accounts**. If an option says Microsoft is responsible for classifying your data or securing your users' phones, it is wrong in every model.

### Defense in depth

Seven layers, outside in: **physical → identity and access → perimeter → network → compute → application → data**. Place a control on its layer:

| Control | Layer |
|---|---|
| Badge access, locked datacenter | Physical |
| MFA, Conditional Access, PIM | Identity and access |
| DDoS protection, edge firewall | Perimeter |
| NSGs, segmentation, VNet peering rules | Network |
| VM hardening, endpoint protection, patching | Compute |
| Secure coding, secrets in Key Vault, WAF in front of the app | Application |
| Encryption at rest, classification, sensitivity labels | Data |

The **CIA triad** (confidentiality, integrity, availability) is what the layers protect. Confidentiality = encryption and access control, integrity = hashing and signatures, availability = redundancy and DDoS protection.

### Zero Trust

- **Three principles:** **Verify explicitly** (authenticate and authorize every request using all available signals), **use least privilege access** (just-in-time and just-enough access, risk-based adaptive policies), **assume breach** (segment, encrypt end to end, monitor continuously, respond).
- **Six foundational pillars:** identities, devices (endpoints), applications, data, infrastructure, networks. A **policy enforcement engine** (Conditional Access) sits in the middle and evaluates signals from all of them.
- Segmentation and real-time traffic protection sit under **networks**, not infrastructure. Shadow IT discovery and in-app permissions sit under **applications**. VMs, containers and servers sit under **infrastructure**.

> **Trap.** Defense in depth is a strategy that supports Zero Trust; it is **not** one of the three principles. "Trust but verify" is the old perimeter model, the opposite of Zero Trust.

### Encryption, hashing, signing

| Technique | Key model | What it gives you | Typical exam scenario |
|---|---|---|---|
| **Symmetric encryption** | One shared key | Fast, bulk data | Disk encryption, database encryption, needs a secret exchanged in advance |
| **Asymmetric encryption** | Public + private pair | Confidentiality with no shared secret | Encrypt with the **recipient's public key**, decrypt with their **private key** |
| **Hashing** | No key (optionally a salt) | One-way, fixed length, same input → same output | Storing passwords (**salted hash**), integrity checks |
| **Digital signature** | Sign with **private** key, verify with **public** key | Authenticity, integrity, non-repudiation | Firmware or document signing; verifier needs the **signer's public key** |

- **Encryption states:** at rest (disk, storage, database), in transit (TLS/HTTPS, VPN), in use (confidential computing, memory enclaves). Each needs its own control; TLS does nothing for a stolen disk.
- **Azure examples:** Storage Service Encryption (on by default), Azure Disk Encryption (BitLocker / dm-crypt), Transparent Data Encryption for Azure SQL, Always Encrypted, customer-managed keys in **Azure Key Vault**.
- Hashing is **not** encryption: you cannot get the original back. Salting defeats rainbow tables.

### Governance, risk, and compliance concepts

- **Governance:** the rules, practices and processes an organization uses to direct and control itself.
- **Risk management:** identify, assess and treat threats to objectives.
- **Compliance:** adhering to laws, regulations and standards; **auditing** verifies it.
- **Data residency:** where data may physically be stored and processed. **Data sovereignty:** whose laws apply to it (the laws of the country where it is collected or held). **Data privacy:** notice, transparency and consent over personal data.
- Common threats you may be asked to name: phishing, password spray, dictionary and brute-force attacks, ransomware, DDoS, data breach, malware.

### Identity concepts

- **Identity is the primary security perimeter** because users, devices, apps and data now live outside the network edge, so access decisions must be driven by verified identity signals rather than by network location.
- **Four pillars of identity:** administration (create and manage identities), authentication (prove who you are), authorization (what you may access), auditing (track who did what, when).
- **Authentication (AuthN) happens first** and produces an identity; **authorization (AuthZ)** decides what that identity can do. A user who signs in with MFA and is then refused a delete is an authorization failure, not an authentication one.
- **Identity provider (IdP):** creates, maintains and manages identity information and issues tokens; enables **single sign-on**. Microsoft Entra ID is an IdP.
- **Modern authentication protocols:** OpenID Connect (authentication → **ID token**), OAuth 2.0 (authorization → **access token** presented to the API), **refresh token** (gets new tokens, proves nothing to an API), SAML and WS-Federation (federation for older enterprise apps).
- **Directory services and Active Directory Domain Services (AD DS):** on-premises, Kerberos, NTLM, LDAP, organizational units, Group Policy. **Microsoft Entra ID** is a cloud identity service that speaks HTTP protocols (OIDC, OAuth 2.0, SAML), has no OUs or GPOs, and is not a rename of AD DS (the rename was from Azure Active Directory).
- **Federation:** a trust relationship between identity providers so one organization accepts tokens issued by another. No accounts are synchronized or duplicated. Synchronization is the hybrid-identity technique inside one organization.

> **Trap.** "Federation requires both organizations to synchronize their users into a shared directory" is **False**. Federation exists precisely so that you do not have to.
## Domain 2 · Capabilities of Microsoft Entra (25–30%)

### The Entra family, in one table

| Product | One-line purpose |
|---|---|
| **Microsoft Entra ID** | Cloud identity and access management: users, groups, devices, apps, authentication, Conditional Access, roles |
| **Microsoft Entra ID Governance** | Entitlement management, access reviews, lifecycle workflows, PIM (governance of who has access and for how long) |
| **Microsoft Entra ID Protection** | Detects identity risk (risky users, risky sign-ins) and feeds risk-based Conditional Access |
| **Microsoft Entra External ID** | B2B collaboration, B2B direct connect, and External ID for customers (CIAM) |
| **Microsoft Entra Global Secure Access** | Identity-centric network access: **Internet Access** (Secure Web Gateway) and **Private Access** (ZTNA, VPN replacement) |
| **Microsoft Entra Verified ID** | Issue and verify decentralized verifiable credentials (W3C DIDs), wallet in Microsoft Authenticator |
| **Microsoft Entra Workload ID** | Identities for apps and services: service principals, managed identities, plus Conditional Access and risk for workloads |
| **Microsoft Entra Agent ID** | Identities for AI agents, created from **agent identity blueprints** |
| **Microsoft Entra Domain Services** | Managed AD DS (Kerberos, NTLM, LDAP, Group Policy) for lift-and-shift legacy apps, no domain controllers to run |
| **Microsoft Entra Connect / Cloud Sync** | Hybrid identity synchronization from on-premises AD DS |
| Microsoft Entra Permissions Management | Was the CIEM tool (permission creep index across Azure, AWS, GCP). **Retired October 2025**; treat it as a distractor |

**Licensing tiers to memorize**

| Tier | Unlocks |
|---|---|
| **Free** | Users, groups, devices, security defaults, basic SSO, SSPR for cloud users (with limits), MFA via security defaults |
| **P1** | **Conditional Access**, dynamic groups, group-based licensing, **SSPR with on-premises writeback**, custom banned passwords, hybrid features, authentication strengths |
| **P2** | Everything in P1 plus **ID Protection** (full risk detections, risk-based policies), **PIM**, **access reviews**, entitlement management |
| **ID Governance** (add-on) | Lifecycle workflows, advanced entitlement management, machine-learning-assisted access reviews |
| **Entra Suite** | P2 + ID Governance + Internet Access + Private Access + Verified ID premium |

### Identity types

| Type | What to know |
|---|---|
| **Users** | Member (internal) or guest (external). Cloud-only or synchronized |
| **Groups** | **Security** groups (permissions, licensing, Conditional Access targeting) and **Microsoft 365** groups (collaboration with mailbox, site, Teams). Membership **assigned** or **dynamic** (rule-based, P1) |
| **Devices** | **Entra registered** = personal/BYOD; **Entra joined** = organization-owned, signed in with work account; **hybrid joined** = joined to AD DS **and** Entra ID. Device state and compliance are Conditional Access signals; registration is free |
| **Applications / service principals** | Registering an app creates a global **application object** (the template: redirect URIs, credentials, requested permissions) and, in your tenant, a **service principal** (the local instance shown under **Enterprise applications** that holds assignments, consent and sign-in policy) |
| **Managed identities** | Special service principals for Azure resources whose credentials the platform manages and rotates; **system-assigned** (tied to one resource, deleted with it) or **user-assigned** (standalone, shareable). The answer to "no credentials in code" |
| **Agent identities** | **Microsoft Entra Agent ID.** Every agent identity is created from an **agent identity blueprint** that records the agent kind, publisher, roles and permissions. **Agent identities hold no credentials of their own**; the blueprint holds the federated credential, certificate or secret and acquires tokens for them. Disable the blueprint to stop the whole fleet; target Conditional Access at the blueprint |

### Hybrid identity

| Method | How it works | Pick it when |
|---|---|---|
| **Password hash synchronization (PHS)** | Hash of the hash synced to the cloud; cloud authenticates | Simplest, most resilient, enables leaked-credential detection |
| **Pass-through authentication (PTA)** | Lightweight agents validate the password against AD DS in real time; nothing stored in the cloud | Policy forbids any password material in the cloud, no AD FS wanted |
| **Federation (AD FS)** | Entra redirects sign-in to the on-premises federation service | Existing AD FS, smart cards, third-party MFA, complex policy |

- **Entra Connect Sync:** the traditional on-premises server, full feature set (device writeback, complex topologies). **Entra Cloud Sync:** lightweight provisioning agents with cloud-managed configuration, supports **disconnected forests** (mergers and acquisitions), simpler HA.
- **Password writeback** (P1) returns SSPR password changes to on-premises AD DS. **Seamless SSO** signs domain-joined users in automatically.

### External identities

| Scenario | Answer | Guest object created? |
|---|---|---|
| Invite a partner user to your SharePoint site or Teams team | **B2B collaboration** (guest user authenticates with their own IdP: Entra, Microsoft account, Google, email OTP, SAML) | **Yes** |
| Partner engineers in a **Teams shared channel** with their home identity | **B2B direct connect** (mutual trust via cross-tenant access settings) | **No** |
| Consumer-facing app with self-service sign-up, social logins and your branding | **External ID for customers** (CIAM) in a separate tenant in the **external configuration** | Separate tenant |

Guests get limited default directory permissions, can be governed with access reviews and entitlement management, and are removed cleanly.

### Authentication methods

| Method | Notes |
|---|---|
| Password | Weakest; pair with MFA or replace |
| Microsoft Authenticator push | With **number matching** against MFA fatigue; passwordless **phone sign-in** available |
| TOTP codes (Authenticator, third-party apps), OATH hardware tokens | "Something you have" |
| SMS and voice | Weakest MFA methods, phishable; Microsoft is retiring its SMS and voice methods in favour of passkeys |
| **Passkeys / FIDO2 security keys** | **Phishing-resistant**, passwordless; passkeys in Authenticator or on hardware keys |
| **Windows Hello for Business** | Phishing-resistant, passwordless; PIN or biometric releases a **device-bound private key** (TPM); biometric never leaves the device, enrol per device |
| **Certificate-based authentication** | Phishing-resistant, smart cards |
| **Temporary Access Pass (TAP)** | Time-limited admin-issued passcode to onboard or recover passwordless users |
| Email OTP | Guests only |
| Security questions | SSPR only, never for sign-in |

- **MFA = two different factor categories:** something you **know** (password, PIN), **have** (phone, key), **are** (biometric). Password plus security questions is still single factor.
- **Phishing-resistant** = passkeys/FIDO2, Windows Hello for Business, certificate-based authentication. A classic Authenticator push approval is not.
- **Authentication strengths** are a Conditional Access grant control: built-in strengths are MFA, passwordless MFA, **phishing-resistant MFA**; you can scope one to a single sensitive app.
- **Security defaults:** free, tenant-wide, preconfigured: MFA registration for everyone, MFA for admins, MFA when needed for users, block legacy authentication, protect privileged actions. **Cannot coexist with Conditional Access.**
- **Self-service password reset (SSPR):** users reset or unlock with registered methods; admin sets who is enabled and how many methods; **combined registration** with MFA; **writeback** to on-premises needs P1 plus Connect or Cloud Sync.
- **Password protection:** **global banned password list** (Microsoft telemetry, always on, **cannot be disabled**) plus a **custom banned list** (P1, up to 1,000 base terms; character substitutions normalized, so blocking "Contoso" blocks "C0nt0so!"). Can be extended to on-premises AD DS with proxy and DC agents.
- **Smart lockout:** locks out attackers guessing a password while recognizing familiar sign-ins from the real user (default 10 failures, then 60-second lockout, increasing).

> **Trap.** Conditional Access is evaluated **after first-factor authentication succeeds**, so it cannot stop a password spray. Smart lockout, Password Protection and ID Protection detections are the answers to guessing attacks.

### Conditional Access

**If** (assignments: signals) **then** (access controls).

| Signals (conditions) | Grant controls | Session controls |
|---|---|---|
| User or group, **agent identity**, workload identity | Block access | Sign-in frequency |
| Resource (cloud app, user action, authentication context) | Require MFA / **authentication strength** | Persistent browser session |
| Network and named locations, IP, GPS | Require compliant device (Intune) | App-enforced restrictions |
| Device platform, device state, filter for devices | Require hybrid Entra joined device | Conditional Access App Control (Defender for Cloud Apps) |
| Client app (browser, mobile, legacy) | Require approved client app / app protection policy | Disable resilience defaults |
| **Sign-in risk** and **user risk** (ID Protection) | Require password change, terms of use | Continuous access evaluation |

- Modes: **Report-only** (evaluate and log without enforcing; review in sign-in logs and the insights workbook), **On**, **Off**. **What If** simulates a policy for one user and scenario.
- Always **exclude break-glass (emergency access) accounts** and monitor them.
- Needs **Entra ID P1**. Risk-based policies need **P2**.
- Common patterns: block legacy authentication, require MFA for admins, require compliant device for Microsoft 365, block by country, require phishing-resistant MFA for one finance app.

### Entra roles versus Azure RBAC

| | Microsoft Entra roles | Azure RBAC roles |
|---|---|---|
| Govern | The directory and Microsoft 365 services | Azure resources |
| Examples | Global Administrator, User Administrator, Helpdesk Administrator, Security Administrator, Compliance Administrator, AI Administrator, Global Reader | Owner, Contributor, Reader, User Access Administrator, custom roles |
| Scope | Tenant, or an **administrative unit** (subset of users, groups, devices) | Management group → subscription → resource group → resource (inherited downward) |
| Relationship | Separate role stores; a Global Administrator has **no** Azure resource rights by default, but can **elevate** to User Access Administrator at root scope | Separate; Owner at subscription grants nothing in Entra |

- **Least privilege picks:** reset passwords for non-admins → **Helpdesk Administrator**; manage users, groups and licenses → **User Administrator**; regional admins limited to one office → role at an **administrative unit** scope. Global Administrator only for emergencies.
- Custom Entra roles exist for finer-grained directory permissions.

### Global Secure Access

- **Microsoft Entra Internet Access:** identity-aware **Secure Web Gateway** for internet and SaaS traffic: web content filtering by category or FQDN, threat intelligence, TLS inspection, universal Conditional Access, Microsoft 365 traffic profile with compliant-network checks.
- **Microsoft Entra Private Access:** **Zero Trust Network Access** to private apps (TCP and UDP) with per-app or Quick Access, Conditional Access on every connection; the **VPN replacement**.
- Both use the Global Secure Access client or remote network connectivity. Bastion (Azure VM RDP/SSH), Azure Firewall (VNet traffic) and Defender for Cloud Apps (SaaS CASB) are the neighbours it gets confused with.

### Identity governance

| Capability | Question it answers |
|---|---|
| **Entitlement management** | How do people request bundles of access? **Access packages** in catalogs with policies (who can request, approvals, expiry); **connected organizations** let partners request and get invited automatically |
| **Access reviews** | Should this person still have it? Reviewers (owners, managers, self) recertify group memberships, app assignments, role assignments and guests on a schedule, with auto-apply removal |
| **Lifecycle workflows** | Joiner, mover, leaver automation from attributes like employeeHireDate and employeeLeaveDateTime: generate a TAP, email the manager, remove groups, disable the account (ID Governance license) |
| **Privileged Identity Management (PIM)** | Just-in-time privilege: **eligible** assignments activated on demand (MFA, justification, approval, ticket, time limit) versus **active** standing assignments; time-bound or permanent; alerts; audit history; works for Entra roles, Azure roles and groups (**P2**) |

> **Trap.** Access reviews recertify access; they do not remove standing privilege by themselves. Scripts that assign roles permanently are still standing access. PIM eligible assignments are the Zero Trust default.

### Microsoft Entra ID Protection

- **User risk** = probability the identity is compromised (leaked credentials, anomalous user activity, threat-intel matches); evaluated mostly **offline**. Remediation: risk-based policy requiring a **secure password change** with MFA.
- **Sign-in risk** = probability that a specific authentication was not performed by the owner (anonymous IP, atypical travel, unfamiliar sign-in properties, password spray, malicious IP, token anomalies); real-time or offline. Remediation: require **MFA**.
- Risk levels low, medium, high; reports: **Risky users**, **Risky sign-ins**, **Risk detections**. Admins confirm compromised, confirm safe, dismiss; users self-remediate through Conditional Access.
- **Licensing:** full detection names and risk-based policies need **P2**. On P1 or Free most detections show only as **"Additional risk detected"**.
- Also covers **workload identities** risk. Feeds signals to Defender XDR and Sentinel.

### Microsoft Entra Verified ID

Issuer signs a credential (a university, an employer), the holder keeps it in a wallet (Microsoft Authenticator) and presents only what is needed, the verifier checks the signature against the issuer's public **decentralized identifier (DID)** without calling the issuer. Use cases: onboarding, proof of employment or education, passwordless recovery. Not B2B, not certificate-based authentication.
## Domain 3 · Capabilities of Microsoft security solutions (35–40%)

This is the heaviest domain. Two halves: Azure infrastructure and Defender for Cloud, then Sentinel, Security Copilot and Defender XDR.

### Core infrastructure security services in Azure

| Service | Layer | What it does | Confused with |
|---|---|---|---|
| **Azure DDoS Protection** | 3–4 (volumetric, protocol, some resource-layer) | Always-on traffic monitoring and automatic mitigation. **Infrastructure protection** is free and untuned; **Network Protection** is enabled per VNet with adaptive tuning, telemetry, alerts, DDoS Rapid Response, cost protection and WAF discount; **IP Protection** protects individual public IPs at lower cost without the extras | WAF (layer 7) |
| **Azure Firewall** | 3–7 | Managed, stateful, cloud-native firewall: application rules by **FQDN**, network rules, NAT rules, **threat-intelligence filtering**, built-in HA and zones; **Premium** adds TLS inspection, IDPS, URL filtering and web categories; **Basic** for SMB; central policy via Firewall Manager | NSG (no FQDN, no threat intel) |
| **Web Application Firewall (WAF)** | 7 | Protects web apps from **OWASP Top 10** (SQL injection, XSS) with managed rule sets and bot protection; deployed on **Application Gateway** (regional) or **Azure Front Door** (global) | DDoS (volumetric), NSG (cannot read HTTP) |
| **Virtual network segmentation** | Network | A **VNet is isolated by default**; subnets segment it; connect with **peering** or VPN and then control with NSGs or a firewall; resource groups and availability zones give **no** isolation | Resource groups |
| **Network security groups (NSGs)** | 3–4 | Rules with **priority 100–4096, lowest number first, stop at first match**; source/destination, port, protocol, allow/deny; **default rules** allow VNet and load-balancer inbound and deny the rest, allow all outbound; associated with a **subnet** or a **NIC** (subnet NSG then NIC NSG inbound); **application security groups** group NICs for rule targets | Azure Firewall |
| **Azure Bastion** | Management | PaaS jump service in the VNet brokering **RDP/SSH over TLS 443** from the portal or native client; VMs need **no public IP** and ports 3389/22 stay closed | Just-in-time VM access (opens the port on demand) |
| **Azure Key Vault** | Application/data | Central store for **secrets, keys, certificates** with RBAC or access policies, logging, soft delete and purge protection; **Standard** = software-protected keys, **Premium** = **HSM-protected** keys; Managed HSM for dedicated FIPS 140-2 Level 3 | Storage account, managed identity (which is how an app authenticates to Key Vault) |

> **Trap.** NSG priority 100 Deny beats priority 200 Allow regardless of how specific the allow rule is. Rule evaluation is by number, not by specificity.

### Microsoft Defender for Cloud

A **cloud-native application protection platform (CNAPP)** for Azure, AWS, GCP, and on-premises through **Azure Arc**.

| Capability | Free or paid | What it gives |
|---|---|---|
| **Foundational CSPM** | **Free** | **Secure score**, recommendations from the **Microsoft cloud security benchmark (MCSB)**, asset inventory, basic regulatory compliance view |
| **Defender CSPM** | Paid plan | **Attack path analysis**, **cloud security explorer**, agentless scanning, governance rules, data-aware posture, extra regulatory standards, security recommendations across clouds |
| **Cloud workload protection (CWP)** | Paid, per resource type | Runtime threat detection and alerts: Defender for **Servers** (includes Defender for Endpoint, **just-in-time VM access**, file integrity monitoring), **Storage** (malware scanning), **Databases** (SQL, open-source, Cosmos DB), **Containers**, **App Service**, **Key Vault**, **Resource Manager**, **DNS**, **APIs**, **AI services** |

- **Security policies** are built on **Azure Policy**: definitions grouped into **initiatives**; MCSB is the default initiative; each non-compliant evaluation becomes a recommendation feeding secure score. Regulatory compliance dashboard maps to standards (ISO 27001, PCI DSS, NIST, CIS).
- **Just-in-time VM access** (Defender for Servers) locks down management ports in the NSG and opens them only for an approved source IP and time window. Bastion avoids exposing the port at all: different approach, both valid, read the wording.
- Security alerts and incidents, workflow automation with Logic Apps, integration with Sentinel and Defender XDR.

**Four scores, four scopes.** Learn to tell them apart:

| Score | Where | Measures |
|---|---|---|
| **Secure score in Defender for Cloud** | Defender for Cloud | Posture of Azure, AWS, GCP resources against MCSB recommendations |
| **Microsoft Secure Score** | Defender portal | Microsoft 365 posture across identity, devices, apps, data (recommended actions, points) |
| **Identity Secure Score** | Entra admin center | Identity best practices; feeds the Identity category of Microsoft Secure Score; recalculates daily |
| **Compliance score** | Purview Compliance Manager | Progress on regulatory improvement actions |

### Azure governance side notes

- **Azure Policy:** enforce and audit resource configuration (effects such as Audit, Deny, DeployIfNotExists); initiatives bundle policies. **Resource locks:** CanNotDelete and ReadOnly on resources, groups or subscriptions. **Azure Blueprints** is deprecated; use Template Specs and Deployment Stacks. **Microsoft Purview** (Data Map and Unified Catalog) governs data, not resources.

### Microsoft Sentinel

**Cloud-native SIEM and SOAR** on a Log Analytics workspace (plus the Sentinel data lake for long-term, low-cost data).

| Stage | Sentinel feature | Definition to memorize |
|---|---|---|
| **Collect** | **Data connectors** and **Content hub** solutions | Hundreds of connectors for Microsoft, third-party, multicloud and on-premises sources (Syslog, CEF, agents, APIs) |
| **Detect** | **Analytics rules** | Run KQL logic on a schedule or in near real time to create alerts and incidents: scheduled, NRT, Microsoft security, **Fusion** (multistage attack correlation), ML behaviour, anomaly, threat intelligence |
| **Investigate** | **Incidents**, investigation graph, entity pages, **UEBA**, **hunting** queries, bookmarks, notebooks, MITRE ATT&CK view | UEBA builds behavioural baselines for users, hosts and entities and flags deviations; hunting is proactive querying before any alert exists |
| **Respond** | **Automation rules** and **playbooks** | Playbooks are **Azure Logic Apps** workflows (revoke sessions, disable users, open tickets); automation rules decide when they run and can also change incident properties |
| **Visualize** | **Workbooks** | Dashboards over ingested data |
| Enrich | **Watchlists**, **threat intelligence** | Reference lists (VIPs, known-bad IPs) and indicators used in rules and hunting |

- **SIEM** = collect, correlate, analyze security data at scale. **SOAR** = orchestrate and automate the response. **XDR** = native detection and response across a vendor's own workloads. Sentinel adds the SIEM and SOAR layer to what Defender XDR does natively.
- **Unified security operations:** Sentinel workspaces connect to the **Microsoft Defender portal**, giving one incident queue with Defender XDR, Exposure Management and Security Copilot. New customers onboard there by default; the **Azure portal Sentinel experience retires March 31, 2027**.

### Microsoft Security Copilot

- Generative AI assistant for security teams, consumed through provisioned **Security Compute Units (SCUs)** rather than per-user seats.
- **Standalone** portal (sessions, **promptbooks** = reusable multi-step workflows, plugins, agents) and **embedded** experiences in Defender, Sentinel (via the Defender portal), Entra, Intune and Purview.
- What it does: incident summaries, guided response, script and file analysis (deobfuscate PowerShell), device and user summaries, natural language to **KQL**, threat intelligence lookups, policy and access explanations.
- **Agents** run tasks autonomously: Phishing Triage Agent (Defender), Conditional Access Optimization Agent (Entra), Vulnerability Remediation Agent (Intune), Threat Intelligence Briefing Agent, alert triage agents in Purview.
- It complements Defender XDR and Sentinel; it is not a replacement and not a Sentinel workbook. Microsoft 365 Copilot is the productivity assistant, a different product.

### Microsoft Defender XDR

The suite that natively coordinates detection, prevention, investigation and response across endpoints, identities, email, and cloud apps. Portal: **security.microsoft.com** (the **Microsoft Defender portal**). "Microsoft 365 Defender" is the retired name.

| Service | Protects | Signature capabilities |
|---|---|---|
| **Defender for Endpoint** | Windows, macOS, Linux, iOS, Android devices | Next-generation protection, attack surface reduction, **EDR**, automated investigation and remediation, **device isolation**, live response, threat and vulnerability management. **P1** = prevention and ASR; **P2** = adds EDR, AIR, threat analytics, MDVM core |
| **Defender for Office 365** | Email and collaboration (Exchange, Teams, SharePoint, OneDrive) | Built-in **EOP**: anti-spam, anti-malware, anti-phishing, **ZAP** (zero-hour auto purge removes already-delivered mail). **Plan 1**: **Safe Attachments** (sandbox detonation before delivery), **Safe Links** (time-of-click URL check), impersonation protection. **Plan 2**: Threat Explorer, **automated investigation and response**, **attack simulation training**, campaign views, threat trackers |
| **Defender for Identity** | On-premises Active Directory | Sensors on **domain controllers** (and AD FS, AD CS, Entra Connect) detect reconnaissance, compromised credentials, **lateral movement** (pass-the-hash, pass-the-ticket), domain dominance (Golden Ticket) |
| **Defender for Cloud Apps** | SaaS applications (CASB) | **Cloud Discovery** of shadow IT (fed by Defender for Endpoint), app catalog risk scores, sanction/unsanction, app connectors, **Conditional Access App Control** session controls (block download on unmanaged devices), SaaS security posture, OAuth app governance |
| **Defender Vulnerability Management** | Asset weaknesses | Continuous inventory of software, browser extensions, certificates, firmware; weakness and exposure assessment; security baselines; risk-based remediation tracking. Included in Defender for Endpoint P2, premium add-on for more |
| **Defender Threat Intelligence** | Analysts' context | Intel profiles of threat actors, articles, indicators and infrastructure data to enrich incidents and hunting |

**Defender portal features**

| Feature | Definition |
|---|---|
| **Incidents** | A collection of correlated **alerts** that together tell one attack story, with timeline and evidence |
| **Action center** | Pending remediation actions awaiting approval and the history of actions taken |
| **Automated investigation and response (AIR)** | Investigates alerts and proposes or applies remediation (quarantine file, remove email) per automation level |
| **Automatic attack disruption** | High-confidence, real-time containment during ransomware or BEC: isolate devices, disable or contain users, to stop lateral movement |
| **Microsoft Secure Score** | Posture measurement with recommended actions in Identity, Device, Apps, Data; can drop when Microsoft adds recommendations or the environment grows |
| **Threat analytics** | Reports from Microsoft researchers on emerging threats mapped to your exposure and incidents |
| **Advanced hunting** | KQL over raw data |
| **Attack simulation training** | Simulated phishing and targeted training (Defender for Office 365 Plan 2) |
| **Microsoft Security Exposure Management** | Enterprise exposure graph, **attack surface map**, **critical asset management**, **initiatives** with an **exposure score**, attack path analysis across on-premises, hybrid and multicloud |
| **Audit** | The Microsoft 365 unified audit log search is also reachable here |

> **Traps.** Safe **Links** = time of click. Safe **Attachments** = sandbox before delivery. **ZAP** = remove after delivery. Defender for **Identity** = on-premises AD; Entra **ID Protection** = cloud identities. Sentinel and Azure Firewall are **not** members of Defender XDR.
## Domain 4 · Capabilities of Microsoft compliance solutions (20–25%)

### Service Trust Portal, privacy principles, Priva

- **Service Trust Portal (STP):** where customers download Microsoft's **independent audit reports** (SOC 1/2, ISO/IEC 27001, FedRAMP, PCI DSS), penetration test summaries, compliance guides and data protection resources; save documents to **My Library**. The **Trust Center** is the public marketing and policy site; it has no downloadable audit evidence. Compliance Manager measures **your** controls; Service health reports outages.
- **Microsoft's six privacy principles:** **Control**, **Transparency**, **Security**, **Strong legal protections**, **No content-based targeting**, **Benefits to you**. Expect a non-principle (shared responsibility, least privilege, residency) hidden among them.
- **Microsoft Priva** (privacy management, now its own portal), five solutions:

| Priva solution | Purpose |
|---|---|
| **Privacy Risk Management** | Policies for **data overexposure**, **data transfer**, **data minimization** across Microsoft 365, with user notifications and remediation |
| **Subject Rights Requests** | Automate discovery, review, redaction and export for **data subject requests** (GDPR access or delete requests) with due-date tracking |
| **Consent Management** | Build and publish consent models to collect and track user consent |
| **Privacy Assessments** | Automate assessments of how personal data is used |
| **Tracker Scanning** | Inventory cookies, pixels and beacons on your public websites against your privacy notice |

### Microsoft Purview compliance management

- **Microsoft Purview portal** = **purview.microsoft.com**, the single portal for every solution under **Solutions**. The Purview **compliance portal** (compliance.microsoft.com) and the Azure Purview governance portal are **retired**. Audit search also appears in the Defender portal.
- **Compliance Manager:** assessments built from **templates** (the default Microsoft data protection baseline plus hundreds of premium regulatory templates: GDPR, ISO/IEC 27001, NIST, HIPAA, PCI DSS, EU AI Act, NIST AI RMF) map **controls** to **improvement actions** with implementation and testing guidance, owners and evidence.
- **Compliance score** = points achieved over points available. Points come from **Microsoft-managed actions** (credited automatically from Microsoft's own implementation and audits) and **your improvement actions** (technical actions can be tested automatically from signals in other solutions; non-technical actions are attested).
- **Action taxonomy:** by function, **preventative** (stop incidents: encryption, access control), **detective** (find them: monitoring, audit), **corrective** (respond after: configuration changes to limit damage). By obligation, **mandatory** vs **discretionary**. Matching items on this taxonomy are common.

> **Trap.** Compliance score is not Secure Score. Secure Score is security configuration posture in the Defender portal; compliance score tracks regulatory improvement actions in Purview. Compliance Manager also is not limited to Microsoft 365 baselines: templates cover external regulations, other Microsoft services and non-Microsoft assets.

### Know your data: classification

| Method | How it identifies content | Use when |
|---|---|---|
| **Sensitive information types (SITs)** | Patterns (regex), keywords, checksums, confidence levels; hundreds built in, custom ones possible | Credit card numbers, passport numbers, national IDs |
| **Exact data match (EDM)** | Hashes of **your actual data table** uploaded; matches only real values | Cut false positives for account numbers, employee IDs |
| **Trainable classifiers** | Machine learning trained on samples; pre-trained (resumes, source code, harassment, contracts) or custom (about 50 samples to train) | Categories of content with no fixed pattern |
| **Document fingerprinting** | Content derived from a template form | Forms and templated documents |
| Named entities | Built-in entity detection (names, addresses) combined with SITs | Person-related data |

**Explorers**

| Tool | Answers |
|---|---|
| **Content explorer** (now **Data explorer**, with Content explorer marked classic) | **What** sensitive content exists and **where** it lives, by label, retention label or SIT; separate list-viewer and content-viewer role groups |
| **Activity explorer** | **What happened** to labeled and sensitive content over time: label applied, changed, removed, DLP matches, file activity, with dozens of filters |

### Protect: sensitivity labels

- A sensitivity label can: **encrypt** with usage rights for specific users, groups or domains (Azure Rights Management), add **content markings** (header, footer, watermark), apply **container settings** to Microsoft 365 groups, Teams and SharePoint sites (privacy, guest access, external sharing, unmanaged device access), extend to Power BI and meetings, and act as a **DLP condition**.
- Labels travel with the content; **one sensitivity label per item** (sublabels count as the one label); an item can also carry **one retention label**.
- **Label policy** publishes labels to users and groups and sets defaults, **mandatory labeling**, downgrade justification and help links. Creating a label without publishing means nobody sees it.
- **Auto-labeling:** **client-side** (recommend or apply in Office apps while editing) versus **service-side** (scan content at rest in SharePoint, OneDrive and Exchange with simulation mode; also files never opened).
- Label **priority** orders labels; when content from several labeled sources is combined, the highest-priority label wins (Copilot output inherits it).

### Prevent: data loss prevention

- **DLP policies** detect sensitive information and enforce **block**, **block with override and justification**, **audit**, **notify (policy tips)**, and generate alerts and incident reports.
- **Locations:** Exchange, SharePoint, OneDrive, Teams chats and channels, **devices (Endpoint DLP)**, on-premises repositories (scanner), Power BI, Fabric, Microsoft 365 Copilot and Copilot Chat, non-Microsoft apps via Defender for Cloud Apps.
- **Endpoint DLP** extends policies to onboarded Windows and macOS devices: copy to USB, print, upload to restricted service domains, paste into unapproved apps.
- DLP alerts appear in the Purview DLP alerts dashboard and can flow to the Defender portal.

> **Trap.** Sensitivity labels protect and classify; **DLP** inspects content at the moment of sharing. Labels do not stop a user emailing a card number; DLP does not encrypt a file. Both can be used together, because DLP can use a label as a condition.

### Govern: data lifecycle and records management

| | Retention **policy** | Retention **label** |
|---|---|---|
| Applied to | Whole **locations** (mailboxes, sites, OneDrive, Microsoft 365 Groups, Teams chats and channels, Copilot interactions), implicitly | Individual **items**, explicitly (manually, by default for a library, or auto-applied by SIT, keyword or classifier) |
| Can | Retain, delete, or retain then delete | The same, plus **declare records**, **event-based retention**, **disposition review** |
| Scope | Static, or **adaptive scopes** built from attributes | Published with a label policy or auto-applied |

- **Principles of retention** when settings conflict: (1) **retention wins over deletion**, (2) **the longest retention period wins**, (3) **explicit inclusion wins over implicit**, (4) **the shortest deletion period wins**. Periods are never added together.
- **Records management** builds on DLM: **records** (limited edits allowed, label change controlled) and **regulatory records** (no edits, no label removal, no deletion before expiry, even by admins), **file plan** descriptors, event-based retention, audited **disposition review** (reviewers delete, extend, relabel or add a stage). **Preservation lock** stops a policy itself from being changed.
- **Unified data governance:** the Purview **Data Map** scans multicloud and on-premises sources for technical metadata and **lineage**; the **Unified Catalog** lets stewards curate governance domains, data products, glossary terms and data quality rules, and see data estate health. This is data governance, not resource governance and not Microsoft 365 explorers.

> **Trap.** "Delete after 3 years" label plus "retain for 7 years" policy = kept for 7 years then deleted. A regulatory record cannot be unlocked or relabeled, which is why a standard record is the answer when the scenario allows occasional edits.
### Insider risk, eDiscovery, and audit

**Insider Risk Management (IRM)**

- Correlates signals (downloads, USB copies, cloud uploads, printing, Copilot prompts) with **triggering events** (HR connector resignation date, account deletion) using policy **templates**: data theft by departing users, data leaks, security policy violations, patient data misuse, **risky AI usage**, and more.
- **Privacy by design:** users are **pseudonymized by default** (for example "AnonIS8-988"); revealing the identity is a separate, audited step; role-based access limits reviewers.
- **Workflow:** policies → alerts → **triage** (needs review, resolved, dismissed) → **investigate** (cases, activity timeline, content) → **action** (notices, escalation to eDiscovery, ServiceNow ticket).
- **Adaptive Protection:** uses IRM risk levels as a dynamic condition so **DLP**, Conditional Access and lifecycle controls tighten for elevated-risk users and relax when risk subsides.

**Neighbours that get confused with IRM**

| Solution | Purpose |
|---|---|
| **Communication Compliance** | Detect inappropriate or non-compliant **messages** (threats, harassment, discrimination, regulatory violations, Copilot prompts) in Teams, Exchange, Viva Engage and third-party sources, with a reviewer workflow: resolve, notify, escalate, tag, remove |
| **Information barriers** | Define **segments** and block communication and collaboration between them in Teams, SharePoint and OneDrive (ethical walls between trading and research) |
| **Privileged Access Management** | Just-in-time, approval-based elevation for privileged **tasks in Exchange Online** |
| **Customer Lockbox** | You approve or reject a Microsoft engineer's request to access your content during support |
| **Data Security Investigations** | AI-assisted investigation of a data incident's scope and impact (newer Purview solution) |

**eDiscovery**

- One **unified eDiscovery** solution in the Purview portal since the classic Content search, eDiscovery (Standard) and eDiscovery (Premium) experiences were retired (August 2025). Capabilities split into **standard** and **premium** feature support by license.
- The **case** is the organizing unit: add **data sources** (custodial and non-custodial), place **holds**, run **searches** with KQL and conditions, review **statistics**, export, and with premium features add **review sets**, advanced indexing, OCR, conversation threading, near-duplicate detection, tagging, analytics and Security Copilot.
- **Content search** lives **inside eDiscovery** as a system-generated case for quick find-and-export with no hold or review needed.
- Copilot prompts and responses are stored in the user's mailbox and are searchable with the **Copilot activity** condition.

**Audit**

| | Audit (Standard) | Audit (Premium) |
|---|---|---|
| Included with | Most Microsoft 365 subscriptions | E5 / A5 / G5, Purview Suite, or the eDiscovery and Audit add-on |
| Retention | **180 days** (was 90) | **1 year** by default; up to **10 years** with the 10-Year Audit Log Retention add-on and a retention policy |
| Extras | Search in the Purview portal and Defender portal, PowerShell, Office 365 Management Activity API | Intelligent insights (MailItemsAccessed, Send, SearchQueryInitiated), higher API bandwidth, custom retention policies |

- The unified audit log records user and admin activity across Exchange, SharePoint, OneDrive, Teams, Entra ID, Purview and Copilot (**CopilotInteraction** events). Entra's own **sign-in logs** and **audit logs** are separate (7 days on Free, 30 days on P1/P2) and live in the Entra admin center.

> **Traps.** Audit Standard is **180 days**, not 90. Content search is not a standalone solution any more. eDiscovery holds preserve; retention policies govern lifecycle; neither replaces the other.

## Numbers to know

| Fact | Value |
|---|---|
| Passing score / time | 700 / 45 minutes |
| NSG rule priorities | 100–4096, lowest number evaluated first |
| Smart lockout defaults | 10 failed attempts, 60-second lockout |
| Custom banned password list | Up to 1,000 base terms (P1) |
| Entra sign-in and audit log retention | 7 days Free, 30 days P1/P2 |
| Audit (Standard) / (Premium) retention | 180 days / 1 year, up to 10 years with add-on |
| Trainable classifier training set | About 50 sample documents |
| DDoS tiers | Infrastructure (free), Network Protection (per VNet), IP Protection (per IP) |
| Defender for Office 365 plans | Plan 1 = Safe Links, Safe Attachments, impersonation; Plan 2 = adds Threat Explorer, AIR, attack simulation training |
| ID Protection detail visibility | P2 for names and risk-based policies; otherwise "Additional risk detected" |
| PIM, access reviews, entitlement management | Entra ID P2 (lifecycle workflows need ID Governance) |
| Conditional Access | Entra ID P1 |
| Sentinel playbook technology | Azure Logic Apps |
| Azure portal Sentinel retirement | March 31, 2027 |
| Security Copilot billing unit | Security Compute Units (SCUs) |
| Key Vault HSM-protected keys | Premium tier |

## If the question says… pick…

| Scenario wording | Answer |
|---|---|
| No credentials stored anywhere for an Azure workload | Managed identity |
| Partners in a Teams shared channel, no guest object | B2B direct connect |
| Consumer app with social sign-in and branding | External ID for customers |
| Provision users from a disconnected forest with lightweight agents | Entra Cloud Sync |
| Passwords must never reach the cloud, no AD FS | Pass-through authentication |
| Regulator demands phishing-resistant MFA for admins | Passkeys / FIDO2 (or WHfB, certificate-based) via authentication strength |
| Onboard a passwordless user with no methods yet | Temporary Access Pass |
| Small tenant, free, MFA for everyone, block legacy auth | Security defaults |
| See what a policy would do before enforcing | Report-only mode (plus What If) |
| Stop password guessing | Smart lockout / Password Protection, not Conditional Access |
| Help desk resets passwords for non-admins only | Helpdesk Administrator |
| Admin scoped to one region's users | Administrative unit |
| No permanent Global Admins, activate with MFA and justification | PIM eligible assignment |
| Owners recertify guests quarterly | Access reviews |
| Self-service catalog of bundled access with approval | Entitlement management access packages |
| Automate onboarding and offboarding tasks | Lifecycle workflows |
| Leaked credentials found | User risk → secure password change |
| Anonymous IP sign-in | Sign-in risk → require MFA |
| Replace VPN with per-app Zero Trust access | Entra Private Access |
| Filter employees' web browsing by category anywhere | Entra Internet Access |
| Verify a diploma cryptographically | Verified ID |
| Central FQDN and threat-intel filtering for VNets | Azure Firewall |
| OWASP Top 10 protection for a web app | Web Application Firewall |
| RDP/SSH with no public IP and closed ports | Azure Bastion |
| Open management ports only on request | Just-in-time VM access |
| Enhanced DDoS for five public IPs only | DDoS IP Protection |
| HSM-backed keys | Key Vault Premium |
| Attack paths and cloud security explorer | Defender CSPM plan |
| Malware in storage, brute force on SQL | Workload protection plans (Defender for Storage, Databases) |
| Ingest firewall, AWS and Entra logs into one SIEM | Sentinel data connectors |
| Detection logic on a schedule | Analytics rules |
| Automatic response actions | Playbooks (Logic Apps) via automation rules |
| Query before an alert exists | Hunting |
| Behavioural baselines for entities | UEBA |
| AI incident summaries and KQL help in Defender | Security Copilot |
| Pass-the-hash and Golden Ticket detection | Defender for Identity |
| Shadow IT discovery and session controls | Defender for Cloud Apps |
| Link weaponized after delivery | Safe Links |
| Attachment detonation before delivery | Safe Attachments |
| Phishing simulations | Defender for Office 365 Plan 2 |
| Isolate a ransomware-infected laptop automatically | Defender for Endpoint (or automatic attack disruption at XDR level) |
| Software and certificate inventory | Defender Vulnerability Management |
| Threat actor profiles and IOCs | Defender Threat Intelligence |
| Single exposure score, critical assets, initiatives | Security Exposure Management |
| Approve pending remediation actions | Action center |
| Download SOC 2 report | Service Trust Portal |
| GDPR data subject access request | Priva Subject Rights Requests |
| Detect personal data over-sharing and transfers | Priva Privacy Risk Management |
| Score against ISO 27001 with improvement actions | Compliance Manager |
| Encrypt and mark a document | Sensitivity label |
| Keep seven years then delete | Retention label or policy |
| Make a Teams team private with no guests by classification | Container sensitivity label |
| Label files at rest that contain card numbers | Service-side auto-labeling |
| Match only real account numbers | Exact data match |
| Find resumes with no fixed pattern | Trainable classifier |
| Who downgraded a label last week | Activity explorer |
| Where sensitive content lives | Data explorer (Content explorer) |
| Warn internally, block externally on card numbers | DLP with policy tips and override |
| Block USB copies of personal data | Endpoint DLP |
| Immutable trade confirmations | Regulatory record |
| Review before deletion at end of retention | Disposition review |
| Catalog SQL, S3 and Power BI with lineage | Purview Data Map and Unified Catalog |
| Departing employee data theft | Insider Risk Management |
| Stricter DLP for high-risk users automatically | Adaptive Protection |
| Harassment in Teams messages | Communication Compliance |
| Trading and research must not talk | Information barriers |
| Legal hold, collect, review, export | eDiscovery case |
| Count mentions of a code name and export | Content search (inside eDiscovery) |
| Ten-year audit retention with insights | Audit (Premium) plus add-on |

## Say this, not that

| Retired or wrong | Current |
|---|---|
| Azure Active Directory, Azure AD, AAD | **Microsoft Entra ID** |
| Azure AD B2B / B2C | **Microsoft Entra External ID** (B2B collaboration; External ID for customers) |
| Microsoft 365 Defender | **Microsoft Defender XDR** in the **Microsoft Defender portal** |
| Azure Security Center / Azure Defender | **Microsoft Defender for Cloud** |
| Azure Sentinel | **Microsoft Sentinel** (unified in the Defender portal) |
| Microsoft Cloud App Security | **Microsoft Defender for Cloud Apps** |
| Azure ATP / Office 365 ATP / Microsoft Defender ATP | Defender for **Identity** / **Office 365** / **Endpoint** |
| Azure Information Protection | **Microsoft Purview Information Protection** |
| Compliance center / Purview compliance portal | **Microsoft Purview portal** (purview.microsoft.com) |
| Content explorer | **Data explorer** (Content explorer is classic) |
| eDiscovery (Standard) / (Premium) / Advanced eDiscovery | **Unified eDiscovery** with standard and premium feature support |
| Advanced Audit | **Audit (Premium)** |
| Azure Purview | **Microsoft Purview** Data Map and Unified Catalog |
| Azure Blueprints | Deprecated; Template Specs and Deployment Stacks |
| Entra Permissions Management | Retired (October 2025) |
| Message packs, per-message billing (Copilot) | Not in SC-900; ignore |

## The last 30 minutes: read twice

- Data, endpoints, identities are **always yours**.
- Zero Trust = **verify explicitly, least privilege, assume breach**; six pillars; defense in depth is not one of the three.
- Encrypt with the recipient's **public** key; sign with your **private** key; hashing is one-way.
- Residency = **where**; sovereignty = **whose laws**.
- ID token = who you are; access token = what you can call.
- Federation = trust, **no sync**. PHS vs PTA vs AD FS.
- B2B collaboration creates a guest; **B2B direct connect does not**.
- Agent identities have **no credentials**; the **blueprint** does.
- Phishing-resistant = passkeys/FIDO2, WHfB, certificates. SMS is not.
- Security defaults are free and **cannot coexist** with Conditional Access; Conditional Access needs **P1**; ID Protection detail and PIM need **P2**.
- Conditional Access runs **after** first-factor auth; grant vs **session** controls; report-only first; exclude break-glass.
- Entra roles ≠ Azure RBAC; administrative units scope Entra roles.
- User risk → password change; sign-in risk → MFA.
- Private Access replaces VPN; Internet Access is the SWG.
- NSG: lowest priority number first, first match wins; subnet or NIC.
- Firewall = FQDN and threat intel; WAF = OWASP layer 7; DDoS = layer 3–4; Bastion = no public IP; JIT = open on request.
- Foundational CSPM free; Defender CSPM paid (attack paths); workload plans detect runtime threats.
- Four scores: Defender for Cloud secure score, Microsoft Secure Score, Identity Secure Score, compliance score.
- Sentinel: connectors → analytics rules → incidents/hunting/UEBA → automation rules + playbooks (Logic Apps) → workbooks.
- Security Copilot: SCUs, promptbooks, agents, embedded and standalone.
- Safe Links (click) vs Safe Attachments (delivery) vs ZAP (after delivery). Plan 2 = simulations and AIR.
- Defender for Identity = on-prem AD sensors on DCs. Cloud Apps = CASB.
- Incident = correlated alerts. Action center = approvals. Attack disruption = automatic containment. Exposure Management = exposure score.
- STP = audit reports; Trust Center = public info; six privacy principles.
- Compliance Manager: Microsoft-managed vs your actions; preventative/detective/corrective.
- Sensitivity label (protect) vs retention label (lifecycle) vs DLP (prevent sharing); one sensitivity label per item; publish with a policy.
- Retention wins, longest wins, explicit wins, shortest deletion wins.
- Regulatory record = immutable. Disposition review = decide at end.
- IRM is pseudonymized by default; Adaptive Protection links IRM to DLP.
- Unified eDiscovery; Content search inside it; Audit Standard **180 days**, Premium **1 year**, up to **10**.
