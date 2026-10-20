# IAM Service Checks

Reference: service-screener-v2 `services/iam/`

## Check: IAM_001 — Root Account MFA
- **API**: `aws iam get-account-summary` → `.SummaryMap.AccountMFAEnabled`
- **Pass**: `AccountMFAEnabled == 1`
- **Fail**: `AccountMFAEnabled == 0`
- **Severity**: 🔴 HIGH | **Pillar**: Security

## Check: IAM_002 — Root Account Access Keys
- **API**: `aws iam get-account-summary` → `.SummaryMap.AccountAccessKeysPresent`
- **Pass**: `AccountAccessKeysPresent == 0`
- **Fail**: `AccountAccessKeysPresent > 0`
- **Severity**: 🔴 HIGH | **Pillar**: Security

## Check: IAM_003 — Password Policy Strength
- **API**: `aws iam get-account-password-policy`
- **Pass**: MinimumPasswordLength >= 14, RequireSymbols, RequireNumbers, RequireUppercase, RequireLowercase, MaxPasswordAge <= 90
- **Fail**: Weak password policy or no policy
- **Severity**: 🔴 HIGH | **Pillar**: Security

## Check: IAM_004 — User MFA Enabled
- **API**: `aws iam list-users` + `list-mfa-devices`
- **Pass**: All console users have MFA enabled
- **Fail**: Console users without MFA
- **Severity**: 🔴 HIGH | **Pillar**: Security

## Check: IAM_005 — Access Key Rotation
- **API**: `aws iam list-access-keys` → `.CreateDate`
- **Pass**: Access keys rotated within 90 days
- **Fail**: Access keys older than 90 days
- **Severity**: 🟡 MEDIUM | **Pillar**: Security

## Check: IAM_006 — Unused Credentials
- **API**: `aws iam generate-credential-report` → `password_last_used`, `access_key_last_used`
- **Pass**: All credentials used within 90 days
- **Fail**: Credentials unused for > 90 days
- **Severity**: 🟡 MEDIUM | **Pillar**: Security

## Check: IAM_007 — Overly Permissive Policies
- **API**: `aws iam list-policies` + `get-policy-version`
- **Pass**: No policies with `"Effect": "Allow", "Action": "*", "Resource": "*"`
- **Fail**: Policies with full admin access
- **Severity**: 🔴 HIGH | **Pillar**: Security

## Check: IAM_008 — IAM Users vs Roles
- **API**: `aws iam list-users`
- **Pass**: Minimal IAM users; workloads use IAM roles
- **Fail**: Many IAM users with programmatic access
- **Severity**: 🟡 MEDIUM | **Pillar**: Security

## Check: IAM_009 — Support Role
- **API**: `aws iam list-entities-for-policy` (AWSSupportAccess)
- **Pass**: Support access role/user configured
- **Fail**: No entity with AWSSupportAccess
- **Severity**: 🟢 IMPROVEMENT | **Pillar**: Operational Excellence

## Check: IAM_010 — Access Analyzer
- **API**: `aws accessanalyzer list-analyzers`
- **Pass**: IAM Access Analyzer enabled
- **Fail**: No analyzer configured
- **Severity**: 🟡 MEDIUM | **Pillar**: Security
