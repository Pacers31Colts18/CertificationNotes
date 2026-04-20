# MS-102 Study Projects

5 hands-on projects mapped to the MS-102 exam skill domains.

---

## Quick Reference: Domain → Project Mapping

| Domain | Weight | Project |
|---|---|---|
| M365 Tenant Management | 10–15% | Project 1 |
| Entra Identity & Access | 25–30% | Projects 2 & 3 |
| Defender XDR Security | 35–40% | Project 4 |
| Purview Compliance | 15–20% | Project 5 |

> **Start with Project 1** to get your dev tenant set up — everything else builds on it. The M365 Developer Program tenant gives you 25 E5 licenses free, which unlocks Defender for Office 365 P2, Purview, and PIM needed for all five projects.

---

## Project 1 — Build a Production-Ready M365 Tenant from Scratch

**Skill Domain:** Deploy and manage a Microsoft 365 tenant (10–15%)

**Description:** Simulate onboarding a fictional company into Microsoft 365 from day one. You'll configure the tenant, domain, admin roles, and client connectivity — the foundational layer everything else depends on.

### Steps

1. Sign up for an M365 Developer tenant (free via [Microsoft 365 Developer Program](https://developer.microsoft.com/en-us/microsoft-365/dev-program))
2. Add and verify a custom domain using DNS TXT records
3. Configure organizational profile settings (locale, privacy, theme)
4. Create a role taxonomy: assign Global Admin, User Admin, Security Admin, Compliance Admin to separate test accounts
5. Use the Microsoft 365 Admin Center to configure service health alerts and message center subscriptions
6. Deploy Microsoft 365 Apps for enterprise using Group Policy and the Office Deployment Tool (ODT) with a custom `config.xml`
7. Configure Outlook and Teams client connectivity — validate autodiscover and DNS SRV records
8. Document the tenant baseline with exported config using PowerShell (`Get-MgOrganization`, `Get-MgDomain`)

### Supplemental Learning

- Udemy course: *Section on Tenant Configuration and Admin Center*
- Microsoft Learn: [Configure your Microsoft 365 tenant](https://learn.microsoft.com/en-us/training/modules/configure-microsoft-365-tenant/)
- YouTube: "Microsoft 365 Admin Center Full Tour" by Andy Malone MVP

---

## Project 2 — Implement Hybrid Identity with Microsoft Entra Connect

**Skill Domain:** Implement and manage Microsoft Entra identity and access (25–30%)

**Description:** Stand up an on-premises Active Directory environment and synchronize it to Microsoft Entra ID using Connect Sync and Connect Cloud Sync. This is the most heavily weighted domain and identity sync is a core real-world skill.

### Steps

1. Spin up a Windows Server VM (Hyper-V, VirtualBox, or Azure free tier) and promote it to Domain Controller
2. Create test OUs, users, and groups in on-prem AD
3. Install and configure **Microsoft Entra Connect Sync** — use Express Settings first, then redo with Custom for granular OU filtering
4. Verify sync in Entra ID admin portal; troubleshoot with `Start-ADSyncSyncCycle` and the Synchronization Service Manager
5. Install **Entra Connect Cloud Sync** agent on a second server and compare the two approaches
6. Configure **Password Hash Synchronization** and test a password change flowing from on-prem to cloud
7. Enable and test **Self-Service Password Reset (SSPR)** with writeback
8. Implement **Seamless Single Sign-On** for domain-joined machines

### Supplemental Learning

- Udemy course: *Module on Identity Synchronization*
- Microsoft Learn: [Implement and manage hybrid identity](https://learn.microsoft.com/en-us/training/paths/implement-manage-hybrid-identity/)
- Docs: [Microsoft Entra Connect Sync vs Cloud Sync comparison](https://learn.microsoft.com/en-us/entra/identity/hybrid/cloud-sync/what-is-cloud-sync)
- YouTube: "Microsoft Entra Connect Deep Dive" by John Savill

---

## Project 3 — Zero Trust Identity: Conditional Access, MFA & PIM

**Skill Domain:** Implement and manage Microsoft Entra identity and access (25–30%)

**Description:** Implement a Zero Trust identity model by designing and enforcing Conditional Access policies, MFA, and privileged identity governance. This is consistently the highest-tested topic in this domain.

### Steps

1. Enable **Per-user MFA** for a test account, then migrate to **Conditional Access-based MFA** (understand the difference)
2. Build a Conditional Access policy library:
   - Require MFA for all users except a break-glass account
   - Block legacy authentication protocols
   - Require compliant device for access to Exchange Online
   - Block access from high-risk sign-in locations
3. Use **Sign-in logs** and **What If tool** in Entra ID to test and validate each policy without locking yourself out
4. Configure **Identity Protection** — set risk-based Conditional Access policies for medium/high user risk and sign-in risk
5. Enable **Privileged Identity Management (PIM)** — configure eligible assignments for Global Admin with approval workflows and time-bound access
6. Conduct a simulated **Access Review** for a security group
7. Configure **Microsoft Entra ID Protection** alerts and review the risky users dashboard

### Supplemental Learning

- Udemy course: *Conditional Access and Identity Protection sections*
- Microsoft Learn: [Implement Conditional Access](https://learn.microsoft.com/en-us/training/modules/implement-azure-active-directory-conditional-access-policies/)
- Microsoft Learn: [Plan a Privileged Identity Management deployment](https://learn.microsoft.com/en-us/entra/id-governance/privileged-identity-management/pim-deployment-plan)
- YouTube: "Conditional Access Masterclass" by Peter Rising MVP

---

## Project 4 — Defend the Tenant with Microsoft Defender XDR

**Skill Domain:** Manage security and threats by using Microsoft Defender XDR (35–40%)

**Description:** This is the highest-weighted domain. Configure the full Defender XDR stack — Defender for Office 365, Defender for Identity, Defender for Cloud Apps, and the unified security portal. Run a simulated attack and investigate the incident.

### Steps

1. Configure **Exchange Online Protection (EOP)** policies: anti-spam, anti-malware, connection filters
2. Enable **Defender for Office 365 Plan 1**: configure Safe Links and Safe Attachments policies (Block, Monitor, Dynamic Delivery modes)
3. Run the **Attack Simulator** in the Defender portal — run a credential harvest phishing simulation and review who clicked
4. Set up **Microsoft Defender for Identity** sensor on your Domain Controller VM (from Project 2), connect to the cloud portal
5. Enable **Microsoft Defender for Cloud Apps** — connect Microsoft 365 as an app, configure an anomaly detection policy, review the Cloud Discovery dashboard
6. In the **Microsoft Defender XDR portal** (security.microsoft.com), review:
   - Secure Score — implement 3–5 recommended improvement actions
   - Incidents queue — understand alert correlation into incidents
   - Threat hunting using **Advanced Hunting** with KQL queries
7. Configure **Microsoft Secure Score** baseline and track it across your other projects
8. Set up email notifications for high-severity alerts

### Supplemental Learning

- Udemy course: *Microsoft 365 Defender and Security Services modules*
- Microsoft Learn: [Defend against threats with Microsoft Defender XDR](https://learn.microsoft.com/en-us/training/paths/sc-200-mitigate-threats-using-microsoft-365-defender/)
- YouTube: "Microsoft Defender for Office 365 Setup" by Andy Malone MVP
- Blog: [Microsoft Tech Community Security blog](https://techcommunity.microsoft.com/t5/security-compliance-and-identity/bg-p/MicrosoftSecurityandCompliance)
- KQL reference: [Advanced Hunting schema reference](https://learn.microsoft.com/en-us/defender-xdr/advanced-hunting-schema-tables)

---

## Project 5 — Build a Compliance Framework with Microsoft Purview

**Skill Domain:** Manage compliance by using Microsoft Purview (15–20%)

**Description:** Implement a realistic compliance posture using Microsoft Purview — covering data classification, retention, DLP, and insider risk. Simulate a compliance investigation end-to-end.

### Steps

1. In the **Microsoft Purview portal** (purview.microsoft.com), explore the Compliance Manager dashboard — review your compliance score and assigned improvement actions
2. Create a **Sensitivity Label** taxonomy (Public → Internal → Confidential → Highly Confidential), configure encryption and content marking for the top two tiers, publish via label policy
3. Configure **Data Loss Prevention (DLP)** policies:
   - Detect US SSNs or credit card numbers in Exchange, SharePoint, and Teams
   - Set policy tip (warn), then escalate to block with override
4. Create **Retention Labels and Policies**:
   - Apply a 7-year retention to Exchange mailboxes
   - Apply a delete-after-3-years policy to a SharePoint site
5. Enable **Communication Compliance** — create a policy that monitors for offensive language in Teams messages
6. Configure an **Insider Risk Management** policy using the "Data theft by departing users" template
7. Place a user mailbox on **Litigation Hold** and perform a **Content Search** / **eDiscovery** case to export results
8. Review the **Audit Log** for a simulated suspicious activity (e.g., mass file download from SharePoint)

### Supplemental Learning

- Udemy course: *Data Governance and Compliance modules*
- Microsoft Learn: [Implement data governance and compliance in Microsoft Purview](https://learn.microsoft.com/en-us/training/paths/purview-implement-data-governance/)
- Microsoft Learn: [Manage compliance in Microsoft 365](https://learn.microsoft.com/en-us/training/paths/manage-compliance-microsoft-365/)
- YouTube: "Microsoft Purview Compliance Full Demo" by John Savill or Inside Cloud and Security channel
