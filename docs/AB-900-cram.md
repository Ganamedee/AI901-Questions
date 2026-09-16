# AB-900 Cram Sheet

**Microsoft 365 Copilot and Agent Administration Fundamentals.** Skills measured as of **July 22, 2026**. Built to be read the night before and skimmed again in the 30 minutes before you sit down.

## Exam facts

| Item | Value |
|---|---|
| Domains and weights | Core features and objects of Microsoft 365 services **30–35%** · Data protection and governance for Microsoft 365 and Copilot **35–40%** · Basic administrative tasks for Copilot and agents **25–30%** |
| Time | **45 minutes** of exam time (about 65 minutes of seat time) |
| Passing score | **700** on a 1–1000 scale |
| Question count | Microsoft's generic figure is **40–60** |
| Item types | Multiple choice, "select two/three", Yes/No statement sets, sentence completion, matching, hot area |
| Languages | English only |
| Learn access during the exam | **No** |
| Renewal | **None.** Fundamentals certifications do not expire |
| Retake | 24 hours after a first failed attempt |
| Certification title | Microsoft 365 Certified: Copilot and Agent Administration Fundamentals |

**What the July 22, 2026 refresh changed.** Three **Minor** wording edits and zero major ones; weights unchanged. The wording that moved is exactly what the exam now expects:

| Older wording | Current wording |
|---|---|
| Exchange Online admin center, distribution lists | **Exchange admin center**, **distribution groups** |
| SharePoint in Microsoft 365 admin center | **SharePoint admin center** (the service is still SharePoint in Microsoft 365) |
| Restricted site access | **Restricted access control** (RAC) |
| Microsoft Purview Content explorer | **Microsoft Purview Data Explorer** |
| Content search as a standalone solution | **Content search in Microsoft Purview eDiscovery** |
| Microsoft 365 Defender | **Microsoft Defender XDR** |
| Copilot pay-as-you-go, generic | Monthly license model compared to pay-as-you-go, **including SharePoint** |

## How to attack the items

- **Least privilege beats Global Administrator on every "who should do this" question.** For Copilot and agent tasks the answer is usually **AI Administrator**; for Purview data security it is **Compliance Administrator**; for billing policies, **Billing Administrator** also qualifies.
- **Portal questions are about which console, not which click.** Know the nine portals and what lives in each, and know that anything under the retired compliance portal now lives at **purview.microsoft.com**.
- **Old numbers are traps:** the 300-seat *minimum* is gone (300 is now a *maximum* on SMB SKUs); Audit Standard is 180 days, not 90; Restricted SharePoint Search is retiring; message packs are now Copilot Credits.
- **Yes/No sets** score each statement separately; hunt for absolutes.
- Most questions cover generally available features; preview features appear only when commonly used.

## Domain 1 · Core features and objects of Microsoft 365 services (30–35%)

### The nine portals

| Portal | URL | What you do there |
|---|---|---|
| **Microsoft 365 admin center** | admin.microsoft.com (also admin.cloud.microsoft) | Users, licenses, groups, domains, org settings, roles, service health, reports, the top-level **Copilot** and **Agents** nodes |
| **Exchange admin center** | admin.exchange.microsoft.com | Mailboxes, distribution groups, mail flow rules, connectors, accepted domains, litigation hold |
| **SharePoint admin center** | admin.microsoft.com/sharepoint | Active sites, sharing policies, access control, **Data access governance** reports, RAC, RCD, OneDrive settings |
| **Microsoft Teams admin center** | admin.teams.microsoft.com | Teams, channels, messaging and meeting policies, **Manage apps** and app permission policies |
| **Microsoft Entra admin center** | entra.microsoft.com | Identities, Conditional Access, Identity Secure Score, authentication methods, PIM (under ID Governance), app registrations, enterprise applications, sign-in and audit logs |
| **Microsoft Defender portal** | security.microsoft.com | Defender XDR, incidents, Microsoft Secure Score, Threat analytics, audit log search |
| **Microsoft Purview portal** | purview.microsoft.com | Every compliance and data security solution under **Solutions**; Compliance Manager at top level |
| **Microsoft Copilot Studio** | copilotstudio.microsoft.com | Makers build agents; publishing sends them to the admin center approval queue |
| **Power Platform admin center** | admin.powerplatform.microsoft.com | Environments, environment roles, DLP connector policies, Copilot hub, Power Platform inventory |

> **Trap.** The Microsoft Purview **compliance portal** is retired. If compliance.microsoft.com is an option, it is the wrong one. "Microsoft 365 Defender" and protection.office.com are retired names too.

### Licensing and SKUs

| SKU | What to know |
|---|---|
| **Microsoft 365 E3** | Core productivity; basic retention and labels; no Copilot |
| **Microsoft 365 E5** | E3 plus advanced security and compliance (Defender, Purview premium, Audit Premium, eDiscovery premium, Entra P2); **still no Copilot** |
| **Microsoft 365 E7** | **GA May 1, 2026.** A strict superset of E5 that adds **Microsoft 365 Copilot**, the **Microsoft Entra Suite** and **Microsoft Agent 365**. The one enterprise SKU that includes Copilot in the base |
| **Microsoft 365 Copilot** (add-on) | About **$30** per user per month, annual commitment; needs a qualifying base plan (E3, E5, E7, F1, F3, Business Basic/Standard/Premium, Office 365 E1/E3/E5, Apps for business/enterprise and more) |
| **Microsoft 365 Copilot Business** | SMB add-on for organizations on Business plans; **same capabilities** as the enterprise add-on; **300-seat maximum**; annual commitment |
| **Business Standard / Premium with Copilot** | Bundled SMB SKUs (GA July 2026), 300 maximum |
| **Microsoft Agent 365** | GA May 1, 2026, licensed **per user** (in Frontier it was per agent instance); included in E7 |
| **Microsoft 365 Copilot Chat** | Included at no cost with an eligible subscription and a work or school account: **web-grounded chat is free**; **work-grounded chat** (Microsoft Graph data), Copilot in the apps, Researcher and Analyst need the **Copilot license** |

- **There is no seat minimum.** Microsoft removed the original 300-seat minimum in January 2024. The only 300 left is a **maximum** on Copilot Business and the bundled SMB SKUs.
- Licenses are made of **service plans**; you can switch off Exchange Online, Teams or SharePoint inside an assignment and keep the rest.
- **Group-based licensing** needs Entra ID P1 (or Office 365 E3/A3/G3 and newer); **no nested groups**; users need a usage location; errors show on the Errors and issues tab (Reprocess). Up to 20 users or groups per assignment action. Dynamic membership rules (department equals Sales) keep it hands-off.
- **Copilot cannot be licensed to guests or cross-tenant users.** After assignment allow **up to 24 hours** and possibly an app restart; Microsoft 365 Apps must be on Current or Monthly Enterprise Channel, not Semi-Annual.

### Exchange objects

