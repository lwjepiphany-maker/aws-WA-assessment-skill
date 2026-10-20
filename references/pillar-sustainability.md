# Pillar: Sustainability

## Design Principles
- Understand your impact
- Establish sustainability goals
- Maximize utilization
- Anticipate and adopt new, more efficient offerings
- Use managed services
- Reduce the downstream impact of your cloud workloads

## Key Assessment Areas

### 1. Region Selection
- Choose regions with lower carbon intensity where possible

### 2. Resource Efficiency
- **Right-sizing**: Minimize over-provisioning
- **Graviton**: Use ARM-based instances (lower energy per compute unit)
- **Serverless**: Adopt Lambda, Fargate to maximize utilization

### 3. Data Management
- **S3 lifecycle**: Move infrequently accessed data to efficient tiers
- **Data retention**: Define and enforce retention policies
- **Compression**: Enable compression for CloudFront, API responses

### 4. Software and Architecture
- **Efficient code**: Optimize Lambda memory/duration
- **Caching**: Reduce redundant computation via CloudFront, ElastiCache
- **Async processing**: Use SQS for decoupled, batch processing

## Service Mapping
| Service | Sustainability Checks |
|---------|----------------------|
| EC2 | Graviton adoption, right-sizing, Auto Scaling efficiency |
| Lambda | Memory optimization (right-sized), runtime efficiency |
| S3 | Lifecycle policies, intelligent tiering adoption |
| RDS | Graviton instances, right-sizing |
| EKS | Graviton node groups, efficient scaling |
| CloudFront | Compression enabled, cache optimization |
| ElastiCache | Graviton nodes, right-sizing |
| DynamoDB | On-demand mode for variable workloads |
| Redshift | RA3 node adoption, concurrency scaling |
