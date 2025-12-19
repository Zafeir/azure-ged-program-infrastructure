# Azure Naming Conventions

## Overview

This document defines the naming standards for all Azure resources in the GED/HSE Program Infrastructure project. Consistent naming improves organization, cost tracking, and operational management.

---

## General Principles

1. **Lowercase preferred** (except where Azure requires mixed case)
2. **Use hyphens** for readability (when allowed by resource type)
3. **Be descriptive** but concise
4. **Include environment** in all resource names (dev/staging/prod)
5. **Follow Azure naming rules** (each resource type has character limits and allowed characters)

---

## Naming Pattern

### Standard Format
```
[resource-abbreviation]-[project-name]-[purpose]-[environment]-[region]-[instance]
```

### Simplified Format (for resources with character limits)
```
[abbreviation][projectname][purpose][env][instance]
```

---

## Project Identifiers

| Component | Value | Usage |
|-----------|-------|-------|
| **Project Name** | `ged-program` or `gedprogram` | Full project identifier |
| **Project Abbreviation** | `ged` or `gp` | Short form for character-limited resources |
| **Environment** | `dev`, `staging`, `prod` | Deployment environment |
| **Region** | `eastus`, `westus2` | Azure region (when needed) |

---

## Resource Type Abbreviations

Following Microsoft's recommended abbreviations:

| Resource Type | Abbreviation | Example |
|---------------|--------------|---------|
| Resource Group | `rg` | `rg-ged-program-dev` |
| Virtual Network | `vnet` | `vnet-ged-program-dev` |
| Subnet | `snet` | `snet-ged-app-dev` |
| Network Security Group | `nsg` | `nsg-ged-web-dev` |
| Virtual Machine | `vm` | `vm-ged-app-dev-001` |
| Storage Account | `st` | `stgedprogramdev01` |
| SQL Database Server | `sql` | `sql-ged-program-dev` |
| SQL Database | `sqldb` | `sqldb-ged-students-dev` |
| App Service Plan | `asp` | `asp-ged-program-dev` |
| App Service / Web App | `app` | `app-ged-portal-dev` |
| Function App | `func` | `func-ged-intake-dev` |
| Logic App | `logic` | `logic-ged-workflow-dev` |
| Key Vault | `kv` | `kv-ged-secrets-dev` |
| Application Insights | `appi` | `appi-ged-program-dev` |
| Log Analytics Workspace | `log` | `log-ged-program-dev` |
| Azure Files Share | `share` | `share-ged-docs-dev` |
| Blob Container | `blob` | `blob-ged-documents` |
| Public IP Address | `pip` | `pip-ged-vm-dev` |
| Load Balancer | `lb` | `lb-ged-web-dev` |
| Network Interface | `nic` | `nic-ged-vm-dev-001` |
| Azure CDN Profile | `cdn` | `cdn-ged-program-dev` |
| Traffic Manager | `tm` | `tm-ged-program-prod` |

---

## Naming Examples by Resource Type

### Resource Groups
**Pattern:** `rg-[project]-[purpose]-[environment]`

```
rg-ged-program-dev          # Main development resource group
rg-ged-program-networking   # Networking resources
rg-ged-program-monitoring   # Monitoring and logging resources
rg-ged-program-prod         # Production resource group
```

---

### Storage Accounts
**Pattern:** `st[projectname][purpose][env][instance]`

**Rules:** 
- 3-24 characters
- Lowercase letters and numbers only
- NO hyphens or special characters
- Must be globally unique

```
stgedprogramdev01           # Main storage account (dev)
stgedprogramdocs01          # Document storage (dev)
stgedprogramlogs01          # Log storage (dev)
stgedprogramprod01          # Main storage account (prod)
```

---

### Virtual Machines
**Pattern:** `vm-[project]-[purpose]-[environment]-[instance]`

```
vm-ged-app-dev-001          # Application server (dev)
vm-ged-db-dev-001           # Database server (dev)
vm-ged-web-prod-001         # Web server (prod)
vm-ged-web-prod-002         # Web server (prod) - second instance
```

---

### Databases
**Pattern:** `sql-[project]-[purpose]-[environment]`

**Database Pattern:** `sqldb-[project]-[purpose]-[environment]`

```
sql-ged-program-dev         # SQL Server instance (dev)
sqldb-ged-students-dev      # Student records database
sqldb-ged-leads-dev         # Lead tracking database
sqldb-ged-analytics-dev     # Analytics database
```

---

### Networking Resources

**Virtual Networks:**
```
vnet-ged-program-dev-eastus     # Main VNet (dev)
vnet-ged-program-prod-eastus    # Main VNet (prod)
```

**Subnets:**
```
snet-ged-web-dev                # Web tier subnet
snet-ged-app-dev                # Application tier subnet
snet-ged-db-dev                 # Database tier subnet
snet-ged-bastion-dev            # Azure Bastion subnet
```

**Network Security Groups:**
```
nsg-ged-web-dev                 # Web tier NSG
nsg-ged-app-dev                 # App tier NSG
nsg-ged-db-dev                  # Database tier NSG
```

---

