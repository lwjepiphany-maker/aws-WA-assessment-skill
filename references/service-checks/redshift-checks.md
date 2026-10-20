# Redshift Service Checks

Reference: service-screener-v2 `services/redshift/`

## Check: REDSHIFT_001 — Encryption at Rest
- **API**: `aws redshift describe-clusters` → `.Encrypted`
- **Pass**: `Encrypted == true`
- **Fail**: `Encrypted == false`
- **Severity**: 🔴 HIGH | **Pillar**: Security

## Check: REDSHIFT_002 — Public Accessibility
- **API**: `aws redshift describe-clusters` → `.PubliclyAccessible`
- **Pass**: `PubliclyAccessible == false`
- **Fail**: `PubliclyAccessible == true`
- **Severity**: 🔴 HIGH | **Pillar**: Security

## Check: REDSHIFT_003 — Audit Logging
- **API**: `aws redshift describe-logging-status`
- **Pass**: `LoggingEnabled == true`
- **Fail**: `LoggingEnabled == false`
- **Severity**: 🟡 MEDIUM | **Pillar**: Security, Operational Excellence

## Check: REDSHIFT_004 — Automated Snapshots
- **API**: `aws redshift describe-clusters` → `.AutomatedSnapshotRetentionPeriod`
- **Pass**: `AutomatedSnapshotRetentionPeriod >= 7`
- **Fail**: `AutomatedSnapshotRetentionPeriod < 7`
- **Severity**: 🟡 MEDIUM | **Pillar**: Reliability

## Check: REDSHIFT_005 — SSL Enforcement
- **API**: `aws redshift describe-cluster-parameters` → `require_ssl`
- **Pass**: `require_ssl == true`
- **Fail**: `require_ssl == false`
- **Severity**: 🟡 MEDIUM | **Pillar**: Security

## Check: REDSHIFT_006 — Version Currency
- **API**: `aws redshift describe-clusters` → `.ClusterVersion`
- **Pass**: Running current cluster version
- **Fail**: Running outdated version
- **Severity**: 🟡 MEDIUM | **Pillar**: Security

## Check: REDSHIFT_007 — Enhanced VPC Routing
- **API**: `aws redshift describe-clusters` → `.EnhancedVpcRouting`
- **Pass**: `EnhancedVpcRouting == true`
- **Fail**: `EnhancedVpcRouting == false`
- **Severity**: 🟢 IMPROVEMENT | **Pillar**: Security
