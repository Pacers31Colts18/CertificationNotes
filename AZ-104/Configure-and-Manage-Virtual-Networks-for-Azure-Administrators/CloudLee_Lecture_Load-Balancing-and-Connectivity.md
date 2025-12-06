# Load Balancing and Connectivity
## Azure Load Balancer
- Distributes connectivity
- Removes from pool if any issues to VM on back-end pool
- Layer 4 Load Balancer
### Key Components
- Front End
  - 1 or more central public/private addresses to reach a solution by.
- Back End
  - Vms or VM Scale Set resources that host an instance of the solution.
- Probe
  - HTTP/HTTPS/TCP probes that check if an instance is healthy
**If using an NSG, allow rules need to be created for probes**
- Rules
  - Load Balances a front-end to a healthy back-end via a port. Can persist/float.
## Azure Load Balancer Considerations
### Special Considerations
- Sticky Sessions (Persistence)
  - Rules can be configured to ensure sessions stick.
- Matching SKUs
  - Public IP addressing to the same backend port in a balancer instance.
- Floating IPs
  - Allow load balancing to the same backend port in a backend instance.
- HA Ports
  - Load balance all protocols on all ports simultaneously.
### Load Balancer SKUs
- Basic
  - EOL 2025
  - 300 instances
  - Supports VMs in Availability Set or Virtual Machine Scale Set
  - HTTP/TCP Health Porbes
  - Region deployment only
  - Open by default. Requires NSG for security.
  - Doesn't support HA ports
  - No SLA
- Standard
  - 1000 instances
  - Supports any VM or Virtual Machine Scale Set from the same Vnet
  - HTTP/HTTPS/TCP Health Probes
  - Supports AZs (regional and global)
  - Traffic blocked by default
  - Supports HA ports
  - 99.9% SLA
## Application Gateway
- Layer 7
### Key Features
- Path based routing
- Multi site routing
- End to end encryption
- Web application firewall (SKU)
- Additional layer 7 features
- Integrated autoscaling
### Key Components
- Front-end
  - Public IP
  - Private IP
  - Both
- Back-end
  - Supports various Azure services that are either public or private
- Listeners and settings
  - Front: port, ssl, multi-site, etc.
  - Back: port, cookie affinity, draining, etc.
- Rules
  - Prioritized rules to tie all settings together.
  - Supports path based rules
## Azure Bastion
- Focused on system administration remote management tools
- Instead of opening all the ports
### Key Components
- Azure Bastion
  - Basic or Standard SKU.
  - Must be deployed to a special subnet
- Connectivity
  - Manage machines on connected networks.
  - Secure with NSG
- Client
  - Management connectivity is over TLS using the Azure portal as a client.
## Azure Firewall
- L3 to L7 connectivity policies
- Fully managed and scalable
- Integrated threat intelligence
- Intrusion detection and prevention
- URL Filtering and Web Categories
- TLS Inspection
### Key Components
- Firewall
  - Enforce rules
  - Deploy to Azure Firewall subnet
  - At least /26 subnet space
- Networking
  - Supports VNet to Vnet filtering/routing
  - Requires route table to be configured
- Firewall Policy
  - Configuration can be captured as a global resource with hierarchy.
