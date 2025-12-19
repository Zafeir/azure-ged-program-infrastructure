# Architecture Decision Records (ADR)

This document tracks key architectural decisions made during the design and implementation of the GED/HSE Program Cloud Infrastructure.

---

## ADR-001: Cloud Platform Selection

**Date:** December 19, 2024  
**Status:** Accepted  
**Decision Maker:** [Your Name]

### Context
Need to select a cloud platform for rebuilding the program's digital infrastructure as a learning project and portfolio piece while preparing for Azure certifications.

### Decision
Selected **Microsoft Azure** as the cloud platform.

### Rationale
- Aligns with AZ-900 and AZ-104 certification path
- Strong enterprise identity and access management (Azure AD/Entra ID)
- Excellent RBAC capabilities for complex permission requirements
- Comprehensive compliance certifications (important for educational data)
- Free tier available for learning and development
- Strong integration between services (Functions, Logic Apps, Storage, etc.)

### Consequences
**Positive:**
- Hands-on experience directly supports certification studying
- Azure's RBAC is industry-leading for complex permission scenarios
- Portfolio demonstrates skills in most enterprise-adopted cloud platform

**Negative:**
- Locked into Azure ecosystem (not multi-cloud)
- Some services have learning curve compared to simpler alternatives

---

## ADR-002: Static Website Hosting Approach

**Date:** December 19, 2024  
**Status:** Accepted

### Context
Need to host the marketing landing page and intake form with global delivery and low cost.

### Decision
Use **Azure Storage Static Website** with **Azure CDN** for content delivery.

### Rationale
- Extremely cost-effective (~$1-2/month for low-traffic site)
- No server management required
- Built-in HTTPS support
- Azure CDN provides global edge locations for fast loading
- Simple deployment process
- Sufficient for marketing landing page requirements

### Alternatives Considered
1. **Azure App Service**
   - ❌ More expensive (~$13+/month)
   - ❌ Overkill for static content
   - ✅ Would provide easier dynamic content if needed later

2. **Azure VM with web server**
   - ❌ Highest cost
   - ❌ Most management overhead
   - ❌ Not appropriate for simple landing page

### Consequences
**Positive:**
- Minimal cost impact on free credit budget
- Fast global delivery of marketing pages
- No server patching or maintenance required
- Scales automatically

**Negative:**
- Limited to static content (HTML/CSS/JS)
- Dynamic form processing requires separate Azure Functions

---

## ADR-003: Form Processing Architecture

**Date:** December 19, 2024  
**Status:** Accepted

### Context
Need to process intake form submissions, perform qualification logic, and trigger automated workflows.

### Decision
Use **Azure Functions** for form processing with **Azure Logic Apps** for workflow orchestration.

### Rationale
- **Azure Functions:**
  - Serverless (pay only for executions)
  - Scales automatically
  - Perfect for event-driven form submissions
  - Can integrate with any backend service

- **Logic Apps:**
  - Visual workflow designer (easier to understand and modify)
  - Built-in connectors for email, database, notifications
  - No-code/low-code approach for business logic
  - Clear visibility into workflow execution

### Workflow
```
Form Submission
    ↓
Azure Function (validates and stores data)
    ↓
Triggers Logic App
    ↓
Qualification Check (Logic App condition)
    ↓
Branch: Qualified / Not Qualified
    ↓
Send appropriate email
Create task for staff
Update database
```

### Consequences
**Positive:**
- Very low cost (free tier covers learning usage)
- Clear separation of concerns (processing vs orchestration)
- Easy to modify workflows without code changes
- Demonstrates serverless architecture understanding

**Negative:**
- Logic Apps can be complex for very intricate logic
- Debugging across Functions + Logic Apps requires understanding both

---

## ADR-004: Database Selection

**Date:** December 19, 2024  
**Status:** Accepted

### Context
Need to store student records, lead data, and application information with strong security and compliance features.

### Decision
Use **Azure SQL Database** (Basic tier for development, scalable for production).

### Rationale
- Familiar SQL syntax (easier learning curve)
- Strong security features (encryption, auditing, threat detection)
- Built-in backup and recovery
- RBAC integration with Azure AD
- Compliance certifications for educational data
- Dynamic Data Masking for sensitive fields
- Row-Level Security possible for multi-tenant scenarios

### Alternatives Considered
1. **Azure Cosmos DB**
   - ❌ More expensive
   - ❌ NoSQL model unnecessary for structured student data
   - ✅ Would be better for global distribution (not required here)

2. **Azure Database for PostgreSQL/MySQL**
   - ✅ Viable alternative, slightly cheaper
   - ❌ Less integrated with Azure ecosystem
   - ❌ Fewer built-in security features

