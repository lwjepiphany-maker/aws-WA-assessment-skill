# WAF (WAFv2) Service Checks

Reference: AWS WAF best practices; complements CloudFront CF_003 (WAF association) with account-wide coverage.

Note: WAF must be assessed in two scopes:
- `CLOUDFRONT` scope (query in us-east-1) — protects CloudFront distributions.
- `REGIONAL` scope (query per region) — protects ALB, API Gateway, AppSync, Cognito.

## Check: WAF_001 — Public Endpoints Protected by WAF
- **API**: `aws wafv2 list-web-acls --scope CLOUDFRONT/REGIONAL` + `list-resources-for-web-acl`
- **Pass**: Internet-facing CloudFront distributions, ALBs, and API Gateways are associated with a Web ACL
- **Fail**: Any public-facing resource has no Web ACL association
- **Severity**: 🟡 MEDIUM | **Pillar**: Security
- **Note**: For public WordPress/e-commerce/login endpoints, treat as 🔴 HIGH.

## Check: WAF_002 — AWS Managed Rule Groups
- **API**: `aws wafv2 get-web-acl` → `.Rules[].Statement.ManagedRuleGroupStatement`
- **Pass**: Uses AWS Managed Rules (e.g., CommonRuleSet, KnownBadInputs, SQLi)
- **Fail**: Web ACL has no managed rule groups (only custom/empty rules)
- **Severity**: 🟡 MEDIUM | **Pillar**: Security

## Check: WAF_003 — Rate-Based Rule
- **API**: `aws wafv2 get-web-acl` → `.Rules[].Statement.RateBasedStatement`
- **Pass**: At least one rate-based rule to throttle abusive clients
- **Fail**: No rate limiting configured
- **Severity**: 🟡 MEDIUM | **Pillar**: Security, Reliability

## Check: WAF_004 — Logging Enabled
- **API**: `aws wafv2 get-logging-configuration --resource-arn <webacl-arn>`
- **Pass**: Logging configured to CloudWatch Logs / S3 / Firehose
- **Fail**: `WAFNonexistentItemException` (no logging)
- **Severity**: 🟡 MEDIUM | **Pillar**: Security, Operational Excellence

## Check: WAF_005 — Default Action
- **API**: `aws wafv2 get-web-acl` → `.DefaultAction`
- **Pass**: DefaultAction is appropriate for the model (Allow with block rules, or Block for allowlist)
- **Fail**: Rules are all in Count mode (not actually blocking)
- **Severity**: 🟢 IMPROVEMENT | **Pillar**: Security
