# KMS Service Checks

Reference: service-screener-v2 `services/kms/`

## Check: KMS_001 — Key Rotation Enabled
- **API**: `aws kms get-key-rotation-status` → `.KeyRotationEnabled`
- **Pass**: `KeyRotationEnabled == true` (for symmetric CMKs)
- **Fail**: `KeyRotationEnabled == false`
- **Severity**: 🟡 MEDIUM | **Pillar**: Security

## Check: KMS_002 — Key Policy Restrictive
- **API**: `aws kms get-key-policy` → policy document
- **Pass**: Key policy restricts access to specific principals
- **Fail**: Key policy allows `"Principal": "*"` without conditions
- **Severity**: 🔴 HIGH | **Pillar**: Security

## Check: KMS_003 — Key State
- **API**: `aws kms describe-key` → `.KeyMetadata.KeyState`
- **Pass**: `KeyState == "Enabled"`
- **Fail**: `KeyState == "PendingDeletion"` (review if intentional)
- **Severity**: 🟡 MEDIUM | **Pillar**: Operational Excellence

## Check: KMS_004 — Key Usage
- **API**: `aws kms describe-key` → `.KeyMetadata.KeyUsage`
- **Pass**: Key is actively used by AWS services
- **Fail**: Key exists but not referenced by any resource
- **Severity**: 🟢 IMPROVEMENT | **Pillar**: Cost Optimization

## Check: KMS_005 — Grant Management
- **API**: `aws kms list-grants`
- **Pass**: Grants are scoped and reviewed
- **Fail**: Excessive or stale grants
- **Severity**: 🟢 IMPROVEMENT | **Pillar**: Security

## Check: KMS_006 — Multi-Region Key
- **API**: `aws kms describe-key` → `.KeyMetadata.MultiRegion`
- **Pass**: Multi-region keys used for cross-region workloads
- **Fail**: Single-region keys for multi-region data
- **Severity**: 🟢 IMPROVEMENT | **Pillar**: Reliability
