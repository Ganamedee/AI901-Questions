# SC-900 and AB-900 Rapid Cram

The short version of both cram sheets: highest-yield facts, product-to-purpose mappings and traps. About twenty minutes of reading.

## SC-900 · where the marks are

Security solutions **35–40%** and Entra **25–30%** are two thirds of the paper. Concepts are only **10–15%**. Spend your time on "which product does this job".

### The 12 facts that pay most

1. **Most of the paper is one question:** nearly every item asks *which capability solves this need*. Learn the one-liner and the neighbour it is confused with.
2. **Zero Trust = verify explicitly, least privilege, assume breach.** Defense in depth is **not** one of them.
3. **Data, devices, identities are always the customer's** in every shared responsibility model. Physical is always Microsoft's in cloud.
4. **Encrypt with the recipient's public key. Sign with your private key. Hashing is one-way** (salted hash for passwords).
5. **Conditional Access needs P1. PIM, ID Protection detail and access reviews need P2.** Security defaults are free and cannot run alongside Conditional Access.
6. **Conditional Access runs after the password is accepted**, so it cannot stop password spray. Smart lockout and Password Protection do.
7. **User risk → force secure password change. Sign-in risk → require MFA.**
8. **Phishing-resistant = passkeys/FIDO2, Windows Hello for Business, certificates.** SMS and push are not.
9. **NSG rules: lowest priority number first, first match wins.** Attach to a subnet or a NIC.
10. **Sensitivity label = protect (encrypt, mark). Retention label = lifespan. DLP = stop it being shared.** One sensitivity label per item.
11. **Retention conflicts: retention beats deletion, longest period wins.** Never added together.
12. **Audit Standard = 180 days.** Premium = 1 year, 10 with the add-on.

### Product to purpose

| Need | Answer |
|---|---|
| App or VM needs secrets with no credentials in code | Managed identity |
| Partner in a Teams shared channel, no guest account | B2B direct connect |
| Consumer app, social sign-in, your branding | External ID for customers |
| Passwords must not reach the cloud, no AD FS | Pass-through authentication |
| Onboard a user with no auth methods yet | Temporary Access Pass |
| Admin scoped to one region's users | Administrative unit |
| No permanent Global Admins | PIM eligible assignment |
| Owners recertify guests quarterly | Access reviews |
| Self-service request for a bundle of access | Entitlement management access package |
| Automate joiner, mover, leaver | Lifecycle workflows |
| Replace the VPN with per-app access | Entra Private Access |
| Filter employee web browsing anywhere | Entra Internet Access |
| Verify a diploma cryptographically | Verified ID |
| Identity for an AI agent | Entra Agent ID (blueprint holds the credentials) |
| Central outbound filtering by FQDN | Azure Firewall |
| SQL injection and XSS on a web app | Web Application Firewall |
| RDP/SSH with no public IP | Azure Bastion |
| Open management ports only on request | Just-in-time VM access |
| Attack paths, cloud security explorer | Defender CSPM (paid) |
| Malware in storage, brute force on SQL | Workload protection plans |
| HSM-backed keys | Key Vault Premium |
| Ingest firewall + AWS + Entra logs into one place | Sentinel data connectors |
| KQL detection on a schedule | Analytics rules |
| Automatic response actions | Playbooks (Logic Apps) via automation rules |
| Search for threats before any alert | Hunting |
| Behaviour baselines per user or host | UEBA |
| AI incident summaries, KQL help | Security Copilot (billed in SCUs) |
| Pass-the-hash, Golden Ticket on-premises | Defender for Identity |
| Shadow IT discovery, block downloads in session | Defender for Cloud Apps |
| Link weaponised after delivery | Safe Links |
| Attachment detonated before delivery | Safe Attachments |
| Malicious mail already in mailboxes | ZAP |
| Phishing simulations | Defender for Office 365 **Plan 2** |
| Isolate a ransomware laptop | Defender for Endpoint |
| Software and certificate inventory | Defender Vulnerability Management |
| One exposure score, critical assets | Security Exposure Management |
| Approve pending remediation | Action center |
| Download Microsoft's SOC 2 / ISO report | Service Trust Portal |
| GDPR subject access request | Priva Subject Rights Requests |
| Score against ISO 27001 with actions | Compliance Manager |
| Find where sensitive content lives | Content / Data explorer |
| Who changed a label last week | Activity explorer |
| Block USB copies of personal data | Endpoint DLP |
| Immutable trade records | Regulatory record |
| Departing employee stealing files | Insider Risk Management |
| Harassment in Teams messages | Communication Compliance |
| Trading and research must not talk | Information barriers |
| Legal hold, collect, review, export | eDiscovery case |
| Keyword search and export, nothing preserved | Content search (inside eDiscovery) |

