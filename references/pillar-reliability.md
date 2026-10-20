# Pillar: Reliability

## Design Principles
- Automatically recover from failure
- Test recovery procedures
- Scale horizontally to increase aggregate workload availability
- Stop guessing capacity
- Manage change in automation

## Key Assessment Areas

### 1. Foundations
- **Service quotas**: Are limits monitored and appropriate?
- **Network topology**: Multi-AZ VPC design, redundant NAT gateways

### 2. Workload Architecture
- **Distributed design**: Loosely coupled components
- **Graceful degradation**: Circuit breakers, retry logic

### 3. Change Management
- **Auto Scaling**: Configured for EC2, EKS, DynamoDB
- **Monitoring**: CloudWatch alarms for failure detection
- **Deployment**: Rollback capabilities

### 4. Failure Management
- **Backup**: RDS automated backups, S3 versioning, EFS backup
- **Multi-AZ**: RDS Multi-AZ, ElastiCache replication, EFS
- **Disaster recovery**: Cross-region replication where applicable
- **DLQ**: Lambda DLQ, SQS DLQ configured

## Service Mapping
| Service | Reliability Checks |
|---------|--------------------|
| RDS | Multi-AZ, automated backups, backup retention, read replicas |
| EC2 | Auto Scaling group, multi-AZ placement, EBS snapshots |
| S3 | Versioning enabled, cross-region replication, lifecycle rules |
| EFS | Backup policy, multi-AZ by default |
| DynamoDB | Point-in-time recovery, global tables, auto-scaling |
| ElastiCache | Multi-AZ, automatic failover, backup enabled |
| Redshift | Automated snapshots, cross-region snapshots |
| Lambda | DLQ configured, reserved concurrency, retry configuration |
| EKS | Multi-AZ node groups, cluster auto-scaler |
| SQS | DLQ configured, message retention, visibility timeout |
| VPC | Multi-AZ subnets, redundant NAT gateways |
