# Pillar: Operational Excellence

## Design Principles
- Perform operations as code (IaC)
- Make frequent, small, reversible changes
- Refine operations procedures frequently
- Anticipate failure
- Learn from all operational failures

## Key Assessment Areas

### 1. Organization
- Are workloads documented with runbooks and playbooks?
- Are operational priorities defined and reviewed?

### 2. Prepare
- **CloudWatch alarms**: Are alarms configured for key metrics?
- **CloudTrail**: Is API activity logging enabled?
- **Auto Scaling**: Are scaling policies defined for variable workloads?
- **IaC adoption**: Are resources managed via CloudFormation/CDK/Terraform?

### 3. Operate
- **Monitoring dashboards**: Are CloudWatch dashboards configured?
- **Log aggregation**: Are logs centralized and searchable?
- **Incident response**: Are SNS topics configured for alarm notifications?
- **Deployment strategy**: Are blue/green or canary deployments used?

### 4. Evolve
- Are operational metrics reviewed regularly?
- Are post-incident reviews conducted?
- Are automation opportunities identified?

## Service Mapping
| Service | Operational Excellence Checks |
|---------|-------------------------------|
| CloudWatch | Alarms configured, dashboards exist, log groups with retention |
| CloudTrail | Trail enabled, multi-region, log file validation |
| Lambda | Error rate monitoring, DLQ configured, versioning |
| EKS | Control plane logging, cluster version currency |
| EC2 | Detailed monitoring, SSM managed, patching |
| API Gateway | Access logging, CloudWatch metrics enabled |
