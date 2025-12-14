# Storage
## Azure Storage Overview
- Highly available
- Massively scalable
- Accessible
- Managed
### Types
- Blobs
  - Object store
  - Text and binary
- Files
  - Managed file shares
  - Varied company data
- Queues
  - Messaging service
  - Application message
- Tables
  - NoSQL store
  - Schemaless
### Key Components
- Storage account
  - Special container with important properties for the storage service
- Storage services
  - Multiple storage services can exist within a single storage account
- Public endpoints
  - Storage services are built for public accessibility by design
#### Storage Account
- Name
- Performance
  - Standard
    - Lowest cost
    - HDD
  - Premium
    - Higher cost
    - SSD
- Type
  - General purpose v2
  - Page
  - Block
  - File
- Redundancy
  - Protect data by replicating across hardware and data centers
##### Types
- General purpose v2
  - Standard HDD
  - Access to all storage services
  - Useful for most scenarios
  - Provides most features
- Premium Block Blobs
  - Premium SSD
  - Block/Append blobs only
  - Low latency, high transaction
  - Limited replication and other features
- Premium Page Blobs
  - Premium SSD
  - Page blobs only
  - High-performance
  - Limited replication options
- Premium File Shares
  - Premium (SSD)
  - File service only
  - High-performance
  - Limited replication, adds NFS support
## Azure Blob Storage Overview
### Key Components
- Storage Account
  - GPv2
  - Block Blob
  - Page Blob
- Blob Container
  - Container for managing access to the unstructured data.
- Blobs
  - Actual objects/files that are stored
### Blob Types
- Block blobs
  - Most common
  - Binary/text
- Append Blobs
  - Built for append operations
  - Logs
- Page Blobs
  - Random access files
  - Used for VM disks and Azure SQL DB files
### Sub-Types
- Blob Version
  - Retain version history of blobs automatically when edited
- Blob Snapshot
  - Read only point in time copy of blob
- Soft Deleted Blobs
  - Blobs that have been deleted but are kept for a retention period
## Azure Storage Data Access Control
| Type | REST | SMB | NFS |
|------|------|-----|-----|
|Blobs | x    |     | x   |
|Files | x    | x   | x   |
|Queues| x    |     |     |
|Tables| x    |     |     |
- All require authentication except anonymous access blobs
- Key
- SAS
- Entra Id
### Access Keys Overview
- Storage Account
  - Managed at the SA level
- Access Keys
  - Provides full unrestricted access to the SA.
- Management
  - Keys can be rotated or disabled entirely for a SA
### Entra ID Based Access
- Identity
  - User, group, or managed identitiy
- Scope
  - Standard RBAC hierarchy down to individual storage service
- Role
  - Built in and custom RBAC roles that target **data operations**
### Shared Access Signatures (SAS)
- Service SAS
  - A token that can provide restricted access to an individual service
- Stored Access Policies
  - Facilitates server-side control of SAS signatures
- Account SAS
  - Access to one or more services, including service level operations
- User-delegation SAS
  - Associated with Entra ID identity that supports blob storage
## Azure Storage Redundancy
### Redundancy Types
- LRS - Locally Redundant Storage
  - 3 copies
  - 1 physical location
  - Synchronous replication
- ZRS - Zone Redundant Storage
  - 3 copies
  - 3 physical locations in the same region
- GRS - Geo-Redundant Storage
  - LRS followed by one asynchronous copy to the secondary region
- GZRS - Geo-zone Redundant Storage
  - ZRS is followed by one aysnchronous copy to the secondary region
### Secondary Read Access
- Supported by RA-GRS or RA-GZRS (w/o the need for a failover to be triggered)
- Can help ensure continuity of access in the event of any outages
- Copy in secondary region is available via a public endpoint
### Storage Account Failover Considerations
- Failover is initiated by the customer manually
- All data in the primary is lost, secondary becomes primary
- After failvover, the new secondary will be configured as LRS
- Failover can result in data loss, replication is asynchronous
### Important Considerations
- Not all types of redundancy are supported by all storage account types
- Redundancy is not a backup
- Can convert from/to many redundancy types, some require support ticket or special process
## Blob Storage Access Tiers
- Hot Tier
  - Highest storage costs
  - Lowes access costs
  - Online, frequent access
- Cool Tier
  - Lower storage costs
  - Higher access costs
  - Online, infrequent acccess
- Archive Tier
  - Lowest storage costs
  - Highest access costs
  - Offline, rarely accessed
  - Rehydration
  - Latency, up to 15 hour delay
  - Fee if deleted/moved earlier than 180 days
### Key Configuration Items
- Storage Accounts
  - General purpose v2
  - Not supported by Premium Block Blob
- Blobs
  - Block blob only
  - Page/append not supported
