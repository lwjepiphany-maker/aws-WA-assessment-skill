# Pillar: Performance Efficiency

## Design Principles
- Democratize advanced technologies
- Go global in minutes
- Use serverless architectures
- Experiment more often
- Consider mechanical sympathy

## Key Assessment Areas

### 1. Selection
- **Compute**: Right instance type/size, Graviton adoption
- **Storage**: Appropriate storage class (gp3 vs io2, S3 tiers)
- **Database**: Right engine and instance class
- **Network**: Appropriate use of CDN, endpoints

### 2. Review
- **Benchmarking**: Performance baselines established
- **Load testing**: Regular load testing conducted

### 3. Monitoring
- **CloudWatch**: Custom metrics for application performance
- **Enhanced monitoring**: RDS, ElastiCache enhanced monitoring

### 4. Trade-offs
- **Caching**: CloudFront, ElastiCache, API Gateway caching
- **Read replicas**: RDS read replicas for read-heavy workloads
- **Edge computing**: Lambda@Edge, CloudFront Functions

## Service Mapping
| Service | Performance Checks |
|---------|-------------------|
| EC2 | Instance type currency, EBS type (gp3 recommended), enhanced networking |
| Lambda | Memory optimization, timeout settings, provisioned concurrency |
| RDS | Instance class, storage type, Performance Insights enabled |
| DynamoDB | Capacity mode (on-demand vs provisioned), DAX usage |
| ElastiCache | Node type, cluster mode, engine version |
| Redshift | Node type, distribution style, sort keys, WLM config |
| CloudFront | Cache hit ratio, compression enabled, HTTP/2 |
| API Gateway | Caching enabled, throttling configured |
| EKS | Node instance types, cluster autoscaler, HPA |
| OpenSearch | Instance type, dedicated master nodes, zone awareness |
| S3 | Transfer acceleration, intelligent tiering |
