## Configure your Microsoft 365 Experience
- When you purchase a M365 subscriptiion, Microsoft creates a Microsoft Entra tenant.

## Configure your M365 Organizational Profile
- Must be GA to update your company's organizational profile.
- Update theme

## Examine the use of roles in the M365 permission model.
### Roles
- Built-in
- Custom
### Scopes
- Limit the range or extent of a role.
- Directory scopes
- Management scopes
  - Based on service or app in M365.
### Assignments
- Direct
- Indirect

## Types and Categories of Roles in M365
- Global Roles
- Service Specific Roles
- Fearture Specific Roles
  - Administrative roles
  - Reader roles
  - Application roles
  
## Manage roles across the M365 Ecosystem
- M365 Admin Center is the main portal for managing and configuring the M365 environment.
- Some M365 services have their own portals and admin centers with their own set of roles.
### App
- M365
  - Built in and custom
  - M365 Admin Center
- Entra ID
  - Data governance roles
  - Entra ID portal
- Defender XDR
  - Security roles
  - Defender portal
- Purview
  - Data catalog roles
  - Purview portal
### M365 Admin Center
- User and group management
- Azure RBAC
- Service specific permission management
- Application and app permissions
### Microsoft Entra ID Portal
### Defender Portal
- Threat investigation
- Incident management
- Advanced threat hunting
- Threat analytics
- Integration with M365
### Purview Portal
- Hub to help orgs meet their regulatory and compliance requirements
- Compliance management
- Data protection
- Risk assessment and insights
- E-discovery and legal hold
- Compliance reporting and auditing
- Collaboration and training
## Explore administrator roles in M365
- M365 uses a permission model called Azure RBAC.
### Security guidelines for assigning roles.
- Only establish 2-4 Global Administrators
- Assign the least permissive role.
- Require MFA for admins.
## Examine best practices when configuring admin roles
1. Least Privilege
  - Specific set of permissions
  - Over a scope
  - For a specific time period
2. Use PIM to grant just in time access
3. MFA for all your admin accounts.
4. Configure recurring access reviews to revoke unneeded permissions over time.
5. Limit GA to less than 5
  - Two break glass accounts
6. Use groups for Entra role assignments and delegate the role assignment.
7. Use cloud native accounts for Microsoft Entra roles.
## Assign admin roles to users in M365
## Delegate admin roles to partners
## Implement role groups in M365
- Simplifiies role assignment process
- Improves security and compliance posture
- Increasing productivity and collaboration
- Assigned groups only
  - isAssignableRole = True
  - Can't uncheck it
  - Can't make existing group a role group
**P1 License**
## Manage permissions using administrative units in Microsoft Entra ID
- Users
- Groups
- Devices
**P1 License**
- Can't nest AUs
- Scoped user account, admins can't create or delete users.
- Adding groups doesn't put members in scope.
## Manage SharePoint permissions to prevent oversharing of data
## Elevate privilges using PIM
Regular Users -----> PIM -----> Admin Roles
## Monitor the health of your M365 services
### M365 Health Dashboard
- Critical Alerts
  - General service incidents
  - Billing issues
  - Service Health and Usage
  - Recommended actions
- M365 Service Health
  - Office on the web
  - Yammer
  - Dynamics CRM
  - MDM about services
## Monitor tenant health using M365 Adoption Score
- Metrics to help an org see where it is on its digital transformation journey.
- Insights
- Recommended actions
- Provides two metrics
  - People experiences
  - Technology experiences
## Monitor tenant health using M365 Usage Analytics
M365 Admin Center ---> Reports ---> Usage
- Import into PowerBI
- Identifiable user info off by default.
## Implement M365 Network Connectivity Assessment and Insights
- Location must be configured
- Option 1:
  - Enable Windows Location Services in devices
  - Setting: LetAppsAccessLocation
- Option 2:
  - Manually add or upload location data
- Option 3:
  - Run the M365 Connectivity Test from your office locations
## Implement M365 Backup
- Fast backup/restore within hours
- Full SharePoint/OneDrive account restore in their exact state.
- Full Exchange mailbox item restores using search.
- Consolidated security and compliance domain management.
**$0.15/GB/Month
- Data never leaves the M365 data trust boundary or geographic locations of your current data residency.
- Backups are immutable unless expressly deleted by the backup tool admin.
- OneDrive, SharePoint, Exchange have multiple physically redundant copies to protect against physical disasters.
## Develop an Incident Response Plan
1. Validate and confirm your tenant is affected.
2. Determine whether the incident is relevant to your company.
3. Review the timeline checks once relevancy and degredation have been established.
4. Develop a backup solution in case the service is degraded longer than an acceptable timeframe.
### Request assistance from Microsoft
## Deploy M365 Apps for Enterprise
### Explore M365 Apps for Enterprise Functionality
- Visio/Project = Separate license
- Must connect to the Internet every 30 days for license validation.
### Complete a self-service installation of M365 Apps for Enterprise
- Uses Click to Run technology
- Needs M365 Account
- Needs admin rights on local pc
- Installs updates automatically in the background from the Internet.
### Deploy M365 Apps for Enterprise with Configuration Manager
- Dashboard where you can deploy Office and monitor updates.
- Integration of the Office Customization Tool.
- Fully supported method of removing existing versions.
- Deployment of app settings include VBA Macro notifications, default file locations, and default file formats.
- Peer cache
### Deploy M365 Apps for Enterprise from the cloud
- Office Content Delivery Network
  - Distributes frequently accessed objects like images and JS files over global network
  - Reduces page load time
  - Access to hosted objects as close to user as possible
  - Private and Public CDN
### Deploy M365 Apps for Enterprise from a local source
- Download to a shared folder on a local network.
1. Create shared folder.
2. Download ODT.
3. Create config file for pilot.
4. Create config file for broad group.
5. Download install package for pilot.
6. Download install package for broad group.
7. Deploy to pilot.
8. Deploy to broad.
## Analyze your M365 Workplace data using Viva Insights
### Examine the analytical features of Viva Insights
- Personal insights
- Team insights
- Organization insights
- Advance insights
#### Metrics
- Workweek span
- Collaboration hours
- After hour collaboration hours
- Meeting hours
- Email hours
- Meeting count
- Emails sent
#### Role descriptions and access levels
- Insights Administrator
- Insights Business Leader
- People Manager
- Analyst
- Analyst (Limited Access)
- Program Manager
  
  
