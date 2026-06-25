# GRC Gap Assessment Program

## Phase 2: Gap Analysis Procedures & Evidence Gathering

**Organization:** [Enterprise / Federal Contractor]  
**Program Owner:** Chief Information Security Officer & Compliance Officer  
**Phase Duration:** Month 2  
**Key Outcome:** Comprehensive gap assessment completed with validated evidence and documented findings  

---

## Executive Summary

Phase 2 operationalizes the assessment framework from Phase 1. This phase contains the actual work: identifying compliance gaps, gathering evidence, validating findings, and documenting results in a format that withstands audit scrutiny.

**Key Objectives:**
1. Execute detailed gap analysis across all 14 NIST 800-171 control families
2. Establish evidence gathering standards (audit-ready rigor)
3. Validate assessment findings through independent review
4. Document gaps with sufficient detail for remediation planning
5. Identify root causes, not just symptoms
6. Ensure consistency and accuracy across all assessments

**Key Outcomes:**
- Comprehensive gap analysis (all 14 control families, ~110 controls)
- Evidence documentation (policies, configs, screenshots, logs)
- Gap validation report (QA-reviewed findings)
- Remediation recommendations (owner, timeline, resources)
- Ready for Phase 3 (Risk Register & Reporting)

---

## Part 1: Gap Analysis Procedure (Six-Step Process)

### The Gap Analysis Workflow

**Step 1: Control Selection & Scoping**

For each NIST 800-171 control:

