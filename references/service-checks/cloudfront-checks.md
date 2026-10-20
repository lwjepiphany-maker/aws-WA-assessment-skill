# CloudFront Service Checks

Reference: service-screener-v2 `services/cloudfront/`

## Check: CF_001 — HTTPS Enforcement
- **API**: `aws cloudfront get-distribution` → `.ViewerProtocolPolicy`
- **Pass**: `ViewerProtocolPolicy == "redirect-to-https"` or `"https-only"`
- **Fail**: `ViewerProtocolPolicy == "allow-all"`
- **Severity**: 🔴 HIGH | **Pillar**: Security

## Check: CF_002 — TLS Minimum Version
- **API**: `aws cloudfront get-distribution` → `.ViewerCertificate.MinimumProtocolVersion`
- **Pass**: `TLSv1.2_2021` or newer
- **Fail**: `TLSv1` or `TLSv1.1_2016`
- **Severity**: 🟡 MEDIUM | **Pillar**: Security

## Check: CF_003 — WAF Integration
- **API**: `aws cloudfront get-distribution` → `.WebACLId`
- **Pass**: WAF WebACL associated
- **Fail**: No WAF protection (`WebACLId` empty)
- **Severity**: 🟡 MEDIUM | **Pillar**: Security

## Check: CF_004 — Access Logging
- **API**: `aws cloudfront get-distribution` → `.Logging.Enabled`
- **Pass**: `Logging.Enabled == true`
- **Fail**: `Logging.Enabled == false`
- **Severity**: 🟡 MEDIUM | **Pillar**: Security, Operational Excellence

## Check: CF_005 — Origin Access Control (OAC)
- **API**: `aws cloudfront get-distribution` → `.Origins.Items[].OriginAccessControlId`
- **Pass**: OAC configured for S3 origins (replaces legacy OAI)
- **Fail**: No OAC/OAI for S3 origins
- **Severity**: 🔴 HIGH | **Pillar**: Security

## Check: CF_006 — Geo Restriction
- **API**: `aws cloudfront get-distribution` → `.Restrictions.GeoRestriction`
- **Pass**: Geo restriction configured if required by compliance
- **Fail**: No geo restriction when compliance requires it
- **Severity**: 🟢 IMPROVEMENT | **Pillar**: Security

## Check: CF_007 — Default Root Object
- **API**: `aws cloudfront get-distribution` → `.DefaultRootObject`
- **Pass**: Default root object configured
- **Fail**: No default root object (may expose directory listing)
- **Severity**: 🟢 IMPROVEMENT | **Pillar**: Security

## Check: CF_008 — Compression Enabled
- **API**: `aws cloudfront get-distribution` → `.DefaultCacheBehavior.Compress`
- **Pass**: `Compress == true`
- **Fail**: `Compress == false`
- **Severity**: 🟢 IMPROVEMENT | **Pillar**: Performance Efficiency, Cost Optimization
