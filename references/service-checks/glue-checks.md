# Glue Service Checks

Reference: service-screener-v2 `services/glue/`

## Check: GLUE_001 — Job Encryption
- **API**: `aws glue get-security-configurations`
- **Pass**: Security configuration with encryption enabled (S3, CloudWatch, job bookmarks)
- **Fail**: No security configuration or encryption disabled
- **Severity**: 🟡 MEDIUM | **Pillar**: Security

## Check: GLUE_002 — Data Catalog Encryption
- **API**: `aws glue get-data-catalog-encryption-settings`
- **Pass**: Catalog encryption and connection password encryption enabled
- **Fail**: Encryption settings disabled
- **Severity**: 🟡 MEDIUM | **Pillar**: Security

## Check: GLUE_003 — Job Bookmark Enabled
- **API**: `aws glue get-jobs` → `.DefaultArguments.--job-bookmark-option`
- **Pass**: `job-bookmark-enable` set
- **Fail**: Job bookmarks disabled (risk of reprocessing)
- **Severity**: 🟢 IMPROVEMENT | **Pillar**: Operational Excellence

## Check: GLUE_004 — CloudWatch Logging
- **API**: `aws glue get-jobs` → `.DefaultArguments.--enable-continuous-cloudwatch-log`
- **Pass**: Continuous CloudWatch logging enabled
- **Fail**: Logging not enabled
- **Severity**: 🟡 MEDIUM | **Pillar**: Operational Excellence

## Check: GLUE_005 — Dev Endpoint Idle
- **API**: `aws glue get-dev-endpoints`
- **Pass**: No idle dev endpoints
- **Fail**: Dev endpoints running without recent activity
- **Severity**: 🟡 MEDIUM | **Pillar**: Cost Optimization, Security

## Check: GLUE_006 — Resource Policy
- **API**: `aws glue get-resource-policy`
- **Pass**: Resource policy configured for cross-account access control
- **Fail**: No resource policy (if cross-account access needed)
- **Severity**: 🟢 IMPROVEMENT | **Pillar**: Security
