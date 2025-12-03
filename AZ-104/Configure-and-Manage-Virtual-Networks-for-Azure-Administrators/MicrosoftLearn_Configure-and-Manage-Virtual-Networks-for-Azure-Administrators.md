# Configure and Manage Virtual Networks for Azure Administrators

## Configure Virtual Networks

### Plan Virtual Networks

#### Things to Know
- An azure virtual network is a logical isolation of the Azure cloud resources.
- You can use virtual networks to provision and manage VPNs in Azure.
- Each virtual network has its own CIDR block and can be linked to other virtual and on-prem networks.
- Can link with on-prem to create a hybrid network.
  - **Can't overlap IP spaces**
- You control DNS and segmentation

### Create Subnets
- A virtual network can be segmented into one or more subnets.
- Provide logical divisions within your network.
- Can help improve security, increase performance, and easier to manage.
- **Subnet address ranges cannot overlap**
#### Reserved Addresses
- Azure reserves 5 IP addresses.
  - Example: 192.168.1.0/24
      - 192.168.1.0
        - ID for the virtual network
      - 192.168.1.1
        - Default gateway
      - 192.168.1.2, 192.168.1.3
        - Azure maps these addresses to the virtual network space.
      - 192.168.1.255
        - Broadcast address
#### Things to Consider
- Service requirements
- Consider network virtual appliances
- Network security groups
  - Can associate 0 or 1 NSG to each subnet in a virtual network.
- Private links
  - Azure Private Link provides private conectivity from a virtual network to Azure PaaS, ccustomer owned, or Microsoft Partner solutions.

 ### Create Virtual Networks
 #### Things to Know
 - Need to define the IP address space for the network.
 - Plan to use an IP address space not in use.
   - Space can be on-prem or in the cloud
   - **NOT BOTH**
   - Once you create the space, it cannot be changed.
- Need to define at least one subnet.
  - Each subnet contains a range of IP addresses that fall within the virtual network address space.
  - Address range must be unique.
  - Can't overlap
- Create in Azure Portal
  - Subscription
  - Resource Group
  - Virtual Network Name
  - Service region
### Plan IP Addressing
#### Things to Know
- Static/Dynamic
- Can separate dynamically and statically assigned IP resources into different subnets.
### Create Public IP Addressing
#### Things to Consider
- IPv4/IPv6/Both
- SKU
  - Basic/Standard
  - Must match load balancer
- Name
- IP Address Assignment
  - Dynamic
  - Static
### Associate Public IP Addresses
- Virtual Machine
  - IP Address Association: NIC
  - Dynamic: Yes
  - Static: Yes
- Internet Load Balancer
  - IP Address Association: Front-end configuration
  - Dyanmic: Yes
  - Static: Yes
- Application Gateway
  - IP Address Association: Front-end configuration
  - Dyanmic: Yes
  - Static: Yes
#### Things to Consider
|Top-Level Resource|IP Address Config|
|----------------------------------------------------------------------------------------|--------------------------|
|VM                                                                                      | NIC                      |
|VPN, Virtual Network Gateway, NAT Gateway                                               | Gateway IP Configuration |
|Public Load Balancer, Application Gateway, Azure Firewall, Route Service, API Management| Front End Configuration  |
|Bastion Host                                                                            | Public IP Configuration  |

**SKU FEATURES**
| Public IP Address | Standard SKU                                       |
|-------------------|----------------------------------------------------|
| Allocation Method | Static                                             |
| Security          | Secure by default                                  |
| Available Zones   | Supportd. Can be nonzonal, zonal, or zone redundant|

### Allocate or Assign Private IP Addresses
- Dyanmic or Static
- VM
  - Private IP Address association
    - NIC
  - Dynamic IP Address
    - Yes
  - Static IP Address
    - Yes
- Internal Load Balancer
  - Private IP address association
    - Front-end configuration
  - Dynamic IP Address
    - Yes
  - Static IP address
    - Yes
- Application Gateway
  - Private IP address association
    - Front-end configuration
  - Dynamic IP Address
    - Yes
  - Static IP address
    - Yes
**Private IP Address Assignment**
- Dynamic
  - Default method
- Static
  - Select and assign any unassigned or unreserved IP address in the range.

