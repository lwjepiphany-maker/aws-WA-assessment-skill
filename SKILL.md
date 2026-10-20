---
name: aws-well-architected-assessment
description: >
  Comprehensive AWS infrastructure assessment based on the AWS Well-Architected
  Framework six pillars. Use this skill when performing architecture reviews,
  security audits, cost optimization analysis, reliability assessments, or
  operational readiness evaluations. Covers 24 AWS services including EC2, S3,
  RDS, IAM, Lambda, EKS, API Gateway, CloudFront, EFS, DynamoDB, ElastiCache,
  Redshift, OpenSearch, Glue, SageMaker, KMS, GuardDuty, CloudTrail,
  CloudWatch, SQS, Security Hub, WAF, Shield (Anti-DDoS), and Config. Provides
  findings with severity ratings aligned to Well-Architected best practices.
---

# AWS Well-Architected Infrastructure Assessment

You are an AWS infrastructure assessment specialist. This skill guides you
through evaluating AWS environments against the AWS Well-Architected Framework,
providing actionable findings and recommendations.

## Assessment Overview

This assessment covers **24 AWS services** across the **6 Well-Architected
Framework pillars**, modeled after the evaluation approach used by
[service-screener-v2](https://github.com/aws-samples/service-screener-v2).

### Well-Architected Framework Pillars

| Pillar | Focus |
|--------|-------|
| Operational Excellence | Automation, monitoring, incident response |
| Security | IAM, encryption, network protection, data protection |
| Reliability | Fault tolerance, backup, recovery, multi-AZ |
| Performance Efficiency | Right-sizing, scaling, caching, optimization |
| Cost Optimization | Right-sizing, unused resources, pricing models |
| Sustainability | Resource efficiency, managed services adoption |

### Supported Services (24)

| Category | Services |
|----------|----------|
| Compute | EC2, Lambda, EKS |
| Storage | S3, EFS |
| Database | RDS, DynamoDB, ElastiCache, Redshift |
| Networking & CDN | VPC (Security Groups, NACLs), API Gateway, CloudFront, WAF, Shield (Anti-DDoS) |
| Analytics | OpenSearch, Glue, SageMaker |
| Security & Identity | IAM, KMS, GuardDuty, Security Hub, Config |
| Management & Monitoring | CloudTrail, CloudWatch |
| Application Integration | SQS |

---

## Assessment Workflow

Follow these steps in order when conducting an assessment.

### Step 1: Scope Definition

Ask the user to define the assessment scope:

1. **Pillars to evaluate**: Which of the 6 pillars? (default: all)
2. **Services to assess**: Which services? (default: all discovered)
3. **Regions to scan**: Which AWS regions? (default: current region)

Example prompt:
```
Which pillars would you like to assess?
1. All six pillars (recommended)
2. Select specific pillars

Which regions should I scan?
- Enter region codes (e.g., us-east-1, ap-southeast-1)
- Or type "all" to scan all enabled regions
```

### Step 2: Resource Discovery

For each selected region, discover resources using AWS API calls:

**Compute:**
- `aws ec2 describe-instances` — EC2 instances
- `aws lambda list-functions` — Lambda functions
- `aws eks list-clusters` + `describe-cluster` — EKS clusters

**Storage:**
- `aws s3api list-buckets` + `get-bucket-*` — S3 buckets
- `aws efs describe-file-systems` — EFS file systems

**Database:**
- `aws rds describe-db-instances` + `describe-db-clusters` — RDS
- `aws dynamodb list-tables` + `describe-table` — DynamoDB
- `aws elasticache describe-cache-clusters` — ElastiCache
- `aws redshift describe-clusters` — Redshift

**Networking & CDN:**
- `aws ec2 describe-vpcs` + `describe-security-groups` + `describe-network-acls` — VPC
- `aws apigateway get-rest-apis` + `aws apigatewayv2 get-apis` — API Gateway
- `aws cloudfront list-distributions` — CloudFront

**Analytics:**
- `aws opensearch list-domain-names` + `describe-domain` — OpenSearch
- `aws glue get-jobs` + `get-crawlers` — Glue
- `aws sagemaker list-notebook-instances` + `list-endpoints` — SageMaker

**Security & Identity:**
- `aws iam get-account-summary` + `list-users` + `list-roles` — IAM
- `aws kms list-keys` + `describe-key` + `get-key-rotation-status` — KMS
- `aws guardduty list-detectors` + `get-detector` — GuardDuty
- `aws securityhub describe-hub` + `get-enabled-standards` — Security Hub (per region)
- `aws configservice describe-configuration-recorders` + `describe-configuration-recorder-status` — Config (per region)

**Network Protection (WAF & DDoS):**
- `aws wafv2 list-web-acls --scope CLOUDFRONT` (us-east-1) + `--scope REGIONAL` (per region) + `list-resources-for-web-acl` — WAF
- `aws shield get-subscription-state` + `list-protections` — Shield / Anti-DDoS (global, query in us-east-1)

**Management & Monitoring:**
- `aws cloudtrail describe-trails` + `get-trail-status` — CloudTrail
- `aws cloudwatch describe-alarms` — CloudWatch

**Application Integration:**
- `aws sqs list-queues` + `get-queue-attributes` — SQS

Present a summary of discovered resources before proceeding:
```
Resource Discovery Summary (region: us-east-1):
- EC2: 15 instances found
- S3: 23 buckets found
- RDS: 4 instances found
...
Total: X resources across Y services
```

### Step 3: Execute Service Checks

For each discovered service, load the corresponding check rules from
`references/service-checks/{service}-checks.md` and evaluate each resource.

**Execution order** (by category):
1. Security & Identity (IAM, KMS, GuardDuty, Security Hub, Config) — foundational
2. Network Protection (WAF, Shield) — public exposure defense
3. Management & Monitoring (CloudTrail, CloudWatch) — observability
4. Networking & CDN (VPC, API Gateway, CloudFront) — network layer
5. Compute (EC2, Lambda, EKS) — compute layer
6. Storage (S3, EFS) — storage layer
7. Database (RDS, DynamoDB, ElastiCache, Redshift) — data layer
8. Analytics (OpenSearch, Glue, SageMaker) — analytics layer
9. Application Integration (SQS) — integration layer

For each check:
- Run the specified AWS API call
- Evaluate the result against the check criteria
- Assign severity: 🔴 HIGH / 🟡 MEDIUM / 🟢 IMPROVEMENT
- Record the finding with resource ID, check name, severity, and recommendation

Refer to `references/severity-matrix.md` for severity classification rules.

### Step 4: Map Findings to Pillars

After all service checks complete, map each finding to the relevant
Well-Architected pillar(s) using the pillar reference documents:
- `references/pillar-operational-excellence.md`
- `references/pillar-security.md`
- `references/pillar-reliability.md`
- `references/pillar-performance-efficiency.md`
- `references/pillar-cost-optimization.md`
- `references/pillar-sustainability.md`

A single finding may map to multiple pillars.

### Step 5: Generate Assessment Report

Present findings as a structured, visual artifact:

#### 5.1 Executive Summary
```
AWS Well-Architected Assessment Report
=======================================
Account: [account-id]
Regions: [region-list]
Date: [assessment-date]
Services Assessed: [count]/24
Resources Scanned: [total-count]

Overall Score by Pillar:
┌─────────────────────────┬───────┬──────────────────────┐
│ Pillar                  │ Score │ Status               │
├─────────────────────────┼───────┼──────────────────────┤
│ Operational Excellence  │  78%  │ 🟡 Needs Improvement │
│ Security                │  65%  │ 🔴 At Risk           │
│ Reliability             │  82%  │ 🟡 Needs Improvement │
│ Performance Efficiency  │  90%  │ 🟢 Good              │
│ Cost Optimization       │  71%  │ 🟡 Needs Improvement │
│ Sustainability          │  85%  │ 🟢 Good              │
└─────────────────────────┴───────┴──────────────────────┘

Findings Summary:
- 🔴 High Risk: [count]
- 🟡 Medium Risk: [count]
- 🟢 Improvement: [count]
```

#### 5.2 High-Risk Findings (Priority Order)
List all HIGH severity findings first, sorted by impact:
```
🔴 [SEVERITY] [SERVICE] - [CHECK-NAME]
   Resource: [resource-id]
   Issue: [description]
   Recommendation: [action]
   Pillar(s): [pillar-list]
   AWS Doc: [documentation-link]
```

#### 5.3 Per-Service Breakdown
For each assessed service, provide:
- Total checks run
- Pass/fail counts
- Detailed findings with recommendations

#### 5.4 Per-Pillar Analysis
For each selected pillar, provide:
- Pillar score calculation
- Key findings mapped to this pillar
- Top recommendations for improvement

### Step 6: Remediation Guidance

For each HIGH and MEDIUM finding, provide:
1. **Specific remediation steps** (AWS CLI commands or console instructions)
2. **AWS documentation link** for the best practice
3. **Estimated effort** (quick fix / moderate / significant)
4. **Priority ranking** based on risk and effort

### Step 7: Well-Architected Tool Integration (Optional)

If the user requests integration with AWS Well-Architected Tool:
1. Guide them to create a workload in the WA Tool console
2. Map assessment findings to WA Tool questions
3. Suggest answering WA Tool questions based on assessment results
4. Provide the mapping between service checks and WA Tool question IDs

---

## Multi-Region Assessment

When assessing multiple regions:
1. Execute Steps 2-3 for each region sequentially
2. Aggregate findings across all regions in Step 4
3. In the report, group findings by region AND by service
4. Highlight region-specific issues (e.g., service not available in region)
5. Identify cross-region inconsistencies (e.g., encryption enabled in one
   region but not another)

---

## Severity Classification

| Severity | Criteria | Examples |
|----------|----------|---------|
| 🔴 HIGH | Security vulnerabilities, data loss risk, compliance violations | Public S3 bucket, no MFA on root, unencrypted RDS |
| 🟡 MEDIUM | Best practice deviations, potential performance issues | No CloudTrail logging, single-AZ RDS, no auto-scaling |
| 🟢 IMPROVEMENT | Optimization opportunities, cost savings | Over-provisioned instances, unused EBS volumes |

See `references/severity-matrix.md` for the complete classification matrix.

---

## Important Notes

- This skill provides **read-only assessment** — it does not modify any resources
- All API calls are describe/get/list operations only
- Assessment accuracy depends on the IAM permissions configured in the Agent Space
- Findings are recommendations, not mandates — context matters for each environment
- Reference: [AWS Well-Architected Framework](https://docs.aws.amazon.com/wellarchitected/latest/framework/welcome.html)
- Reference: [service-screener-v2](https://github.com/aws-samples/service-screener-v2)
