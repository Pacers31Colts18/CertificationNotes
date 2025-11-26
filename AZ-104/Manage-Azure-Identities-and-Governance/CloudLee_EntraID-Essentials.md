# **Entra ID Essentials**

## Entra ID User Identities

- Users > User ID > Resources

## Entra ID Application Identities

### Key Features
- Helps control access to an app and the access an app has to other resources.
- App can reside anywhere, inside or outside of Azure.
- Apps must register with an Entra ID tenant
    - Applilcation Registration
- Authentication relies on client secret or certificate.

## Managed Identities

### Key Features
- Provides an identity to a resource that exists within an Azure subscription.
- Authentication managed by Azure.
- **System-Assigned** - enabled for a single resource as long as it exists.
- **User-Assigned** - you may create a managed identity to be used by one or more resources.

## Entra ID Groups

### Key Features
- Simplifies assignment of Entra ID roles, Azure RBAC roles, and Entra ID licensing.
- Allows an owner to be assigned.
- Static/Dynamic
## Microsoft 365 Groups
### Key Features
- Simplifies administration of collaborative spaces for users/projects/teams.
- Allows an owner to be specified.
- Additional features such as expiry, sensitive labels, etc.
- Static/Dynamic

## Entra ID Dynamic Groups
- User/M365/Device
### Important Considerations
- Users/M365 - P1 Licensing
- Can't manually change
- Can't mix user/device membership

## Entra ID Administrative Units
### Key Features
- Simplifies the assignment of permissions to Entra ID objects
- Can mix users/devices/groups
- Assigned/Dynamic
- Objects can be in multiple AUs.
### Important Considerations
- **Requires P1 Licensing**
- Does not apply to members of a security group
- Can't nest Administrative Units