1. Identify control family (3.1 through 3.14)
2. Define control scope (which systems, which users, which data?)
3. Determine applicability (does this control apply to our environment?)
4. Identify control owner (who's responsible for this?)
5. Schedule assessment (timing, interview, evidence gathering)

**Example:**
```
Control: 3.5.3 (Multi-factor Authentication)
Scope: All user accounts with access to CUI systems
Applicable Systems: Active Directory, VPN, Cloud platforms (Azure, AWS), VDI
Control Owner: Identity & Access Manager
Assessment Type: Technical review + policy review + user sample testing
```

---

**Step 2: Current State Evidence Gathering**

**What counts as evidence?**

| Evidence Type | Example | Audit Weight |
|---------------|---------|--------------|
| **Policy/Procedure** | MFA Policy document | ✅ Critical |
| **Configuration** | Screenshots of Okta MFA enforcement | ✅ Critical |
| **Logs/Monitoring** | User MFA enrollment report | ✅ Critical |
| **Interview/Attestation** | IT Manager confirms MFA enabled for admins | ⚠️ Supplemental |
| **Testing/Validation** | Test login demonstrates MFA requirement | ✅ Critical |

**Evidence Gathering Checklist:**

For each control, collect:
- [ ] Written policy or procedure (if required by control)
- [ ] Configuration evidence (screenshots, system settings)
- [ ] Activity logs (last 90 days minimum)
- [ ] User sample testing (randomized, documented)
- [ ] Interview with control owner
- [ ] Exception documentation (if applicable)

**Example Evidence Package for MFA Control:**

```
Control 3.5.3 - MFA Evidence Package

1. Policy Evidence:
   - Identity & Access Management Policy (v3.2, dated 2024)
   - Section 5.3: "Multi-factor authentication required for all privileged accounts"
   - Section 5.4: "MFA required for remote access (VPN, RDP)"

2. Configuration Evidence:
   - Okta admin panel screenshot (MFA policy enforcement enabled)
   - VPN server config (hardware token MFA requirement)
   - Azure AD conditional access policy (MFA for all cloud access)

3. Logs/Monitoring Evidence:
   - Okta enrollment report (dated 2024-06-25): 847 users enrolled in MFA
   - Okta failed MFA attempts (last 30 days): 23 failed attempts logged
   - VPN authentication logs (last 30 days): 100% of logins include MFA token

4. User Sample Testing:
   - Test User 1 (admin): Attempted login without MFA token → Rejected
   - Test User 2 (regular user): Attempted VPN access without MFA → Rejected
   - Test User 3 (contractor): Attempted cloud access without MFA → Rejected

5. Control Owner Interview:
   - Identity Manager confirms: "MFA required for all privileged users. Regular users: MFA optional for local access, required for VPN/cloud."
   - Identified gap: Regular users not required to use MFA for local access

6. Exception Documentation:
   - 12 service accounts excluded from MFA (documented, approved)
   - Service account justification: "Automated processes cannot use MFA"
   - Exception approval: CRO approval on file (Appendix D)
```

---

**Step 3: Target State Definition**

For each control, define: "What does NIST 800-171 require?"

**Source Material:**
- NIST SP 800-171 control description
- NIST SP 800-171 implementation guidance
- NIST SP 800-171B (enhanced controls, if applicable)
- Industry best practices (SANS, NIST Cybersecurity Framework)
- Audit findings from prior assessments

**Example Target State for MFA:**

```
Control 3.5.3 - Target State

NIST 800-171 Requirement: 
"Use multi-factor authentication for local and remote access to privileged accounts."

Target State Definition:
1. MFA required for ALL accounts with access to CUI systems
   - Includes: Admins, regular users, contractors, service accounts
2. MFA method: One of the following
   - FIDO2 security keys (preferred)
   - Hardware tokens (acceptable)
   - Software authenticator apps (acceptable for non-privileged access)
   - SMS (not preferred, but acceptable as fallback)
3. MFA coverage: 100% of users with CUI access
4. MFA enforcement: Automatic, no exceptions (except documented, approved)
5. MFA testing: Annual verification that MFA is enforced
6. MFA monitoring: Log all MFA attempts (success/failure), monitor for anomalies

Target: NIST 800-171 3.5.3 FULLY IMPLEMENTED
```

---

**Step 4: Gap Identification & Analysis**

**Compare current state vs. target state.**

```
Control 3.5.3 - Gap Analysis

Current State:
- Admins: MFA required (100% enforcement)
- Regular users: MFA optional (60% enrollment)
- Contractors: MFA optional (40% enrollment)
- Service accounts: MFA excluded (documented exception)
- Remote access: MFA required (100% enforcement)
- Local access: MFA optional (no enforcement)

Target State:
- All users with CUI access: MFA required (100% enforcement)
- All access types: MFA required

GAP IDENTIFIED:
- Regular users: 40% not using MFA (should be 100%)
- Contractors: 60% not using MFA (should be 100%)
- Local access: No MFA enforcement (should be required)
- Service accounts: Need compensating controls (if MFA cannot be implemented)

ROOT CAUSE ANALYSIS:
- Why aren't regular users required to use MFA?
  → Reason: Okta policy set to "encourage" not "require"
  → Reason: No formal policy requiring MFA for all users
  → Reason: Perceived user experience impact (slower login)

- Why aren't contractors required to use MFA?
  → Reason: Contractor access managed separately (different system)
  → Reason: No contractor onboarding procedure that includes MFA

IMPACT OF GAP:
- Regular user account compromise → Attacker gains CUI system access
- Contractor account compromise → Attacker gains vendor/CUI access
- No MFA on local access → Insider threat risk (physical theft, unauthorized access)
```

---

**Step 5: Evidence Validation & Quality Assurance**

**Validate that evidence actually proves what you claim it proves.**

**Validation Checklist:**

```
Evidence Validation Questions:

1. Is the evidence current?
   □ Dated within last 90 days?
   □ Configuration matches current system state?
   □ Logs cover assessment period?

2. Is the evidence authentic?
   □ Screenshots show actual system (not mock/example)?
   □ Logs are from actual monitoring system?
   □ Policy is official/signed version?

3. Does the evidence prove the claim?
   □ "MFA required" - Does Okta config actually enforce it?
   □ "100% of users enrolled" - Does enrollment report cover all users?
   □ "No failed logins" - Does log data support this?

4. Is there any contradictory evidence?
   □ Does config evidence contradict policy?
   □ Do logs show MFA being bypassed?
   □ Does interview contradict written evidence?

5. Is the evidence sufficient?
   □ Single screenshot, or comprehensive evidence package?
   □ One user test, or representative sample?
   □ One data source, or multiple corroborating sources?

Example Validation:
Assessor claims: "MFA is required for all users"
Evidence: Screenshot of Okta policy = "Enforce MFA: Enabled"
Validation check: 
  - Policy screenshot current? ✓ (dated 2024-06-20)
  - Does it actually enforce? Need to verify with enrollment data
  - Enrollment report shows: 847/950 users enrolled (89%, not 100%)
  - REVISED CLAIM: "MFA is enforced for policy but only 89% of users are enrolled"
```

---

**Step 6: Gap Documentation & Remediation Recommendation**

**Document each gap in standardized format:**

```
GAP DOCUMENTATION TEMPLATE

Gap ID: 3.5.3-GAP-001
Control: 3.5.3 (Multi-factor Authentication)
Severity: HIGH
Status: Open (Not Remediated)

Current State:
- MFA required for admins (100%)
- MFA required for remote access (100%)
- MFA optional for regular users (60% enrollment)
- MFA optional for local access

Target State:
- MFA required for all CUI-access users (100%)
- MFA required for all access types (local and remote)

Gap Description:
Regular users and contractors are not required to implement MFA for local access. Approximately 40% of regular users and 60% of contractors are not enrolled in MFA. This creates authentication weakness and increases risk of credential compromise.

Evidence:
- Okta policy screenshot (MFA enforcement enabled for admins only)
- Enrollment report (60% of regular users enrolled)
- Security policy (MFA required for admins and remote, no requirement for local access)

Root Cause:
- Okta policy configured to "encourage" MFA for regular users, not "enforce"
- No formal organizational policy requiring MFA for all users
- User experience concerns (slower login) prevented mandatory MFA

Risk Assessment:
- Likelihood: MEDIUM (credential theft is common)
- Impact: HIGH (MFA bypass = CUI system access compromise)
- Regulatory: CRITICAL (NIST 800-171 requirement, CMMC audit failure)
- Risk Score: 8/10 (HIGH priority)

Remediation Recommendation:
1. Create formal policy: "MFA required for all users with CUI access"
2. Implement Okta policy change: Change enforcement from "encourage" to "require"
3. Implement contractor MFA requirement: Update contractor access procedures
4. Implement compensating control for local access: Device-based MFA or passwordless
5. Timeline: 30 days to enforce, 60 days for full enrollment
6. Owner: Identity & Access Manager
7. Validation: Re-assess in 60 days, confirm 100% enrollment

Estimated Cost:
- Okta policy change: $0 (existing tool)
- Hardware tokens (backup): $2,000 (100 tokens @ $20)
- Staff time (implementation): 40 hours @ $75/hr = $3,000
- Total: $5,000

Estimated Benefit (Risk Reduction):
- Prevents credential theft attacks: ~$1-5M per incident
- Reduces audit risk: Eliminates major NIST 800-171 finding
- Improves compliance posture: Demonstrates control maturity
```

---

## Part 2: Evidence Gathering Standards

### What Makes Evidence "Audit Ready"?

**Three criteria:**

1. **Authentic:** Evidence shows actual system state (not example, not outdated)
2. **Complete:** Evidence package covers the full control requirement
3. **Verifiable:** Someone else can independently validate the evidence

### Evidence Documentation Chain

**For each piece of evidence, document:**

```
Evidence Chain Format:

Evidence ID: 3.5.3-EV-001
Control: 3.5.3 (Multi-factor Authentication)
Evidence Type: Configuration Screenshot
Description: Okta admin console showing MFA enforcement policy

Evidence Source:
- System: Okta production environment
- Date Collected: 2024-06-25
- Time: 14:30 UTC
- Collected By: John Smith (Security Analyst)
- Collection Method: Manual screenshot from admin console

Evidence Details:
- Policy Name: "Enforce MFA for Privileged Access"
- Policy Status: ENABLED
- Affected Users: All users in "Admins" group (847 users)
- MFA Methods: Okta Verify, Hardware tokens, FIDO2
- Enforcement Level: Required (not optional)

Chain of Custody:
- Collected: 2024-06-25 by John Smith
- Verified: 2024-06-25 by Sarah Johnson (Compliance Officer)
- Stored: Secure SharePoint folder (access restricted to assessment team)
- Integrity: Not modified since collection

Validation Notes:
- Evidence is current (collected this week)
- Policy matches current Okta environment
- Covers the MFA enforcement requirement
- Corroborated by Okta enrollment data
```

### Evidence Types & Audit Weight

**Critical Evidence (Must Have):**
- Official policy or procedure document (signed/dated)
- System configuration evidence (screenshots, configs)
- Activity logs (user enrollment, login attempts)
- Test results (verification that control works)

**Supplemental Evidence (Nice to Have):**
- Interview notes (control owner confirms implementation)
- Training records (users trained on MFA)
- Audit reports (third-party verification)

**Weak Evidence (Don't Rely On):**
- Verbal statements without documentation
- Outdated policies (>1 year old)
- Anecdotal observations ("Most users have MFA")
- Single data point with no corroboration

---

## Part 3: Detailed Control Family Examples

### Example 1: Access Control Gap (Simple)

**Control Family: 3.1 Access Control**

**Scenario:** Small federal contractor with 50 employees

---

**Control: 3.1.1 (Authorized Access)**

**Current State Assessment:**

Evidence gathered:
- Policy: "Access Policy v2.1" - requires authorization before access
- Active Directory: 45 of 50 users have accounts
- 5 contractors have temporary access through shared admin account
- Interviews: Access owner confirms "We review access annually"

**Target State:**

NIST requirement: "Authorized personnel have access to information systems and associated facilities based on need-to-know and job function."

Target implementation:
- All users have unique, identifiable accounts
- No shared accounts
- Access granted by role/job function
- Annual review of access rights
- Documented access decisions

**Gap Identified:**

Current: 5 contractors using shared admin account (violates requirement for unique accounts)
Target: Each contractor has unique account with appropriate access level

Gap Description: "Shared admin account used for contractor access violates NIST 3.1.1 requirement for unique, identifiable access."

Root Cause: "No contractor onboarding procedure; easier to give contractors admin access than set up unique accounts."

**Evidence:**
- Active Directory screenshots showing shared "contractor-admin" account
- User management log showing this account used by 5 different people
- Interview: "We'll get around to fixing it, but it's been working fine"

**Risk Assessment:**
- Likelihood: MEDIUM (any contractor could abuse access)
- Impact: HIGH (admin account = full system compromise)
- Regulatory: CRITICAL (NIST 800-171 violation, CMMC audit failure)
- Risk Score: 8/10 (HIGH priority)

**Remediation:**
1. Create 5 unique contractor accounts (within role capability, not admin)
2. Remove contractor access from shared admin account
3. Implement contractor onboarding procedure (includes account creation)
4. Validate in 30 days
5. Owner: IT Manager
6. Cost: ~$1,000 (staff time, 15 hours)

---

### Example 2: Encryption Gap (Moderate Complexity)

**Control Family: 3.13 System & Information Integrity**

**Scenario:** Mid-size federal contractor with hybrid infrastructure (on-premise + cloud)

---

**Control: 3.13.1 (Information Encryption)**

**Current State Assessment:**

**Evidence collected:**

1. Encryption Policy (v3.0)
   - Requires encryption for data at rest
   - Requires encryption for sensitive data in transit
   - No specific encryption standards mandated

2. Database Encryption (On-Premise)
   - SQL Server encrypted at rest (AES-256)
   - Regular backups encrypted
   - Evidence: SQL Server configuration + backup logs

3. Data in Transit (On-Premise)
   - File transfers use SFTP (encrypted)
   - Web traffic uses HTTPS
   - Database connections use SSL/TLS
   - Evidence: Network config screenshots + security scan results

4. Cloud Storage (Azure)
   - Azure Storage accounts: Encryption enabled at storage account level
   - Individual file encryption: Not all files encrypted
   - Evidence: Azure admin portal screenshots

5. Email Encryption
   - Outlook: S/MIME available, not required
   - Email retention: 30% of sensitive emails are unencrypted
   - Evidence: Email audit logs + user survey

6. Unencrypted Data Stores Identified:
   - Shared file server (legacy): Contains some unencrypted documents (2TB out of 10TB)
   - User endpoints: Local drives not encrypted (no BitLocker mandate)
   - Evidence: File server scan + endpoint inventory

**Target State:**

NIST 800-171 3.13.1 requirement: "Protect information system and information at rest and in transit."

Target implementation (NIST intent):
- All data at rest: Encrypted (no unencrypted CUI)
- All data in transit: Encrypted (HTTPS, TLS 1.2+, encrypted tunnels)
- Encryption algorithms: NIST-approved (AES-256, SHA-256, etc.)
- Key management: Secure key storage and rotation
- Exceptions: Documented, approved, compensating controls in place

**Gap Analysis:**

```
Gap 1: Legacy File Server Unencrypted Data
Current: 2TB of files on legacy file server unencrypted
Target: All data at rest encrypted
Gap: 20% of file server data not encrypted
Root Cause: Legacy system, planned for decommissioning but still in use

Gap 2: User Endpoint Encryption
Current: BitLocker not required on user laptops/desktops
Target: All endpoints with CUI access have drive encryption
Gap: ~40% of endpoints without BitLocker
Root Cause: User resistance to BitLocker performance impact

Gap 3: Email Encryption
Current: S/MIME available, not required; 30% of sensitive emails unencrypted
Target: Encryption required for all CUI-containing emails
Gap: 30% of sensitive communications not encrypted
Root Cause: User inconvenience, lack of enforcement policy

Gap 4: Azure File Encryption Granularity
Current: Encryption at storage account level (all-or-nothing)
Target: Individual file encryption with key management
Gap: No file-level encryption control
Root Cause: Architectural decision made for ease of management
```

**Evidence Package:**

- File server audit: 2TB unencrypted identified
- BitLocker group policy report: 40% non-compliant
- Email audit: 30% of CUI emails sent unencrypted
- Azure config: Storage-level encryption only, no file-level encryption

**Risk Assessment:**

```
Gap 1 - Legacy File Server (HIGH): 
- Likelihood: MEDIUM (file server accessible to internal staff)
- Impact: HIGH (2TB of CUI unencrypted)
- Regulatory: CRITICAL (NIST 800-171 violation)
- Risk Score: 8/10

Gap 2 - Endpoint Encryption (HIGH):
- Likelihood: HIGH (laptop theft/loss common)
- Impact: HIGH (endpoints contain CUI)
- Regulatory: CRITICAL (NIST requirement)
- Risk Score: 8/10

Gap 3 - Email Encryption (MEDIUM):
- Likelihood: MEDIUM (email interception possible)
- Impact: MEDIUM (email may contain CUI)
- Regulatory: HIGH (encryption in transit required)
- Risk Score: 6/10

Gap 4 - Azure Granularity (MEDIUM):
- Likelihood: LOW (Azure inherently secure)
- Impact: MEDIUM (no per-file encryption control)
- Regulatory: MEDIUM (acceptable but not best practice)
- Risk Score: 5/10
```

**Remediation Plan:**

```
Gap 1 Remediation:
- Action: Identify all unencrypted files on legacy server
- Action: Migrate data to encrypted Azure storage OR
- Action: Apply file-level encryption to legacy server (BitLocker folder encryption)
- Timeline: 60 days (migration takes time)
- Cost: $5,000 (migration staff time, potential new storage)
- Owner: Infrastructure Manager
- Validation: File server encryption audit in 60 days

Gap 2 Remediation:
- Action: Require BitLocker on all laptops with CUI access
- Action: Create BitLocker Group Policy for managed devices
- Action: Provide exemption process for users with documented performance needs
- Timeline: 30 days enforcement, 60 days full deployment
- Cost: $1,000 (staff time, help desk support)
- Owner: IT Manager
- Validation: Group Policy compliance report in 60 days

Gap 3 Remediation:
- Action: Implement Exchange Online encryption for CUI-containing emails
- Action: Create email policy: "Encrypt all emails to external addresses"
- Action: Train users on S/MIME usage for sensitive communications
- Timeline: 14 days implementation, 30 days enforcement
- Cost: $2,000 (policy implementation, user training)
- Owner: Email Administrator
- Validation: Email audit in 30 days

Gap 4 Remediation:
- Action: Evaluate Azure file encryption options (client-side encryption, Azure encryption)
- Action: Document why storage-level encryption is acceptable (if it is)
- Action: If file-level encryption needed, implement client-side encryption library
- Timeline: 30 days (evaluation), 60 days (implementation if needed)
- Cost: $3,000-5,000 (architecture review, possible new tools)
- Owner: Cloud Architect
- Validation: Azure encryption audit in 60 days

Total Remediation Cost: ~$11,000
Total Remediation Timeline: 60 days to close critical gaps, 90 days for full compliance
```

---

### Example 3: Incident Response Gap (High Complexity)

**Control Family: 3.6 Incident Response**

**Scenario:** Federal contractor with 200 employees, handling classified CUI, no formal incident response program

---

**Control: 3.6.1 (Incident Response Procedures)**

**Current State Assessment:**

**Evidence collected:**

1. Incident Response Documentation:
   - No formal IR policy or procedures
   - Email chain from 2023 breach: "Who do we call if something happens?"
   - SOC team has informal procedures (documented in Slack)
   - Evidence: Email screenshots, Slack channel archive

2. Incident Contact Information:
   - No centralized incident contact list
   - CISO email known by some staff
   - Contracts manager responsible for breach notification (unclear why)
   - Evidence: Org chart, emails to random people about incidents

3. Incident Logs:
   - 3 suspected incidents in past 2 years (2021, 2022)
   - No formal documentation of what happened
   - No timelines, no containment steps, no lessons learned
   - Evidence: Email confirmations, IT ticket system (incomplete)

4. Incident Classification:
   - No severity classification system
   - No escalation criteria
   - No defined roles/responsibilities
   - Evidence: Incident emails lack any classification

5. Breach Notification:
   - No documented breach notification procedures
   - No customer/partner notification process
   - No regulatory reporting procedures
   - Evidence: HIPAA incident (2022) - "We notified customers verbally because we didn't know the process"

6. Incident Response Team:
   - No formal IR team designated
   - CISO responds to everything (reactive, not planned)
   - No IR training
   - No incident drills/tabletop exercises
   - Evidence: Interview with CISO - "I just handle it as it comes"

7. Post-Incident Process:
   - No lessons learned documentation
   - No post-incident review meetings
   - No remediation tracking for incident findings
   - Evidence: No post-incident review documents found

**Target State:**

NIST 800-171 3.6.1: "Establish procedures to respond to security incidents including incident handling, notification, and recovery."

Target implementation (NIST intent):
- Formal IR procedures documented (who, what, when, how)
- IR team identified with clear roles
- Incident classification and severity levels defined
- Escalation procedures (who to notify, when)
- Breach notification procedures (internal + external)
- Containment, investigation, recovery procedures
- Post-incident review process
- Annual IR testing/drills

**Gap Analysis:**

```
Gap 1: No Documented IR Procedures
Current: IR handled ad-hoc, no formal procedures
Target: Documented procedures for all incident phases (detect, contain, investigate, recover, notify)
Gap: Complete lack of formal IR procedures
Severity: CRITICAL
Risk: Every incident handled differently, inconsistently, ineffectively

Gap 2: No IR Team / Roles Defined
Current: CISO responds to everything, no team structure
Target: Designated IR team with defined roles (incident commander, investigator, communicator, etc.)
Gap: No formal team structure or role assignments
Severity: CRITICAL
Risk: Incidents may be missed, response delayed, coordination poor

Gap 3: No Incident Classification
Current: Incidents not classified by severity
Target: Severity tiers (CRITICAL, HIGH, MEDIUM, LOW) with escalation criteria
Gap: No formal classification system
Severity: HIGH
Risk: Critical incidents treated as routine, routine incidents escalate unnecessarily

Gap 4: No Breach Notification Procedures
Current: No documented process for notifying customers/partners/regulators
Target: Formal breach notification procedures aligned to HIPAA, GDPR, state law
Gap: Ad-hoc breach notification, compliance risk
Severity: CRITICAL
Risk: Non-compliant breach notification = regulatory fines ($1000s-$100Ks per incident)

Gap 5: No IR Testing/Tabletop Exercises
Current: No incident drills or simulation testing
Target: Annual IR tabletop exercises, incident simulation testing
Gap: IR procedures untested and unreliable
Severity: HIGH
Risk: Procedures sound good on paper but fail in real incident

Gap 6: No Post-Incident Review Process
Current: Incidents handled but no lessons learned captured
Target: Formal post-incident review (within 5 days), action items tracked, remediation validated
Gap: No continuous improvement in incident response
Severity: HIGH
Risk: Same mistakes repeated in future incidents
```

**Evidence Package:**

- Lack of IR policy documents
- Incident emails showing inconsistent handling
- HIPAA breach (2022) - informal notification
- Interview notes showing reactive approach
- Org chart showing no IR team

**Risk Assessment:**

```
CRITICAL RISK AREAS:

Lack of IR Procedures (CRITICAL):
- Every incident is handled differently
- Containment procedures unknown
- Investigation procedures unknown
- Response times unmeasured (could be 24+ hours to detect)
- Estimated impact: 2-3x longer incident response time

Lack of Breach Notification (CRITICAL):
- HIPAA breach (2022) notified verbally (non-compliant)
- Risk of regulatory fines: $100-$1,500 per patient per violation
- Estimated exposure: If 1,000 patient records breached, $100K-$1.5M in fines

Lack of IR Team (CRITICAL):
- CISO as single point of failure
- Incident response paralyzed if CISO unavailable
- No surge capacity for multiple simultaneous incidents
- Risk: Incidents undetected or mishandled

Overall Risk Score: 9/10 (CRITICAL)
```

**Remediation Plan (4-Phase IR Implementation):**

```
Phase 1: IR Framework & Procedures (Month 1)
- Develop IR procedures document (who, what, when, how)
- Define incident severity classification (CRITICAL, HIGH, MEDIUM, LOW)
- Define escalation criteria and contact list
- Create incident response playbooks for top 5 threat scenarios
- Establish breach notification procedures (HIPAA, state law)
- Cost: $8,000 (30 hours consulting @ $250/hr + internal staff time)

Phase 2: IR Team & Training (Month 2)
- Designate IR team (Incident Commander, Investigator, Communicator, Evidence Officer)
- Assign roles and responsibilities
- Conduct IR training for team (SANS IR, NIST incident handling)
- Create IR contact list and escalation procedures
- Cost: $12,000 (IR training for 5-person team @ $2,400/person)

Phase 3: Incident Detection & Response Infrastructure (Month 3)
- Deploy SIEM for incident detection (if not present)
- Set up alerting for CRITICAL/HIGH severity incidents
- Create incident tracking system (ticketing)
- Establish evidence preservation procedures
- Cost: $15,000 (SIEM licensing, configuration, staff time)

Phase 4: Testing & Continuous Improvement (Month 4)
- Conduct tabletop exercise (simulate incident response)
- Test breach notification procedures
- Validate IR playbooks with real scenario
- Establish post-incident review process
- Plan annual IR refresher training
- Cost: $5,000 (tabletop facilitation, review meetings)

Total Remediation Cost: ~$40,000
Total Timeline: 4 months to operationalize, ongoing improvement
Expected Benefit:
- Reduce incident response time: 24+ hours → 2-4 hours
- Comply with HIPAA/regulatory requirements
- Reduce breach notification risk: $100K+ in avoided fines
- Reduce breach damage: Faster containment = smaller impact
```

---

## Part 4: Quality Assurance & Validation

### Assessment Validation Procedure

**Who validates the assessment?**

Independent QA reviewer (not the assessor who performed the assessment)

**What do they validate?**

1. **Completeness:** Were all 14 control families assessed?
2. **Accuracy:** Is the gap analysis correct (current state vs. target)?
3. **Evidence:** Is evidence sufficient to support the finding?
4. **Risk Scoring:** Is the risk score reasonable given the facts?
5. **Remediation:** Is the remediation recommendation practical and timely?

**Validation Checklist:**

```
QA Validation Checklist for Each Gap

□ Gap ID and control correctly identified
□ Current state description accurate (supported by evidence)
□ Target state definition matches NIST requirement
□ Root cause analysis makes sense
□ Evidence package is complete and credible
□ Risk scoring is justified (impact × likelihood × regulatory)
□ Remediation is specific and actionable (not vague)
□ Remediation timeline is realistic (not too aggressive, not too lenient)
□ Remediation owner is identified (not vague "IT will do it")
□ Remediation cost estimate is reasonable
□ Assessment is free of assessor bias
```

**Validation Result:**

```
QA Validation Summary

Gap 3.5.3-GAP-001 (MFA for Regular Users)
- Assessor Finding: Current state 60% adoption, target 100%, gap HIGH priority
- QA Validation: Evidence shows 60% enrollment, policy shows optional not required
- QA Conclusion: ✓ APPROVED - Finding is accurate and well-supported
- Recommendation: Approved for Phase 3 Risk Register

Gap 3.13.1-GAP-002 (Unencrypted File Server)
- Assessor Finding: 2TB unencrypted, risk HIGH
- QA Validation: File server audit confirmed 2TB, but assessor didn't check for compensating controls
- QA Conclusion: ⚠️ CONDITIONAL - Add analysis of file access restrictions (if access is restricted, impact may be lower)
- Recommendation: Resubmit with access control analysis

Gap 3.6.1-GAP-001 (No IR Procedures)
- Assessor Finding: No formal IR procedures, gap CRITICAL
- QA Validation: Confirmed - no IR policy or documented procedures found
- QA Conclusion: ✓ APPROVED - Finding is accurate and critical
- Recommendation: Approved for Phase 3 Risk Register, recommend executive briefing on criticality
```

---

## Part 5: Assessment Documentation Standards

### Audit-Ready Documentation Format

**What makes documentation "audit-ready"?**

1. **Traceable:** Every claim can be traced to evidence
2. **Complete:** All 14 control families covered
3. **Consistent:** Same format for all findings
4. **Current:** Evidence dated within 90 days
5. **Clear:** Someone unfamiliar with your org can understand it

### Gap Assessment Report Structure

```
NIST 800-171 GAP ASSESSMENT REPORT
[Organization Name]
Assessment Date: [Date]
Assessment Period: [Start Date - End Date]
Assessor(s): [Names, Credentials]
QA Reviewer: [Name, Credentials]

EXECUTIVE SUMMARY
Overall Compliance Status: XX% (YY controls implemented, ZZ gaps identified)
Critical Gaps: [Number] requiring immediate remediation
High Gaps: [Number] requiring 30-day remediation
Timeline to Full Compliance: [Estimated months]
Estimated Remediation Cost: $[Amount]
Key Risks: [1-3 sentence summary of biggest risks]

FINDINGS BY CONTROL FAMILY
3.1 Access Control: XX% compliant (Y gaps identified)
  - Gap 3.1.1-001: Shared accounts (CRITICAL)
  - Gap 3.1.2-001: No access reviews (HIGH)
3.2 Awareness & Training: XX% compliant
[Continue for all 14 families]

DETAILED GAP FINDINGS
[For each gap: Current state, Target state, Gap description, Evidence, Risk score, Remediation]

REMEDIATION PRIORITIZATION
[Rank gaps by priority: CRITICAL 1-7 days, HIGH 14-30 days, MEDIUM 30-90 days, LOW 90-180 days]

RISK REGISTER (Detailed - See Phase 3)
[Gap ID, Control, Severity, Current/Target, Remediation plan, Owner, Timeline, Cost]

METHODOLOGY APPENDIX
A. Assessment Procedures
B. Evidence Standards
C. Risk Scoring Methodology
D. Framework Mapping (NIST + CMMC + others)

EVIDENCE APPENDIX
A. Policies and Procedures
B. System Configuration Screenshots
C. Activity Logs and Reports
D. Interview Notes
E. Test Results
```

### Quick Reference: Gap Severity Definitions

Use these definitions consistently across all gap documentation:

**CRITICAL (Risk Score 9-10):**
- Severe compliance violation (immediate audit failure)
- High breach/incident risk
- Regulatory violation with significant penalties
- Remediation: 1-7 days
- Examples: No encryption for CUI data, no access controls, no incident response procedures

**HIGH (Risk Score 7-8):**
- Significant compliance gap
- Moderate breach/incident risk
- Regulatory violation or audit finding
- Remediation: 14-30 days
- Examples: MFA not required for all users, incomplete encryption, weak access reviews

**MEDIUM (Risk Score 5-6):**
- Notable compliance gap
- Lower breach risk but material
- Audit observation or corrective action
- Remediation: 30-90 days
- Examples: Encryption granularity, training coverage gaps, monitoring gaps

**LOW (Risk Score 3-4):**
- Minor compliance gap
- Low breach risk
- Audit best practice recommendation
- Remediation: 90-180 days
- Examples: Documentation updates, tool enhancements, process optimizations

---
