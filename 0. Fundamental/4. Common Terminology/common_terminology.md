# Common Terminology

## Core Operations

### Provision / Launch

- **Definition**: Create and deploy AWS resources (instances, databases, services)
- **Usage**: "Provision an EC2 instance" or "Launch a Lambda function"
- **Context**: Initial resource creation, setting up infrastructure

### Elastic / Managed

- **Definition**: Auto-scaling services where AWS runs and maintains the infrastructure for you
- **Elastic**: Automatically scales up/down based on demand (e.g., Elastic Beanstalk, Auto Scaling)
- **Managed**: AWS handles operational tasks like patching, backups, monitoring (e.g., RDS, Lambda)
- **Benefit**: Reduces operational overhead, focuses on application logic

### Endpoint

- **Definition**: Entry point to an AWS service, often region-specific
- **Types**:
  - Service endpoints (e.g., `s3.amazonaws.com`, `lambda.us-east-1.amazonaws.com`)
  - VPC endpoints (private connectivity to AWS services)
  - API Gateway endpoints (REST/HTTP APIs)
- **Usage**: Used for service access, API calls, resource connections

### Service Quotas

- **Definition**: Account-level limits on AWS resources and operations
- **Examples**: EC2 instance limits, Lambda concurrent executions, S3 bucket count
- **Management**: Can be viewed in Service Quotas console, increased via support requests
- **Default Limits**: Vary by account type and region

### Event-driven

- **Definition**: Architecture pattern where actions trigger events that invoke other services
- **Common Services**: EventBridge, SQS, SNS, Lambda
- **Pattern**: Service A → Event → Service B (loosely coupled, scalable)
- **Use Cases**: Microservices, serverless architectures, decoupled systems

---

## Resource Management

### ARN (Amazon Resource Name)

- **Definition**: Unique identifier for any AWS resource
- **Format**: `arn:partition:service:region:account-id:resource`
- **Usage**: IAM policies, cross-service references, resource identification

### Tags

- **Definition**: Key-value pairs attached to resources for organization and cost tracking
- **Common Tags**: Environment (dev/prod), Project, Owner, Cost Center
- **Use Cases**: Resource organization, cost allocation, automation, compliance

### Resource Limits

- **Definition**: Maximum number of resources per account/region
- **Types**: Soft limits (can be increased), hard limits (cannot be changed)
- **Examples**: VPCs per region, security groups per VPC, IAM roles per account

---

## Networking

### VPC (Virtual Private Cloud)

- **Definition**: Logically isolated network section in AWS cloud
- **Purpose**: Private network environment with custom IP ranges and routing

### Subnet

- **Definition**: Range of IP addresses within a VPC
- **Types**: Public (Internet access) or Private (no direct Internet access)
- **Placement**: Single Availability Zone

### Security Group

- **Definition**: Virtual firewall controlling inbound/outbound traffic
- **Characteristics**: Stateful, applied at instance level, default deny inbound

### NACL (Network ACL)

- **Definition**: Stateless firewall at subnet level
- **Characteristics**: Stateless, subnet-level, explicit allow/deny rules

---

## Compute

### Instance

- **Definition**: Virtual server in AWS (EC2, RDS, etc.)
- **Types**: On-Demand, Reserved, Spot (for EC2)
- **Characteristics**: Configurable CPU, memory, storage, networking

### Container

- **Definition**: Lightweight, portable application package
- **Services**: ECS, EKS, Fargate
- **Benefit**: Consistent deployment across environments

### Serverless

- **Definition**: Run code without managing servers
- **Services**: Lambda, API Gateway, DynamoDB
- **Benefit**: Pay per use, automatic scaling, no infrastructure management

---

## Storage

### Bucket

- **Definition**: Container for objects in S3
- **Characteristics**: Globally unique name, region-specific, unlimited objects
- **Use Cases**: File storage, static website hosting, data backup

### Object

- **Definition**: File stored in S3 bucket
- **Components**: Key (name), data, metadata
- **Size**: Up to 5TB per object

### Volume

- **Definition**: Block storage device (EBS) attached to EC2 instances
- **Types**: gp3, io1, st1, sc1 (different performance/cost characteristics)
- **Persistence**: Data persists independently of instance lifecycle

---

## Security

### IAM (Identity and Access Management)

- **Definition**: Service for managing users, groups, roles, and permissions
- **Core Components**: Users, Groups, Roles, Policies
- **Purpose**: Control who can access what resources

### Policy

- **Definition**: JSON document defining permissions (allow/deny)
- **Types**: Managed, Inline, Resource-based
- **Structure**: Effect, Action, Resource, Condition

### Role

- **Definition**: Temporary credentials assumed by users/services
- **Benefit**: No permanent credentials, time-limited access
- **Use Cases**: Cross-account access, service-to-service communication

### MFA (Multi-Factor Authentication)

- **Definition**: Additional security layer requiring multiple authentication factors
- **Types**: Virtual MFA device, hardware token, SMS
- **Use Cases**: Root account, privileged users, sensitive operations

---

## Monitoring & Logging

### CloudWatch

- **Definition**: Monitoring and observability service
- **Features**: Metrics, logs, alarms, dashboards
- **Use Cases**: Performance monitoring, troubleshooting, cost tracking

### CloudTrail

- **Definition**: Service logging API calls and account activity
- **Purpose**: Audit, compliance, security analysis
- **Logs**: Who did what, when, from where

### Metrics