## Configure Network Security Groups
- A way to limit network traffic to resources in your virtual network.
### Implement Network Security Groups
- Can assign to a subnet (most common) or network interface.
- Single NSG can be associated multiple times.
- Lists the security rules that allow/deny inbound/outbound traffic.
#### Things to Know
- Overview page from a VM provide info about the associated NSGs
#### NSGs and Subnets
- Use NSG to restrict traffic flow to all machines that reside within the subnet.
- Each subnet can have a maximum of one associated NSG.
#### NSGs and NICs
- Define NSG rules to control all traffic that flows through the NIC.
- Each NIC that exists in a subnet can have zero or one associated NSGs.
### Determine NSG Rules
- Enable you to filter network traffic that can flow in and out of subnets and network interfaces.
- Default rules can't be deleted. Add other rules at a higher priority
  - 65xxx = Default rules
  - Smaller number = higher priority
#### Things to Know
**Common Conditions**
| Setting            | Value                                                                     |
| -------------------|---------------------------------------------------------------------------|
| Source             | Any IP address, My IP address, service tag, or Application Security group |
| Source port ranges | Specify the ports on which the rule allows or denies traffic              |
| Destination        | Any IP address, service tag, or Application Security Group                |
| Protocol           | TCP/UDP/ICMP. Default = Any                                               |
| Priority           | Value between 100-4096                                                    |
#### Inbound Traffic Rules
- Azure sets 3 default rules
- These rules deny inbound traffic
#### Outbound Traffic Rules
- Azure sets 3 default rules
- These rules allow outbound traffic to the internet and your virtual network.
### Determine NSG Effective Rules
- Evaluated independently for the subnet and NIC.
- An allow rule must exist at both levels for traffic to be admitted.
#### Inbound
1. NSG rule processed
2. NIC rule processed
#### Outbound
1. NIC rule processed
2. NSG rule processed
#### NSG Evaluation
- Inbound and outbound rules are considered based on the priority and processing order.
#### Things to Consider
- Consider allowing all traffic.
- Consider importance of allow rules
  - Must be applied at both levels
- Consider intra-subnet traffic.
- Consider rule priority
  - Lower the number, higher the priority
  - Leave gaps in priority numbering such as 100, 200, 300
  - Gaps in numbering allow you to add rules w/o having to edit existing rules.
#### View Effective Security Rules
- You can use this to verify which security rules are applied to your machines, subnets, and NICs.
- A part of the Network Watcher tools
### Create NSG Rules
#### Things to Know
- Source
  - Identifies how the security rule controls **inbound** traffic.
- Destination
  - Identifies how the security rule controls **outbound** traffic.
- Service
  - Destianation protocol and port range for the security rule.
  - SSH, RDP, FTP are predefined.
- Priority
  - Set the number
- Name
  - Custom name
### Implement Application Security Groups
- To logically group VMs by workload
- Extend your applications structure
- ASGs logically group VMs, web servers, app servers
- Define rules to control the traffic flow
- Wrap the ASG within an NSG for added security
#### Things to Know
- Work the same as NSGs but for an app-centric way of looking.
#### Things to Consider
- Several advantages:
  - IP address maintenance
  - Consider no subnets
    - Don't need to distribute servers across specific subnets
  - Simplified rules
    - Help eliminate need for multiple rulesets
  - Workload support
  - Service tags
    - Help minimize complexity
## Host your domain on Azure DNS
### What is Azure DNS?
- Allows you to host and manage your domains
- Not a domain registrar
#### DNS Record Types
- A
  - Host record
  - Maps the domain or host name to IP
- CNAME
  - Used to create an alias from one domain name to another domain name
- MX
  - Mail exchange record
- TXT
  - Text record
  - Used to associate text strings with a domain name
  - Azure and M365 use TXT to verify domain ownership
### Why use Azure DNS?
- Improved security
- Ease of use
- Private DNS domains
- Alias record sets
#### Security Features
- RBAC
- Activity log
- Resource locking
#### Ease of Use
- Same Azure creds, contract, and billing
#### Private Domains
- Lets you create private zones
- Provide name resolution for VMs within a virtual network and between virtual networks without having to create a custom DNS solution.
- Benefits:
  - Supported as part of Azure infrastructure
  - All DNS record types are supported
  - Host names automatically maintained
  - Split-horizon DNS support
#### Alias Record Sets
- Can setup an alias record to direct traffic to an Azure public IP address, Adzure Traffic Manager profile, or an Azure CDN endpoint.
- Supported in the following DNS record types
  - A
  - AAAA
  - CNAME
