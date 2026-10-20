# Shield / Anti-DDoS Service Checks

Reference: AWS Shield best practices.

Note: AWS Shield Standard is enabled automatically and free for all CloudFront, Route 53, and Global
Accelerator resources — it requires no configuration and is NOT what these checks evaluate. These
checks assess AWS Shield Advanced (the paid Anti-DDoS subscription) and its protections.

## Check: SHLD_001 — Shield Advanced Subscription
- **API**: `aws shield get-subscription-state`
- **Pass**: `SubscriptionState == "ACTIVE"`
- **Fail**: `SubscriptionState == "INACTIVE"`
- **Severity**: 🟢 IMPROVEMENT | **Pillar**: Reliability, Security
- **Note**: Optional for dev/sandbox accounts. For business-critical public workloads with
  availability/SLA requirements, treat as 🟡 MEDIUM. Shield Advanced has a significant monthly cost —
  always flag the cost tradeoff rather than recommending unconditionally.

## Check: SHLD_002 — Critical Public Resources Protected
- **API**: `aws shield list-protections` (only when SHLD_001 is ACTIVE)
- **Pass**: Internet-facing CloudFront, ALB/NLB, EIP, and Route 53 resources have Shield protections
- **Fail**: Subscribed to Shield Advanced but key public resources unprotected
- **Severity**: 🟡 MEDIUM | **Pillar**: Reliability

## Check: SHLD_003 — Proactive Engagement / Emergency Contacts
- **API**: `aws shield describe-emergency-contact-settings` + `describe-drt-access`
- **Pass**: Emergency contacts set and SRT (Shield Response Team) access configured
- **Fail**: No emergency contacts / SRT access when Shield Advanced is active
- **Severity**: 🟢 IMPROVEMENT | **Pillar**: Operational Excellence
- **Note**: Only applicable when SHLD_001 is ACTIVE.

## Check: SHLD_004 — WAF Pairing for Layer-7 DDoS
- **API**: correlate with WAF_001 (rate-based rules on protected resources)
- **Pass**: Shield-protected public resources also have WAF with rate-based rules (L7 mitigation)
- **Fail**: Shield Advanced without paired WAF rate limiting
- **Severity**: 🟢 IMPROVEMENT | **Pillar**: Security, Reliability
