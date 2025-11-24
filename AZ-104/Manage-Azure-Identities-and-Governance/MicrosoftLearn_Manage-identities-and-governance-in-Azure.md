# Microsoft Learn - Manage Identities and Governance in Azure
## Understand Microsoft Entra ID
## Examine Microsoft Entra ID
- Multi-tenant by design
## Compare Entra ID and AD DS
- Entra ID Characteristics:
  - Primarily an identity solution
  - Designed for port 80/443 communication
  - Multi-tenant directory service
  - Flat structure
  - No LDAP, Rest API over HTTP/HTTPS
  - No Kerberos Auth
    - SAML
    - WS-Federation
    - Open ID Connect - Authorization
    - Oath - Authorization
  - Includes federation services
    - example: Google/Meta
## Compare P1 and P2 Plans
**P1 Features**
- Self service group management
- Advanced security reports and alerts
- MFA
- MIM licensing
- SLA - 99.9%
- Password reset with writeback
- Cloud app discovery feature of Entra ID
- CA based on device, group, location
- Microsoft Entra ID Connect Health
**P2 Features**
- Entra ID Protection
- PIM
## Examine Microsoft Entra Domain Services
**Limitations**
- Only the base computer AD object is supported
- Cant extend schema
- OU structure is flat only
- Built-in GPO exists for computer/user accounts
- Can't target OUs with built-in GPO
- No WMI or Security Group filtering