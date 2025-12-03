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
