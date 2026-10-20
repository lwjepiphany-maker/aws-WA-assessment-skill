# VPC Service Checks

Reference: service-screener-v2 `services/ec2/` (VPC checks embedded in EC2)

## Check: VPC_001 — Flow Logs Enabled
- **API**: `aws ec2 describe-flow-logs` (filter by VPC)
- **Pass**: Flow logs enabled for VPC
- **Fail**: No flow logs configured
- **Severity**: 🟡 MEDIUM | **Pillar**: Security, Operational Excellence

## Check: VPC_002 — Security Group Default Restrictive
- **API**: `aws ec2 describe-security-groups` (default SG)
- **Pass**: Default SG has no inbound rules allowing external traffic
- **Fail**: Default SG has permissive inbound rules
- **Severity**: 🟡 MEDIUM | **Pillar**: Security

## Check: VPC_003 — Unused Security Groups
- **API**: `aws ec2 describe-security-groups` + `describe-network-interfaces`
- **Pass**: Security group is attached to resources
- **Fail**: Security group has no associated ENIs
- **Severity**: 🟢 IMPROVEMENT | **Pillar**: Operational Excellence

## Check: VPC_004 — NACL Overly Permissive
- **API**: `aws ec2 describe-network-acls`
- **Pass**: NACLs have specific allow/deny rules
- **Fail**: NACLs allow all traffic (0.0.0.0/0 on all ports)
- **Severity**: 🟡 MEDIUM | **Pillar**: Security

## Check: VPC_005 — NAT Gateway Redundancy
- **API**: `aws ec2 describe-nat-gateways`
- **Pass**: NAT Gateway in each AZ with private subnets
- **Fail**: Single NAT Gateway for multi-AZ deployment
- **Severity**: 🟡 MEDIUM | **Pillar**: Reliability

## Check: VPC_006 — VPC Endpoints
- **API**: `aws ec2 describe-vpc-endpoints`
- **Pass**: VPC endpoints configured for frequently used services (S3, DynamoDB)
- **Fail**: No VPC endpoints (traffic goes through NAT/IGW)
- **Severity**: 🟢 IMPROVEMENT | **Pillar**: Security, Cost Optimization

## Check: VPC_007 — Subnet Multi-AZ
- **API**: `aws ec2 describe-subnets`
- **Pass**: Subnets span at least 2 AZs
- **Fail**: All subnets in single AZ
- **Severity**: 🟡 MEDIUM | **Pillar**: Reliability
