# Core AWS Concepts

## 1. Regions & Availability Zones (AZs)

### Overview

AWS infrastructure is organized geographically into **Regions** and **Availability Zones** to provide high availability, fault tolerance, and low latency.

### Regions

- **Definition**: A geographical area containing multiple isolated data centers
- **Example**: `us-east-1` (N. Virginia), `eu-west-1` (Ireland), `ap-south-1` (Mumbai)
- **Characteristics**:
  - Each region is completely independent and isolated
  - Regions are separated by significant geographical distance
  - Data replication across regions is not automatic
  - Pricing may vary by region
- **Selection Criteria**:
  - Latency requirements (proximity to users)
  - Compliance and data residency requirements
  - Service availability (not all services available in all regions)
  - Cost considerations

### Availability Zones (AZs)

- **Definition**: One or more discrete data centers within a region, each with redundant power, networking, and connectivity
- **Characteristics**:
  - Each AZ is isolated from failures in other AZs
  - Connected through low-latency, high-throughput, and highly redundant networking
  - Typically 2-6 AZs per region
  - AZs are physically separated within a region
- **Use Cases**:
  - High availability deployments (multi-AZ)
  - Disaster recovery
  - Load distribution
  - Data replication

### Key Considerations

- **Resource Placement**: Most AWS services ask "In which region do you want this resource?"
- **Data Transfer**: Cross-region data transfer incurs costs
- **Service Availability**: Some services are region-specific
- **Compliance**: Choose regions based on data residency requirements

---

## 2. Resource Identifiers

### ARN (Amazon Resource Name)

- **Definition**: A unique identifier for any AWS resource
- **Format**: `arn:partition:service:region:account-id:resource-type/resource-id`
- **Components**:
  - **Partition**: Usually `aws` (can be `aws-cn` for China, `aws-us-gov` for GovCloud)
  - **Service**: The AWS service (e.g., `s3`, `iam`, `lambda`)
  - **Region**: The region where the resource resides (can be empty for global services)
  - **Account ID**: The 12-digit AWS account ID
  - **Resource**: The resource identifier (format varies by service)

### Examples

- **S3 Bucket**: `arn:aws:s3:::my-bucket-name`
- **IAM User**: `arn:aws:iam::123456789012:user/john`
- **Lambda Function**: `arn:aws:lambda:us-east-1:123456789012:function:my-function`
- **EC2 Instance**: `arn:aws:ec2:us-east-1:123456789012:instance/i-1234567890abcdef0`

### Use Cases

- **IAM Policies**: Reference resources by ARN
- **Resource Tagging**: Identify resources across services
- **Cross-Service Integration**: Reference resources in different services
- **Auditing & Logging**: Track resource usage and access

### Other Identifiers

- **Resource IDs**: Service-specific identifiers (e.g., EC2 instance IDs)
- **Tags**: Key-value pairs for resource organization and management

---

## 3. IAM (Identity & Access Management)

### Overview

IAM is the foundation of AWS security, controlling who can access what resources and how.

### Core Concepts

#### Users

- **Definition**: Individual accounts representing people or applications
- **Characteristics**:
  - Unique username and credentials
  - Can have access keys for programmatic access
  - Can belong to multiple groups
  - Can have inline or attached policies

#### Groups

- **Definition**: Collections of users with shared permissions
- **Characteristics**:
  - Users can belong to multiple groups
  - Groups cannot contain other groups
  - Policies attached to groups apply to all members
  - Simplifies permission management

#### Roles

- **Definition**: Temporary credentials assumed by users, services, or applications
- **Characteristics**:
  - No permanent credentials (password or access keys)
  - Assumed via STS (Security Token Service)
  - Time-limited permissions
  - Used for cross-account access and service-to-service communication
- **Common Use Cases**:
  - EC2 instances accessing S3
  - Lambda functions accessing other services
  - Cross-account access
  - Federated access

#### Policies

- **Definition**: JSON documents that define permissions (allow/deny)
- **Structure**:
  - **Version**: Policy language version
  - **Statement**: Array of permission statements
  - **Effect**: `Allow` or `Deny`
  - **Action**: What actions are allowed/denied
  - **Resource**: Which resources the policy applies to
  - **Condition**: Optional conditions for when policy applies
- **Types**:
  - **Managed Policies**: Reusable policies created by AWS or users
  - **Inline Policies**: Embedded directly in users, groups, or roles
  - **Resource-Based Policies**: Attached to resources (e.g., S3 bucket policies)

### Best Practices

- **Principle of Least Privilege**: Grant minimum necessary permissions
- **Use Roles**: Prefer roles over users for applications
- **Regular Audits**: Review and remove unused permissions
- **MFA**: Enable Multi-Factor Authentication for sensitive operations
- **Separate Accounts**: Use separate accounts for different environments

---

## 4. Networking (VPC Basics)

### Overview

Virtual Private Cloud (VPC) is your isolated network environment in AWS, providing control over network configuration and security.

### Core Components

#### VPC (Virtual Private Cloud)

