# Implement and Manage Storage in Azure
## Configure Storage Accounts
### Implement Azure Storage
#### Things to Know
- Structured
  - Relational
  - Shared Schema
  - DBs
    - Azure Table Storage
    - Azure Cosmos DB
    - Azure SQL DB
- Unstructured
  - Least organized
  - Nonrelational
  - Azure Blob
  - Azure Data Lake
- VM Data
  - Disks and files
  - Persistent blob storage
  - Fully managed file shares in the cloud
#### Things to Consider
- Durability and Availability
  - Replicate across data centers or regions
- Secure Access
  - All data encrypted
  - Fine grain control
- Scalability
- Manageability
  - Microsoft handles hardware for you
- Accessability
  - HTTP/HTTPS anywhere in the world
  - SDKs
### Explore Azure Storage Services
- Containers
  - Massively scalable object store for text and binary data.
- Tables
  - Ideal for structured, non-relational data
- Queues
  - Messaging store for reliable messageing betwen app components
- Files
  - Managed file shares for cloud and on-prem deployments
#### Azure Blob Storage
- Ideal for:
  - Images
  - Docs
  - Audio/Video
  - Big data
  - Backup file
  - DBs
  - Logs
#### Azure Files
- Accessed via SMB/NFS, REST
- Common scenarios:
  - On-prem apps and file shares
  - Config files
  - Logs, metrics, crash dumps
#### Azure Queue Storage
- Can be up to 64kb in size
#### Azure Table Storage
- Key/Attribute store with a schemaless design
### Determine Storage Account Types

| Storage Account          | Recommended Usage                   |
|--------------------------|-------------------------------------|
| Standard general purpose | Most scenarios                      |
| Premium block blobs      | High transaction rates, low latency |
| Premium file shares      | ENT or high performance             |
| Premium page blobs       | High performance page blob          |

#### Things to Know
- Standard
  - HDD
  - Lowest cost per GB
- Premium
  - SSD
### Determine Replication Strategies
- LRS
  - 3 replicas
  - 1 region
- ZRS
  - 3 replicas
  - 3 zones
  - 1 region
- GRS
  - 6 replicas
  - 2 regions (3 per region)
- RA-GRS
  - GRS + read access to secondary
#### Things to Consider
- Node in Data Center Unavailable
  - LRS
  - ZRS
  - GRS
  - RA-GRS
  - GZRS
  - RA-GZRS
- Entire Data Center Unavailable
  - ZRS
  - GRS
  - RA-GRS
  - GZRS
  - RA-GZRS
- Region-wide outage
  - GRS
  - RA-GRS
  - GZRS
  - RA-GZRS
- Read access during region wide outage
  - RA-GRS
  - RA-GZRS
### Access Storage
- Container Service
```powershell
\\mystorageaccount.blob.core.windows.net
```
- Table Service
```powershell
\\mystorageaccount.table.core.windows.net
```
- Queue Service
```powershell
\\mystorageaccount.queue.core.windows.net
```
- File Service
```powershell
\\mystorageaccount.file.core.windows.net
```
- Can configure a custom domain name
  - Subdomain: blob.contoso.com
  - AZ Storage: \\<storageacconut>\blob.core.windows.net
  - CNAME: contosoblobs.blob.core.windows.net
### Secure Storage Endpoints
- Firewalls and VNets restrict access to the storage account from specific subnets on Virtual Networks or Public IPs
- Subnets and Virtual Networks must exist in the same region or region pair as the SA
#### Things to Know
- Can configure the service to allow access to one or more IP ranges.
## Configure Azure Blob Storage
### Implement Azure Blob Storage
- Unstructured data
- Text/binary data
- Object storage
- Use cases:
  - Images/docs directly to a browser
  - Files for distributed access
  - Audio/video
  - Disaster recovery
  - Analysis
#### Things to Know
- 3 resources to store and manage data
  - Storage account
    - Containers
      - Blobs
### Create Blob Containers
#### Things to Know
- Blobs must be in a container
- Containers organize blob storage
- Can store unlimited number of blobs
- Storage account can cointain unlimited number of containers
- Must create a storage account before you can upload data
#### Configure a Container
- Name
  - Unique within the storage account
- Public access level
  - Private
    - No anonymous access
  - Blob
    - Anonymous for blob only
  - Container
    - Public read and list access for the entire container
### Assign Blob Access Tiers
- Hot
  - Access or modified frequently
  - Highest storage cost
  - Lowest access cost
- Cool
  - Large amounts of infrequently accessed data
  - 30+ days
  - Lower storage costs, higher access costs vs. Hot
- Cold
  - 90+ days
  - Lower storage costs, higher access costs vs. Cool
- Archive
  - Offline tier
  - 180+ days
  - Highest access costs
  - Most cost effectice for storage
