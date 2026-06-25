# GRC Gap Assessment Program

## Phase 1: Assessment Framework & Methodology

**Organization:** [Enterprise / Federal Contractor]  
**Program Owner:** Chief Information Security Officer & Compliance Officer  
**Phase Duration:** Month 1  
**Key Outcome:** Assessment framework operational and documented  

---

## Executive Summary

Phase 1 establishes the foundation for a comprehensive GRC Gap Assessment program. This phase defines the assessment methodology, control evaluation procedures, risk scoring framework, and compliance mapping to drive organizational compliance maturity.

**Key Objectives:**
1. Establish GRC gap assessment framework aligned to NIST 800-171
2. Define control evaluation procedures (current state vs. target state)
3. Create risk-based gap prioritization methodology
4. Develop compliance mapping across multiple frameworks
5. Document assessment procedures for consistent, repeatable evaluations
6. Establish baseline compliance metrics and improvement tracking

**Key Outcomes:**
- Assessment framework documented
- Control evaluation procedures defined
- Risk scoring methodology established
- Compliance framework mapping (NIST 800-171 + others)
- Assessment templates ready for Phase 2
- Gap prioritization procedures documented

---

## Part 1: The GRC Gap Assessment Challenge

### What is a Compliance Gap?

**Definition:** A gap is the difference between current state (what you have) and target state (what compliance requires) for a specific security control or process.

**Examples of Gaps:**

| Control | Current State | Target State | Gap |
|---------|---------------|--------------|-----|
| MFA (NIST 3.5.3) | MFA enabled for 60% of users | MFA required for 100% of users | 40% user population not covered |
| Encryption (NIST 3.13.1) | Data encrypted at rest, not in transit | All data encrypted at rest and in transit | No in-transit encryption |
| Access Reviews (NIST 3.5.9) | Annual access reviews performed | Quarterly access reviews required | Reviews only annual, need quarterly |
| Incident Response (NIST 3.6.1) | Basic IR procedures documented | Formal IR procedures with playbooks | No playbooks, procedures are basic |

### Why Gap Assessments Matter

**Business Impact:**
- Compliance violations = fines ($100K-$10M+)
- Audit failures = contract termination (federal contractors)
- Security breaches = expensive, avoidable
- Board visibility = governance credibility

**The Gap Assessment Solves:**
- Know exactly where you stand vs. requirements
- Prioritize which gaps to fix first (risk-based)
- Track progress (how far until compliant?)
- Executive visibility (what does remediation cost?)

---

## Part 2: NIST 800-171 Assessment Framework

### NIST SP 800-171 Overview

**What it is:** Security controls for protecting controlled unclassified information (CUI) in federal systems and contractors.

**Who needs it:** Any defense contractor, federal subcontractor handling CUI.

**Scope:** 14 control families covering 110+ individual controls

### NIST 800-171 Control Families

| Family | Focus | Example Controls |
|--------|-------|------------------|
| **3.1** | Access Control | User identity, authentication, authorization |
| **3.2** | Awareness & Training | Security training, awareness programs |
| **3.3** | Audit & Accountability | Logging, monitoring, audit trails |
| **3.4** | Configuration Management | Baseline configs, change management |
| **3.5** | Identification & Authentication | MFA, password policies, credential management |
| **3.6** | Incident Response | IR procedures, breach notification, lessons learned |
| **3.7** | Maintenance | System maintenance, vulnerability management |
| **3.8** | Media Protection | Data classification, media handling, destruction |
| **3.9** | Personnel Security | Background checks, access agreements, termination |
| **3.10** | Physical & Environmental | Physical security, access controls, environmental |
| **3.11** | Planning | Security planning, contingency planning |
| **3.12** | System & Communications Protection | Network security, encryption, segmentation |
| **3.13** | System & Information Integrity | Malware protection, monitoring, patch management |
| **3.14** | Supply Chain Risk Management | Vendor assessment, monitoring, risk management |

---

## Part 3: Gap Assessment Methodology

### Gap Assessment Approach

**Step 1: Control Inventory**
- List all NIST 800-171 controls applicable to the organization
- Identify which controls are in scope (technology, process, personnel)
- Map controls to business systems and processes

**Step 2: Current State Assessment**
- For each control, evaluate: "What do we have today?"
- Gather evidence: policies, procedures, configurations, audit logs
- Document implementation level: Not Implemented / Partially Implemented / Implemented / Optimized

**Step 3: Target State Definition**
- Define: "What does NIST 800-171 require?"
- Reference control description, intent, and supplemental guidance
- Identify implementation examples and best practices

**Step 4: Gap Analysis**
- Compare current state vs. target state
- Document the gap: What's missing? What's incomplete?
- Assess impact and severity of the gap

