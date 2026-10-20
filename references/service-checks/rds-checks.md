# RDS Service Checks

Reference: service-screener-v2 `services/rds/`

## Check: RDS_001 — Encryption at Rest
- **API**: `aws rds describe-db-instances` → `.StorageEncrypted`
- **Pass**: `StorageEncrypted == true`
- **Fail**: `StorageEncrypted == false`
- **Severity**: 🔴 HIGH | **Pillar**: Security

## Check: RDS_002 — Multi-AZ Deployment
- **API**: `aws rds describe-db-instances` → `.MultiAZ`
- **Pass**: `MultiAZ == true`
- **Fail**: `MultiAZ == false`
- **Severity**: 🔴 HIGH | **Pillar**: Reliability

## Check: RDS_003 — Public Accessibility
- **API**: `aws rds describe-db-instances` → `.PubliclyAccessible`
- **Pass**: `PubliclyAccessible == false`
- **Fail**: `PubliclyAccessible == true`
- **Severity**: 🔴 HIGH | **Pillar**: Security

## Check: RDS_004 — Automated Backups
- **API**: `aws rds describe-db-instances` → `.BackupRetentionPeriod`
- **Pass**: `BackupRetentionPeriod >= 7`
- **Fail**: `BackupRetentionPeriod < 7` or `0`
- **Severity**: 🟡 MEDIUM | **Pillar**: Reliability

## Check: RDS_005 — Minor Version Auto Upgrade
- **API**: `aws rds describe-db-instances` → `.AutoMinorVersionUpgrade`
- **Pass**: `AutoMinorVersionUpgrade == true`
- **Fail**: `AutoMinorVersionUpgrade == false`
- **Severity**: 🟡 MEDIUM | **Pillar**: Security, Operational Excellence

## Check: RDS_006 — Performance Insights
- **API**: `aws rds describe-db-instances` → `.PerformanceInsightsEnabled`
- **Pass**: `PerformanceInsightsEnabled == true`
- **Fail**: `PerformanceInsightsEnabled == false`
- **Severity**: 🟢 IMPROVEMENT | **Pillar**: Performance Efficiency

## Check: RDS_007 — Deletion Protection
- **API**: `aws rds describe-db-instances` → `.DeletionProtection`
- **Pass**: `DeletionProtection == true`
- **Fail**: `DeletionProtection == false`
- **Severity**: 🟡 MEDIUM | **Pillar**: Reliability

## Check: RDS_008 — IAM Authentication
- **API**: `aws rds describe-db-instances` → `.IAMDatabaseAuthenticationEnabled`
- **Pass**: `IAMDatabaseAuthenticationEnabled == true`
- **Fail**: `IAMDatabaseAuthenticationEnabled == false`
- **Severity**: 🟢 IMPROVEMENT | **Pillar**: Security

## Check: RDS_009 — Engine Version Currency
- **API**: `aws rds describe-db-instances` → `.EngineVersion`
- **Pass**: Running a supported, non-deprecated engine version
- **Fail**: Running deprecated or end-of-life version
- **Severity**: 🔴 HIGH | **Pillar**: Security

## Check: RDS_010 — Enhanced Monitoring
- **API**: `aws rds describe-db-instances` → `.MonitoringInterval`
- **Pass**: `MonitoringInterval > 0`
- **Fail**: `MonitoringInterval == 0`
- **Severity**: 🟢 IMPROVEMENT | **Pillar**: Operational Excellence
