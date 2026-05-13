---
title: "Week 09: AI for Vulnerability Management and Secure Software Engineering"
layout: default
permalink: /lectures/week09/
---

# Week 09: AI for Vulnerability Management and Secure Software Engineering
## From Vulnerability Lists to Risk-Based Remediation

Welcome to Week 9 of **Applied AI for Cybersecurity**.

This week focuses on how AI can support vulnerability management, secure software engineering, code review, exploit prediction, dependency risk analysis, and software supply-chain security.

The main question is:

> How can AI help security teams decide what to fix first, and how can it support safer software development?

The central lesson is:

> AI can help prioritise and explain software security risk, but it must not replace secure engineering discipline, expert review, testing, and governance.

---

# 1. Learning Objectives

By the end of this week, you should be able to:

1. Explain how AI can support vulnerability management.
2. Distinguish vulnerability severity, exploitability, exposure, asset criticality, and business impact.
3. Explain why CVSS alone is not enough for remediation prioritisation.
4. Identify useful features for vulnerability prioritisation.
5. Describe how AI can support secure code review.
6. Explain the risks of AI-assisted software engineering.
7. Discuss software supply-chain and dependency risk.
8. Design a risk-based vulnerability prioritisation model.
9. Evaluate false positives and false negatives in code security tools.
10. Explain how Secure by Design and SSDF principles relate to AI-supported software security.

---

# 2. Why Vulnerability Management Needs Prioritisation

Organisations usually have more vulnerabilities than they can fix immediately. Security teams must decide which vulnerabilities create the greatest practical risk.

Important questions include:

- Is the vulnerable asset internet-facing?
- Is the affected system business-critical?
- Is sensitive data involved?
- Is there known exploitation in the wild?
- Is a public exploit available?
- Is a patch available?
- Are compensating controls in place?
- What is the operational cost of patching?

A CVSS score is useful, but it is not the whole risk picture.

Example:

```text
Vulnerability A:
CVSS 9.8, internal test server, no sensitive data, no public exploit

Vulnerability B:
CVSS 8.1, internet-facing VPN, public exploit, known exploitation
```

Vulnerability B may be more urgent even though its CVSS score is lower.

---

# 3. Key Concepts

| Concept | Meaning |
|---|---|
| Vulnerability | A weakness that may be exploited |
| CVE | Identifier for a publicly known vulnerability |
| CVSS | Technical severity scoring system |
| Exploitability | Likelihood or feasibility of exploitation |
| Exposure | Whether the vulnerable asset can be reached |
| Asset criticality | Business importance of affected system |
| Compensating control | Existing control that reduces risk |
| Remediation | Fixing or mitigating the vulnerability |

Further reading:

- CVE: <https://www.cve.org/>
- CVSS: <https://www.first.org/cvss/>
- CISA Known Exploited Vulnerabilities Catalog: <https://www.cisa.gov/known-exploited-vulnerabilities-catalog>

---

# 4. AI for Vulnerability Prioritisation

AI can combine vulnerability, asset, threat, and business context.

Possible features:

| Feature | Meaning |
|---|---|
| CVSS score | Technical severity |
| exploit_available | Whether public exploit exists |
| known_exploited | Evidence of exploitation in the wild |
| asset_exposure | Internet-facing or internal |
| asset_criticality | Business importance |
| data_sensitivity | Type of data processed |
| patch_available | Whether fix exists |
| compensating_control | WAF, EDR, segmentation, access control |
| vulnerability_age | Time since disclosure |
| threat_intel_mentions | Whether threat reports mention exploitation |
| dependency_depth | Direct or transitive dependency |

Possible output:

```text
Priority: High
Reasons:
- internet-facing service
- exploit available
- known exploited vulnerability
- authentication system affected
- patch available
```

---

# 5. AI Problem Framing

## 5.1 Risk Scoring

Most vulnerability management tasks are better framed as risk scoring than simple classification.

```text
Input: vulnerability + asset + exposure + exploit + business context
Output: remediation priority score
```

## 5.2 Ranking

A practical model may output a ranked remediation list.

```text
1. Internet-facing VPN vulnerability with known exploitation
2. Identity provider weakness affecting privileged users
3. Public web app flaw with exploit available
```

## 5.3 Exploit Prediction

AI can estimate whether a vulnerability is likely to be exploited.

Possible signals:

- CVSS vector
- CWE category
- affected vendor and product
- public proof-of-concept
- exploit kit inclusion
- social media or forum mentions
- threat intelligence references
- age of vulnerability