#### Compare Access Tiers
| Comparison | Hot | Cool | Cold | Archive |
| -------------------------|------|------|------|----------|
|Availability              |99.9% |99%   |99%   |99%       |
|Availablity (RA-GRS Reads)|99.99%|99.9% |99.9% |99.9%     |
|Latency                   |ms    |ms    |ms    |hours     |
|Minimum storage duration  |N/A   |30d   |90d   |180d      |
### Add Blob Lifecycle Management Rules
- Transitioning of blobs to cooler storage tier to optimize for performance and cost.
- Delete at end of lifecycle
- Apply rules to filtered paths in storage account
### Determine blob object replication
- Asynchronous to any other region
- Minimize latency for read requests
- Increases efficiency for compute workloads
- Optimizes data distribution
- Optimizes costs
#### Things to Know
- Blob versioning needs to be enabled on source and destination accounts
- Doesn't support blob snapshots
- Supported when source and destination accounts are in the Hot, Cool, and Cold tiers
  - Source and destination can be in different tiers.
- Create replication policy that specifies source and destination
- One or more rules
### Manage Blobs
- 3 types:
  - Block
    - Most scenarios
    - Ideal for text and binary data
    - Default
  - Page
    - Up to 8TB in size
    - More frequent read/write
    - Azure VMs use Page blobs for disks
  - Append
    - Also blocks of data
    - Append operations
      - Logging
### Blob Storage Pricing
- Cost depends on
  - Volume
  - Quantity and types of operations
  - Data redundancy options selected
## Configure Azure Storage Security
### Review Azure Storage security strategies
#### Things to Know
- Encryption at rest
- Encryption in transit
  - Can require secure transfer
    - HTTP refused
    - SMb 3.0 enabled
- Encryption models
- Authorize requests
  - Use Entra ID w/ managed identities
- RBAC
- Storage Analytics
### Create Shared Access Signatures
- URI that grants restricted access
- Types of SAS:
  - User Delegation SAS
    - **safest**
  - Service SAS
  - Account SAS
- Best Practicies
  - Always use HTTPS
  - User delegation SAS is safest
  - Set expiration to smallest useful time
  - Least privilege
  - Not always correct solution
### Identify URI and SAS Parameters
- Storage version - sv
- Storage service - ss
- Start time - st
- Expiry time - et
- Resource - r
- Permissions - sp
- IP range - sip
- Signature - sig
### Determine Azure Storage Encryption
#### Things to Know
- Automatically encrypted before written to Azure Storage
- Automatically decrypted when retrieved
- Transparent to users
- 256-bit AES
- All new and existing, can't be disabled
#### Configure Azure Storage Encryption
- Infrastructure Encryption
  - Can be enabled for entire SA or a scope
  - When enabled for SA, data is encrypted twice
    - Service Level
    - Infrastructure Level
  - Platform Managed Keys
    - Generated, stored, managed by Azure
  - Customer-managed keys
### Create customer-managed keys
#### Things to Know
- More flexibility and greater control
- Can create, disable, audit, rotate, and define access controls for keys.
- Can be used with Azure Storage encryption
### Apply Azure Storage Security Best Practices
- Storage Insights
  - Comprehensive monitoring of your accounts
#### Benefits
- Detailed metrics and logs
- Enhanced security and compliance
- RBAC
- Unified view
#### Security Uses
- Real-time monitoring
- Security auditing
- Health Analysis and optimization
## Configure Azure Files
### Compare storage for file shares and blob data
#### Things to Know
- Serverless
- Almost unlimited storage
  - 100 TiB
- Data encryption
- Access from anywhere
- Integrate into existing environment
- Previous versions and backups
- Redundancy
#### Compare to Blob Storage
| Files                          | Blob                                          |
|--------------------------------|-----------------------------------------------|
|SMB/NFS, Client Libraries, REST | Client Libraries, REST                        |
|Directory objects, file shares  | Flat namespace, accessed through container    | 
| Ideal lift and shift           | Ideal for support streaming and random access |
### Manage Azure File Shares
#### Types
- Premium
  - SSD
- Standard
  - HDD
  - GPv2
#### Types of Authentication
- Identity based over SMB
- Access key
- SAS token
#### Create SMB Azure File Shares
- Port 445
- Enable secure transfer
### Create file share snapshots
#### Things to Know
- Provided at file share level
- Incremental
- Minimizes time required to create share snapshots
- Need most recent to restore
- Can retrieve individual file
### Implement Soft Delete
- Enabled at storage account level
- Transitions content to soft delete state
- Lets you configure retention period
  - 1 to 365 days
- Can be enabled on new or existing
#### Things to Consider
- Recover from accidental data loss
- Upgrade scenarios
- Ransomware protection
- Long-term retention
- Business continuity
### Consider Azure File Sync
- Transforms Windows Server into a quick cahce of files
- SMB/NFS/FTPS
- Supports as many caches as you need.