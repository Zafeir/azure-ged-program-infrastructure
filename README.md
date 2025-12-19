Azure GED/HSE Program Cloud Infrastructure
Project Overview
This project demonstrates enterprise-level cloud infrastructure design for an educational enrollment program, featuring multi-channel marketing integration, role-based access control, automated workflows, and compliance with FERPA requirements.
Built with: Microsoft Azure | Bicep/ARM Templates | Power BI | Azure Functions | Logic Apps

Business Context
In my previous role managing enrollment and marketing for a GED/HSE program, I oversaw a complete digital infrastructure handling:

Multi-channel marketing campaigns across Meta (Facebook/Instagram), Google Ads, bus advertisements, and print materials
Lead generation and qualification processing hundreds of prospects monthly
Sensitive student data management including personal documents, educational records, and compliance tracking
Role-based access requirements for 6 different staff positions with varying permission levels
Automated workflows for enrollment, document verification, and employment placement

This project recreates that infrastructure using modern Azure services, demonstrating cloud architecture, security, compliance, and business process automation.

Architecture
High-Level Components
Marketing & Lead Generation Layer

Static website on Azure Storage with CDN
Multi-channel campaign tracking via Application Insights
Azure Functions for form processing
Logic Apps for automated lead qualification workflows

Data & Document Management

Azure SQL Database for student records
Azure Files/Blob Storage for sensitive documents
Encryption at rest and in transit
Audit logging for compliance

Identity & Access Management

Azure AD (Entra ID) with 6 custom roles
Role-Based Access Control (RBAC) across all resources
Multi-Factor Authentication (MFA)
Privileged Identity Management (PIM)
Conditional Access policies

Analytics & Monitoring

Power BI dashboards (role-specific views)
Azure Monitor with custom alerts
Application Insights for performance tracking
Cost Management and optimization

Business Process Automation

Automated qualified/non-qualified lead workflows
Document upload and verification processes
Employment opportunity matching
Email notifications and task management


Role-Based Access Control Implementation
Custom Azure Roles Defined
RoleAccess LevelPermissionsProgram DirectorFull AccessAll student data, documents, educational records, employment tracking, system administrationOffice ManagerFull Personal DataAll personal documents, student contact info, limited educational data accessProgram ManagerEducational FocusEducational history, test scores, employment documentation, prerequisite verificationCase ManagerOperationalStudent login credentials, basic information, application status - no sensitive documentsMarketing ManagerAnalytics OnlyLead data, campaign metrics, qualification rates - no individual student PIIIntake CoordinatorFront-EndInitial intake forms, basic student info, pre-enrollment data only

Security & Compliance

Encryption: All data encrypted at rest (AES-256) and in transit (TLS 1.2+)
Authentication: Multi-Factor Authentication enforced for all users
Access Control: Least-privilege access model with conditional access policies
Audit Logging: Complete audit trail of all data access and modifications
Compliance: FERPA-aligned data handling and retention policies
Network Security: Network Security Groups (NSGs) and Azure Firewall rules


Business Impact
Metrics & Results

Cost Optimization: [To be calculated] % reduction through right-sizing and auto-scaling
Processing Time: Automated workflows reduce manual processing time by [estimated] hours/week
Security: Zero-trust architecture with role-based access eliminates unauthorized data exposure
Scalability: Infrastructure handles 10x traffic spikes during campaign launches
Compliance: Automated audit logging ensures FERPA compliance documentation


Technical Implementation
Azure Services Used

Compute: Azure App Service, Azure Functions, Virtual Machines
Storage: Azure Storage (Blob, Files), Azure SQL Database
Networking: Virtual Networks, NSGs, Azure CDN, Traffic Manager
Identity: Azure AD (Entra ID), RBAC, PIM, Conditional Access
Integration: Azure Logic Apps, Azure Automation
Analytics: Application Insights, Azure Monitor, Power BI
Security: Azure Key Vault, Azure Security Center, Microsoft Defender
DevOps: Azure DevOps, GitHub Actions, Bicep/ARM Templates

Infrastructure as Code
All infrastructure is defined in Bicep templates for:

Repeatable deployments
Version control
Disaster recovery
Environment consistency (dev/staging/prod)


Repository Structure
├── README.md
├── architecture/
│   ├── diagrams/           # Architecture and workflow diagrams
│   ├── decisions.md        # Architectural decision records
│   └── business-context.md # Detailed business requirements
├── infrastructure/
│   ├── bicep/             # Bicep templates for all resources
│   ├── scripts/           # Deployment and management scripts
│   └── deployment-guide.md
├── security/
│   ├── rbac-setup.md      # RBAC configuration details
│   ├── compliance.md      # Compliance checklist and documentation
│   └── audit-logs.md      # Audit logging configuration
├── workflows/
│   ├── logic-apps/        # Logic App definitions
│   └── functions/         # Azure Functions code
├── analytics/
│   ├── power-bi/          # Power BI dashboard files
│   └── dashboards.md      # Dashboard documentation
├── costs/
│   ├── analysis.md        # Cost analysis and breakdowns
│   └── optimization.md    # Cost optimization strategies
└── docs/
    ├── setup-guide.md     # Step-by-step setup instructions
    └── lessons-learned.md # Project insights and learnings

Getting Started
Prerequisites

Azure subscription (free tier available)
Azure CLI installed
PowerShell 7+ or Bash
Git installed

Quick Deploy
bash# Clone repository
git clone https://github.com/zafeir/azure-ged-program-infrastructure.git
cd azure-ged-program-infrastructure

# Login to Azure
az login

# Deploy infrastructure
cd infrastructure/bicep
az deployment group create --resource-group rg-ged-program --template-file main.bicep
Detailed setup instructions available in docs/setup-guide.md

Learning Objectives
This project demonstrates proficiency in:

Cloud Architecture: Designing scalable, secure multi-tier applications
Identity & Access Management: Implementing enterprise-grade RBAC and zero-trust security
Compliance: Understanding data privacy regulations and implementing controls
Automation: Building business process automation with serverless technologies
DevOps: Infrastructure as Code and CI/CD practices
Cost Management: Optimizing cloud spending while maintaining performance
Analytics: Building data-driven dashboards for business insights


Certifications

Microsoft Azure Fundamentals (AZ-900) - [Date]
Microsoft Azure Administrator (AZ-104) - In Progress


Contact
Moises Arias

LinkedIn: https://www.linkedin.com/public-profile/settings?trk=d_flagship3_profile_self_view_public_profile
Email: Moisesoarias1@gmail.com


License
This project is licensed under the MIT License - see the LICENSE file for details.

Acknowledgments
This project was inspired by real-world experience managing digital infrastructure for educational programs, with a focus on demonstrating how cloud technologies solve actual business challenges while maintaining security and compliance.

If you find this project helpful, please consider giving it a star!
Last Updated: December 2025