- **Definition**: Data points representing resource performance
- **Examples**: CPU utilization, request count, error rate
- **Retention**: 15 months (varies by granularity)

### Alarms

- **Definition**: Automated notifications when metrics cross thresholds
- **Actions**: SNS notifications, Auto Scaling, EC2 actions
- **Use Cases**: Cost alerts, performance issues, capacity planning

---

## Messaging & Integration

### Queue

- **Definition**: Message buffer for asynchronous communication (SQS)
- **Types**: Standard (at-least-once), FIFO (exactly-once, ordered)
- **Use Cases**: Decoupling services, buffering, load leveling

### Topic

- **Definition**: Pub/sub communication channel (SNS)
- **Pattern**: One publisher, multiple subscribers
- **Use Cases**: Notifications, fan-out messaging, alerts

### Event

- **Definition**: State change or action that triggers a response
- **Service**: EventBridge (event router)
- **Use Cases**: Event-driven architectures, integration patterns

---

## Database

### Instance

- **Definition**: Database server (RDS, DynamoDB, etc.)
- **Types**: Primary, Read Replica, Multi-AZ
- **Characteristics**: Configurable compute, memory, storage

### Replica

- **Definition**: Copy of database for read scaling or backup
- **Types**: Read Replica (read-only), Multi-AZ (standby for failover)
- **Use Cases**: Read scaling, disaster recovery, high availability

### Cluster

- **Definition**: Group of database instances working together
- **Examples**: RDS Aurora Cluster, ElastiCache Cluster
- **Benefit**: High availability, automatic failover, load distribution

---

## Cost Management

### On-Demand

- **Definition**: Pay-as-you-go pricing model
- **Benefit**: No upfront commitment, flexible
- **Use Cases**: Variable workloads, testing, short-term projects

### Reserved Instance

- **Definition**: 1-3 year commitment for discounted pricing
- **Types**: Standard, Convertible, Scheduled
- **Benefit**: Up to 72% savings vs. On-Demand

### Spot Instance

- **Definition**: Bid on unused EC2 capacity at discounted rates
- **Risk**: Can be interrupted with 2-minute notice
- **Use Cases**: Fault-tolerant, flexible workloads, batch processing

### Savings Plan

- **Definition**: Flexible pricing model with 1-3 year commitment
- **Benefit**: Discounts on compute usage (EC2, Lambda, Fargate)
- **Flexibility**: Can change instance types, regions, operating systems

---

## Deployment & Orchestration

### Stack

- **Definition**: Collection of AWS resources managed as a unit (CloudFormation)
- **Operations**: Create, Update, Delete
- **Benefit**: Infrastructure as code, version control, rollback

### Blue/Green Deployment

- **Definition**: Deployment strategy with two identical environments
- **Process**: Deploy new version to green, switch traffic, keep blue as rollback
- **Benefit**: Zero-downtime deployments, instant rollback

### Canary Deployment

- **Definition**: Gradual rollout of new version to subset of users
- **Process**: Deploy to small percentage, monitor, gradually increase
- **Benefit**: Risk mitigation, early issue detection

---

## High Availability & Disaster Recovery

### Multi-AZ (Availability Zone)

- **Definition**: Deployment across multiple Availability Zones
- **Benefit**: High availability, automatic failover
- **Use Cases**: Production databases, critical applications

### Disaster Recovery (DR)

- **Definition**: Strategy to recover from catastrophic failures
- **Types**: Backup & Restore, Pilot Light, Warm Standby, Multi-Site
- **Metrics**: RTO (Recovery Time Objective), RPO (Recovery Point Objective)

### Backup

- **Definition**: Copy of data for recovery purposes
- **Types**: Automated (RDS snapshots), Manual (EBS snapshots)
- **Retention**: Configurable retention periods

### Snapshot

- **Definition**: Point-in-time copy of storage volume or database
- **Characteristics**: Incremental (only changed blocks), region-specific
- **Use Cases**: Backup, disaster recovery, migration

---

## Additional Important Terms

### Region

- **Definition**: Geographic area containing multiple Availability Zones
- **Examples**: us-east-1, eu-west-1, ap-south-1
- **Considerations**: Latency, compliance, service availability, pricing

### Availability Zone (AZ)

- **Definition**: Isolated data center within a region
- **Characteristics**: Redundant power, networking, physically separated
- **Use Cases**: High availability, fault tolerance

### Edge Location

- **Definition**: Data center for CloudFront (CDN) content delivery
- **Purpose**: Cache content closer to users for lower latency
- **Global**: Hundreds of locations worldwide

### API Gateway

- **Definition**: Managed service for creating REST and HTTP APIs
- **Features**: Authentication, throttling, caching, monitoring
- **Use Cases**: Microservices, serverless backends, API management

### State

- **Definition**: Current configuration and data of resources
- **Management**: Terraform state, CloudFormation stack state
- **Importance**: Tracks desired vs. actual infrastructure

### Drift

- **Definition**: Difference between expected and actual resource configuration
- **Detection**: CloudFormation drift detection, Terraform plan
- **Cause**: Manual changes outside of IaC

### Idempotent

- **Definition**: Operation that produces same result when repeated
- **Importance**: Safe to retry, predictable infrastructure changes
- **Examples**: Most AWS API calls are idempotent

---

## Summary

Understanding these common AWS terminologies is essential for:

- Effective communication with team members
- Navigating AWS documentation and services
- Designing scalable and reliable architectures
- Troubleshooting and problem-solving
- Passing AWS certifications

Master these terms to build a strong foundation for working with AWS services and architectures.
