# S3 Service Checks

Reference: service-screener-v2 `services/s3/`

## Check: S3_001 — Public Access Block
- **API**: `aws s3control get-public-access-block` (account level) + `aws s3api get-public-access-block` (bucket level)
- **Pass**: All four public access block settings enabled
- **Fail**: Any public access block setting disabled
- **Severity**: 🔴 HIGH
- **Pillar**: Security
- **Recommendation**: Enable all public access block settings at account and bucket level.

## Check: S3_002 — Default Encryption
- **API**: `aws s3api get-bucket-encryption`
- **Pass**: Server-side encryption configured (SSE-S3 or SSE-KMS)
- **Fail**: No default encryption
- **Severity**: 🔴 HIGH
- **Pillar**: Security
- **Recommendation**: Enable default encryption with SSE-S3 or SSE-KMS.

## Check: S3_003 — Versioning
- **API**: `aws s3api get-bucket-versioning`
- **Pass**: `Status == "Enabled"`
- **Fail**: Versioning not enabled or suspended
- **Severity**: 🟡 MEDIUM
- **Pillar**: Reliability
- **Recommendation**: Enable versioning for data protection and recovery.

## Check: S3_004 — Lifecycle Policy
- **API**: `aws s3api get-bucket-lifecycle-configuration`
- **Pass**: Lifecycle rules configured
- **Fail**: No lifecycle configuration
- **Severity**: 🟡 MEDIUM
- **Pillar**: Cost Optimization
- **Recommendation**: Configure lifecycle rules to transition/expire objects.

## Check: S3_005 — Access Logging
- **API**: `aws s3api get-bucket-logging`
- **Pass**: Server access logging enabled
- **Fail**: No logging configured
- **Severity**: 🟡 MEDIUM
- **Pillar**: Security, Operational Excellence
- **Recommendation**: Enable server access logging for audit trail.

## Check: S3_006 — Bucket Policy Overly Permissive
- **API**: `aws s3api get-bucket-policy`
- **Pass**: No `Principal: "*"` without conditions
- **Fail**: Policy allows public access via wildcard principal
- **Severity**: 🔴 HIGH
- **Pillar**: Security
- **Recommendation**: Restrict bucket policy to specific principals and conditions.

## Check: S3_007 — SSL/TLS Enforcement
- **API**: `aws s3api get-bucket-policy`
- **Pass**: Policy includes `aws:SecureTransport` condition
- **Fail**: No TLS enforcement in bucket policy
- **Severity**: 🟡 MEDIUM
- **Pillar**: Security
- **Recommendation**: Add policy condition to deny non-HTTPS requests.

## Check: S3_008 — MFA Delete
- **API**: `aws s3api get-bucket-versioning` → `.MFADelete`
- **Pass**: MFA Delete enabled on critical buckets
- **Fail**: MFA Delete not enabled
- **Severity**: 🟢 IMPROVEMENT
- **Pillar**: Security
- **Recommendation**: Enable MFA Delete for critical data buckets.

## Check: S3_009 — Intelligent Tiering
- **API**: `aws s3api get-bucket-intelligent-tiering-configuration`
- **Pass**: Intelligent tiering configured for variable access patterns
- **Fail**: No intelligent tiering on large buckets
- **Severity**: 🟢 IMPROVEMENT
- **Pillar**: Cost Optimization
- **Recommendation**: Enable S3 Intelligent-Tiering for automatic cost savings.
