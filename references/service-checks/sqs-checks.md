# SQS Service Checks

Reference: service-screener-v2 `services/sqs/`

## Check: SQS_001 — Server-Side Encryption
- **API**: `aws sqs get-queue-attributes` → `SqsManagedSseEnabled` or `KmsMasterKeyId`
- **Pass**: SSE enabled (SQS-managed or KMS)
- **Fail**: No encryption configured
- **Severity**: 🟡 MEDIUM | **Pillar**: Security

## Check: SQS_002 — Dead Letter Queue
- **API**: `aws sqs get-queue-attributes` → `RedrivePolicy`
- **Pass**: DLQ configured with `maxReceiveCount`
- **Fail**: No redrive policy
- **Severity**: 🟡 MEDIUM | **Pillar**: Reliability

## Check: SQS_003 — Queue Policy Restrictive
- **API**: `aws sqs get-queue-attributes` → `Policy`
- **Pass**: Policy restricts access to specific principals
- **Fail**: Policy allows `"Principal": "*"` without conditions
- **Severity**: 🔴 HIGH | **Pillar**: Security

## Check: SQS_004 — VPC Endpoint Usage
- **API**: Check if SQS VPC endpoint exists in VPC
- **Pass**: SQS VPC endpoint configured for private access
- **Fail**: No VPC endpoint (traffic goes through internet)
- **Severity**: 🟢 IMPROVEMENT | **Pillar**: Security

## Check: SQS_005 — Message Retention
- **API**: `aws sqs get-queue-attributes` → `MessageRetentionPeriod`
- **Pass**: Retention period set appropriately (not default 4 days if longer needed)
- **Fail**: Default retention may cause message loss
- **Severity**: 🟢 IMPROVEMENT | **Pillar**: Reliability

## Check: SQS_006 — Visibility Timeout
- **API**: `aws sqs get-queue-attributes` → `VisibilityTimeout`
- **Pass**: Visibility timeout >= 6x Lambda/consumer timeout
- **Fail**: Visibility timeout too short for consumer processing time
- **Severity**: 🟢 IMPROVEMENT | **Pillar**: Reliability
