# Azure Cost Optimization Reporting Tool (v1.02)
The Azure Cost Optimization Reporting Tool (ACORT) is a free, open-source tool designed to help Azure consumers improve the cost efficiency of their deployments. It performs a multi-subscription assessment of your Azure resources against Microsoft's cost optimization best practices defined in the [Well-Architected Framework](https://docs.microsoft.com/en-us/azure/architecture/framework/cost/) and [Cloud Adoption Framework](https://docs.microsoft.com/en-us/azure/cloud-adoption-framework/get-started/manage-costs). A recurring email report is generated containing optimizations for each subscription with associated cost data pulled from the previous month.

* Assess your Azure workloads against 32 Microsoft cost optimization best practices scoped to subscriptions, management groups, or the entire tenant.
* Get an efficiency score for each subscription and total cost optimization potential ($).
* Receive a recurring (weekly or monthly) email report.
* Leverage cost data to understand optimization potential and determine remediation priority.
* Incorporates all Azure Advisor recommendations.

## Table of Contents
* [Assessment Scope](#assessmentscope)
* [Change Log](#changelog)
* [Prerequisites](#prerequisites)

## <a id="assessmentscope"></a> Assessment Scope

### Azure Advisor
* Imports all Azure Advisor cost recommendations (reserved instances, VM SKU size etc.)

### Orphaned Resources
* Unattached Public IP addresses
* Unattached Managed Disks
* VMs deallocated for more than 90 days
* Snapshots older than 1 year
* Empty Availability Sets
* Unattached Network Interfaces
* Unattached Network Security Groups
* Empty Load Balancers

### Sentinel
* Sentinel Workspaces with a retention period configured beyond free period (> 90 days)
* Sentinel Workspaces not using an optimal commitment tier based on previous 31 days of ingestion

### Log Analytics
* Log Analytics Workspaces with a retention period configured beyond free period (> 31 days)
* Log Analytics Workspaces not using an optimal commitment tier based on average daily data ingestion
* Log Analytics workspaces using legacy Per-Node pricing tier

### Hybrid Benefit
* Windows VMs without Hybrid Benefit
* Windows VM Scale Sets without Hybrid Benefit
* SQL Databases not using Hybrid Benefit
* SQL Managed Instances not using Hybrid Benefit
* Red Hat Enterprise Linux VMs not using Hybrid Benefit
* SUSE Linux Enterprise Server VMs not using Hybrid Benefit

### Non-Production Subscription Optimizations
* No use of Dev/Test subscription offer
* VMs in Dev/Test subscriptions without an auto-shutdown schedule
* Recovery Services Vaults in Dev/Test subscriptions using Geo-Redundant Storage (GRS)
* Premium SKU Managed Disks in Dev/Test subscriptions
* Premium SKU Storage Accounts in Dev/Test subscriptions
* Storage Accounts using Zone-Redundant Storage in Dev/Test Subscriptions
* Storage Accounts using Geo-Redundant Storage in Dev/Test Subscriptions
* Storage Accounts using Geo-Zone-Redundant Storage in Dev/Test Subscriptions
* Storage Accounts using Read-Access Geo-Redundant Storage in Dev/Test Subscriptions
* Storage Accounts using Read-Access Geo-Zone-Redundant Storage in Dev/Test Subscriptions

### Virtual Machines
* VMs in 'Stopped' power state

### Storage Accounts
* Legacy v1 Storage Accounts
* Storage Accounts without data lifecycle management rules

## <a id="prerequisites"></a> Prerequisites
* A user with the `Contributor` role on a subscription to deploy the resources.
* A user with a mailbox to send the email report.
* A user with `User Access Administrator` or `Owner` on the subscriptions or management groups to be included in the assessment.