| Object | Purpose | Trap |
|---|---|---|
| **User mailbox** | Auto-provisioned when an Exchange license is assigned (50 or 100 GB) | Removing the license removes the mailbox after a grace period |
| **Shared mailbox** | Team address such as hr@; **no license needed up to 50 GB**; delegates get **Full Access** and **Send As** or **Send on Behalf** | Do not share a user mailbox password |
| **Room / equipment mailbox** | Resource mailboxes that auto-accept or decline bookings; room = location, equipment = projector or vehicle | |
| **Distribution group** | Mail distribution only; the portal tab says **Distribution list** | Cannot hold permissions or licenses |
| **Dynamic distribution group** | Membership recalculated from a recipient filter at send time | Mail only |
| **Mail-enabled security group** | Receives mail **and** grants permissions | The answer when both are needed |
| **Microsoft 365 group** | Collaboration workspace: group mailbox, calendar, SharePoint site, Planner, Teams | Heavier than a distribution group |
| Mail flow (transport) rules, connectors, accepted domains, litigation hold | Inspect and act on messages, route mail, define handled domains, preserve mailbox content | |

### SharePoint and OneDrive objects

- **Team site** (tied to a Microsoft 365 group, collaboration) versus **communication site** (broadcast, one-to-many). **Hub sites** connect related sites for shared navigation, branding and news while each keeps its own permissions. Private channels get their own site.
- **Permission levels:** Full Control, Design, **Edit** (manage lists plus contribute), **Contribute** (add, edit, delete items), **Read** (view and **download**), **View Only** (view in browser, **no download**). Default groups: **Owners = Full Control, Members = Edit, Visitors = Read**.
- **Inheritance** flows site → library → folder → item; **break inheritance** to give a folder unique permissions. Sensitivity labels do not apply to folders.
- **Sharing links:** Anyone (anonymous), People in your organization, People with existing access, Specific people. Tenant sharing defaults and the default link type live at **SharePoint admin center > Policies > Sharing**; OneDrive settings are in the SharePoint admin center too.

### Teams objects

- **Standard channel** (everyone in the team), **private channel** (subset, own SharePoint site), **shared channel** (people from other teams or other organizations via **B2B direct connect**, no guest account), org-wide team.
- **Policies:** messaging policies (delete or edit sent messages, GIFs, chat), meeting policies (recording, transcription, anonymous join), app permission and setup policies; **Teams apps > Manage apps** controls org-wide app availability; a custom policy targets a department.
- Every team provisions a Microsoft 365 group, a SharePoint site and a group mailbox.

### Entra objects and admin basics

- **Users:** member or guest (B2B). **Groups:** security (permissions, Conditional Access targeting, licensing), Microsoft 365, mail-enabled security, distribution; **dynamic membership** from attributes. **Administrative units** scope admin roles.
- **Domains:** add at Microsoft 365 admin center > Settings > Domains; verify with a **TXT** (or MX) record; the wizard then supplies service records. **Org settings > Organization profile** holds organization information, privacy profile (statement URL, contact), release preferences.
- **Roles:** assign per user at Users > Active users > user > **Manage roles**; tenant-wide at Roles > Role assignments. Key roles and what they are for:

| Role | Use it for |
|---|---|
| **Global Administrator** | Emergencies only; Microsoft calls it highly privileged |
| **AI Administrator** | Copilot settings, Copilot reports, pay-as-you-go billing, **agent approvals and ownership** |
| **Compliance Administrator** | Purview solutions including **DSPM for AI** |
| **Billing Administrator** | Subscriptions, invoices, pay-as-you-go billing policies |
| **License Administrator** | Assign and remove licenses only |
| **User Administrator** | Create and manage users, groups, licenses |
| **Helpdesk Administrator** | Password resets for non-admins |
| **Exchange / SharePoint / Teams Administrator** | Their workload only |
| **Global Reader / AI Reader / Reports Reader** | View only; can see agent registries and reports but cannot approve or block |

- **Service health** (incidents, advisories), **Message center** (changes and deprecations), **Reports > Usage** (adoption) in the Microsoft 365 admin center.
### Security principles and Microsoft Defender XDR

- **Zero Trust:** **verify explicitly**, **use least privilege access** (PIM just-in-time is the textbook example), **assume breach** (segment, encrypt, monitor with Defender XDR and Sentinel, rehearse response). Defense in depth is a supporting strategy, not one of the three.
- **Authentication** proves who you are; **authorization** decides what you may do. A user who passes MFA and is then denied a SharePoint delete failed **authorization**.
- **MFA methods:** Authenticator push with number matching, TOTP, **passkeys/FIDO2**, Windows Hello for Business, certificate-based, SMS and voice (weakest, being retired), Temporary Access Pass for onboarding and recovery. **Phishing-resistant** = passkeys/FIDO2, Windows Hello for Business, certificates. Microsoft's **mandatory MFA** for admin portals and Azure Resource Manager is in force with no opt-out.
- **Legacy authentication** (IMAP, POP, SMTP basic auth) bypasses MFA; block it with Conditional Access, security defaults, or the newer **Baseline Security Mode** in Org settings > Security and privacy.
- **Security defaults:** free preconfigured protections (MFA registration, MFA for admins, block legacy auth). Cannot coexist with Conditional Access.

**Defender XDR services**

| Service | Protects | Remember |
|---|---|---|
| **Defender for Office 365** | Email and collaboration | **Safe Attachments** = sandbox before delivery; **Safe Links** = time-of-click; **ZAP** = remove after delivery; **attack simulation training** and automated investigation need **Plan 2** |
| **Defender for Endpoint** | Devices | EDR, isolation, attack surface reduction, vulnerability management; feeds Cloud Discovery |
| **Defender for Identity** | On-premises Active Directory | Sensors on domain controllers detect lateral movement and credential theft |
| **Defender for Cloud Apps** | SaaS and shadow IT | Cloud Discovery, app risk scores, sanction/unsanction, session controls |
| **Defender Vulnerability Management** | Asset weaknesses | Inventory, exposure, remediation |

- The **Microsoft Defender portal** (security.microsoft.com) correlates alerts into **incidents** with one attack story (phishing → compromised account → malicious upload). **Microsoft Secure Score** lives here with **Identity, Device, Apps, Data** categories; its Identity category is fed by **Identity Secure Score** in Entra.

### Entra ID and core security features

| Feature | What to know |
|---|---|
| **Conditional Access** | If (user, resource, device state, named location, risk) then (block, require MFA, require compliant device, authentication strength). Create in **report-only** first; test with **What If**; **exclude break-glass accounts**; the target selector is now **Resources (formerly cloud apps)**. Evaluated at sign-in, not at license assignment. Path: Entra ID > Conditional Access > Policies |
| **Identity Secure Score** | Entra ID > Identity Secure Score; improvement actions with points; **recalculates every 24 hours**; feeds Microsoft Secure Score; not a count of risky users, not compliance score |
| **Authentication methods** | Entra ID > Authentication methods > Policies; reset a user's methods or issue a **Temporary Access Pass** when a phone is lost |
| **Privileged Identity Management** | **ID Governance > Privileged Identity Management**; **eligible** (activate on demand with MFA, justification, approval, duration) versus **active** (always on); Entra ID P2; audit history 30 days; break-glass accounts stay permanent |
| **ID Protection** | Risky users and risky sign-ins (atypical travel, leaked credentials); confirm safe, dismiss, or confirm compromised; users self-remediate with MFA or password change through risk-based Conditional Access |
| **Sign-in logs** | Every authentication with the **Conditional Access tab** showing which policy applied; diagnose error **53003** here |
| **Audit logs** | Directory changes: who added a member to a group, who edited a policy. The **unified audit log** in Purview spans all of Microsoft 365 and Copilot |
| **Enterprise applications** | The **service principal**: SSO (SAML or OIDC), user and group assignment, consent, sign-in activity, central revocation at offboarding |
| **App registrations** | The **application object**: redirect URIs, credentials, requested API permissions. Registration creates both objects |
| **Consent** | Users may consent to low-risk delegated permissions (per tenant settings); high-privilege or application permissions need **admin consent** after reviewing publisher and scopes; enable the admin consent request workflow |
| **Guests** | Invite as **B2B guest** for a vendor needing one site; govern with access reviews; never share credentials or create a member account |