## 5.4 Human-in-the-Loop Review

The model should support remediation decisions. It should not blindly decide patching order because remediation can disrupt services.

---

# 6. Secure Software Engineering

Secure software engineering means building security into the software lifecycle rather than adding it after deployment.

NIST SP 800-218 defines the Secure Software Development Framework, or SSDF, as a set of fundamental, sound practices for secure software development. CISA Secure by Design emphasises that software products should treat security as a core business requirement rather than shifting preventable risk to customers.

Key stages:

```text
requirements
→ design
→ implementation
→ code review
→ testing
→ dependency management
→ deployment
→ monitoring
→ maintenance
```

AI may support many stages, but it does not remove the need for secure design, testing, review, and governance.

---

# 7. AI for Secure Code Review

AI can assist secure code review by identifying suspicious patterns.

| Vulnerability | Possible Signal |
|---|---|
| SQL injection | User input concatenated into SQL string |
| XSS | Unsanitised input rendered in HTML |
| Command injection | User input passed to shell command |
| Hardcoded secrets | API key or password in source code |
| Insecure crypto | Weak algorithm or hardcoded key |
| Path traversal | User-controlled file path |
| Unsafe deserialisation | Untrusted object deserialisation |
| Broken access control | Missing permission checks |

AI support may include:

- explaining why code is risky
- suggesting safer patterns
- prioritising findings
- reducing duplicate warnings
- summarising security review results

Warning:

> AI-generated secure-code suggestions must be reviewed and tested.

---

# 8. AI for Dependency and Supply-Chain Risk

Modern software depends on external libraries, containers, and services.

Risks include:

- vulnerable dependencies
- abandoned packages
- malicious packages
- typosquatting
- dependency confusion
- compromised maintainers
- insecure container images
- secrets in repositories
- build pipeline compromise

AI can help by:

- ranking dependency risk
- detecting suspicious package names
- summarising advisories
- mapping dependency chains
- prioritising patches
- identifying unusual package behaviour

But software supply-chain security requires controls beyond AI.

---

# 9. Case Study 1: CVSS Is Not Enough

## Scenario

| Vulnerability | CVSS | Asset | Exposure | Exploit |
|---|---:|---|---|---|
| V1 | 9.8 | Internal test server | Internal only | No public exploit |
| V2 | 8.1 | VPN gateway | Internet | Exploit available and known exploited |

## Discussion

V2 may deserve higher priority because it is internet-facing and actively exploited. This shows that risk-based prioritisation must include exploitability and asset context, not only severity.

---

# 10. Case Study 2: AI-Assisted Secure Code Review

## Scenario

```text
query = "SELECT * FROM users WHERE name = '" + user_input + "'"
```

Possible issue:

```text
SQL injection
```

A useful AI assistant should explain:

- user input is directly concatenated into SQL
- an attacker may modify query logic
- parameterised queries should be used
- the code should be tested
- similar patterns should be searched elsewhere

---

# 11. Case Study 3: Dependency Risk

## Scenario

A project depends on a package with:

```text
critical CVE
public exploit
no maintainer activity for 18 months
used by authentication component
patch available
```

Risk-increasing evidence:

- critical vulnerability
- exploit available
- authentication component
- patch available
- abandoned package

Risk-reducing evidence may include:

- component not exposed
- vulnerable function not used
- strong compensating controls

---

# 12. Week 9 Summary

```text
Vulnerability prioritisation requires severity, exploitability, exposure, asset criticality, and business impact.
CVSS is useful but insufficient alone.
AI can support risk scoring, ranking, exploit prediction, and secure code review.
False positives waste developer and security-team time.
False negatives leave exploitable weaknesses.
AI-assisted secure software engineering still requires testing, review, governance, and secure-by-design practice.
```

Final takeaway:

> AI can help decide what to fix first, but secure software still depends on disciplined engineering, testing, review, and accountability.

---

# 13. Lab Sheet 9: AI-Assisted Vulnerability Prioritisation and Secure Code Review

## Lab Overview

In this lab, you will rank vulnerabilities, analyse code security findings, and design an AI-assisted remediation prioritisation approach.

## Lab Dataset A: Vulnerability Records