- **Definition**: A logically isolated section of AWS cloud dedicated to your account
- **Characteristics**:
  - Each VPC has its own IP address range (CIDR block)
  - Default VPC is created in each region
  - Can have multiple VPCs per region
  - VPCs are region-specific

#### Subnets

- **Definition**: A range of IP addresses in your VPC
- **Types**:
  - **Public Subnet**: Has route to Internet Gateway (IGW)
  - **Private Subnet**: No direct route to Internet
- **Characteristics**:
  - Subnets exist within a single Availability Zone
  - Each subnet has its own CIDR block
  - Can span multiple subnets across AZs for high availability

#### Route Tables

- **Definition**: Set of rules (routes) that determine where network traffic is directed
- **Characteristics**:
  - Each subnet must be associated with a route table
  - Default route table is created with VPC
  - Routes define target for specific IP ranges
  - Can have custom route tables per subnet

#### Security Groups

- **Definition**: Virtual firewall controlling inbound and outbound traffic
- **Characteristics**:
  - Stateful (return traffic automatically allowed)
  - Applied at instance level
  - Default deny all inbound, allow all outbound
  - Can reference other security groups
  - Rules can be added/removed without instance restart

#### Network ACLs (NACLs)

- **Definition**: Stateless firewall at subnet level
- **Characteristics**:
  - Stateless (must define both inbound and outbound rules)
  - Applied at subnet level
  - Default allow all traffic
  - Rules evaluated in order (lowest number first)
  - Can explicitly deny traffic

### Managed Services in VPCs

- **RDS**: Database instances can be placed in VPC subnets
- **Lambda**: Functions can be configured with VPC access
- **ECS**: Containers run in VPC subnets
- **ElastiCache**: Caching services within VPC
- **Elasticsearch**: Search services in VPC

### Additional Networking Components

- **Internet Gateway (IGW)**: Allows communication between VPC and Internet
- **NAT Gateway**: Enables private subnets to access Internet
- **VPC Peering**: Connect two VPCs
- **VPN**: Connect on-premises networks to VPC
- **Direct Connect**: Dedicated network connection to AWS

---

## 5. Billing & Pricing Fundamentals

### Overview

Understanding AWS pricing models and cost management is crucial for optimizing cloud spend.

### Pricing Dimensions

#### Compute

- **EC2**: Pay for instance hours (on-demand, reserved, spot)
- **Lambda**: Pay per request and compute time
- **ECS/Fargate**: Pay for vCPU and memory resources
- **Elastic Beanstalk**: No additional charge (pay for underlying resources)

#### Storage

- **S3**: Pay for storage class, requests, and data transfer
- **EBS**: Pay for volume size and type
- **EFS**: Pay for storage and throughput
- **Glacier**: Lower cost for archival storage

#### Data Transfer

- **Inbound**: Free (data into AWS)
- **Outbound**: Charged (data out of AWS)
- **Cross-Region**: Higher costs
- **Cross-AZ**: Charged for data transfer between AZs
- **Internet Egress**: Charged based on volume tiers

### Cost Management Tools

#### Cost Explorer

- **Purpose**: Visualize, understand, and manage AWS costs
- **Features**:
  - Cost and usage reports
  - Forecasting
  - Cost breakdown by service, region, tags
  - Custom date ranges and filters
- **Use Cases**:
  - Identify cost trends
  - Analyze spending patterns
  - Forecast future costs
  - Optimize resource usage

#### Budgets

- **Purpose**: Set custom cost and usage budgets
- **Types**:
  - **Cost Budgets**: Track actual vs. planned spend
  - **Usage Budgets**: Track usage of services
  - **Reservation Budgets**: Track utilization of reserved instances
- **Features**:
  - Alerts when thresholds are exceeded
  - Multiple alert thresholds (50%, 80%, 100%)
  - Email and SNS notifications

### Free Tier

- **Always Free**: Services with permanent free tier (e.g., Lambda 1M requests/month)
- **12-Month Free**: New AWS accounts get 12 months of free tier
- **Trials**: Short-term free trials for specific services
- **Important**: Monitor usage to avoid charges after free tier expires

### Billing Alarms

- **Purpose**: Get notified when costs exceed thresholds
- **Setup**:
  - Create CloudWatch billing metric alarm
  - Set threshold (e.g., $100/month)
  - Configure SNS notification
- **Best Practices**:
  - Set multiple thresholds (warning and critical)
  - Monitor daily/weekly/monthly
  - Review and adjust regularly

### Cost Optimization Strategies

- **Right-Sizing**: Match instance types to workload requirements
- **Reserved Instances**: Commit to 1-3 year terms for discounts
- **Spot Instances**: Use for fault-tolerant, flexible workloads
- **Tagging**: Organize resources for cost allocation
- **Lifecycle Policies**: Automate data archival and deletion
- **Regular Reviews**: Audit unused resources and optimize continuously

---

## Summary

These core concepts form the foundation of AWS:

- **Regions & AZs**: Geographic distribution and high availability
- **ARNs**: Universal resource identification
- **IAM**: Security and access control
- **VPC**: Network isolation and security
- **Billing**: Cost management and optimization

Mastering these fundamentals is essential for effectively using AWS services and building scalable, secure, and cost-efficient cloud solutions.
