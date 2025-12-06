# Load Balancing and Connectivity
## Configure a Load Balancer for a Web App on a VM
- Create a Resource > Visual Studio 2022 VM
- Standard_B1s SKU
- Install **Custom Script Extension**
- Create another VM
- **SKUs need to match**
- If on Standard, need a NSG to allow the traffic.
- Create a Resource > Load Balancer
## Application Gateway
- If using private, you do need a static private IP.
- Create a backend pool for app resources and static web resources.
## Configure Azure Bastion
- Use Bastion
- Standard, you cannot downgrade to Basic. Can only upgrade from Basic to Standard.
## Azure Firewall
- Configure a firewall to support:
  - Centralized network security with a Firewall deployed to a hub VNet
  - Parent and child policies
    - Must be in the same region
  - Spoke-to-spoke (transitive routing) via the Firewall
  - Inbound RDP access (using DNAT rules)
  - Outbound web filtering (blocking a URL and web categories)
- Add Rule Collection
  - Rule Collection Type
    - Network
    - Application
    - DNAT
  - Priority
    - Number
  - Rule collection action
    - Allow/deny
    - group policy kql