### Configure Azure DNS to host your domain
#### Configure a public DNS zone
1. Create a DNS zone in Azure
   - Following details needed:
     - Susbcription
     - Resource group
     - Domain name
     - Resource group location
2. Get your Azure DNS name servers
   - Get name servers
   - Update registrar information
3. Update the domain registrar setting
   - Edit the Name records with new NS records
   - Called domain delegation
4. Verify delegation of domain name services
   - Query the SOA record
```powershell
nslookup -type=SOA joeloveless.dev
```
5. Configure your custom DNS settings
   - A record
     - Name
     - Type = A
     - TTL
     - IP Address
  - CNAME record
    - Name: www
    - TTL: 600 seconds
    - Type = CNAME
#### Configure a private DNS zone
- Can be used to assign DNS names to VMs in your Azure virtual network
1. Create a private DNS zone
   - Subscription
   - Resource group
   - Name
   - Resource group location
2. Identify virtual networks
   - Virtual network names need to be added to private zone.
3. Link your virtual network to private DNS zone
   - Create a virtual network link
### Dynamically resolve resource name by using an Alias record
- Load balancers distribute inbound data requests and traffic across one or more servers
#### What is an apex domain?
- Domains highest level
- @ symbol = apex domain in DNS records
#### What are alias records?
- Enables a zone apex domain to reference other Azure resources from the DNS zones.
- Can point to the following
  - Traffic manager profile
  - Azure CDN endpoints
  - Public IP resource
  - Front-door profile
- Alias record support the following:
  - A
  - AAAA
  - CNAME
#### Use for Alias records
- Prevenet dangling DNS records
- Updates DNS record set automatically when an IP address changes
- Hosts load-balanced applications at the zone apex
- Points zone apex to Azure CDN endpoints
## Configure Azure Virtual Network Peering
- Peering provides secure communication between resources in peered networks.
### Determine Azure Virtual Network Peering Uses
- Two types:
  - Global or Regional
- Connect **two** networks
  - Can peer across subscription and tenants
- Uses Azrure backbone for privacy and isolation
- Easy to setup seamless data transfer, great performance
#### Things to Know
- Regional
  - Same Azure public cloud region
  - Same China cloud region
  - Same Azure government cloud region
- Global
  - Any Azure public cloud region
  - Any China cloud region
  - Global peering of virtual networks in different Azure government cloud regions isn't permitted
#### Things to Consider
- Private
  - On Azure backbone
- Performance
  - Azure infrastructure
- Simplified communication
- Seamless disk transfer
- No resource disruptions
  - No downtime when creating or after
### Determine gateway transit and connectivity
- Gateway transit allows peered virtual networks to share the gateway and get across to resources
- No VPN gateway is required in the peered spoke virtual network
- Default VNET peering provides full connectivity
#### Things to Know
- Virtual network can only have one VPN gateway
- Gateway transit supported for both regional and global virtual network peering
- Gateway transit allows peered virtual networks to share the gateway and get access to external resources
- You can apply NSGs in a virtual network to block/allow access to other virtual networks or subnets.
### Create virtual network peering
#### Things to Know
- Network Contributor role or Custom role
- To create peering
  - 2 virtual machines
- The 2nd virtual machine in the peering is the **remote network**
#### Key Scenarios
- Data replication
- Database failover
- **VNET address spaces cannot overlap**
#### How to check your peering status
- Azure Resource Manager Deployment
  - Status conditions: Initiated/Connected
  - Classic Deplyoment: Updating also
- When you create the initial peering to the 2nd virtual network from the first virtual network the peering status for the first is **initiated**
- Subsequent peering fro the second virtual network to the first virtual network
  - Peering status for both networks
    - **Connected**
  - 1st virtual network will change from **initiated** to **connected**
### Extend peering with user-defined routes and service chaining
- Virtual network peering is non-transitive
- Example:
  - 3 virtual networks
    - A
    - B
    - C
  - Peered:
    - A <-----> B
    - B <-----> C
  - Not Peered
    - A <-----> C
#### Things to know about extended peering
- Hub and spoke network
  - All the spoke virtual networks can then peer with the hub virtual network
- User-Defined Route
  - Virtual network peering enables the next hop in a **user-defined** route to be the IP address of a VM in teh peered virtual network or a VPN gateway.
- Service Chaining
  - Used to direct traffic from one virtual network to a virtual appliance or gateway
  - 
        


