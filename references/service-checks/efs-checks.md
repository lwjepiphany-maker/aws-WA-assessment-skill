# EFS Service Checks

Reference: service-screener-v2 `services/efs/`

## Check: EFS_001 — Encryption at Rest
- **API**: `aws efs describe-file-systems` → `.Encrypted`
- **Pass**: `Encrypted == true`
- **Fail**: `Encrypted == false`
- **Severity**: 🔴 HIGH
- **Pillar**: Security
- **Recommendation**: Enable encryption at rest using KMS. Note: requires recreating the file system.

## Check: EFS_002 — Encryption in Transit
- **API**: `aws efs describe-mount-target-security-groups` + mount target config
- **Pass**: Mount targets enforce TLS (port 2049 with TLS)
- **Fail**: TLS not enforced
- **Severity**: 🟡 MEDIUM
- **Pillar**: Security
- **Recommendation**: Use EFS mount helper with TLS option enabled.

## Check: EFS_003 — Backup Policy
- **API**: `aws efs describe-backup-policy`
- **Pass**: `Status == "ENABLED"`
- **Fail**: Backup not enabled
- **Severity**: 🟡 MEDIUM
- **Pillar**: Reliability
- **Recommendation**: Enable automatic backups via AWS Backup.

## Check: EFS_004 — Lifecycle Policy
- **API**: `aws efs describe-lifecycle-configuration`
- **Pass**: Lifecycle policies configured (transition to IA)
- **Fail**: No lifecycle policy
- **Severity**: 🟡 MEDIUM
- **Pillar**: Cost Optimization
- **Recommendation**: Configure lifecycle policy to move infrequent data to IA storage class.

## Check: EFS_005 — File System Policy
- **API**: `aws efs describe-file-system-policy`
- **Pass**: Resource policy configured (e.g., enforce TLS, restrict root access)
- **Fail**: No file system policy
- **Severity**: 🟡 MEDIUM
- **Pillar**: Security
- **Recommendation**: Configure file system policy to enforce encryption in transit and restrict access.

## Check: EFS_006 — Access Points
- **API**: `aws efs describe-access-points`
- **Pass**: Access points configured with POSIX user and root directory
- **Fail**: No access points (direct mount target access only)
- **Severity**: 🟢 IMPROVEMENT
- **Pillar**: Security
- **Recommendation**: Use EFS access points for application-specific entry points with enforced user identity.
