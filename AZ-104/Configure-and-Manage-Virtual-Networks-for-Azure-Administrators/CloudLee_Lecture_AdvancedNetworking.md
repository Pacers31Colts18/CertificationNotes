#Advanced Networking
## User-Defined Routing
### Custom Routes
- Like a map full of detours that define traffic.
### Implementation
- Route Table
  - Contains a list of routes that define where traffic goes.
- Assignment
  - Can be assigned to one or more VNet **subnets**
- Routes
  - Defines the **next hop** for a specific destination (address prefix)
    - Name
    - Address Prefix
    - Destination Address
      - Service Tag or CIDR
    - Next Hop
      - Defines where the traffic should go
### Rule Processing
- Use longest prefix match
### Important Limitations
- Virtual networks include default/system routes
- Route precedence
  - Custom > BGP > Default
- Routes can be advertised to a route table
## VNet Peering
- Connect private connectivity to isolated virtual networks w/o having to use Public IPs.
### Key Components
- VNet Peering
  - Two peers are crearted. One for each direction in the peering.
- Routes
  - System routes are automatically updated to allow connectivity.
  - Spoke1-Vnet ----> hub-vnet -----> spoke2-vnet
  - Spoke1-Vnet -----x-----> spoke2-vnet
**Traffic not encrypted**
### Important Limitations
- Works across regions/subscriptions/tenants
- Unsupported for overlapping IP ranges.
- Transitive routing not possible by default (need a router)
## Service Endpoints
### Key Components
- Subnet
  - Service Endpoints are configured on a per-subnet basis.
- Service Endpoint
  - Enabled for a specific **resource provider** for the given subnet.
- Routes
  - When configured, a **system route** is automatically generated.
## Private Link
### Key Components
- Private Endpoint
  - Network interface that is deployed to a subnet within a VNet.
- Resource
  - The target resource/sub-resource
  - Can be a different region
- DNS Integration
  - When configured a **Private DNS Zone** will use the private IP addressing.
## Resource Firewalls
### Key Components
  - Resource
    - Most Azure services built for public availability network restrictions
  - Network Rules
    - Once on, all traffic is blocked except what is allowed.
  - Exceptions
    - Can be enabled for the platform.
## VPN Gateway
### Site to Site VPN Configuration
- VNet Gateway (VPN)
  - Configured as **VPN Type** and Policy (static) or **route-based** routing
  - Local Network Gateway
  - **Remote networks** available via customer
  - VPN Device (Requires public IP)
  - VPN Connection
    - IPSec IKE encrypted tunnel
      - Encrypted using passphrase
### Point to Site (P2S) Configuration
- VNet Gateway (VPN)
  - Configured as VPN type, and Route-based routing
- Authentication
  - Cert-based, RADIUS, or AAD Auth.
- VPN Connection
  - Client required to establish the tunnel.
    - OpenVPN (SSL/TLS)
    - SSTP (TLS)
    - IPSec (IKEv2)
## ExpressRoute
### Key Components
On-Prem ----> Partner Edge ----> Microsoft Edge
- VNet Gateway
  - Configured as **ExpressRoute** type with BGP routing.
- ExpressRoute Circuit
  - Determines peering location/provider, bandwith, billing model, SKU
- ExpressRoute Peering
  - Microsoft: to public MS Services
  - Private: to one or more Azure VNets
###  Considerations
- Can coexist with VPN (not Basic SKU)
- Can support Fast Path (Ultra/ERGw3Az SKU)
- Premium supports cross-geography & greater limits.
## Virtual WAN
### Key Components
- Hub
  - One or more Microsoft managed VNets within a regioon.
- Hub Gateway
  - Microsoft-managed gateway that is deployed as part of the hub.
- Connections
  - Supports ER, S2S, P2S, VNet to VNet, and hub to hub connectivity.
## Azure DNS
### Public Zones
#### Key Components
- Public Zone
  - Collection of publicly available records to resolve names to IPs
- Records
  - Supports common DNS records
- Delegation
  - Your domain registrar NS records must point to Azure DNS.
### Private Zones
#### Key Components
- Private Zone
  - Can only be used by VNets for private IPs
- VNet Link
  - VNets must be linked to (at most one)  zone to use a Private Zone.
- Records
  - Registered automatically using VM Private IP, or created manually.
