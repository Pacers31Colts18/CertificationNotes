# Monitoring
## Azure Monitor Overview
### Key Products and Features
- Azure Monitor
  - Cetnralized
  - Cloud and Hybrid
  - Apps to Tenants
  - Fully managed
  - Monitoring data
    - Metrics Explorer
    - Log Routing
  - Monitor Alerts
    - Alerts
    - Actions
  - Azure Monitor Logs
    - aka Log Analytics
    - KQL
  - Insights
    - Apps
    - VMs
    - Containers
    - Networks
    - continually growing list
  ### Monitoring Data Overview
  - Data Sources
    - Apps
      - App Insights
    - OS
      - VM Agent
    - Resources
      - Platform provided
    - Subscription
      - Activity Log
    - Tenant
      - AAD Reports
  - Data Types
    - Metrics
      - Small numeric information over time
        - CPU utilization
        - Storage requests
        - Page load time
    - Logs
      - Repo events
      - Storage reads
      - DB errors
  - Data Usage
    - Analyze
      - Azure Monitor Logs
    - Visualize
      - Metrics Explorer
    - Respond
      - Alerts
    - Integrate
### Diagnostic Settings
#### Routing Platform Logs & Metrics
- Platform Data
  - Metrics and Logs emitted by the platform can be routed
- Diagnostic Settings
  - Select the Metrics and Log data that needs to be routed
- Destination
  - Send to Log Analytics, Azure Storage, Event Hubs, or Partner Solutions
  - 0-365 days (0 = Infinite)
  ### Data Collection Rules
  #### Routing OS Metrics and Logs
  - Azure Monitor Agent
    - Supports Windows/Linux both in Azure and on-prem (Arc Enabled)
  - Data Collection Rule
    - Define the data source and (optional) Data Collection Endpoint
  - Azure Monitor Logs
    - An Azure Monitor Logs Workspace is required for the data destination.
## Activity Log
- Azure Tools and Apps
  - Portal
    - Power off VM
  - Powershell
  - Azure CLI
    - List Account Keys
  - SDK
- ARM Rest API
  - Subscriptions
  - Deployments
  - Resources
  - Tags
  - Tenants
- Azure Tools and Apps ----> ARM REST API
### Key Features
- Logs subscription-level operations performed via the ARM REST API
- Covers REST write operations (PUT, POST, DELETE) for each subscription
- Provides up to 90 days worth of data, without any further configuration
- Supports Diagnostic Settings routing to Storage, Monitor Logs, and Event Hubs
## Azure Monitor Logs Overview
### Overview
- Monitor Logs Workspace (Log Analytics Workspace)
  - Stored in **Tables**
    - App Events
    - Event
    - SysLog
    - Heartbeat
    - Alert
  - Once stored:
    - Workbooks
    - Queries
    - Integrations
### Implementation Tasks
1. Workspace
   - The Log Analytics Workspace is the storage repository and permiter for analytics.
2. Data Sources
   - Connect OS with agents, route with Diagnostic Settings, or integrate with other services.
3. Analyze
    - KQL underpins analytics capabilities
### KQL
- Count
  - Count the number of records
```powershell
Event 
| count
```
- Filter
  - Filter results based on conditions
```powershell
Event
| where EventLevelName == "Error"
```
- Summarize
  - Aggregate the information in a table
```powershell
Heartbeat
| where TimeGenerated >ago(1h)
| summarize count() by Computer
```
## Azure Monitor Alerts
- Resources ----> Monitoring Data -----> Alerts -----> Actions
### Alert Rules
#### Key Elements
- Condition
  - Evaluate a Resource for a Signal for the specified Scope.
- Action Group
  - Notification and/or Action to be triggered if the Condition is true.
    - Email/phone/sms
    - Azure Automation
    - API actions
    - very flexible
- Alert
  - Alert is created/logged when an Alert Rule is triggered.
### Key Considerations
- Alerts are throttled
  - 1 SMS/Call every 5 minutes
  - 100 emails per hour
- Some basic alert management capabilities are included
  - open/close/comments/etc
- Queries from Azure Monitor Logs can be saved and used for Azure Monitor Alerts
## Network Watcher
- Monitoring Netwokrs
  - Various tols and features to centrally monitor your networked solutions and services
  - Monitoring
  - Diagnostics
  - Logging
- Network Watcher Resource
  - Automatically enabled regional instances
### Monitoring Features
- Topology
  - Network map automatically generated to illustrate network relationships.
- Connection Monitor
  - Monitor connectivity and latency between endpoints (inside/outside of Azure)
### Diagnostic Features
- IP Flow Verify (NSG)
  - Determine whether packets for a VM are blocked or allowed by an NSG.
- Effective Security Rules (NSG)
  - View the collection of NSG security rules that are applied to a VM/NIC.
- Next Hop
  - Determine the path a packet will take from source to destination (routing)
- Packet Capture
  - Capture all network packet data sent to or from a VM (capture to VM or Azure Storage)
- Connection Troubleshooting
  - Perform direct TCP/ICMP checks from a VM, Bastion, or App Gateway to a VM/FQDN/IP
- VPN Troubleshoot
  - Capture detailed diagnostics like connection stats, CPU/memory info, IKE errors, etc.
### Logging Features
- NSG Flow Logs
  - Detailed logging of all IP flows going in and out of an NSG (captured every 1min to JSON)
- Traffic Analysis
  - Aggregates data to provide insights around security, hot-spots, connectivity, etc.
  - 