### Consequences
**Positive:**
- Industry-standard relational model for structured data
- Excellent security and compliance features
- Easy to query and report on
- Scales as program grows

**Negative:**
- Slightly more expensive than open-source alternatives
- Need to manage schema and migrations

---

## ADR-005: Document Storage Approach

**Date:** December 19, 2024  
**Status:** Accepted

### Context
Need to securely store sensitive documents (SS cards, birth certificates, transcripts) with role-based access and compliance.

### Decision
Use **Azure Blob Storage** with private containers and **Azure AD authentication**.

### Rationale
- Designed for unstructured data (PDFs, images, scans)
- Encryption at rest automatically enabled
- Fine-grained access control via RBAC
- Soft delete for recovery
- Versioning available
- Cost-effective storage (~$0.02/GB/month for hot tier)
- Lifecycle management for tiering to cool/archive storage

### Security Implementation
- Private containers (no anonymous access)
- Azure AD authentication required
- Separate containers for different document types
- RBAC permissions map to staff roles
- Audit logging enabled
- Immutability policies for compliance

### Alternatives Considered
1. **Azure Files**
   - ✅ Good alternative, SMB protocol support
   - ❌ Slightly more expensive
   - ✅ Easier for file share scenarios (not needed here)

2. **SharePoint Online**
   - ✅ Better collaboration features
   - ❌ Outside Azure ecosystem
   - ❌ More complex integration

### Consequences
**Positive:**
- Purpose-built for document storage
- Excellent cost-to-storage ratio
- Strong security and compliance features
- Can set retention policies

**Negative:**
- Requires managing access policies per container/blob
- No built-in document preview (need separate service)

---

## ADR-006: Identity and Access Management

**Date:** December 19, 2024  
**Status:** Accepted

### Context
Six different staff roles require distinct access levels to different data types and systems. Must ensure least-privilege access and maintain audit trail.

### Decision
Implement **Azure AD (Entra ID)** with **custom RBAC roles** and **Conditional Access policies**.

### Rationale
- Azure AD natively integrates with all Azure services
- Custom roles can define precise permissions
- Conditional Access enforces MFA and device compliance
- Privileged Identity Management (PIM) for admin access
- Complete audit logging
- Single sign-on across all systems

### RBAC Strategy
- Create 6 custom roles mapping to staff positions
- Use Azure AD groups for role assignment
- Implement least-privilege principle
- Regular access reviews (quarterly simulation)

### Security Enhancements
- MFA required for all users
- Conditional Access: require compliant devices for sensitive data
- PIM: admin roles require justification and approval
- Sign-in risk policies
- Impossible travel detection

### Consequences
**Positive:**
- Industry-standard identity management
- Granular control over permissions
- Strong audit trail for compliance
- Simplified user management

**Negative:**
- More complex initial setup
- Requires understanding of Azure AD concepts

---

## ADR-007: Monitoring and Analytics Strategy

**Date:** December 19, 2024  
**Status:** Accepted

### Context
Need visibility into system performance, security events, costs, and business metrics across multiple stakeholder perspectives.

### Decision
Implement **Application Insights** for application monitoring, **Azure Monitor** for infrastructure, and **Power BI** for business analytics.

### Rationale
**Application Insights:**
- Tracks page views, form submissions, campaign sources
- Performance monitoring
- Custom events for business metrics
- Real-time analytics

**Azure Monitor:**
- Infrastructure health and performance
- Alert rules for failures or anomalies
- Log aggregation
- Security event monitoring

**Power BI:**
- Role-specific dashboards
- Marketing analytics (leads, costs, ROI)
- Operational metrics (processing times, document status)
- Executive dashboards (enrollment, placement, costs)

### Dashboard Strategy
Create separate Power BI dashboards for each role:
- **Marketing Manager:** Campaign performance, lead sources, qualification rates
- **Program Director:** Overall program health, enrollment trends, outcomes
- **Office Manager:** Document completion, appointment scheduling
- **Program Manager:** Student progress, employment matching

### Consequences
**Positive:**
- Comprehensive visibility across all layers
- Each role sees only relevant metrics
- Data-driven decision making
- Demonstrates analytics capabilities

**Negative:**
- Multiple tools to learn and configure
- Requires setting up data connections

---

## ADR-008: Infrastructure as Code Approach

**Date:** December 19, 2024  
**Status:** Accepted

### Context
Need repeatable, version-controlled infrastructure deployment for learning, documentation, and potential disaster recovery.

### Decision
Use **Azure Bicep** for infrastructure as code.

