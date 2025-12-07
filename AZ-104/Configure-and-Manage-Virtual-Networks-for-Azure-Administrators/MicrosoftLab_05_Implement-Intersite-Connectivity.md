# Lab 05 - Implement Intersite Connectivity
## Tasks
- Task 1: Create a virtual machine in a virtual network.
  - Resource Group: az104-rg5
    - Virtual Machine Name: CoreServicesVM
    - Virtual Network Name: CoreServicesVnet
      - Address Range: 10.0.0.0/16
      - Subnet Name: Core
      - Subnet Address Range: 10.0.0.0/24
- Task 2: Create a virtual machine in a different virtual network.
  - Resource Group: az104-rg5
    - Virtual Machine Name: ManufacturingVM
    - Virtual Network Name: ManufacturingVNet
      - Address Range: 172.16.0.0/16
      - Subnet Name: Manufacturing
      - Subnet Address Range: 172.16.0.0/24
- Task 3: Use Network Watcher to test the connection between virtual machines.
- Task 4: Configure virtual network peerings between different virtual networks.
- Task 5: Use Azure PowerShell to test the connection between virtual machines.
- Task 6: Create a custom route.