### Pairs they will try to swap

| This | Not this |
|---|---|
| Defender for **Identity** = on-premises AD | Entra **ID Protection** = cloud identities |
| **Microsoft Secure Score** = M365 posture | **Secure score in Defender for Cloud** = Azure/AWS/GCP resources |
| **Identity Secure Score** = Entra identity only | **Compliance score** = Compliance Manager regulatory |
| **Bastion** = never expose the port | **JIT access** = open it briefly on request |
| **Azure Firewall** = FQDN, threat intel | **NSG** = IP, port, protocol only |
| **DDoS** = layer 3–4 volumetric | **WAF** = layer 7 OWASP |
| **Sentinel** = SIEM + SOAR, any source | **Defender XDR** = native detection across Microsoft workloads |
| **Grant** controls (MFA, compliant device) | **Session** controls (sign-in frequency, app-enforced) |
| **Retention policy** = whole location | **Retention label** = individual item, records, disposition |
| **Trust Center** = public info | **Service Trust Portal** = downloadable audit reports |

### Say the new name

Microsoft Entra ID (not Azure AD) · Microsoft Defender XDR (not Microsoft 365 Defender) · Microsoft Defender for Cloud (not Security Center) · Microsoft Purview portal (not compliance center) · unified eDiscovery (not Standard/Premium) · Audit Premium (not Advanced Audit).

## AB-900 · where the marks are

Data protection and governance **35–40%** is the biggest slice and almost all of it is Purview plus SharePoint oversharing. Core services **30–35%**, Copilot and agent admin **25–30%**.

### The 12 facts that pay most

1. **Least privilege wins every "who should do this".** Copilot and agents → **AI Administrator**. Purview and DSPM → **Compliance Administrator**. Billing policies → Billing Administrator. Global Admin is the wrong answer unless nothing else fits.
2. **Copilot only sees what the user can already see.** It queries Microsoft Graph as the signed-in user. Indexing grants nothing. The real risk is oversharing.
3. **RAC changes access. RCD changes discoverability.** Restricted SharePoint Search is retiring (blocked from 31 July 2026), so answer **RCD**.
4. **purview.microsoft.com.** The compliance portal is retired. **Data explorer** finds sensitive info. **Content search lives inside eDiscovery**.
5. **Block removes the agent from people who already installed it. Remove only takes it out of inventory.**
6. **Agent approvals: Microsoft 365 admin center > Agents > All agents > Requests.** Only AI Administrator and Global Administrator can approve.
7. **Researcher and Analyst sit outside all agent settings.** Tenant-wide **Block** is the only control; you cannot scope them to a group. Analyst is the Excel one.
8. **No 300-seat minimum.** 300 is a **maximum** on the Business SKUs. **E5 does not include Copilot; E7 does.**
9. **Pay-as-you-go is two steps:** create the billing policy, then connect it on the **Pay-as-you-go services** tab. Path is **Copilot > Billing & usage**.
10. **Budgets only send email. They never cap spend.** $0.01 per Copilot Credit.
11. **Audit logs are not for usage reporting.** Use the Copilot usage report or the **Copilot Dashboard in Viva Insights**.
12. **Copilot licences take up to 24 hours to appear** and cannot be given to guests.

