# Severity Classification Matrix

## Severity Levels

### 🔴 HIGH RISK
**Definition**: Critical issues that pose immediate security vulnerabilities,
data loss risk, or compliance violations. Require urgent remediation.

**Criteria** (any one triggers HIGH):
- Data exposed to public internet (S3, RDS, Redshift, OpenSearch)
- No encryption on data at rest for sensitive services
- Root account without MFA
- Overly permissive IAM policies (Action: *, Resource: *)
- Security group allowing 0.0.0.0/0 on sensitive ports
- GuardDuty disabled or unresolved HIGH findings
- CloudTrail not enabled or not multi-region
- Deprecated/EOL runtime or engine versions
- EKS secrets not encrypted, public API endpoint unrestricted

### 🟡 MEDIUM RISK
**Definition**: Best practice deviations that could lead to operational issues,
reduced reliability, or security gaps. Should be addressed in planned work.

**Criteria** (any one triggers MEDIUM):
- Single-AZ deployments for production workloads
- Backup retention < 7 days
- No access logging (S3, API Gateway, CloudFront)
- No DLQ configured for async processing
- Access keys not rotated within 90 days
- Unused credentials > 90 days
- No CloudWatch alarms for critical metrics
- Missing WAF protection on public endpoints
- No VPC Flow Logs
- Outdated (but not EOL) software versions

### 🟢 IMPROVEMENT
**Definition**: Optimization opportunities that can improve cost efficiency,
performance, or operational maturity. Address as part of continuous improvement.

**Criteria** (any one triggers IMPROVEMENT):
- Previous-generation instance/node types
- gp2 volumes (should be gp3)
- No lifecycle policies on S3/EFS
- Missing X-Ray tracing
- No VPC endpoints for AWS services
- Default monitoring (not enhanced/detailed)
- Missing cost allocation tags
- No intelligent tiering on S3
- Compression not enabled on CloudFront

## Pillar-Severity Mapping

| Pillar | Typical HIGH | Typical MEDIUM | Typical IMPROVEMENT |
|--------|-------------|----------------|---------------------|
| Security | Public access, no encryption, no MFA | No logging, weak policies | Code signing, VPC endpoints |
| Reliability | No backups, single-AZ critical | Short retention, no DLQ | Auto-scaling, reserved concurrency |
| Performance | — | Outdated versions | Right-sizing, caching |
| Cost | — | Idle resources | Previous-gen types, lifecycle |
| Ops Excellence | No CloudTrail | No alarms, no dashboards | Detailed monitoring, tracing |
| Sustainability | — | — | Graviton adoption, right-sizing |

## Score Calculation

Per-pillar score = (passed checks / total applicable checks) × 100

| Score Range | Status |
|-------------|--------|
| 90-100% | 🟢 Good |
| 70-89% | 🟡 Needs Improvement |
| 0-69% | 🔴 At Risk |