### Rationale
- Native Azure IaC language (better than ARM JSON)
- Cleaner syntax than ARM templates
- Compiles to ARM for deployment
- Better IDE support and validation
- Microsoft's recommended approach
- Version control via Git

### Structure
```
infrastructure/
├── main.bicep              # Entry point, references modules
├── modules/
│   ├── networking.bicep    # VNets, NSGs, etc.
│   ├── compute.bicep       # VMs, App Services
│   ├── storage.bicep       # Storage accounts, containers
│   ├── database.bicep      # SQL Database
│   ├── identity.bicep      # Azure AD resources
│   └── monitoring.bicep    # App Insights, alerts
└── parameters/
    ├── dev.parameters.json
    └── prod.parameters.json
```

### Alternatives Considered
1. **Terraform**
   - ✅ Multi-cloud support
   - ❌ Not learning Terraform right now (focusing on Azure certs)
   - ❌ Additional tool to learn

2. **ARM Templates (JSON)**
   - ✅ Native Azure
   - ❌ Verbose and hard to read
   - ❌ Microsoft recommends Bicep instead

### Consequences
**Positive:**
- Complete infrastructure documentation in code
- Can rebuild entire environment from scratch
- Version control shows evolution of design
- Demonstrates modern DevOps practices

**Negative:**
- Learning curve for Bicep syntax
- Must keep code synchronized with manual changes

---

## ADR-009: Cost Optimization Strategy

**Date:** December 19, 2024  
**Status:** Accepted

### Context
Working with $200 free credit over 22 days. Must demonstrate cost-conscious architecture while building functional system.

### Decision
Implement **multi-layered cost optimization** with monitoring and automation.

### Strategies

**1. Right-Sizing**
- Use smallest viable SKUs (B-series VMs, Basic SQL tier)
- Scale up only when demonstrating performance needs

**2. Auto-Shutdown**
- VMs automatically shut down at night
- Logic Apps pause during non-business hours
- Development resources deleted when not actively learning

**3. Storage Tiering**
- Hot tier for active documents
- Cool tier for documents >90 days old
- Archive tier for retention-only documents

**4. Reserved Capacity**
- In production: would use reserved instances
- Document cost savings (30-70% reduction)

**5. Monitoring**
- Azure Cost Management budgets and alerts
- Daily cost review
- Advisor recommendations followed

### Cost Tracking
- Tag all resources with: Environment, Project, Owner, CostCenter
- Weekly cost analysis by service
- Document cost trends and optimizations

### Consequences
**Positive:**
- Demonstrates financial responsibility
- Real-world cost optimization skills
- Stays within free credit budget
- Provides concrete savings numbers for resume

**Negative:**
- Auto-shutdown can interrupt demos
- Smallest SKUs may have performance limitations

---

## ADR-010: Disaster Recovery Approach

**Date:** December 19, 2024  
**Status:** Planned

### Context
Production systems require business continuity planning. Need to demonstrate understanding of RTO/RPO concepts.

### Decision
Implement **Azure Site Recovery** with documented failover procedures.

### Approach
- **Primary Region:** East US
- **Secondary Region:** West US 2
- **RTO Target:** 15 minutes
- **RPO Target:** 1 hour

### Components
- Azure Site Recovery for VM replication
- Geo-redundant database backups
- Traffic Manager for automatic failover
- Documented runbook for manual failover

### Testing
- Test failover quarterly (simulated)
- Document results and lessons learned
- Update runbooks based on tests

### Consequences
**Positive:**
- Demonstrates enterprise-level thinking
- Shows understanding of business continuity
- Differentiates from basic tutorials

**Negative:**
- Additional complexity and cost
- Requires maintaining two regions

---

## Decision Log Summary

| ADR | Decision | Status | Impact |
|-----|----------|--------|--------|
| 001 | Microsoft Azure platform | Accepted | Foundation |
| 002 | Static website + CDN | Accepted | Cost-effective |
| 003 | Functions + Logic Apps | Accepted | Serverless |
| 004 | Azure SQL Database | Accepted | Security-focused |
| 005 | Blob Storage for documents | Accepted | Compliant |
| 006 | Azure AD + Custom RBAC | Accepted | Security |
| 007 | Multi-tool monitoring | Accepted | Visibility |
| 008 | Bicep IaC | Accepted | Repeatability |
| 009 | Cost optimization | Accepted | Budget-conscious |
| 010 | Site Recovery DR | Planned | Enterprise-ready |

---

*Architecture decisions are living documents. As implementation progresses, decisions may be revisited based on learnings, constraints, or changing requirements.*

**Last Updated:** December 19, 2024
