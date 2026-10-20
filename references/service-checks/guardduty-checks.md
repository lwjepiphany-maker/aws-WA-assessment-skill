# GuardDuty Service Checks

Reference: service-screener-v2 `services/guardduty/`

## Check: GD_001 — Detector Enabled
- **API**: `aws guardduty list-detectors` + `get-detector`
- **Pass**: At least one detector enabled with `Status == "ENABLED"`
- **Fail**: No detector or detector disabled
- **Severity**: 🔴 HIGH | **Pillar**: Security

## Check: GD_002 — S3 Protection
- **API**: `aws guardduty get-detector` → `.DataSources.S3Logs.Status`
- **Pass**: `Status == "ENABLED"`
- **Fail**: S3 protection not enabled
- **Severity**: 🟡 MEDIUM | **Pillar**: Security

## Check: GD_003 — EKS Protection
- **API**: `aws guardduty get-detector` → `.Features` (EKS_AUDIT_LOGS)
- **Pass**: EKS audit log monitoring enabled
- **Fail**: EKS protection not enabled
- **Severity**: 🟡 MEDIUM | **Pillar**: Security

## Check: GD_004 — Malware Protection
- **API**: `aws guardduty get-detector` → `.Features` (EBS_MALWARE_PROTECTION)
- **Pass**: Malware protection enabled
- **Fail**: Malware protection not enabled
- **Severity**: 🟡 MEDIUM | **Pillar**: Security

## Check: GD_005 — Lambda Protection
- **API**: `aws guardduty get-detector` → `.Features` (LAMBDA_NETWORK_LOGS)
- **Pass**: Lambda network activity monitoring enabled
- **Fail**: Lambda protection not enabled
- **Severity**: 🟡 MEDIUM | **Pillar**: Security

## Check: GD_006 — RDS Protection
- **API**: `aws guardduty get-detector` → `.Features` (RDS_LOGIN_EVENTS)
- **Pass**: RDS login activity monitoring enabled
- **Fail**: RDS protection not enabled
- **Severity**: 🟡 MEDIUM | **Pillar**: Security

## Check: GD_007 — Unarchived Findings
- **API**: `aws guardduty list-findings` (filter: non-archived, severity >= HIGH)
- **Pass**: No unresolved HIGH/CRITICAL findings
- **Fail**: Unresolved HIGH/CRITICAL findings present
- **Severity**: 🔴 HIGH | **Pillar**: Security

## Check: GD_008 — Finding Export
- **API**: `aws guardduty describe-publishing-destination`
- **Pass**: Findings exported to S3 for long-term retention
- **Fail**: No export destination configured
- **Severity**: 🟢 IMPROVEMENT | **Pillar**: Security, Operational Excellence
