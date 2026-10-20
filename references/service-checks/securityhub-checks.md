# Security Hub Service Checks

Reference: AWS Foundational Security Best Practices; extends service-screener-v2 security posture coverage.

Note: Security Hub is a Cloud Security Posture Management (CSPM) aggregation layer. These checks
assess whether the account has centralized, continuous security posture monitoring — a gap that a
one-time assessment cannot fill on its own.

## Check: SH_001 — Security Hub Enabled
- **API**: `aws securityhub describe-hub` (per region)
- **Pass**: Returns a Hub ARN (subscribed)
- **Fail**: `InvalidAccessException: Account ... is not subscribed to AWS Security Hub`
- **Severity**: 🟡 MEDIUM | **Pillar**: Security, Operational Excellence
- **Note**: For accounts with public-facing production workloads, treat as 🔴 HIGH.

## Check: SH_002 — Foundational Security Best Practices Standard
- **API**: `aws securityhub get-enabled-standards` → `.StandardsSubscriptions[].StandardsArn`
- **Pass**: AWS Foundational Security Best Practices (FSBP) standard subscribed
- **Fail**: FSBP not enabled
- **Severity**: 🟡 MEDIUM | **Pillar**: Security

## Check: SH_003 — CIS AWS Benchmark Standard
- **API**: `aws securityhub get-enabled-standards` → `.StandardsSubscriptions[].StandardsArn`
- **Pass**: CIS AWS Foundations Benchmark subscribed
- **Fail**: CIS benchmark not enabled
- **Severity**: 🟢 IMPROVEMENT | **Pillar**: Security

## Check: SH_004 — Finding Integrations (GuardDuty / Inspector / Access Analyzer)
- **API**: `aws securityhub list-enabled-products-for-import`
- **Pass**: GuardDuty (and where used, Inspector, IAM Access Analyzer, Macie) findings imported
- **Fail**: Enabled detectors/analyzers exist but are not integrated into Security Hub
- **Severity**: 🟡 MEDIUM | **Pillar**: Security, Operational Excellence

## Check: SH_005 — Cross-Region Finding Aggregation
- **API**: `aws securityhub list-finding-aggregators` + `get-finding-aggregator`
- **Pass**: A finding aggregator is configured to consolidate findings across regions
- **Fail**: No aggregator; findings siloed per region
- **Severity**: 🟢 IMPROVEMENT | **Pillar**: Operational Excellence

## Check: SH_006 — Unresolved Critical/High Findings
- **API**: `aws securityhub get-findings` filtered on `SeverityLabel = CRITICAL/HIGH` and `RecordState = ACTIVE`
- **Pass**: No unresolved CRITICAL/HIGH findings
- **Fail**: Active CRITICAL/HIGH findings present
- **Severity**: 🔴 HIGH | **Pillar**: Security
- **Note**: Only applicable when SH_001 passes.
