# CloudTrail Service Checks

Reference: service-screener-v2 `services/cloudtrail/`

## Check: CT_001 — Trail Enabled
- **API**: `aws cloudtrail describe-trails` + `get-trail-status`
- **Pass**: At least one trail enabled and logging
- **Fail**: No trail or trail not logging
- **Severity**: 🔴 HIGH | **Pillar**: Security

## Check: CT_002 — Multi-Region Trail
- **API**: `aws cloudtrail describe-trails` → `.IsMultiRegionTrail`
- **Pass**: `IsMultiRegionTrail == true`
- **Fail**: `IsMultiRegionTrail == false`
- **Severity**: 🔴 HIGH | **Pillar**: Security

## Check: CT_003 — Log File Validation
- **API**: `aws cloudtrail describe-trails` → `.LogFileValidationEnabled`
- **Pass**: `LogFileValidationEnabled == true`
- **Fail**: `LogFileValidationEnabled == false`
- **Severity**: 🟡 MEDIUM | **Pillar**: Security

## Check: CT_004 — S3 Bucket Encryption
- **API**: Check S3 bucket used by trail for encryption
- **Pass**: Trail S3 bucket has SSE-KMS encryption
- **Fail**: No encryption or SSE-S3 only
- **Severity**: 🟡 MEDIUM | **Pillar**: Security

## Check: CT_005 — CloudWatch Logs Integration
- **API**: `aws cloudtrail describe-trails` → `.CloudWatchLogsLogGroupArn`
- **Pass**: CloudWatch Logs integration configured
- **Fail**: No CloudWatch Logs delivery
- **Severity**: 🟡 MEDIUM | **Pillar**: Operational Excellence, Security

## Check: CT_006 — Management Events
- **API**: `aws cloudtrail get-event-selectors`
- **Pass**: Management events (read + write) captured
- **Fail**: Management events not fully captured
- **Severity**: 🟡 MEDIUM | **Pillar**: Security

## Check: CT_007 — Data Events
- **API**: `aws cloudtrail get-event-selectors` → data event selectors
- **Pass**: Data events enabled for critical resources (S3, Lambda)
- **Fail**: No data events configured
- **Severity**: 🟢 IMPROVEMENT | **Pillar**: Security
