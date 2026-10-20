# CloudWatch Service Checks

Reference: service-screener-v2 `services/cloudwatch/`

## Check: CW_001 — Billing Alarm
- **API**: `aws cloudwatch describe-alarms` (filter: namespace=AWS/Billing)
- **Pass**: Billing alarm configured
- **Fail**: No billing alarm
- **Severity**: 🟡 MEDIUM | **Pillar**: Cost Optimization

## Check: CW_002 — Root Account Usage Alarm
- **API**: `aws cloudwatch describe-alarms` + CloudTrail metric filters
- **Pass**: Alarm for root account sign-in events
- **Fail**: No root usage monitoring
- **Severity**: 🔴 HIGH | **Pillar**: Security

## Check: CW_003 — Unauthorized API Call Alarm
- **API**: `aws logs describe-metric-filters` (filter for UnauthorizedAPICalls)
- **Pass**: Metric filter and alarm for unauthorized API calls
- **Fail**: No monitoring for unauthorized calls
- **Severity**: 🟡 MEDIUM | **Pillar**: Security

## Check: CW_004 — Security Group Change Alarm
- **API**: `aws logs describe-metric-filters` (filter for SecurityGroupChanges)
- **Pass**: Alarm for security group modifications
- **Fail**: No monitoring for SG changes
- **Severity**: 🟡 MEDIUM | **Pillar**: Security

## Check: CW_005 — Log Group Retention
- **API**: `aws logs describe-log-groups` → `.retentionInDays`
- **Pass**: Retention policy set (not indefinite)
- **Fail**: No retention policy (logs kept forever)
- **Severity**: 🟡 MEDIUM | **Pillar**: Cost Optimization

## Check: CW_006 — Log Group Encryption
- **API**: `aws logs describe-log-groups` → `.kmsKeyId`
- **Pass**: KMS encryption configured
- **Fail**: No KMS encryption (default encryption)
- **Severity**: 🟢 IMPROVEMENT | **Pillar**: Security

## Check: CW_007 — Alarm Actions Configured
- **API**: `aws cloudwatch describe-alarms` → `.AlarmActions`
- **Pass**: Alarms have SNS notification actions
- **Fail**: Alarms with no actions configured
- **Severity**: 🟡 MEDIUM | **Pillar**: Operational Excellence
