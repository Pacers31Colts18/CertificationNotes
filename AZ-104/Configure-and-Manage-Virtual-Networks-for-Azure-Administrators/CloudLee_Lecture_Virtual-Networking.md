# Virtual Networking
## Virtual Networks
### Key Components
- Virtual Network
  - Network space isolated from other public or private networks.
- Subnets
  - Spaces that can be carved up within a virtual network for further isolation.
- Network interface(s)
  - Provides connectivity using automatically assigned private IP.
### Considerations
- Address space
  - IPv4
    - /2 to /29 subnets
  - IPv6
    - /64 subnets
- DNS
  - Provided for you, but you can use custom DNS servers also.
- Protocols
  - TCP, UDP, ICMP
### Default Routes
- Connectivity between subnets
- Connectitvity to the internet
- System connectivitiy (VNet Peering)
## IP Addressing
### Private IP Addressing
#### How It Works
- Association
  - Associated by resource configuration, or network interfaces (VMs)
- Address Allocation
  - Dynamic or Static but can't be reserved in advance.
- Address Availability
  - Azure reserves the first four and last IP addresses in the subnet for system use.
### Public IP Addressing
#### How It Works
- Association
  - Independent resource (basic/standard) that can be associated with other resources
- Address Allocation
  - Dynamic
    - Assigned when associated (basic)
  - Static
    - Assigned when created (basic/standard)
  - IP Address Availability
    - Assigned from a pool, or a public IP prefix, or a custom IP address prefix
### Outbound Connectivity Overview
#### How It Works
- VM Default
  - If no IP address is assigned, Microsoft will provide a public IP.
- VM Public IP
  - If a public IP resource is associated the VM will use it for outbound access.
- Public Load Balancer SNAT
  - Traffic can be routed out via the public IP of a load balancer.
- NAT Gateway
  - Provides connectivity (using automatically assigned private IP)
## Network Security Groups
### Routes vs NSGs
- Routes = Roads
- Network Traffic = Vehicles
- NSGs = Guards
### Network Security Groups
- Contains a list of inbound rules and outbound rules
- Assignment
  - Network interface
  - Subnet
  - Both
- Security Rules
  - Each rule defines traffic that should be allowed or denied
- Name
  - Custom label
- Priority
  - Lower number = Higher priority
- Traffic Definition
  - Port
  - Protocol
  - Source
  - Destination
- Action
  - Allow
  - Deny
- Inbound
  1. Subnet NSG
  2. VM
- Outbound
  1. VM
  2. Subnet
## Augmented Security Rules
### Service Tags
- Microsoft managed
- A grtoup of IP address prefixes that are used to point to Microsoft services for source/destination
- Simplifies rules for common services.
- IP addresses are automatically updated.
- Examples:
  - SQL.AusEast
  - Storage
### Application Security Groups
- Customer managed
- A way for grouping VMs together for use as a source/destination, more easily than manual IP addressing.
- Simplifies rules for customer solutions
- Provides a "tag" for VMs
- Example:
  - ASGWebServers
  - ASGManagementVMs
### Things you should know
- Network interfaces assigned to an ASG must be from the same Vnet as the first assigned interface.
- If you use an ASG for both source and destination field, they must belong to the same Vnet.
- Can't create your own service tatg, all created/managed by Microsoft.
