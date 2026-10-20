# ElastiCache Service Checks

Reference: service-screener-v2 `services/elasticache/`

## Check: ELASTICACHE_001 — Encryption at Rest
- **API**: `aws elasticache describe-cache-clusters` / `describe-replication-groups` → `.AtRestEncryptionEnabled`
- **Pass**: `AtRestEncryptionEnabled == true`
- **Fail**: `AtRestEncryptionEnabled == false`
- **Severity**: 🔴 HIGH | **Pillar**: Security

## Check: ELASTICACHE_002 — Encryption in Transit
- **API**: `aws elasticache describe-replication-groups` → `.TransitEncryptionEnabled`
- **Pass**: `TransitEncryptionEnabled == true`
- **Fail**: `TransitEncryptionEnabled == false`
- **Severity**: 🔴 HIGH | **Pillar**: Security

## Check: ELASTICACHE_003 — Multi-AZ / Automatic Failover
- **API**: `aws elasticache describe-replication-groups` → `.AutomaticFailover`
- **Pass**: `AutomaticFailover == "enabled"`
- **Fail**: `AutomaticFailover == "disabled"`
- **Severity**: 🟡 MEDIUM | **Pillar**: Reliability

## Check: ELASTICACHE_004 — Engine Version Currency
- **API**: `aws elasticache describe-cache-clusters` → `.EngineVersion`
- **Pass**: Running supported, current engine version
- **Fail**: Running outdated or deprecated version
- **Severity**: 🟡 MEDIUM | **Pillar**: Security

## Check: ELASTICACHE_005 — Backup Enabled
- **API**: `aws elasticache describe-replication-groups` → `.SnapshotRetentionLimit`
- **Pass**: `SnapshotRetentionLimit > 0`
- **Fail**: `SnapshotRetentionLimit == 0`
- **Severity**: 🟡 MEDIUM | **Pillar**: Reliability

## Check: ELASTICACHE_006 — Node Type Currency
- **API**: `aws elasticache describe-cache-clusters` → `.CacheNodeType`
- **Pass**: Current generation node type (r7g, m7g, etc.)
- **Fail**: Previous generation node type (r5, m5, etc.)
- **Severity**: 🟢 IMPROVEMENT | **Pillar**: Performance Efficiency, Cost Optimization

## Check: ELASTICACHE_007 — Auth Token (Redis AUTH)
- **API**: `aws elasticache describe-replication-groups` → `.AuthTokenEnabled`
- **Pass**: `AuthTokenEnabled == true`
- **Fail**: `AuthTokenEnabled == false`
- **Severity**: 🟡 MEDIUM | **Pillar**: Security
