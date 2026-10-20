# API Gateway Service Checks

Reference: service-screener-v2 `services/apigateway/`

## Check: APIGW_001 — Access Logging
- **API**: `aws apigateway get-stages` → `.accessLogSettings`
- **Pass**: Access log settings configured with destination ARN
- **Fail**: No access logging configured
- **Severity**: 🟡 MEDIUM | **Pillar**: Operational Excellence, Security

## Check: APIGW_002 — Authorization
- **API**: `aws apigateway get-resources` + `get-method` → `.authorizationType`
- **Pass**: Methods have authorization (IAM, Cognito, Lambda, API Key)
- **Fail**: `authorizationType == "NONE"` on non-public endpoints
- **Severity**: 🔴 HIGH | **Pillar**: Security

## Check: APIGW_003 — Throttling Configuration
- **API**: `aws apigateway get-stages` → `.methodSettings.*.throttlingRateLimit`
- **Pass**: Throttling limits configured
- **Fail**: Default throttling only (no custom limits)
- **Severity**: 🟡 MEDIUM | **Pillar**: Reliability, Security

## Check: APIGW_004 — WAF Integration
- **API**: `aws wafv2 get-web-acl-for-resource`
- **Pass**: WAF WebACL associated with API stage
- **Fail**: No WAF protection
- **Severity**: 🟡 MEDIUM | **Pillar**: Security

## Check: APIGW_005 — TLS Version
- **API**: `aws apigateway get-domain-names` → `.securityPolicy`
- **Pass**: `securityPolicy == "TLS_1_2"`
- **Fail**: `securityPolicy == "TLS_1_0"`
- **Severity**: 🟡 MEDIUM | **Pillar**: Security

## Check: APIGW_006 — CloudWatch Metrics
- **API**: `aws apigateway get-stages` → `.methodSettings.*.metricsEnabled`
- **Pass**: CloudWatch metrics enabled
- **Fail**: Metrics disabled
- **Severity**: 🟢 IMPROVEMENT | **Pillar**: Operational Excellence

## Check: APIGW_007 — Caching
- **API**: `aws apigateway get-stages` → `.cacheClusterEnabled`
- **Pass**: Caching enabled for appropriate stages
- **Fail**: No caching configured
- **Severity**: 🟢 IMPROVEMENT | **Pillar**: Performance Efficiency

## Check: APIGW_008 — X-Ray Tracing
- **API**: `aws apigateway get-stages` → `.tracingEnabled`
- **Pass**: `tracingEnabled == true`
- **Fail**: `tracingEnabled == false`
- **Severity**: 🟢 IMPROVEMENT | **Pillar**: Operational Excellence
