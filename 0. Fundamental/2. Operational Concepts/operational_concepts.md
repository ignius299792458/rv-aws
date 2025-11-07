# Operational Concepts (Common Everywhere)

## 1. Provisioning Resources

Resources in AWS can be created and managed through multiple methods:

- **Console (UI)**: Web-based graphical interface for manual resource creation and management
- **CLI**: AWS Command Line Interface for scripted and command-based operations
- **SDKs**: Software Development Kits for programmatic resource management in various programming languages
- **IaC (Infrastructure as Code)**: Tools like CloudFormation (AWS native) and Terraform (multi-cloud) that allow you to define infrastructure in code files, enabling version control, repeatability, and automated deployments

**Use Case**: Choose the method based on your needs - Console for quick tests, CLI for automation scripts, SDKs for application integration, and IaC for production environments requiring consistency and versioning.

---

## 2. Tags

Tags are key-value pairs attached to AWS resources that provide metadata for:

- **Billing**: Organize and track costs by department, project, or environment
- **Organization**: Group and identify resources across your infrastructure
- **Automation**: Enable automated actions based on tag values (e.g., backup policies, resource lifecycle management)
- **Compliance**: Categorize resources for regulatory and governance requirements

**Best Practice**: Use consistent tagging strategies (e.g., `Environment: prod`, `Project: webapp`, `Owner: team-name`) across all resources for effective resource management.

---

## 3. Encryption

AWS Key Management Service (KMS) provides centralized encryption key management used across multiple services:

- **S3**: Encrypt objects at rest and in transit
- **RDS**: Encrypt databases and snapshots
- **EBS**: Encrypt volumes and snapshots
- **Other Services**: Lambda, EFS, Secrets Manager, and many more

**Key Types**:

- **AWS Managed Keys**: Automatically managed by AWS (free)
- **Customer Managed Keys (CMK)**: Full control over key policies and rotation
- **Customer Owned Keys**: Bring your own keys (BYOK) for external key management

**Benefits**: Data protection, compliance requirements, and defense-in-depth security strategy.

---

## 4. Monitoring & Logging

### CloudWatch

AWS's native monitoring and observability service providing:

- **Metrics**: Performance data from AWS services and custom applications
- **Alarms**: Automated notifications and actions based on metric thresholds
- **Dashboards**: Visual representation of metrics and logs
- **Logs**: Centralized log collection and analysis
- **Insights**: Automated anomaly detection and troubleshooting

### CloudTrail

API activity logging service for:

- **Auditing**: Track all API calls made to AWS services
- **Compliance**: Maintain records of who did what, when, and from where
- **Security**: Detect unauthorized access attempts and policy violations
- **Troubleshooting**: Review API call history to diagnose issues

**Integration**: CloudWatch and CloudTrail work together to provide comprehensive observability - CloudWatch for performance, CloudTrail for security and compliance.

---

## 5. High Availability & Fault Tolerance

AWS services are designed to support resilient architectures through:

- **Multi-AZ (Availability Zone)**: Deploy resources across multiple data centers within the same region to protect against single data center failures
- **Multi-Region**: Distribute resources across different geographic regions for disaster recovery and reduced latency
- **Auto Scaling**: Automatically adjust capacity based on demand
- **Load Balancing**: Distribute traffic across multiple resources
- **Backup & Replication**: Automated data replication and backup strategies

**Design Principle**: Design for failure - assume components will fail and build systems that continue operating despite failures.

**Common Patterns**:

- Active-Passive: Primary region active, secondary on standby
- Active-Active: Multiple regions serving traffic simultaneously
- Pilot Light: Minimal resources in secondary region, scale up on demand

---

## 6. Shared Responsibility Model

A security framework that divides responsibilities between AWS and the customer:

### AWS Responsibility (Security OF the Cloud)

- Physical infrastructure security
- Hardware and software of managed services
- Network infrastructure
- Hypervisor and host operating system
- Foundation services (compute, storage, database, networking)

### Customer Responsibility (Security IN the Cloud)

- Data encryption and classification
- Access management (IAM policies, user credentials)
- Application security and patching
- Network security (security groups, NACLs, firewalls)
- Operating system configuration (for EC2 instances)
- Client-side data protection

**Key Point**: The model varies by service type:

- **Infrastructure Services (EC2)**: Customer has more responsibility
- **Container Services (RDS, Lambda)**: AWS manages more, customer manages less
- **Abstracted Services (S3, DynamoDB)**: AWS manages most infrastructure

**Best Practice**: Understand your responsibilities for each service you use and implement appropriate security controls.
