# Pillar: Security

## Design Principles
- Implement a strong identity foundation
- Enable traceability
- Apply security at all layers
- Automate security best practices
- Protect data in transit and at rest
- Keep people away from data
- Prepare for security events

## Key Assessment Areas

### 1. Identity and Access Management
- **IAM**: MFA enabled, password policy strong, access keys rotated
- **Root account**: MFA enabled, no access keys, minimal usage
- **Least privilege**: No wildcard (*) policies, unused permissions removed
- **KMS**: Customer-managed keys used, key rotation enabled

### 2. Detection
- **GuardDuty**: Enabled in all regions, findings reviewed
- **CloudTrail**: Enabled, multi-region, log file validation, S3 delivery
- **CloudWatch**: Security-related alarms configured

### 3. Infrastructure Protection
- **VPC**: Security groups restrictive, no 0.0.0.0/0 ingress on sensitive ports
- **NACLs**: Properly configured network boundaries
- **CloudFront**: WAF integration, HTTPS enforcement
- **API Gateway**: Authorization configured, throttling enabled

### 4. Data Protection
- **S3**: Bucket policies restrictive, encryption enabled, public access blocked
- **RDS**: Encryption at rest, SSL connections enforced
- **EFS**: Encryption at rest and in transit
- **DynamoDB**: Encryption enabled, VPC endpoints used
- **Redshift**: Encryption enabled, audit logging on
- **SQS**: Server-side encryption enabled
- **EBS**: Default encryption enabled

### 5. Incident Response
- **GuardDuty**: Auto-remediation configured
- **CloudWatch**: Alarm actions configured for security events
- **SNS**: Notification topics for security alerts

## Service Mapping
| Service | Security Checks |
|---------|----------------|
| IAM | MFA, password policy, access key age, unused credentials, policy scope |
| KMS | Key rotation, key policy, grant management |
| GuardDuty | Detector enabled, finding types, notification configured |
| S3 | Public access block, encryption, bucket policy, ACLs |
| RDS | Encryption, public access, IAM auth, SSL |
| EC2 | IMDSv2, EBS encryption, security group rules |
| VPC | Flow logs, security group rules, NACL rules |
| EKS | Secrets encryption, private endpoint, security groups |
| CloudFront | HTTPS, TLS version, WAF, OAI/OAC |
| API Gateway | Authorization, TLS, resource policy |
