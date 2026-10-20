# DynamoDB Service Checks

Reference: service-screener-v2 `services/dynamodb/`

## Check: DYNAMODB_001 — Encryption (CMK)
- **API**: `aws dynamodb describe-table` → `.SSEDescription`
- **Pass**: SSE enabled with KMS CMK
- **Fail**: Using default encryption only (AWS owned key)
- **Severity**: 🟡 MEDIUM | **Pillar**: Security

## Check: DYNAMODB_002 — Point-in-Time Recovery
- **API**: `aws dynamodb describe-continuous-backups` → `.PointInTimeRecoveryDescription.PointInTimeRecoveryStatus`
- **Pass**: `PointInTimeRecoveryStatus == "ENABLED"`
- **Fail**: `PointInTimeRecoveryStatus == "DISABLED"`
- **Severity**: 🔴 HIGH | **Pillar**: Reliability

## Check: DYNAMODB_003 — Auto Scaling / On-Demand
- **API**: `aws dynamodb describe-table` → `.BillingModeSummary.BillingMode`
- **Pass**: `PAY_PER_REQUEST` or provisioned with auto-scaling configured
- **Fail**: Provisioned without auto-scaling
- **Severity**: 🟡 MEDIUM | **Pillar**: Reliability, Cost Optimization

## Check: DYNAMODB_004 — Deletion Protection
- **API**: `aws dynamodb describe-table` → `.DeletionProtectionEnabled`
- **Pass**: `DeletionProtectionEnabled == true`
- **Fail**: `DeletionProtectionEnabled == false`
- **Severity**: 🟡 MEDIUM | **Pillar**: Reliability

## Check: DYNAMODB_005 — Tags Present
- **API**: `aws dynamodb list-tags-of-resource`
- **Pass**: Table has cost allocation tags
- **Fail**: No tags
- **Severity**: 🟢 IMPROVEMENT | **Pillar**: Cost Optimization
