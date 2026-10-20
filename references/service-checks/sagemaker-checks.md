# SageMaker Service Checks

Reference: service-screener-v2 `services/sagemaker/`

## Check: SM_001 — Notebook Instance Encryption
- **API**: `aws sagemaker describe-notebook-instance` → `.KmsKeyId`
- **Pass**: KMS key configured for notebook encryption
- **Fail**: No KMS key (using default encryption)
- **Severity**: 🟡 MEDIUM | **Pillar**: Security

## Check: SM_002 — Notebook Direct Internet Access
- **API**: `aws sagemaker describe-notebook-instance` → `.DirectInternetAccess`
- **Pass**: `DirectInternetAccess == "Disabled"`
- **Fail**: `DirectInternetAccess == "Enabled"`
- **Severity**: 🟡 MEDIUM | **Pillar**: Security

## Check: SM_003 — Notebook Root Access
- **API**: `aws sagemaker describe-notebook-instance` → `.RootAccess`
- **Pass**: `RootAccess == "Disabled"`
- **Fail**: `RootAccess == "Enabled"`
- **Severity**: 🟡 MEDIUM | **Pillar**: Security

## Check: SM_004 — Notebook Instance VPC
- **API**: `aws sagemaker describe-notebook-instance` → `.SubnetId`
- **Pass**: Notebook deployed in VPC
- **Fail**: No VPC configuration
- **Severity**: 🟡 MEDIUM | **Pillar**: Security

## Check: SM_005 — Endpoint Encryption
- **API**: `aws sagemaker describe-endpoint-config` → `.KmsKeyId`
- **Pass**: KMS key configured for endpoint
- **Fail**: No KMS key
- **Severity**: 🟡 MEDIUM | **Pillar**: Security

## Check: SM_006 — Idle Notebook Instances
- **API**: `aws sagemaker list-notebook-instances` → `.NotebookInstanceStatus`
- **Pass**: Notebooks in `InService` are actively used
- **Fail**: Notebooks in `InService` with no recent activity
- **Severity**: 🟡 MEDIUM | **Pillar**: Cost Optimization

## Check: SM_007 — Endpoint Auto Scaling
- **API**: `aws application-autoscaling describe-scalable-targets` (SageMaker namespace)
- **Pass**: Auto-scaling configured for production endpoints
- **Fail**: No auto-scaling on endpoints
- **Severity**: 🟢 IMPROVEMENT | **Pillar**: Performance Efficiency, Cost Optimization
