# AWS Config Service Checks

Reference: AWS Config best practices; foundational dependency for Security Hub compliance checks.

Note: AWS Config records resource configuration changes over time and underpins most Security Hub
FSBP/CIS controls. Without a Config recorder, many posture/compliance checks cannot run.

## Check: CFG_001 — Configuration Recorder Enabled
- **API**: `aws configservice describe-configuration-recorders` + `describe-configuration-recorder-status`
- **Pass**: A recorder exists and `recording == true`
- **Fail**: No recorder, or recorder stopped
- **Severity**: 🟡 MEDIUM | **Pillar**: Security, Operational Excellence

## Check: CFG_002 — Records All Resource Types
- **API**: `aws configservice describe-configuration-recorders` → `.recordingGroup`
- **Pass**: `allSupported == true` (and `includeGlobalResourceTypes == true` in the home region)
- **Fail**: Only a subset of resource types recorded
- **Severity**: 🟡 MEDIUM | **Pillar**: Operational Excellence

## Check: CFG_003 — Delivery Channel Configured
- **API**: `aws configservice describe-delivery-channels`
- **Pass**: Delivery channel to an S3 bucket (and optionally SNS) configured
- **Fail**: No delivery channel
- **Severity**: 🟡 MEDIUM | **Pillar**: Operational Excellence

## Check: CFG_004 — Multi-Region Coverage
- **API**: `aws configservice describe-configuration-recorders` (per region)
- **Pass**: Config enabled in all regions holding resources
- **Fail**: Config missing in regions that contain workloads
- **Severity**: 🟡 MEDIUM | **Pillar**: Security, Operational Excellence

## Check: CFG_005 — Config Rules / Conformance Packs
- **API**: `aws configservice describe-config-rules` + `describe-conformance-packs`
- **Pass**: Managed rules or a conformance pack deployed for continuous compliance
- **Fail**: Recorder on but no rules evaluating compliance
- **Severity**: 🟢 IMPROVEMENT | **Pillar**: Security