**Step 5: Risk Scoring**
- Score gap by severity (CRITICAL, HIGH, MEDIUM, LOW)
- Consider: Data at risk, exploit likelihood, business impact
- Prioritize which gaps to remediate first

**Step 6: Remediation Planning**
- Create action plan for each significant gap
- Assign owner, timeline, resources
- Define success criteria and validation method

---

## Part 4: Control Evaluation Framework

### Maturity Levels

Each control is evaluated on a 4-point maturity scale:

| Level | Definition | Example |
|-------|-----------|---------|
| **0: Not Implemented** | No evidence of implementation | "We don't have MFA yet" |
| **1: Partially Implemented** | Implemented for some systems/users | "MFA enabled for admins only, not all users" |
| **2: Implemented** | Meets control requirements | "MFA required for all user accounts" |
| **3: Optimized** | Enhanced implementation, continuous improvement | "MFA + passwordless + continuous verification" |

### Control Evaluation Procedure

For each NIST 800-171 control:

**Evidence Gathering:**
1. Policy or procedure documentation
2. Configuration evidence (screenshots, configs)
3. Logs or monitoring data
4. Interview with control owner
5. Testing/validation evidence

**Current State Documentation:**

```
Control: 3.5.3 (Multi-factor Authentication)
Description: Use multi-factor authentication for local and remote access

Current State Assessment:
- Admins: MFA enabled via Okta (100% coverage)
- Regular users: MFA optional, ~60% adoption
- VPN: MFA required via hardware tokens (100%)
- Cloud access: MFA via Okta (85% coverage)
- Overall: PARTIALLY IMPLEMENTED (1.5/3.0)

Evidence:
- Okta configuration (see Appendix A)
- VPN token distribution logs (see Appendix B)
- User MFA enrollment report (see Appendix C)

Gaps:
- Regular user MFA not mandatory (required by control)
- Cloud coverage at 85%, not 100% (need to reach all cloud users)

Target State:
- MFA required for ALL user access (local, remote, cloud, VPN)
- MFA method: Okta (primary) or hardware tokens (backup)
- Coverage: 100% of user population

Gap: Approximately 40% of regular users not covered by MFA requirement
```

---

## Part 5: Risk Scoring for Gap Prioritization

### Gap Severity Framework

Gaps are scored on IMPACT × LIKELIHOOD × REGULATORY EXPOSURE:

**Impact (What's at risk?)**
- CRITICAL: Data breach = $10M+ loss, contract termination, criminal liability
- HIGH: Data breach = $1-10M loss, significant business disruption
- MEDIUM: Data breach = $100K-$1M loss, operational impact
- LOW: Data breach = <$100K loss, minimal business impact

**Likelihood (How likely to be exploited?)**
- CRITICAL: Actively exploited, public zero-day, easy to exploit
- HIGH: Known vulnerability, exploitation tools available, network-accessible
- MEDIUM: Known vulnerability, requires some skill, limited accessibility
- LOW: Obscure vulnerability, requires advanced skill or physical access

**Regulatory Exposure (What's the compliance risk?)**
- CRITICAL: Federal requirement, audit failure = contract termination
- HIGH: Federal requirement, audit failure = fines + probation
- MEDIUM: Industry requirement, audit failure = corrective action
- LOW: Best practice, audit finding = noted but not critical

### Gap Risk Score Calculation

```
Gap Risk Score = (Impact + Likelihood + Regulatory) / 3

Score Ranges:
9-10: CRITICAL - Remediate immediately (1-7 days)
7-8: HIGH - Remediate within 30 days
5-6: MEDIUM - Remediate within 90 days
3-4: LOW - Include in annual remediation cycle
1-2: MINIMAL - Monitor, include in next update
```

**Example:**

```
Control: 3.5.3 (MFA)
Impact: 9 (Account compromise = data access, breach risk)
Likelihood: 8 (MFA bypass/phishing common, 40% users unprotected)
Regulatory: 9 (NIST 800-171 requirement, audit critical)

Gap Risk Score = (9 + 8 + 9) / 3 = 8.67 → HIGH
Remediation Timeline: 30 days
```

---

## Part 6: Compliance Framework Mapping

### Multi-Framework Alignment

Organizations often must comply with multiple frameworks. This program maps NIST 800-171 to other requirements:

**Primary Framework: NIST SP 800-171**
- 14 control families
- ~110 individual controls
- Federal contractor requirement
- Alignment target: 100%

**Secondary Frameworks:**

| Framework | Applicability | Key Controls | Overlap with NIST 800-171 |
|-----------|---------------|--------------|--------------------------|
| **CMMC 2.0** | Federal contractors | Access control, incident response, supply chain | 95%+ (CMMC is based on NIST 800-171) |
| **SOX ITGC** | Public companies | Change management, segregation of duties, audit trails | 70% (overlaps on IT controls) |
| **HIPAA** | Healthcare orgs | Access control, encryption, audit logs, breach notification | 65% (overlaps on data protection) |
| **ISO 27001** | International standard | Information security management, risk assessment | 75% (broader scope, overlaps on core controls) |
| **PCI-DSS** | Payment processors | Encryption, access control, logging, vulnerability scanning | 60% (specific to payment card data) |

### Mapping Strategy

**If assessing a federal contractor handling CUI:**
- Primary focus: NIST 800-171 (100% compliance required)
- Secondary: CMMC alignment (will be assessed during CMMC audit)
- Tertiary: SOX/HIPAA/ISO (if applicable to organization)

**Example Mapping:**

```
NIST 800-171 3.5 (Access Control)
├── Maps to: CMMC 2.0 Access Control
├── Maps to: SOX ITGC (User Access Management)
├── Maps to: HIPAA (Access Controls)
├── Maps to: ISO 27001 (User Access Management)
└── Maps to: PCI-DSS (Cardholder Data Access)

Assessment finds: MFA not required for all users
Impact on NIST: Non-compliant with 3.5.3
Impact on CMMC: Would fail CMMC assessment (AC-2.2)
Impact on SOX: Compensating control missing (higher audit risk)
Impact on HIPAA: Non-compliant (access control violation)

Recommendation: Implement MFA organization-wide (solves all frameworks)
```

---

## Part 7: Assessment Documentation Templates

### Gap Assessment Report Template

**Report Structure:**

```
NIST 800-171 GAP ASSESSMENT REPORT
Organization: [Company Name]
Assessment Date: [Date]
Assessment Scope: All 14 control families (110+ controls)
Assessor: [Name, Credentials]

EXECUTIVE SUMMARY
- Overall Compliance Status: X% compliant (Y controls fully implemented, Z gaps identified)
- Critical Gaps: [Number] requiring immediate remediation
- Estimated Remediation Timeline: [Timeline]
- Estimated Remediation Cost: $[Amount]

FINDINGS SUMMARY BY CONTROL FAMILY
3.1 Access Control: 40% compliant (4 of 10 controls fully implemented, 6 gaps)
3.2 Awareness: 60% compliant
3.3 Audit & Accountability: 50% compliant
[Continue for all 14 families]

CRITICAL GAPS REQUIRING IMMEDIATE ACTION
1. MFA (3.5.3) - Not required for all users
2. Incident Response (3.6.1) - No formal IR procedures
3. Encryption (3.13.1) - No encryption for data in transit

HIGH PRIORITY GAPS (30-day timeline)
[List 5-10 high-priority gaps]

MEDIUM PRIORITY GAPS (90-day timeline)
[List medium-priority gaps]

DETAILED CONTROL FINDINGS
[For each gap: Current state, target state, gap description, risk score, remediation recommendation]

RISK REGISTER (See Phase 3 deliverable)

APPENDICES
- A: Evidence collected (policies, configs, logs)
- B: Control-by-control detailed findings
- C: Remediation recommendations by priority
```

---

## Part 8: Success Metrics

### Phase 1 Completion Metrics

| Metric | Target | Evidence |
|--------|--------|----------|
| Assessment framework documented | 100% | Framework document delivered |
| Control evaluation procedures | 100% (all 14 families) | Procedures for all families documented |
| Risk scoring methodology | Defined | Scoring framework + examples |
| Compliance mapping | 3+ frameworks mapped | NIST + CMMC + SOX/HIPAA/ISO |
| Assessment templates | Ready for Phase 2 | Gap assessment template ready |
| Baseline metrics | Established | Current state vs. target defined |

### Ongoing Program Metrics

| KPI | Target | Owner |
|-----|--------|-------|
| Assessment completion time | <60 days (all controls) | Compliance Team |
| Gap identification accuracy | 100% (validated) | Assessor |
| Risk scoring consistency | Consistent across controls | Quality Assurance |
| Remediation timeline accuracy | 90%+ on-time | Remediation Team |
| Compliance improvement rate | 5-10% per quarter | Leadership |

---

## Part 9: Assessment Cadence

### Timing & Frequency

**Initial Assessment:** Comprehensive (60-90 days)
- All 14 control families
- All ~110 controls
- Detailed current state
- Establishes baseline

**Annual Re-Assessment:** Comprehensive update (30-45 days)
- Re-evaluate all controls
- Confirm remediation completion
- Identify new gaps
- Update risk register

**Quarterly Gap Review:** Focused (1-2 days)
- Spot-check critical/high gaps
- Confirm remediation progress
- Monitor for new risks
- Update metrics

**Continuous Monitoring:** Ongoing
- Monitor compliance drift (policy changes, tech changes)
- Alert on new risks
- Track emerging compliance requirements

---