### Where things live

| Task | Portal |
|---|---|
| Users, licences, groups, domains, roles, **Copilot**, **Agents** | Microsoft 365 admin center |
| Mailboxes, **distribution groups**, mail flow rules | Exchange admin center |
| Active sites, sharing policies, **Data access governance**, RAC, RCD | SharePoint admin center |
| Teams, channels, messaging policies, **Manage apps** | Teams admin center |
| Conditional Access, Identity Secure Score, authentication methods | Entra admin center (**PIM is under ID Governance**) |
| Incidents, Microsoft Secure Score, audit search | Defender portal |
| Labels, DLP, retention, DSPM for AI, eDiscovery, Audit | Purview portal |
| Makers build agents | Copilot Studio |
| Copilot Studio agent governance, environment roles, connector DLP | Power Platform admin center |
| **Copilot Dashboard** | Viva Insights app, not the admin center |

### Purview tool to job

| Need | Answer |
|---|---|
| Where does sensitive data live | **Data explorer** (Content explorer is classic) |
| What happened to a label, DLP matches over time | Activity explorer |
| Which AI apps are used, sensitive prompts, overshared sites | **DSPM for AI** (weekly top-100 SharePoint assessment) |
| Stop Copilot summarising labelled files | DLP policy, **Microsoft 365 Copilot and Copilot Chat** location |
| Delete Copilot prompts after 90 days | Retention policy for **Copilot interactions** |
| Review harassing Copilot prompts | Communication Compliance, Detect Microsoft Copilot interactions |
| Score repeated attempts to extract secrets via prompts | Insider Risk Management, **Risky AI usage** |
| EU AI Act readiness | Compliance Manager AI templates |
| Prove which files Copilot touched | Audit, **CopilotInteraction** |
| A user's Copilot prompts for a legal case | eDiscovery on their **mailbox**, Copilot activity condition |
| Keyword search and export for legal | Content search inside eDiscovery |

### Copilot and agent admin

| Situation | Answer |
|---|---|
| User can open a file but Copilot returns nothing from it | The label grants **VIEW but not EXTRACT** |
| Label on a Copilot-generated document | Inherits the **highest-priority** source label |
| Copilot must never use the web | Turn off **Allow web search in Copilot** |
| Only Finance may use agents | Agents > Settings > **User access** > specific group |
| Agent update asks for more permissions | **Pending update**; users stay on the old version until approved |
| Maker submitted a Copilot Studio agent | Still needs Microsoft 365 admin center approval |
| Copilot Studio licence but cannot build | Missing **Environment Maker** role |
| End user of a published agent | Needs no licence or environment role, just the endpoint |
| Unlicensed users need work-grounded chat | Pay-as-you-go billing policy |
| SharePoint agent prompt for an unlicensed user | **12 credits** (2 generative + 10 graph grounding) |
| Find oversharing before rollout | SharePoint admin center > Reports > **Data access governance** |
| 400 overshared sites, no business context | **Site access reviews** delegated to owners |

### Traps

- **Exchange admin center** and **distribution groups** (the tab says Distribution list).
- Owners = Full Control, **Members = Edit**, Visitors = Read. **View Only** blocks download.
- Shared mailbox needs **no licence** up to 50 GB. Mail-enabled security group when you need mail **and** permissions.
- Blocking an Agent Builder or Copilot Studio agent also hits Outlook and Teams; blocking a SharePoint or Foundry agent only hits Copilot Chat.
- Admin pins max **3**, up to 6 hours to appear.
- Prompts: save, share, **schedule**, delete.

## If you have ten minutes left

Read the numbered lists at the top of each exam. Those 24 facts cover more marks than anything else on this page.