| ID | CVSS | Asset | Exposure | Exploit Available | Known Exploited | Data Sensitivity | Patch Available |
|---|---:|---|---|---|---|---|---|
| V1 | 9.8 | Test server | Internal | No | No | Low | Yes |
| V2 | 8.1 | VPN gateway | Internet | Yes | Yes | Medium | Yes |
| V3 | 7.5 | HR database | Internal | No | No | High | No |
| V4 | 6.8 | Public web app | Internet | Yes | No | High | Yes |
| V5 | 5.9 | Developer tool | Internal | Yes | No | Low | Yes |
| V6 | 9.0 | Identity provider | Internet | No | No | High | Yes |
| V7 | 4.3 | Archive server | Internal | No | No | Low | No |
| V8 | 7.2 | Payment API | Internet | Yes | Yes | High | Yes |

## Lab Task 1 — Prioritise Vulnerabilities

Rank the vulnerabilities from highest to lowest remediation priority. Do not rank by CVSS alone.

| Rank | Vulnerability ID | Reason |
|---|---|---|
| 1 |  |  |
| 2 |  |  |
| 3 |  |  |
| 4 |  |  |
| 5 |  |  |

## Lab Task 2 — Design a Risk Score

Create a risk score using 6–8 indicators.

| Indicator | Score Contribution | Reason |
|---|---:|---|
|  |  |  |
|  |  |  |
|  |  |  |

Define thresholds:

| Score Range | Priority |
|---|---|
| 0–30 |  |
| 31–60 |  |
| 61–80 |  |
| 81–100 |  |

## Lab Task 3 — Code Finding Analysis

| ID | Finding |
|---|---|
| C1 | User input concatenated into SQL query |
| C2 | Hardcoded API key in repository |
| C3 | Weak hash function used for password storage |
| C4 | File path built from user input |
| C5 | Debug endpoint exposed in production |
| C6 | Dependency has known critical CVE |

For each finding:

| ID | Vulnerability Type | Risk | Additional Evidence Needed | Suggested Remediation |
|---|---|---|---|---|
| C1 |  |  |  |  |
| C2 |  |  |  |  |
| C3 |  |  |  |  |
| C4 |  |  |  |  |
| C5 |  |  |  |  |
| C6 |  |  |  |  |

## Lab Task 4 — False Positive and False Negative Costs

Choose three findings.

| Finding ID | False Positive Cost | False Negative Cost |
|---|---|---|
|  |  |  |
|  |  |  |
|  |  |  |

## Lab Task 5 — Secure Development Workflow

Design a workflow showing where AI can help:

```text
requirements → design → coding → code review → testing → dependency scanning → deployment → monitoring
```

For each stage, state:

- AI support
- human review required
- possible risk

## Lab Deliverable

Submit a worksheet containing:

1. Vulnerability priority ranking.
2. Risk scoring model.
3. Code finding analysis.
4. False positive/negative analysis.
5. Secure development workflow.

Recommended length:

```text
1200–1800 words
```

---

# 14. Exercises

## Exercise 1 — Concept Check

1. What is the difference between severity and risk?
2. Why is CVSS alone insufficient?
3. What is exploitability?
4. What is exposure?
5. What is Secure by Design?
6. What is SSDF?
7. What is a false positive in code security scanning?
8. Why can dependency risk be difficult to assess?
9. What is software supply-chain security?
10. Why should AI code review output be validated?

## Exercise 2 — Short Analytical Answer

Write 250–300 words:

**Question:** Why should vulnerability prioritisation combine technical severity, exploitability, asset context, and business impact?

## Exercise 3 — Secure Code Review

List five code patterns that an AI-assisted secure code review tool should detect.

## Exercise 4 — Dependency Risk

Explain why a low-severity vulnerability in an internet-facing authentication component may be more urgent than a higher-severity vulnerability in an isolated test system.

---

# 15. Further Reading

## Core Reading

1. **NIST SP 800-218: Secure Software Development Framework**  
   <https://csrc.nist.gov/pubs/sp/800/218/final>

2. **CISA Secure by Design**  
   <https://www.cisa.gov/securebydesign>

3. **CISA Known Exploited Vulnerabilities Catalog**  
   <https://www.cisa.gov/known-exploited-vulnerabilities-catalog>

4. **CVE Program**  
   <https://www.cve.org/>

5. **CVSS by FIRST**  
   <https://www.first.org/cvss/>

6. **OWASP Top 10 Web Application Security Risks**  
   <https://owasp.org/www-project-top-ten/>

## Suggested Search Topics

- AI for vulnerability prioritisation
- exploit prediction models
- AI-assisted secure code review
- software supply-chain security
- dependency risk scoring
- Secure by Design practices
- SSDF implementation
