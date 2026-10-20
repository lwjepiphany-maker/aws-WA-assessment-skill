# OpenSearch Service Checks

Reference: service-screener-v2 `services/opensearch/`

## Check: OS_001 — Encryption at Rest
- **API**: `aws opensearch describe-domain` → `.EncryptionAtRestOptions.Enabled`
- **Pass**: `Enabled == true`
- **Fail**: `Enabled == false`
- **Severity**: 🔴 HIGH | **Pillar**: Security

## Check: OS_002 — Node-to-Node Encryption
- **API**: `aws opensearch describe-domain` → `.NodeToNodeEncryptionOptions.Enabled`
- **Pass**: `Enabled == true`
- **Fail**: `Enabled == false`
- **Severity**: 🔴 HIGH | **Pillar**: Security

## Check: OS_003 — HTTPS Enforcement
- **API**: `aws opensearch describe-domain` → `.DomainEndpointOptions.EnforceHTTPS`
- **Pass**: `EnforceHTTPS == true`
- **Fail**: `EnforceHTTPS == false`
- **Severity**: 🔴 HIGH | **Pillar**: Security

## Check: OS_004 — VPC Deployment
- **API**: `aws opensearch describe-domain` → `.VPCOptions`
- **Pass**: Domain deployed in VPC
- **Fail**: Public domain (no VPC config)
- **Severity**: 🔴 HIGH | **Pillar**: Security

## Check: OS_005 — Zone Awareness
- **API**: `aws opensearch describe-domain` → `.ClusterConfig.ZoneAwarenessEnabled`
- **Pass**: `ZoneAwarenessEnabled == true`
- **Fail**: `ZoneAwarenessEnabled == false`
- **Severity**: 🟡 MEDIUM | **Pillar**: Reliability

## Check: OS_006 — Dedicated Master Nodes
- **API**: `aws opensearch describe-domain` → `.ClusterConfig.DedicatedMasterEnabled`
- **Pass**: `DedicatedMasterEnabled == true` (for production domains)
- **Fail**: No dedicated master nodes
- **Severity**: 🟡 MEDIUM | **Pillar**: Reliability, Performance Efficiency

## Check: OS_007 — Audit Logging
- **API**: `aws opensearch describe-domain` → `.LogPublishingOptions.AUDIT_LOGS`
- **Pass**: Audit logs published to CloudWatch
- **Fail**: No audit logging
- **Severity**: 🟡 MEDIUM | **Pillar**: Security

## Check: OS_008 — Engine Version
- **API**: `aws opensearch describe-domain` → `.EngineVersion`
- **Pass**: Running current supported version
- **Fail**: Running outdated version
- **Severity**: 🟡 MEDIUM | **Pillar**: Security
