# Cloud Lee - Identity and Access Management

## Entra ID Roles
**Implementation**
- Usage Overview
  - Security Principal
    - Who/What
    - User, security group, app, managed
  - Role Definition
    - What are the permissions?
    - Built-In or Custom
      - Owner
      - Contributor
      - Reader
  - Scope
    - Where will they apply
    - Management group
    - Subscription
    - Resource group
    - Resource
## Azure AD Roles
**Implementation**
- Security Principal
  - Users, groups, applications
- Role Definition
  - Built-in
  - Custom
  - **Custom needs a P1 license**
- Scope
  - Tenant
  - Administrative Unit
  - Application
## Azure RBAC Custom Roles
- What it's made up of?
  - Metadata
    - Name
    - Description
    - ID
  - Permissions
    - For **management/data** operations
      - Actions
        - Allowed control plane actions
      - Not Actions
        - Subtracted control plane actions
      - Data Actions
        - Allowed data plane actions
      - Not Data Actions
        - Subtracted data plane actions
  - Scope
    - Defines what the role can be used for
  - Assignable Scopes
    - Root
```powershell
/*
```
  - Available to all scopes. Built-in only
- Management groups
```powershell
/providers/Microsoft.Management/ManagementGroups/ID
```
- Subscriptions
```powershell
/subscriptions/ID
```
- Resource Groups
```powershell
/subscriptions/ID/resourcegroups/Name
```
- Azure RBAC custom roles are available w/o any special licensing requirements
- Azure RBAC is not policy
  - RBAC = Permissions
  - Policy = Standards
- To configure Azure RBAC custom roles you require **Owner** or **User Access Admin** permissions.



  