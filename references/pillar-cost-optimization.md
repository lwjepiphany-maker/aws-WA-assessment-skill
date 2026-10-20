# Pillar: Cost Optimization

## Design Principles
- Implement cloud financial management
- Adopt a consumption model
- Measure overall efficiency
- Stop spending money on undifferentiated heavy lifting
- Analyze and attribute expenditure

## Key Assessment Areas

### 1. Practice Cloud Financial Management
- **Tagging**: Resources tagged for cost allocation
- **Budgets**: AWS Budgets configured

### 2. Expenditure and Usage Awareness
- **Cost allocation tags**: Enabled and applied
- **Unused resources**: Idle instances, unattached EBS, unused EIPs

### 3. Cost-Effective Resources
- **Right-sizing**: Over-provisioned instances identified
- **Pricing models**: Reserved Instances, Savings Plans, Spot usage
- **Managed services**: Serverless adoption where appropriate

### 4. Manage Demand and Supply
- **Auto Scaling**: Scale down during low demand
- **Scheduled scaling**: Time-based scaling policies

### 5. Optimize Over Time
- **New services**: Evaluate newer, cost-effective alternatives
- **Storage lifecycle**: S3 lifecycle policies, EBS snapshot cleanup

## Service Mapping
| Service | Cost Checks |
|---------|------------|
| EC2 | Stopped instances, previous-gen types, unattached EBS, unused EIPs |
| RDS | Idle instances, previous-gen types, over-provisioned storage |
| Lambda | Over-provisioned memory, unused functions |
| S3 | Lifecycle policies, intelligent tiering, incomplete multipart uploads |
| DynamoDB | Capacity mode optimization, unused tables |
| ElastiCache | Idle clusters, previous-gen node types |
| Redshift | Idle clusters, reserved node coverage |
| EKS | Over-provisioned node groups, Spot instance usage |
| CloudFront | Price class optimization, unused distributions |
| OpenSearch | Instance right-sizing, reserved instance coverage |
| EFS | Lifecycle policy (IA storage class), unused file systems |
| SQS | Unused queues, message retention optimization |
| Glue | Idle dev endpoints, job bookmark optimization |
| SageMaker | Idle notebook instances, endpoint auto-scaling |