> **Traps.** Identity Secure Score (Entra, identity only) is not Microsoft Secure Score (Defender, tenant-wide). Conditional Access and Identity Secure Score are under **Entra ID**; PIM is under **ID Governance**. It is Microsoft Entra ID, never Azure AD.

## Domain 2 · Data protection and governance for Microsoft 365 and Copilot (35–40%)

The heaviest domain. Everything here lives at **purview.microsoft.com** unless stated. Compliance Manager sits at the top level of the left navigation; the other solutions sit under **Solutions**, grouped as Core, Risk and Compliance, Data Governance, Data Security.

### The Purview solution map

| Solution | Does | Copilot-specific hook |
|---|---|---|
| **Information Protection** | Sensitivity labels, label policies, auto-labeling, **Data explorer**, Activity explorer | Copilot honors label encryption (needs VIEW **and** EXTRACT); output inherits the highest-priority label |
| **Data Loss Prevention** | Detect and block sensitive data leaving via email, Teams, SharePoint, devices | Location **Microsoft 365 Copilot and Copilot Chat** |
| **Data Lifecycle Management** | Retention policies and labels | Retention policy for **Copilot interactions** (prompts and responses in the user's mailbox) |
| **Records Management** | Records, regulatory records, file plan, disposition | Separate solution from DLM |
| **Insider Risk Management** | Score risky user behaviour | **Risky AI usage** template; prompt injection and protected-material detection |
| **Communication Compliance** | Review messages for policy violations | **Detect Microsoft Copilot interactions** template; prompts and responses appear as separate entries |
| **DSPM for AI** | AI-specific posture: which AI apps are used, sensitive data in prompts, risky users, overshared sites | Weekly **top-100 SharePoint sites** data risk assessment; one-click policies |
| **Compliance Manager** | Compliance score, assessments, improvement actions | **AI regulation templates** (EU AI Act, NIST AI RMF, ISO/IEC 42001) |
| **eDiscovery** | Cases, holds, searches, review sets; **contains Content search** | Search a mailbox with the **Copilot activity** condition |
| **Audit** | Unified audit log | **CopilotInteraction** operation, AccessedResources with SensitivityLabelId, **XPIADetected** prompt-injection flag |
| **Information Barriers** | Block communication between segments | Not supported on agent embedded files |

### Classification

- **Sensitive information types (SITs):** regex patterns, keywords, checksums, confidence levels; hundreds built in, custom possible.
- **Exact data match (EDM):** hash and upload your own table so only genuine values match; the cure for false positives on account numbers.
- **Trainable classifiers:** machine learning on samples (custom needs about 50 documents); pre-trained for resumes, source code, contracts, harassment; for content with no fixed pattern.
- **Document fingerprinting:** match documents built from a template.

### Sensitivity labels

- A label can (1) **encrypt** with usage rights for users, groups or domains, (2) add **content markings** (header, footer, watermark), (3) apply **container settings** to groups, Teams and sites (privacy, guest access, external sharing, unmanaged devices), and serve as a **DLP condition**. Retention periods are **not** a sensitivity label function.
- **Publish with a label policy** or nobody sees the label in Office. Policies set default label, mandatory labeling, justification on downgrade. Classic scheme uses **+ Create a label**; the modern scheme (tenants created after October 1, 2025) uses **+ Create > Label**.
- **Auto-labeling:** client-side (recommend or apply while editing in Office) versus **service-side** (scan content at rest in SharePoint, OneDrive, Exchange; simulation mode first).
- **One sensitivity label per item**; sublabels count as one. An item can also carry one retention label.
- **Label priority** orders labels; **Copilot output inherits the highest-priority (most restrictive) label** of the sources it used, in Word, PowerPoint and Outlook and in Copilot Chat summaries. Copilot Studio shows a shield icon with the highest label used.
- **EXTRACT usage right:** on encrypted content Copilot needs **VIEW and EXTRACT**. Viewer-only permission means Copilot returns nothing from the file (it may still link to it). Copilot never elevates permissions.
- External auditors cannot open an encrypted file: **add their organization or accounts to the label's encryption permissions**; do not remove encryption or convert to PDF.
- Not returned by Copilot: **S/MIME** mail, **password-protected** documents (unless already open), content blocked by the PowerShell-only **BlockContentAnalysisServices** label setting. **Customer Key / BYOK** content **is** supported.

### Data loss prevention

- Locations include Exchange, SharePoint, OneDrive, Teams, **devices (Endpoint DLP)**, Power BI, Fabric, and **Microsoft 365 Copilot and Copilot Chat**.
- Actions: block, block with **override and business justification**, audit, notify with **policy tips**; **incident reports and alerts** must be switched on in the rule for admins to be notified (recipients, severity).
- **DLP for Copilot, the four pairs:** content contains **sensitivity label** → prevent Copilot from processing (excluded from the summary, may still be cited); content contains **SIT** → prevent **processing prompts** (no response at all); content contains **SIT** → prevent **web searches**; **email received from external users** (preview) → excluded from grounding to reduce prompt injection.
- You **cannot** put a sensitivity-label condition and a SIT condition in the **same rule**; make two rules in one policy. Calendar invites are not covered; Office apps evaluate at file open.
- **Endpoint DLP** needs devices onboarded (Purview or Defender for Endpoint): USB copy, print, upload to restricted domains, clipboard.
- DLP alerts are handled at Data Loss Prevention > **Alerts** (active, investigating, resolved, dismissed); after false positives, tune conditions, exceptions or confidence.
- **Power Platform DLP** (admin.powerplatform.microsoft.com > Policies > Data policies) is a **connector** policy for agents and flows, a different thing from Purview DLP.

> **Trap.** A sensitivity label alone stops Copilot only when its encryption denies the user EXTRACT. To keep permitted-but-sensitive files out of Copilot answers, use a **DLP policy for the Copilot location** with the label as the condition. To hide a whole site, use **restricted content discovery**.

### Retention and records

| | Retention **policy** | Retention **label** |
|---|---|---|
| Applied to | Whole locations, implicitly (mailboxes, sites, OneDrive, Groups, Teams chats and channels, **Copilot interactions**) | Individual items, explicitly or auto-applied |
| Extras | Adaptive or static scopes; preservation lock | Records, regulatory records, event-based retention, **disposition review** |

- **Data Lifecycle Management** = everyday retain and delete. **Records Management** = adds records (limited edits), **regulatory records** (immutable, no label removal even by admins), file plan, audited disposition. Both are separate solutions.
- **Principles of retention:** retention wins over deletion → longest retention wins → explicit wins over implicit → shortest deletion wins. Periods are never summed. Two policies, 5-year retain vs 1-year delete: kept **5 years**, then deleted.
- **Adaptive scopes** target users, groups or sites by attribute (department equals Finance) and follow changes automatically.
- Copilot prompts and responses are governed by a retention policy that targets **Copilot interactions**; a hold preserves them, deleting the mailbox destroys everything.
- Basic retention is in E3; auto-apply by classifier and disposition review need E5.
### Risk and discovery tools

**Insider Risk Management**

- Templates: data theft by departing users, data leaks, security policy violations, **risky AI usage** (risky prompts, sensitive responses, prompt injection, protected material), healthcare. **Triggering events** (HR resignation date, account deletion) activate scoring; indicators such as downloads, USB, cloud uploads, printing.
- **Pseudonymized by default** (AnonIS8-988); revealing identity is an audited step. Workflow: **policies → alerts → triage → investigate (case) → action** (notice, escalation to eDiscovery, ServiceNow). Do not disable the account before investigating.
- In June 2026 you can pick **which AI apps** an IRM policy monitors, reducing noise and pay-as-you-go audit charges.

**Communication Compliance**

- Detects harassment, threats, discrimination, regulatory violations (FINRA, MNPI) in Teams, Exchange, Viva Engage and **Copilot prompts and responses** using classifiers; template **Detect Microsoft Copilot interactions**; locations Microsoft Copilot experiences, Enterprise AI apps, Other AI apps.
- Reviewer actions: **resolve, tag, notify the user, escalate (including to eDiscovery), remove the Teams message**. No identity actions, no label application.
- Reviewers must hold a Communication Compliance role group **and** be listed in the policy's Reviewers field. No pay-as-you-go charge for Microsoft 365 Copilot data; non-Microsoft AI data needs pay-as-you-go.

**DSPM for AI (Data Security Posture Management for AI)**

- Inventory of AI apps and agents (**Copilot experiences and agents**, **Enterprise AI apps** such as Foundry, ChatGPT Enterprise, Claude Enterprise, **Other AI apps** detected in the browser), sensitive data in prompts and responses, risky users, **data risk assessments** of SharePoint sites, **one-click policies** that create DLP, IRM and Communication Compliance policies (Detect risky AI usage, Control unethical behavior in AI, Detect sensitive info shared in AI prompts in Edge, and more).
- The **default assessment runs automatically every week for the top 100 most-used SharePoint sites**; custom assessments can be added; allow **24 hours** after enabling one-click policies for data to show.
- Three entries exist in the portal: unified **DSPM** (GA May 2026), **DSPM for AI (classic)**, **Data Security Posture Management (classic)**. **Exam wording is DSPM for AI.** No retirement date for classic is published.
- **Roles:** Entra **Compliance Administrator**, Global Administrator, or the Purview Compliance Administrator role group. SharePoint, Teams and Billing administrators cannot open it.

**Compliance Manager**

- Assessments from **regulatory templates** (GDPR, ISO 27001, HIPAA, NIST, plus **AI regulations**: EU AI Act, NIST AI RMF, ISO/IEC 42001), controls (Microsoft-managed versus customer-managed), **improvement actions** with owners and evidence, a **compliance score**. DSPM for AI links to it for "guided assistance to AI regulations".
- It is not Secure Score (security posture) and not the Service Trust Portal (Microsoft's own audit reports).

**Explorers and search: which tool answers which question**

| Question | Tool | Path |
|---|---|---|
| **Where** is sensitive information and **what** labels are on it | **Data explorer** (the July 2026 objective's tool; the old one is **Content Explorer (classic)**) | Solutions > Information Protection > **Explorers > Data explorer**; classic under Data Lifecycle Management > Explorers |
| **What happened** to labeled content: label applied, changed, removed, DLP matches, external shares, over time | **Activity explorer** (about 50 filters; predefined sets such as Endpoint DLP activities) | Within a solution's Explorers, or DSPM > Discover > Activity explorer > AI activities |
| Files and emails containing a keyword for a legal matter, exported | **Content search inside eDiscovery** (a system-generated case named Content search) | Solutions > **eDiscovery > Content Search** |
| Preserve, collect, review and export for litigation | **eDiscovery case** with holds, searches, review sets (premium features by license) | Solutions > eDiscovery |
| A user's Copilot prompts and responses for six months | eDiscovery search of the **user's mailbox** with the **Copilot activity** condition | Solutions > eDiscovery |
| Prove which files Copilot touched and whether they were labeled | **Audit** search for **CopilotInteraction** with AccessedResources / SensitivityLabelId | Purview > Audit, or Defender portal > Audit |
| Adoption and usage for leadership | **Copilot usage report** or **Copilot Dashboard**, never the audit log | Microsoft 365 admin center; Viva Insights |

- **Unified eDiscovery** since August 31, 2025: classic Content search, Standard and Premium retired; one solution with standard and **premium** feature support (advanced indexing, review sets, OCR, threading, tagging, analytics, Security Copilot). Renames: collections → **statistics**, jobs → **processes**, the case is the organizing unit.
- To see prompt and response **content** in Activity explorer you need the **Content Explorer Content Viewer** role group. Data explorer has independent List viewer and Content viewer role groups.
- **Audit (Standard)** retains **180 days** (one year with E5, Purview Suite or the add-on); up to 10 concurrent search jobs, one unfiltered; Copilot interactions are logged with no extra configuration; audit for **non-Microsoft AI apps** is pay-as-you-go. Audit search works in the Purview portal **and** the Defender portal.

> **Traps.** "Audit logs are not intended for usage reporting" is Microsoft's own warning. Content explorer is classic; **Data explorer** is the answer. Content search is **inside eDiscovery**. DSPM for AI is opened by a **Compliance Administrator**, not a SharePoint administrator.

### Copilot data security and responsible AI

- **Copilot only sees what the user can see.** It retrieves through **Microsoft Graph** with the signed-in user's identity, so SharePoint permissions, mailbox rights, label usage rights, DLP and Conditional Access all apply; nothing is elevated; indexing never grants access. The real risk is the opposite: **overshared** sites (Everyone except external users, Anyone links) are reachable, so fix oversharing before rollout.
- **Architecture:** **Work IQ** is the intelligence layer (data layer = Microsoft Graph + **Copilot connectors**, formerly Graph connectors; context layer = the **semantic index**; skills and tools layer). The **semantic index** is a permission-aware lexical and semantic index over Graph and connector content. The **orchestrator** grounds the prompt, calls the LLM (models from several providers, inside the Microsoft 365 service boundary), then applies compliance checks. Synced connectors are semantically indexed; federated (MCP) connectors retrieve in real time with no data movement.
- Two users with identical permissions can get different answers because **Graph relevance signals** (recency, collaborators, meetings) differ. Permissions define what *can* be used; relevance defines what *is* used.
- **Data handling:** prompts, responses and Graph data are **not used to train the foundation models**; processing stays in the Microsoft 365 service boundary (EU Data Boundary where applicable); interactions are stored in the **user's mailbox** where audit, retention and eDiscovery apply.
- **Web grounding:** the tenant setting **Allow web search in Copilot** (Microsoft 365 admin center) turns web grounding on or off for Copilot and Researcher; there is no per-site allow list for standard Researcher.
- **Responsible AI principles (six):** fairness, reliability and safety, privacy and security, inclusiveness, **transparency** (citations and source links), **accountability** (human review before consequential actions). Grounding reduces but does not eliminate fabrication; human review remains a documented practice.
- **Auditing Copilot:** unified audit log records **CopilotInteraction** (RecordType values CopilotInteraction, ConnectedAIAppInteraction, AIAppInteraction), with **AccessedResources**, **SensitivityLabelId** and the **XPIADetected** cross-prompt-injection flag. Part of Audit Standard, no extra setup.

### SharePoint oversharing and SharePoint Advanced Management

**Data access governance (DAG) reports**: SharePoint admin center > **Reports > Data access governance**.

| Report group | Reports | Window |
|---|---|---|
| **Snapshot** | Site permissions across your organization (recommended), Sensitivity label applied to files, Site permissions for users | Point in time |
| **Activity** | **Sharing links** (Anyone, People in your organization, Specific people), **Shared with Everyone except external users (EEEU)** | Last **28 days** |

- Remediation from the report: **restricted access control**, **site access review** (delegate to site owners; track on My review requests; status stays pending until the owner finishes), Change history, Get AI insights.
- Needs SharePoint Administrator plus **SharePoint Advanced Management (SAM)**. **E5 without SAM** gets activity reports capped at **10,000 sites**, no snapshot reports, no remedial actions. Data must be pseudonymized-off in Reports settings for DAG to work.

**RAC versus RCD: the distinction Domain 2 loves**

| | **Restricted access control (RAC)** | **Restricted content discovery (RCD)** |
|---|---|---|
| Changes who can access the site | **Yes**: only members of the specified groups (up to **10** per site); prior permissions and links stop working; a user needs site permission **and** group membership | **No**: permissions untouched, users with access still open the site directly |
| Effect on Copilot and org-wide search | Blocked because access is gone | Hidden by concealment (unless the user recently interacted with the content) |
| Scope | Sites; also OneDrive via a tenant policy | SharePoint sites only, not OneDrive |
| Use when | Access itself is too broad | Permissions are correct or under review and you want the site out of Copilot temporarily |
| Where | Tenant: Policies > Access control > **Site-level access restriction**; per site: Active sites > site > Settings > **Restricted site access** | Active sites > site > **Settings** tab > **Restrict content discovery** On |

- **Restricted SharePoint Search (RSS)**, the allow-list of sites for search and Copilot, is **retiring**: new enablement blocked from **July 31, 2026**; Microsoft points to RCD instead. While RSS is on, SharePoint cannot be a knowledge source for declarative agents. Never recommend it.
- **SAM licensing:** the **Copilot-readiness subset** of SAM (RCD, sharing links and EEEU reports, permission state reports, site access reviews, change history, recent admin actions, sensitivity label report with E5) unlocks when **at least one user** holds a Copilot license. The full feature set (for example **restricted site creation**) needs the **SAM Plan 1** add-on, which **E7** bundles. Plain E3 does not include it; Entra P2 is unrelated.
- **Sharing defaults** (default link type Specific people, external sharing level) are at SharePoint admin center > **Policies > Sharing**; RCD also removes the Agent icon from a site and stops its content being added to other agents.

> **One line to memorize.** RAC changes **access**. RCD changes **discoverability**. RSS is retiring; answer RCD.
## Domain 3 · Basic administrative tasks for Copilot and agents (25–30%)

### Copilot, Copilot Chat, and agents

| | **Microsoft 365 Copilot** | **Agents** |
|---|---|---|
| Nature | Reactive, assistive, inside Word, Excel, PowerPoint, Outlook, Teams and Copilot Chat | Task-specific software that can run on schedules or triggers, chain steps, connect to systems |
| Data access | Only what the signed-in user can access | Can use service accounts or managed identities; needs approval and permission management |
| Customization | Tenant configuration, prompts | Fully customizable, lifecycle managed |
| Example | Draft an Outlook email from a meeting | Nightly invoice processing across systems |

- **Copilot Chat** two modes: **web-grounded** (free with an eligible subscription and a work account, enterprise data protection) and **work-grounded** over Microsoft Graph (**requires the Copilot license**). Unlicensed users can still use agents that ground on organizational data if a **pay-as-you-go billing policy** covers them.
- **Prebuilt Microsoft agents:** Prompt Coach, Writing Coach, Career Coach, Word/Excel/PowerPoint agents (use Anthropic models; the provider must be enabled), and the two advanced agents below. **Ready-made SharePoint site agents** are auto-created per site.

**Researcher versus Analyst**

| | **Researcher** | **Analyst** |
|---|---|---|
| Does | Deep multi-step research across Graph work data, Copilot connectors and the **Bing** index; cited reports | Chain-of-thought data analysis with Python; Microsoft says it is **better suited than Researcher for Excel** |
| Limits | **25 queries per user per month**; web use follows the tenant **Allow web search in Copilot** toggle; **Researcher with Computer Use** adds a Windows 365 virtual computer with its own three policies (Agents > Researcher > Computer use) | |
| Status and license | Both GA **June 2, 2025**; both need a **Microsoft 365 Copilot license**; no add-on; preinstalled and pre-pinned (Researcher cannot be unpinned by users) | |
| Governance | **Outside all agent settings**: they are core Copilot Chat **Tools** and stay available even when agents are disabled; the **only** control is a tenant-wide **Block** on each; **Edit users is disabled**, so no per-group scoping | |

### Agent taxonomy

| | **Declarative agents** | **Custom engine agents** |
|---|---|---|
| Hosting | In Microsoft 365, none needed | **Outside** Microsoft 365 |
| Model and orchestration | Copilot's orchestrator and models | Fully customizable (your model, your orchestration) |
| Proactive actions | **Not supported** (user-initiated only) | **Supported** |
| Compliance | Inherit Microsoft 365 compliance | Builder owns compliance and Responsible AI |
| Designed for | Individual use | Individual and group collaboration, inside and outside Microsoft 365 |

**Who builds what**

| Persona | Tool | Notes |
|---|---|---|
| Users | **Agent Builder in Microsoft 365 Copilot** (New agent in the Copilot app; the old name "Copilot Studio lite" is retired) or the **agent tool in SharePoint** | Needs a Copilot license, or pay-as-you-go enabled for the tenant |
| Makers | **Copilot Studio** | Connectors, actions, topics; governed in the Power Platform admin center; needs Copilot Studio license plus an environment role |
| Developers | **Microsoft 365 Agents SDK** / **Agents Toolkit** (formerly Teams Toolkit), Microsoft Foundry | Pro-code |

**Limits you can be asked**

| Tool | Knowledge and field limits |
|---|---|
| **Agent Builder** | **20 knowledge sources total**: up to 4 public URLs (two levels deep, no query strings), 100 SharePoint sites/folders/files, 1 SharePoint list, 50 OneDrive files, 5 Teams chat URLs, 20 embedded files; description 1,000 chars; instructions 8,000 chars; **no documented starter-prompt maximum**; **code interpreter and image generator are on by default**; Describe tab (natural language) and Configure tab stay in sync |
| **SharePoint agent** | **20 source items** total (sites, libraries, folders, files); **maximum 3 starter prompts**; welcome message; stored as an **.agent file** whose permissions govern access; created from New > Agent, the AI actions menu, or a file's context menu; needs Edit on the site |
| **Copilot Studio** | 500 knowledge sources, 8,000-character instructions, 500 files, 512 MB per file, 100 skills, 1,000 topics, 25 SharePoint site URLs with generative orchestration |

- **Knowledge source licensing:** code interpreter, image generator, web search and scoped web search need **no license and no metering**; SharePoint, OneDrive, embedded files, Copilot connectors and Dataverse need a **Copilot license or metered usage**; **email, People, Teams messages and meetings need the Copilot license itself**.
- Embedded files live in tenant-owned **SharePoint Embedded** containers (app name Declarative Agent); do not delete them. **Information barriers are not supported** on embedded files. "Only use specified sources" prioritizes sources but cannot fully block general knowledge; use Copilot Studio for stricter control.
- **Microsoft Agent 365** (GA May 1, 2026, per user, in E7) is the control plane for agents wherever they were built: identity (**Entra Agent ID**), registry, approvals, observability. **Copilot Tuning** is an early-access preview, not GA. **Frontier** is the opt-in early-access release channel: Copilot > Settings > Copilot Frontier, default **No access**, options All users or Specific users; three-tier release model Frontier / Standard / Deferred; Frontier never overrides Agents settings.

### Licensing models and billing

| Model | Who | How billed | Where |
|---|---|---|---|
| **Monthly per-user license** | Heavy daily users | Fixed per seat (about $30 enterprise; Copilot Business about $21 list) | Billing > Licenses, group-based licensing |
| **Pay-as-you-go** | Unlicensed occasional users, agents | **$0.01 per Copilot Credit** billed to an **Azure subscription**; the Azure meter is still named **Copilot Studio** | **Copilot > Billing & usage** (up to **50** billing policies) |
| **Copilot credit policy** | Prepaid credits, no Azure subscription | Prepaid packs | Up to **10** per tenant; **Copilot Chat only** |
| **Copilot Studio capacity pack** | Predictable agent capacity | **$200 per pack per month for 25,000 credits**, consumed **first**, before pay-as-you-go; overage enforced at **125%** | Power Platform / Copilot Studio |
| **Copilot Credit Pre-Purchase Plan** | Committed annual spend | Copilot Credit Commit Units, one-year term, **no cancellations or exchanges** | Azure portal > Reservations |
| **SharePoint agents** | Copilot-licensed users pay nothing extra; unlicensed users need pay-as-you-go | **12 credits per complex prompt** (generative answer 2 + tenant graph grounding 10) | Up to **10** SharePoint agent billing policies, one security group each |

- **Copilot Credit consumption:** classic answer 1, generative answer 2, agent action 5, tenant graph grounding 10, agent flow actions 13 per 100. Licensed users incur **no charge** for these in employee-facing scenarios. Never say one message equals one credit.
- **Pay-as-you-go prerequisites:** an **Azure subscription and resource group in the same tenant**, **Owner or Contributor** on both, and the **Billing Administrator, AI Administrator or Global Administrator** role; at least one SharePoint license in the tenant.
- **Two-step setup:** (1) **Billing policies** tab > Add a billing policy (name, subscription, resource group, region, All users or a group, optional budget); (2) **Pay-as-you-go services** tab > connect the policy to a service (**Microsoft 365 Copilot Chat**, **SharePoint agents**, or the Copilot Retrieval API preview). Skip step 2 and pay-as-you-go stays disabled.
- **Budgets notify only.** Default alert threshold 100%, alerts can take 24 hours, usage continues past the budget, users are never charged personally.
- **Wrong places:** Billing > Pay-as-you-go (that page is for Microsoft 365 Backup, SharePoint storage and High Volume Email and only links onward); Org settings > Pay-as-you-go services is **legacy** (Disconnect previous billing before linking a new policy).
- **Hybrid answer pattern:** licenses for the 100 daily analysts, a pay-as-you-go policy for the 600 occasional users. There is no such thing as an individual pay-as-you-go license, and E5 does not include Copilot; E7 does.

> **Traps.** No 300 minimum; 300 is a maximum on SMB SKUs. Copilot Business has the **same capabilities** as the enterprise add-on. Three limits, three things: **50** pay-as-you-go policies, **10** credit policies, **10** SharePoint agent policies.
### Administrative tasks for Copilot

**Assign licenses**

- Per user: Users > Active users > user > **Licenses and apps** > Microsoft 365 Copilot > Save. Product-first: Billing > Licenses > Microsoft 365 Copilot > Assign licenses (20 users or groups at a time). Groups: Groups > Active groups > group > Licenses. Bulk: Microsoft Graph PowerShell SDK.
- Allow **up to 24 hours** and an app restart. **Guests and cross-tenant users cannot be licensed.** Education tenants find Copilot under A3/A5 Extra Features for faculty.

**Monitor usage and adoption**

| Need | Tool | Path and facts |
|---|---|---|
| Enabled versus active users, per-app usage, last activity, CSV export | **Microsoft 365 Copilot usage report** | Reports > Usage > Microsoft 365 Copilot > **Copilot** > Readiness tab (first) and **Usage** tab; data within **48 hours** of end of day UTC; readiness within 72 hours |
| Credits consumed per user, agent, billing policy, agent-user pair | **Credits report** | Reports > Usage > Microsoft 365 Copilot > **Credits**; 30 days of history, no data before May 3, 2025, alerts when a user passes **2,000 credits** |
| Agent usage | **Agents report** | Reports > Usage > Microsoft 365 Copilot > **Agents**; the original report (GA, up to 72 hours latency, excludes SharePoint and Microsoft agents) and the new Agents usage report (preview, within an hour, includes declarative, SharePoint and custom engine agents) |
| Impact, assisted hours, sentiment, trends by department for executives | **Copilot Dashboard** in **Viva Insights** (Teams or web app) | Not opened from the admin center; an **AI Administrator** enables and delegates access; the old admin-center enable control was removed, access follows the Viva Insights web app setting; privacy: minimum group size and exclusions |
| Compliance evidence | Purview audit log | Never for usage reporting |

- **Copilot Analytics** is the umbrella: admin center readiness and adoption report, **Copilot Dashboard**, **Agent Dashboard**, **Consumption Dashboard**, ready-to-use reports, advanced Power BI reporting through Viva Insights.
- Reporting roles: **AI Administrator** (Copilot reports in the admin center), Global Administrator assigns **Insights Analyst** (builds Power BI templates) and **Insights Administrator** (Analyst Workbench settings), **Audit Reader** (audit search), **Copilot Studio Author** (per-agent analytics), Reports Reader and Usage Summary Reports Reader (view, limited detail).

**Manage prompts**: **save** (name and description), **share** with users or groups, **schedule** to run at set times with output delivered to the user, **delete** stale prompts; the four verbs the objective names.

### Administrative tasks for agents

**The Agents node** (top level in the Microsoft 365 admin center, not under Copilot; the legacy Copilot > Settings > Data access > Agents page still exists with a Manage all agents link):

| Sub-page | What is there |
|---|---|
| **Agents > Overview** | Hero metrics (agent registry count, active users last 30 days, agent run-time, registry sync) and governance cards: **Pending requests**, **Agents at risk**, **Agents without owners**, **Agents with exceptions**; risk types such as shadow agent, no owner, excessive permissions (critical), prompt injection, sensitive data access (high) |
| **Agents > All agents > Registry** | Inventory with publisher types **Microsoft agents, External partner-built, Published by your org, Shared by creator**; filters; export; add agent (manifest ZIP); **Manage pinned agents** |
| **Agents > All agents > Requests** | The **approval queue** with states **Pending review** (new, button **Publish to store**), **Pending update** (new version; users stay on the previous version; button **Update in store**), **Pending activate** (template agent to instantiate), plus **Allow user to install** for a blocked Microsoft agent (Unblock first, then Approve or Reject); **Reject submission** from the ellipsis |
| **Agents > Tools > Requests** | **MCP server and tool approvals**, a separate queue |
| **Agents > Settings** | Five areas: **Agent management rules** (Install Microsoft agents; Reassign ownerless Agent Builder agents to the manager), **Allowed agent types** (built by Microsoft, by your org, by external publishers; Microsoft agents stay **visible** when disabled, users just cannot install them), **Templates** (security or policy templates), **Sharing** (All, No users, Specific; governs Agent Builder agents only, and under No users people can still share with specific individuals), **User access** (All users default, No users, Specific users/groups) |

- **Who can approve:** **AI Administrator** and **Global Administrator** only. Global Reader, AI Reader, Security Administrator, Reports Reader can view but not act.
- **Approval workflow for Pending review:** open the request, review **capabilities, data sources, security and permissions, custom actions**, **Publish to store**, choose who can install, optionally who gets it preinstalled, pick a policy template, **review permissions** and grant admin consent if appropriate, Publish.
- **Availability and installation are independent** on the Users tab: **Installed for** (Just me, Entire organization, Specific users) versus **Available to** (No users, All users, Specific users). Installing to the entire organization installs regardless of availability.
- **Agent actions:** Install, Uninstall, **Block**, Update in store, **Pin for users** (maximum **3** admin pins, up to **6 hours** to appear, agent must be deployed and not blocked; users cannot unpin admin pins). **Connected agents:** up to **10** per agent. The details pane can show up to ten tabs (Details, Users, Data & Tools, Security, Permissions, Certification, **Activity**, Agent instances, Connected Agents, Computer use); the **Risks** column, Security tab and Activity tab need **E7 or Agent 365**.

| Action | Effect |
|---|---|
| **Block** | Stops all use in the tenant **and removes the agent from users who already installed it** |
| **Uninstall / Remove** | Takes it out of the inventory; it can be re-acquired from the store; admins can only remove shared and custom LOB agents |

- **Blocking scope:** blocking an **Agent Builder or Copilot Studio** agent affects Copilot **and** Outlook and Teams; blocking a **SharePoint or Microsoft Foundry** agent affects **Copilot Chat only**. For the Teams app surface, the **Teams admin center > Teams apps > Manage apps** is the control.
- **Lifecycle:** creation → approval and deployment → maintenance → block → removal; updates that expand permissions arrive as **Pending update** and must be reviewed, users keep the prior version; communicate retirement 30 days ahead. Policy-based lifecycle rules went GA June 2, 2026.
- **Per-agent Activity tab:** active users, **sessions** (a new session after **30 minutes** of inactivity), exceptions, run-time; supported for Agent Builder, SharePoint and Agents Toolkit agents.
- **Agent instances:** "AI teammate" template agents are instantiated with their own Entra agent identity, license, mailbox, OneDrive and Teams presence; instance actions are Block, Unblock, Delete; activation is a separate workflow from publishing.

**Power Platform admin center division of labor**

| Built with | Managed primarily in | Notes |
|---|---|---|
| Agent Builder, SharePoint | **Microsoft 365 admin center** | Registry, requests, settings, usage |
| **Copilot Studio** | **Power Platform admin center** (DLP connector policies, **Editor** and **Viewer** sharing roles, sharing limits, environment groups, Copilot hub, Power Platform inventory, Advisor) | **Still needs Microsoft 365 admin center approval** to reach the tenant-wide Copilot or Teams catalog; Copilot Studio agents get an Agent ID and registry entry automatically |

- **Environment roles** (Power Platform admin center > Environments > environment > Settings > Users + permissions): **Environment Maker** creates and edits agents, **Environment Admin** full control, **Basic User** only interacts with shared agents. A Copilot Studio license without a maker role cannot build. **End users** of a published agent need neither a Copilot Studio license nor an environment role, only access to the published endpoint (consumption may still be metered).
- Troubleshooting permission errors: Agents > All agents > agent > **Permissions** tab ("Settings > Integrated apps" is the retired surface). Copilot not appearing: check the license, the app version and channel, service health.

## Numbers to know

| Fact | Value |
|---|---|
| Passing score / time | 700 / 45 minutes |
| Copilot license propagation | Up to 24 hours |
| Copilot usage report latency | Within 48 hours (readiness 72 hours) |
| Credits report | 30 days of history; alert above 2,000 credits per user |
| Pay-as-you-go rate | $0.01 per Copilot Credit; Azure meter named Copilot Studio |
| Credits per action | Classic 1, generative 2, agent action 5, tenant graph grounding 10; SharePoint agent prompt 12 |
| Capacity pack | $200 for 25,000 credits per month, consumed first; overage at 125% |
| Policy limits | 50 pay-as-you-go billing policies, 10 Copilot credit policies, 10 SharePoint agent billing policies |
| Budget behavior | Notification only; default 100%; alerts up to 24 hours |
| Researcher | 25 queries per user per month |
| Admin pins | 3, up to 6 hours to appear |
| Connected agents | 10 per agent |
| RAC groups | 10 per site |
| Agent session timeout | 30 minutes of inactivity |
| Audit (Standard) retention | 180 days; 1 year with E5 or add-on |
| Audit search jobs | 10 concurrent, 1 unfiltered; completed jobs kept 30 days |
| DAG activity reports | Last 28 days; 10,000 sites without SAM |
| DSPM for AI default assessment | Top 100 SharePoint sites, weekly; 24 hours for one-click policy data |
| Copilot Business seats | 300 maximum; no minimum anywhere |
| Agent Builder knowledge | 20 sources (4 URLs, 100 SharePoint, 1 list, 50 OneDrive, 5 Teams chats, 20 files) |
| SharePoint agent | 20 source items, 3 starter prompts |
| Copilot Studio | 500 knowledge sources, 8,000-character instructions |
| Trainable classifier samples | About 50 |
| Group-based licensing | Entra ID P1 or Office 365 E3+; no nested groups |
| RSS retirement | New enablement blocked from July 31, 2026 |
| E7 and Agent 365 GA | May 1, 2026 |
| Researcher and Analyst GA | June 2, 2025 |
| PIM audit history | 30 days |
| Identity Secure Score refresh | Every 24 hours |

## If the question says… pick…

| Scenario wording | Answer |
|---|---|
| Configure labels, DLP, retention, eDiscovery | purview.microsoft.com (never the retired compliance portal) |
| Find where sensitive information lives | **Data explorer** |
| Who changed a label, DLP matches over time | Activity explorer |
| AI-specific oversharing and risky prompts | **DSPM for AI** |
| Keyword search and export for legal, no hold | **Content search inside eDiscovery** |
| A user's Copilot prompts for a legal case | eDiscovery on the mailbox with the Copilot activity condition |
| Prove which files Copilot referenced | Audit log, CopilotInteraction |
| Report adoption to leadership | Copilot usage report or Copilot Dashboard, not audit logs |
| Who manages Copilot compliance policies | Compliance Administrator |
| Who approves an agent request | AI Administrator (or Global Administrator) |
| Who opens Copilot reports and the dashboard | AI Administrator |
| Hide a site from Copilot while permissions are reviewed | Restricted content discovery |
| Restrict who can open a site at all | Restricted access control |
| Recommended oversharing control instead of Restricted SharePoint Search | RCD |
| Site owners review their own oversharing | Site access reviews from the DAG report |
| Change the default sharing link to Specific people | SharePoint admin center > Policies > Sharing |
| Keep labeled files out of Copilot answers for permitted users | DLP policy, Copilot location, sensitivity label condition |
| Copilot returns nothing from a file the user can open | Label encryption grants VIEW but not EXTRACT |
| Label on a Copilot-generated document | Highest-priority source label |
| Copilot must not use the web | Turn off Allow web search in Copilot |
| Delete Copilot prompts after 90 days | Retention policy for Copilot interactions |
| Harassing Copilot prompts reviewed by a person | Communication Compliance, Detect Microsoft Copilot interactions |
| Repeated attempts to extract confidential content via prompts | Insider Risk Management, Risky AI usage |
| EU AI Act readiness | Compliance Manager AI templates |
| Disable Researcher or Analyst | Block each tenant-wide; not possible per group |
| Which agent for Excel-heavy analysis | Analyst |
| Agent with its own model that acts proactively | Custom engine agent |
| Assistant scoped to one library, built by a site owner | SharePoint agent (.agent file) |
| Pilot early-access features | Copilot > Settings > Copilot Frontier (default No access) |
| Copilot missing 30 minutes after assignment | Wait up to 24 hours, restart the app |
| Occasional users without seats | Pay-as-you-go billing policy |
| Billing policy exists but users still blocked | Connect it on the Pay-as-you-go services tab |
| Budget reached | Email alerts only, usage continues |
| Create billing policies | Copilot > Billing & usage |
| Credits per user and agent | Reports > Usage > Microsoft 365 Copilot > Credits |
| Run a prompt automatically every Monday | Schedule the prompt |
| Only Finance may use agents | Agents > Settings > User access > Specific users/groups |
| Where a submitted agent waits | Agents > All agents > Requests |
| Make an agent unusable immediately, even where installed | Block |
| Updated agent asks for more permissions | Review the Pending update; users keep the old version |
| Copilot Studio agent performance detail | Power Platform admin center |
| Power user with a Copilot Studio license cannot build | Assign Environment Maker in the environment |
| Block a third-party agent in Teams specifically | Teams admin center > Manage apps |
| Copilot for a guest user | Not possible |
| Enterprise SKU that includes Copilot | Microsoft 365 E7 |
| Minimum seats to buy Copilot | None |

## Say this, not that

| Retired or wrong | Current |
|---|---|
| Microsoft 365 Defender, protection.office.com | **Microsoft Defender XDR** in the **Microsoft Defender portal** (security.microsoft.com) |
| Purview compliance portal, compliance.microsoft.com | **Microsoft Purview portal** (purview.microsoft.com) |
| Azure AD, AAD | **Microsoft Entra ID** |
| Exchange Online admin center, distribution lists | **Exchange admin center**, **distribution groups** (the tab says Distribution list) |
| SharePoint in Microsoft 365 admin center | **SharePoint admin center** |
| Restricted site access | **Restricted access control** (the portal says Site-level access restriction) |
| Content explorer | **Data explorer**; the old tool is Content Explorer (classic) |
| Standalone Content search | **Content search in eDiscovery** |
| eDiscovery (Standard) / (Premium) | **Unified eDiscovery** with premium features |
| Copilot Studio lite | **Agent Builder in Microsoft 365 Copilot** |
| Teams Toolkit | **Microsoft 365 Agents Toolkit** |
| Microsoft Graph connectors | **Microsoft 365 Copilot connectors** |
| Message packs, per-message billing | **Copilot Credits**, **Copilot Studio capacity packs** |
| Integrated apps | **Agents** section of the Copilot Control System |
| Copilot > Agents > Requested agents | **Agents > All agents > Requests** |
| Copilot with commercial data protection, Copilot for Microsoft 365 | **Microsoft 365 Copilot Chat (with enterprise data protection)**, **Microsoft 365 Copilot** |
| Agent 365 preview | **Generally available** (May 1, 2026) |
| 300-seat minimum | **No minimum**; 300 maximum on SMB SKUs |
| Audit 90 days | **180 days** |

## The last 30 minutes: read twice

- Least privilege always: **AI Administrator** for Copilot and agents, **Compliance Administrator** for Purview and DSPM, Global Administrator only in emergencies.
- **purview.microsoft.com**; the compliance portal is retired.
- **Data explorer** finds sensitive content; **Activity explorer** shows what happened; **Content search lives inside eDiscovery**.
- Copilot sees only what the user sees; Graph plus semantic index; no model training on your data; interactions live in the user's mailbox.
- Encrypted content needs **VIEW and EXTRACT**; output inherits the **highest-priority label**; DLP has a **Copilot location**; label and SIT conditions cannot share one rule.
- Retention wins, longest wins; Copilot interactions have their own retention location; regulatory records are immutable.
- **RAC changes access; RCD changes discoverability; RSS is retiring (July 31, 2026).** DAG reports: SharePoint admin center > Reports > Data access governance; activity window 28 days.
- SAM: Copilot license unlocks the readiness subset; full SAM needs Plan 1 or E7.
- DSPM for AI: weekly top-100 assessment, one-click policies, Compliance Administrator.
- IRM Risky AI usage, pseudonymized; Communication Compliance Detect Microsoft Copilot interactions; audit **CopilotInteraction** with XPIADetected; audit is **not** for usage reporting.
- Researcher and Analyst: GA, license required, **outside agent settings**, tenant-wide Block only, Analyst for Excel, Researcher 25 queries a month.
- Declarative (no hosting, no proactive) vs custom engine (own model, proactive, builder owns compliance).
- Agent Builder 20 sources; SharePoint agent 20 items and 3 starter prompts; code interpreter and image generator on by default; email and Teams knowledge need the license itself.
- Copilot Chat web free, work-grounded needs a license; **no 300 minimum**; Copilot Business = same features, 300 max; **E7 includes Copilot**; Agent 365 GA per user.
- **$0.01 per Copilot Credit**; SharePoint agent prompt = 12; packs $200 for 25,000 consumed first; 125% overage; 50 / 10 / 10 policy limits.
- Pay-as-you-go: Azure subscription + resource group, Owner or Contributor, eligible admin role; **two steps** (policy, then connect a service); **budgets notify only**; path **Copilot > Billing & usage**.
- License propagation 24 hours; guests cannot be licensed; usage report 48 hours; Credits report 2,000-credit alert; Copilot Dashboard lives in **Viva Insights**.
- Prompts: save, share, schedule, delete.
- **Agents > All agents > Requests**: Pending review (Publish to store), Pending update (Update in store, users stay on the old version), Pending activate; MCP tools have their own queue; only AI Administrator and Global Administrator approve.
- Agents > Settings: management rules, allowed agent types (Microsoft agents stay visible), templates, sharing (Agent Builder only), user access.
- **Block** removes from installs; **Remove** only takes it out of inventory; Agent Builder and Copilot Studio blocks reach Outlook and Teams, SharePoint and Foundry blocks reach Copilot Chat only.
- Installed for versus Available to are independent; 3 pins, 6 hours; 10 connected agents; Activity tab needs E7 or Agent 365.
- Copilot Studio agents are governed in the **Power Platform admin center** but still need admin center approval; Environment Maker to build; end users need nothing but the endpoint.