### App Services & Functions

**App Service Plans:**
```
asp-ged-program-dev             # Dev app service plan
asp-ged-program-prod            # Prod app service plan
```

**Web Apps:**
```
app-ged-portal-dev              # Main web portal (dev)
app-ged-intake-dev              # Intake form application (dev)
```

**Function Apps:**
```
func-ged-intake-dev             # Intake form processing
func-ged-notifications-dev      # Notification sender
func-ged-workflows-dev          # Workflow automation
```

---

### Serverless & Integration

**Logic Apps:**
```
logic-ged-qualified-lead-dev    # Qualified lead workflow
logic-ged-nonqualified-dev      # Non-qualified lead workflow
logic-ged-document-upload-dev   # Document upload workflow
logic-ged-employment-match-dev  # Employment matching workflow
```

---

### Security & Monitoring

**Key Vault:**
```
kv-ged-secrets-dev              # Secrets and certificates (dev)
kv-ged-secrets-prod             # Secrets and certificates (prod)
```

**Application Insights:**
```
appi-ged-portal-dev             # Portal monitoring
appi-ged-functions-dev          # Functions monitoring
appi-ged-program-prod           # Production monitoring
```

**Log Analytics:**
```
log-ged-program-dev             # Centralized logging (dev)
log-ged-program-prod            # Centralized logging (prod)
```

---

### Storage Components

**File Shares:**
```
share-ged-documents-dev         # Document file share
share-ged-backups-dev           # Backup file share
```

**Blob Containers:**
```
blob-ged-student-docs           # Student document storage
blob-ged-intake-forms           # Intake form submissions
blob-ged-marketing-assets       # Marketing materials
blob-ged-backups                # Backup storage
```

---

## Tags Strategy

All resources should be tagged with the following:

| Tag Name | Purpose | Example Values |
|----------|---------|----------------|
| `Environment` | Deployment environment | `dev`, `staging`, `prod` |
| `Project` | Project identifier | `ged-program` |
| `Owner` | Person responsible | `[Your Name]` |
| `CostCenter` | For cost allocation | `marketing`, `operations`, `it` |
| `Purpose` | Specific function | `web-app`, `database`, `storage` |
| `CreatedDate` | When resource was created | `2024-12-19` |
| `ManagedBy` | Management method | `manual`, `bicep`, `terraform` |

### Example Tag Set
```json
{
  "Environment": "dev",
  "Project": "ged-program",
  "Owner": "Your Name",
  "CostCenter": "it",
  "Purpose": "student-database",
  "CreatedDate": "2024-12-19",
  "ManagedBy": "bicep"
}
```

---

## Special Naming Considerations

### Character Limits
Some Azure resources have strict character limits:
- **Storage accounts:** 3-24 characters
- **Key Vault:** 3-24 characters
- **SQL Server:** 1-63 characters
- **VM names:** 1-64 characters (Windows), 1-64 characters (Linux)

When hitting limits, prioritize:
1. Resource type abbreviation
2. Project identifier
3. Environment
4. Instance number

### Globally Unique Names
These resources must be globally unique across ALL of Azure:
- Storage accounts
- Key Vaults
- App Services
- Function Apps
- CDN profiles

**Strategy:** Add your initials or a random number if your preferred name is taken
```
stgedprogramdev01      # If taken...
stgedprogramdevjd01    # Add initials
stgedprogramdev4721    # Or add random digits
```

---

## Environment Suffixes

| Environment | Suffix | Purpose |
|-------------|--------|---------|
| **Development** | `dev` | Learning, testing, experimentation |
| **Staging** | `staging` | Pre-production validation (if implemented) |
| **Production** | `prod` | Live production systems (if implemented) |

For this portfolio project, we'll primarily use `dev` environment.

---

## Instance Numbering

When you need multiple instances of the same resource type:

**Pattern:** `-001`, `-002`, `-003`

```
vm-ged-web-dev-001
vm-ged-web-dev-002
vm-ged-web-dev-003
```

**Why 3 digits?**
- Allows for up to 999 instances
- Maintains alphabetical sorting
- Professional standard

---

## Quick Reference Checklist

Before creating any Azure resource, verify:

- [ ] Does the name follow the standard pattern?
- [ ] Is the environment suffix included (`dev`)?
- [ ] Is it within the character limit for that resource type?
- [ ] Does it use allowed characters only?
- [ ] Will it be globally unique (if required)?
- [ ] Are appropriate tags defined?
- [ ] Is it documented in the naming log?

---

## Naming Log

Track all created resources in `docs/resource-inventory.md` with:
- Resource name
- Resource type
- Purpose
- Creation date
- Status (active/deleted)

---

## References

- [Microsoft Azure Naming Conventions Best Practices](https://docs.microsoft.com/en-us/azure/cloud-adoption-framework/ready/azure-best-practices/naming-and-tagging)
- [Azure Resource Naming Rules and Restrictions](https://docs.microsoft.com/en-us/azure/azure-resource-manager/management/resource-name-rules)

---

**Last Updated:** December 19, 2024  
**Version:** 1.0  
**Status:** Active
