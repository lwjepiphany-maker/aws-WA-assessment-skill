# EC2 Service Checks

Reference: service-screener-v2 `services/ec2/`

## Check: EC2_001 — IMDSv2 Enforcement
- **API**: `aws ec2 describe-instances` → `.MetadataOptions.HttpTokens`
- **Pass**: `HttpTokens == "required"`
- **Fail**: `HttpTokens == "optional"`
- **Severity**: 🔴 HIGH
- **Pillar**: Security
- **Recommendation**: Enforce IMDSv2 to prevent SSRF-based credential theft.

## Check: EC2_002 — EBS Volume Encryption
- **API**: `aws ec2 describe-volumes` → `.Encrypted`
- **Pass**: `Encrypted == true`
- **Fail**: `Encrypted == false`
- **Severity**: 🔴 HIGH
- **Pillar**: Security
- **Recommendation**: Enable EBS encryption. Set default encryption in account settings.

## Check: EC2_003 — Public IP Assignment
- **API**: `aws ec2 describe-instances` → `.PublicIpAddress`
- **Pass**: No public IP or justified (web-facing)
- **Fail**: Public IP on non-web-facing instances
- **Severity**: 🟡 MEDIUM
- **Pillar**: Security
- **Recommendation**: Use private subnets with NAT Gateway or ALB for internet access.

## Check: EC2_004 — Security Group Open Ingress
- **API**: `aws ec2 describe-security-groups` → `.IpPermissions`
- **Pass**: No rules with `0.0.0.0/0` on ports 22, 3389, 3306, 5432, 1433
- **Fail**: Open ingress on sensitive ports
- **Severity**: 🔴 HIGH
- **Pillar**: Security
- **Recommendation**: Restrict security group rules to specific CIDR ranges.

## Check: EC2_005 — Detailed Monitoring
- **API**: `aws ec2 describe-instances` → `.Monitoring.State`
- **Pass**: `State == "enabled"`
- **Fail**: `State == "disabled"`
- **Severity**: 🟢 IMPROVEMENT
- **Pillar**: Operational Excellence
- **Recommendation**: Enable detailed monitoring for 1-minute metric granularity.

## Check: EC2_006 — Instance Generation Currency
- **API**: `aws ec2 describe-instances` → `.InstanceType`
- **Pass**: Current generation instance type
- **Fail**: Previous generation (m4, c4, r4, t2, etc.)
- **Severity**: 🟡 MEDIUM
- **Pillar**: Performance Efficiency, Cost Optimization
- **Recommendation**: Migrate to current-gen instances (m7i, c7g, r7g, t3).

## Check: EC2_007 — EBS Volume Type
- **API**: `aws ec2 describe-volumes` → `.VolumeType`
- **Pass**: `gp3`, `io2`, or appropriate type
- **Fail**: `gp2` (predecessor to gp3)
- **Severity**: 🟢 IMPROVEMENT
- **Pillar**: Performance Efficiency, Cost Optimization
- **Recommendation**: Migrate gp2 volumes to gp3 for better price-performance.

## Check: EC2_008 — Stopped Instances
- **API**: `aws ec2 describe-instances` → `.State.Name`
- **Pass**: Instance running or recently stopped
- **Fail**: Instance stopped for > 30 days
- **Severity**: 🟡 MEDIUM
- **Pillar**: Cost Optimization
- **Recommendation**: Terminate or snapshot long-stopped instances to save costs.

## Check: EC2_009 — SSM Managed
- **API**: `aws ssm describe-instance-information`
- **Pass**: Instance appears in SSM inventory
- **Fail**: Instance not managed by SSM
- **Severity**: 🟡 MEDIUM
- **Pillar**: Operational Excellence, Security
- **Recommendation**: Install SSM Agent for patch management and remote access.

## Check: EC2_010 — Auto Scaling Group Membership
- **API**: `aws autoscaling describe-auto-scaling-instances`
- **Pass**: Instance is part of an ASG
- **Fail**: Standalone instance without ASG
- **Severity**: 🟢 IMPROVEMENT
- **Pillar**: Reliability
- **Recommendation**: Use Auto Scaling Groups for automatic recovery and scaling.