- Access Tier
  - Default is defined for a storage accont
  - Can be assigned per blob
## Blob Storage Lifecycle Management
- Policy
  - Lifecycle management
### Key Configuration Items
- Storage Account
  - General Purpose v2
  - Premium Block Blob
  - Blob Storage (legacy)
- Blobs
  - Block/Append only
- Management Policy
  - Supports complex rules with filters, blob sub-types, and actions
## Block Blob Object Replication
- Geographic deployment
- Replica storage of primary
  - Read Only
  - Primary: USA
  - Secondary: Europe, Japan
### Key Components
- Source Storage Account
  - General purpose v2
  - Premium Block
- Destination Storage Account(s)
  - Up to two destination accounts
  - Can be same/different region/sub/tenant
- Replication Policy
  - Source & Destination containers for replication, including rules and filters
## Immutable Blob Storage
- Time based retention
- WORM
  - Write Once Read Many
- Legal Hold
  - Create and read blobs
  - Can't delete/modify any blobs
### Key Components
- Storage Account
  - General Purpose v2
  - Premium Block Blob
- Access Policy
  - Time: retention period
    - Can be locked
  - Legal
    - On/Off as needed
- Scope
  - Container-level scoped
  - Version-level scoped
## Azure Storage Encryption
- Azure Storage Service Encryption (SSE)
- Optional: Infrastructure Encryption
- SSL/TLS can be enforced
### Configuration Key Components
- Server-side encryption (SSE)
  - Encryption **at rest**
- Encryption key
  - Platform managed key
  - Customer managed key
    - Optional
      - Azure Key Vault
      - Blob and Files OR Queues and Tables
- Identity
  - Managed identity is required
- Encryption Scopes (optional)
  - Optionally define blobs/conainers to be encrypted with a CMK or PMK.
## Azure Files
### Storage Tiers
- Premium
  - SSD
  - Highest performance
  - Single digit ms latency
  - SMB/NFS shares
  - Provisioned billing only
- Transaction Optimized
  - HDD
  - High price for storage
  - Low costs for transaction
  - SMB
  - Pay as you go
- Hot
  - HDD
  - Mid price for both storage and transactions
  - SMB
  - Pay as you go
- Cool
  - HDD
  - Lowest price for storage, high price for transactions
  - SMB
  - Pay as you go
### Key Components
- Storage Account
  - General purpose v2
  - Premium File storage
- File Share
  - SMB: Supports all tiers/redundancy
  - NFS: Premium and LRS/ZRS only
- Client Connectivity
  - REST API for apps
  - SMB/NFS for users
## Azure Files Connectivity and Access Control
### Client Connectivity
- SMB Shares
  - Connection
    - SMB 3.0 - Internet
    - SMB 2.1 - VNet
- Access Control Lists
  - Win32ACLS w/ Kerberos and NTLMv2
- NFS Shares
  - Connection
    - NFS 4.1 via VNET Only
  - ACLS
    - POSIX w/ host-based auth
### Active Directory Source
- SMB Shares - Identity based auth
  - AD
    - Sync identities that authenticate against on-prem AD
  - Azure AD Domain Services
    - Identities that authenticate against Azure AD DS
#### Azure AD DS
- Azure AD Kerberos
  - Hybrid identities that authenticate against Azure AD via (Hybrid) Entra-ID joined devices
### Configure Access Permissions
1. Configure the identity source
   - Enable the AD source
   - Only one can be selected for a storage account
2. Assign Share permissions
   - Assign permissions at the share level for identities to access Azure Files
3. Assign directory/file permissions
   - Mount the share with the account and configure permissions
## Azure File Sync
### Key Components
- File Share
  - SMB share with GPv2 or Premium File Storage Account
- Sync Service
  - Servers register to one only; they can then belong to many sync groups
- Endpoints
  - Cloud Endpoint: Azure File Share
  - Server Endpoint: Local Folder
## Azure Storage Data Transfer Tools
### Import/Export
- Purpose: Move large volumes of data
- Customer disks
  - 1 or more physical disks
- Supported services
  - Blobs
    - Import/Export
  - Files
    - Import
- Process
  - Disks are managed using a windows tool
  - Manage job through portal
  - waimport tool
### Data Box
- Purpose: Move large volumes of data
- Data Box
  - Data Box/Disk/Heavy (offline)
  - Gateway (online) appliances
- Supported Services
  - Blobs
    - Block/page
  - Managed disks
  - Azure Files
  - ALDS Gen2
- Process
  - Order the device
  - Connect and use locally
  - Return
### AZCopy
- Purpose: Manage data across platforms
- AZCopy Tool
  - Cross platform/cmdline tool
- Supported Services
  - Blobs
  - Files