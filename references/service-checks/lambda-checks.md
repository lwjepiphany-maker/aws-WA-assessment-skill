# Lambda Service Checks

Reference: service-screener-v2 `services/lambda_/`

## Check: LAMBDA_001 — Runtime Currency
- **API**: `aws lambda list-functions` → `.Runtime`
- **Pass**: Supported, non-deprecated runtime
- **Fail**: Deprecated or end-of-life runtime (python3.8, nodejs14.x, etc.)
- **Severity**: 🔴 HIGH
- **Pillar**: Security, Operational Excellence
- **Recommendation**: Upgrade to a supported runtime version.

## Check: LAMBDA_002 — Dead Letter Queue Configuration
- **API**: `aws lambda get-function-configuration` → `.DeadLetterConfig`
- **Pass**: DLQ (SQS or SNS) configured
- **Fail**: No DLQ configured
- **Severity**: 🟡 MEDIUM
- **Pillar**: Reliability
- **Recommendation**: Configure a DLQ to capture failed async invocations.

## Check: LAMBDA_003 — Execution Role Scope
- **API**: `aws iam get-role-policy` / `list-attached-role-policies`
- **Pass**: Role follows least privilege (no `*` resource with broad actions)
- **Fail**: Role has overly permissive policies (e.g., `Action: *`)
- **Severity**: 🔴 HIGH
- **Pillar**: Security
- **Recommendation**: Scope IAM role to minimum required permissions.

## Check: LAMBDA_004 — Environment Variable Encryption
- **API**: `aws lambda get-function-configuration` → `.KMSKeyArn`
- **Pass**: KMS key configured for environment variable encryption
- **Fail**: Using default encryption (no customer-managed KMS key)
- **Severity**: 🟡 MEDIUM
- **Pillar**: Security
- **Recommendation**: Use a customer-managed KMS key for sensitive env vars.

## Check: LAMBDA_005 — Timeout Configuration
- **API**: `aws lambda get-function-configuration` → `.Timeout`
- **Pass**: Timeout set appropriately (not default 3s for complex functions)
- **Fail**: Default timeout (3s) on functions with external dependencies
- **Severity**: 🟡 MEDIUM
- **Pillar**: Reliability
- **Recommendation**: Set timeout based on expected execution duration.

## Check: LAMBDA_006 — Memory Optimization
- **API**: `aws lambda get-function-configuration` → `.MemorySize`
- **Pass**: Memory sized appropriately (use Lambda Power Tuning)
- **Fail**: Default 128MB or significantly over-provisioned
- **Severity**: 🟢 IMPROVEMENT
- **Pillar**: Cost Optimization, Performance Efficiency
- **Recommendation**: Use AWS Lambda Power Tuning to find optimal memory.

## Check: LAMBDA_007 — VPC Configuration
- **API**: `aws lambda get-function-configuration` → `.VpcConfig`
- **Pass**: Functions accessing VPC resources are VPC-attached
- **Fail**: Functions accessing private resources without VPC config
- **Severity**: 🟡 MEDIUM
- **Pillar**: Security
- **Recommendation**: Attach Lambda to VPC when accessing private resources.

## Check: LAMBDA_008 — Tracing Enabled
- **API**: `aws lambda get-function-configuration` → `.TracingConfig.Mode`
- **Pass**: `Mode == "Active"`
- **Fail**: `Mode == "PassThrough"`
- **Severity**: 🟢 IMPROVEMENT
- **Pillar**: Operational Excellence
- **Recommendation**: Enable X-Ray active tracing for observability.

## Check: LAMBDA_009 — Reserved Concurrency
- **API**: `aws lambda get-function-concurrency`
- **Pass**: Reserved concurrency set for critical functions
- **Fail**: No reserved concurrency on critical functions
- **Severity**: 🟢 IMPROVEMENT
- **Pillar**: Reliability
- **Recommendation**: Set reserved concurrency to guarantee capacity.

## Check: LAMBDA_010 — Code Signing
- **API**: `aws lambda get-function` → `.CodeSigningConfigArn`
- **Pass**: Code signing configured
- **Fail**: No code signing
- **Severity**: 🟢 IMPROVEMENT
- **Pillar**: Security
- **Recommendation**: Enable code signing to ensure deployment integrity.
