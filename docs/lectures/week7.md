---
title: "Week 7: AI for Security Operations and Threat Intelligence"
layout: default
permalink: /lectures/week5/
---

# Week 7: AI for Security Operations and Threat Intelligence  
## From Alerts to Prioritised Security Decisions

Welcome to Week 7 of **Applied AI for Cybersecurity**.

In Week 1, we introduced the foundations of applying AI to cybersecurity. In Week 2, we studied AI for network intrusion and DDoS detection. In Week 3, we focused on malware, phishing, and malicious URL detection.

This week focuses on a broader operational question:

> How can AI support security teams in handling alerts, correlating evidence, prioritising incidents, and using threat intelligence?

This week is not only about detecting attacks. It is about using AI to support **security operations**, where defenders must make decisions under uncertainty, time pressure, and limited analyst capacity.

---

# 1. Learning Objectives

By the end of this week, you should be able to:

1. Explain the role of AI in security operations.
2. Distinguish between events, alerts, incidents, and cases.
3. Explain the purpose of SIEM, SOAR, and threat intelligence.
4. Describe how AI can support alert triage and incident prioritisation.
5. Explain how weak signals can be correlated into a stronger incident.
6. Use threat intelligence to enrich security evidence.
7. Map evidence to attacker behaviour using frameworks such as MITRE ATT&CK.
8. Explain the difference between automated response and human-in-the-loop response.
9. Discuss the risks of over-automation in security operations.
10. Design an explainable AI-assisted incident triage process.

---

# 2. Why Security Operations Matter

Cybersecurity is not only about building detection models. In real organisations, detection is only one part of a larger operational process.

Security teams must answer questions such as:

- Which alerts matter most?
- Which alerts are duplicates?
- Which alerts belong to the same incident?
- Which users, hosts, domains, IP addresses, or files are involved?
- Is this behaviour mapped to a known attacker technique?
- Should the analyst monitor, investigate, escalate, contain, or close?
- Which actions can be automated safely?
- Which actions require human approval?

This is where **security operations** becomes important.

Security operations combines:

- Monitoring
- Detection
- Alert triage
- Threat intelligence
- Incident investigation
- Response coordination
- Evidence preservation
- Reporting
- Continuous improvement

AI can help with many of these tasks, but the final objective is not simply prediction. The objective is better security decision-making.

---

# 3. Events, Alerts, Incidents, and Cases

Students often use these terms interchangeably, but in security operations they mean different things.

| Term | Meaning | Example |
|---|---|---|
| Event | A recorded activity | A user logs in at 03:00 |
| Alert | A warning generated from one or more events | Login from unusual location |
| Incident | A meaningful security situation requiring investigation or response | Possible compromised account |
| Case | A managed investigation containing evidence, notes, tasks, and actions | Incident response case for suspected credential theft |

## Example

Suppose a system records these events:

```text
03:01 — User logs in from unusual country
03:03 — MFA fails twice
03:04 — MFA succeeds
03:07 — User accesses sensitive folder
03:10 — User downloads 2 GB
```

A security tool may generate alerts:

```text
Alert 1: Unusual login location
Alert 2: Multiple MFA failures
Alert 3: Large data download
```

An analyst may correlate these into one incident:

```text
Incident: Possible account compromise and data exfiltration
```

A case may then be opened to manage investigation and response.

---

# 4. SIEM, SOAR, and Threat Intelligence

## 4.1 SIEM

A **Security Information and Event Management** system collects, stores, correlates, and analyses security logs and events.

A SIEM may collect data from:

- Firewalls
- Endpoint detection tools
- Identity systems
- Cloud platforms
- Email security tools
- Web application firewalls
- DNS logs
- IDS/IPS sensors
- Vulnerability scanners

Typical SIEM tasks include:

- Log collection
- Normalisation
- Correlation
- Alert generation
- Dashboards
- Investigation search
- Reporting

Microsoft Sentinel is an example of a cloud-native security platform that provides attack detection, threat visibility, hunting, and threat response capabilities. Further reading: [Microsoft Sentinel documentation](https://learn.microsoft.com/en-us/azure/sentinel/).  

---

## 4.2 SOAR

**Security Orchestration, Automation, and Response** helps coordinate and automate security workflows.

SOAR may help to:

- Create incident tickets
- Enrich alerts with threat intelligence
- Query related logs
- Notify analysts
- Run playbooks
- Contain suspicious activity
- Standardise investigation tasks
- Document response actions

Automation must be handled carefully. Some actions are low risk, while others can disrupt business operations.

Example:

| Action | Automation Suitability |
|---|---|
| Query threat intelligence | Good candidate for automation |
| Collect related logs | Good candidate for automation |
| Create ticket | Good candidate for automation |
| Disable user account | Usually requires approval |
| Isolate production server | Requires approval |
| Block entire country | Requires approval |
| Delete files | Requires approval |

Microsoft Sentinel automation rules can be used to manage and orchestrate threat response, with triggers, conditions, and actions. Further reading: [Microsoft Sentinel automation rules](https://learn.microsoft.com/en-us/azure/sentinel/create-manage-use-automation-rules).

---

## 4.3 Threat Intelligence

Threat intelligence is knowledge about threats, attackers, infrastructure, tactics, techniques, and indicators.

Threat intelligence may include:

- Malicious IP addresses
- Malicious domains
- File hashes
- Malware family names
- Phishing infrastructure
- Command-and-control servers
- Vulnerabilities being exploited
- Attacker tactics and techniques
- Reports about threat actors
- Indicators of compromise

Threat intelligence helps analysts answer:

```text
Have we seen this indicator before?
Is this IP known as malicious?
Is this domain associated with malware?
Does this behaviour match a known attacker technique?
What other systems may be affected?
```

However, threat intelligence should not be used blindly. A known bad IP is useful evidence, but absence from a blocklist does not prove safety.

---

# 5. Practical Security Operations Workflow

A practical AI-assisted security operations workflow may be described as:

```text
1. Collect telemetry
2. Normalise and enrich events
3. Generate alerts
4. Group related alerts
5. Correlate evidence into incidents
6. Enrich with threat intelligence
7. Map to attacker behaviour
8. Prioritise risk
9. Decide response action
10. Document, learn, and improve
```

## 5.1 Collect Telemetry

Telemetry may include:

- Authentication logs
- Endpoint process logs
- Firewall logs
- DNS logs
- Cloud API logs
- Email security logs
- Web proxy logs
- IDS alerts
- Vulnerability scan results

## 5.2 Normalise and Enrich

Normalisation converts different formats into a common structure.

Enrichment adds context such as:

- User role
- Asset criticality
- Location
- Threat intelligence
- Vulnerability status
- Data sensitivity
- Business function
- Previous behaviour

## 5.3 Alert Grouping

Many tools generate duplicate or related alerts. AI can help group them.

Example:

```text
Alert: Unusual login
Alert: MFA anomaly
Alert: Suspicious file access
Alert: Large download
```

These may be grouped into:

```text
Possible account compromise incident
```

## 5.4 Incident Prioritisation

Risk can be based on:

- Evidence strength
- Asset criticality
- User privilege
- Data sensitivity
- Attack stage
- Threat intelligence match
- Business impact
- Confidence level
- Response urgency

---

# 6. How AI Supports Security Operations

AI can support security operations in several ways.

| Task | AI Support |
|---|---|
| Alert deduplication | Group repeated or similar alerts |
| Alert prioritisation | Rank alerts by risk |
| Anomaly detection | Identify unusual behaviour |
| Entity behaviour analytics | Learn normal behaviour of users, hosts, or services |
| Threat intelligence enrichment | Add reputation, context, and known associations |
| Incident summarisation | Summarise long evidence trails |
| Attack mapping | Suggest possible ATT&CK techniques |
| Response recommendation | Suggest containment or investigation steps |
| Case management | Recommend next tasks |
| Hunting support | Suggest queries or suspicious patterns |

AI should be treated as a decision-support layer, not as an unquestionable authority.

---

# 7. Alert Triage

Alert triage is the process of deciding which alerts require attention.

The analyst usually asks:

- Is this alert real or a false positive?
- Is it already contained?
- Is the affected asset critical?
- Is the user privileged?
- Is there supporting evidence?
- Are there related alerts?
- Is threat intelligence available?
- What is the likely impact?
- What should happen next?

## Example

Alert:

```text
Suspicious login from unusual country
```

Possible interpretations:

| Context | Interpretation |
|---|---|
| User is travelling | May be legitimate |
| User is also active locally | Possible impossible travel |
| MFA failed repeatedly before success | More suspicious |
| User is privileged admin | Higher risk |
| Followed by data download | Higher risk |
| IP is known malicious | Higher risk |

A good AI-assisted triage system should not only say:

```text
Risk score: 86
```

It should explain why.

---

# 8. Correlating Weak Signals

In security operations, a single alert may not prove an attack. Multiple weak signals may form stronger evidence.

Example:

```text
Weak signal 1: Login from unusual location
Weak signal 2: MFA failures
Weak signal 3: Access to sensitive data
Weak signal 4: Large download
Weak signal 5: Endpoint runs suspicious script
```

Individually, each signal may be explainable. Together, they may indicate an incident.

AI can help correlate signals across:

- Time
- Users
- Devices
- IP addresses
- Domains
- Files
- Processes
- Cloud resources
- Email messages

## Main lesson

> The value of AI in security operations is often not detecting one alert, but connecting many weak signals into an explainable incident.

---

# 9. Threat Intelligence Enrichment

Threat intelligence enrichment means adding external or internal threat context to an event or alert.

## Example

Alert:

```text
Host 10.0.5.23 connects to 185.199.x.x
```

Enrichment may add:

```text
IP reputation: suspicious
Associated malware family: unknown
ASN: cloud hosting provider
First seen: 2 days ago
Related domains: 3
Internal history: never contacted before
Threat feed match: yes
```

This helps the analyst assess risk.

## Useful Enrichment Questions

- Is the IP or domain known malicious?
- Is it newly registered?
- Has this host contacted it before?
- Is the destination expected for the business?
- Is the destination associated with malware, phishing, or C2?
- Are other internal hosts contacting the same indicator?
- Is there a known vulnerability being exploited?

## Warning

Threat intelligence is useful but incomplete.

```text
Known malicious → stronger evidence
Unknown → not necessarily safe
No match → not proof of benign activity
```

---

# 10. MITRE ATT&CK Mapping

MITRE ATT&CK is a knowledge base of adversary tactics and techniques. The Enterprise Matrix includes tactics and techniques across platforms such as Windows, macOS, Linux, SaaS, IaaS, identity providers, network devices, containers, and others. Further reading: [MITRE ATT&CK Enterprise Matrix](https://attack.mitre.org/matrices/enterprise/).  

## Why ATT&CK Mapping Is Useful

ATT&CK helps analysts describe attacker behaviour using a shared vocabulary.

Example:

| Evidence | Possible ATT&CK Interpretation |
|---|---|
| Phishing email with attachment | Initial Access |
| PowerShell command | Execution |
| New scheduled task | Persistence |
| Credential dumping tool | Credential Access |
| Network scanning | Discovery |
| Remote service connection | Lateral Movement |
| Large data transfer | Exfiltration |
| File encryption | Impact |

## Example

Raw evidence:

```text
winword.exe launches powershell.exe
powershell.exe downloads executable
new scheduled task created
external C2 connection observed
```

Possible behaviour mapping:

```text
Initial Access → Execution → Persistence → Command and Control
```

This mapping makes the investigation easier to explain.

---

# 11. Incident Prioritisation

Not every incident has equal priority.

A useful prioritisation model may consider:

| Factor | Question |
|---|---|
| Asset criticality | Is the affected asset important? |
| User privilege | Is the user an administrator or high-value target? |
| Data sensitivity | Is sensitive data involved? |
| Evidence strength | How strong is the evidence? |
| Threat intelligence | Are known malicious indicators involved? |
| Attack stage | Is the attack early or already causing impact? |
| Spread | Are multiple systems affected? |
| Business impact | Is a critical service at risk? |
| Confidence | How certain is the detection? |
| Response cost | Would containment disrupt operations? |

## Example Risk Score

```text
Privileged user involved: +20
Sensitive data accessed: +20
Known malicious IP: +25
Multiple related alerts: +15
Business-critical asset: +20
Known maintenance window: -20
User travel confirmed: -15
```

Risk scoring should be explainable. A score without evidence is not enough.

---

# 12. Human-in-the-Loop Security Operations

Human-in-the-loop means the AI system supports the analyst, but humans remain responsible for important decisions.

## AI Can Often Automate

- Alert grouping
- Threat intelligence lookup
- Evidence collection
- Ticket creation
- Incident summary generation
- Low-risk notification
- Query suggestion
- Log retrieval

## Human Approval Is Usually Needed For

- Disabling accounts
- Isolating production servers
- Blocking business-critical traffic
- Deleting files
- Revoking privileged access
- Public incident reporting
- Declaring a major incident
- Legal or regulatory notifications

## Why Human Oversight Matters

AI can be wrong because of:

- Missing context
- Poor data quality
- Outdated threat intelligence
- Misleading correlations
- Biased training data
- Adversarial manipulation
- Incorrect thresholds

A high-confidence AI result may still require human review if the response action is high impact.

---

# 13. Case Study 1: Account Compromise or Legitimate Travel?

## Scenario

A senior university administrator logs in from another country at 08:30. The system flags the login as suspicious.

Additional events:

```text
08:30 — Login from foreign country
08:32 — MFA success
08:40 — Access to finance documents
08:45 — Download of 500 MB
09:00 — Helpdesk confirms the user is attending a conference abroad
```

## Possible Interpretation

| Evidence | Interpretation |
|---|---|
| Foreign login | Initially suspicious |
| MFA success | Could be legitimate or compromised |
| Finance access | Expected if user role requires it |
| Download | Could be normal or suspicious |
| Travel confirmed | Reduces risk |

## Security Operations Lesson

The initial alert may be legitimate. The analyst should not automatically disable the account without checking context.

Possible response:

```text
Monitor session
Confirm device identity
Check whether access matches user role
Require step-up authentication if uncertainty remains
Avoid disruptive action unless stronger evidence appears
```

---

# 14. Case Study 2: Endpoint Alert Correlation

## Scenario

An endpoint tool generates three alerts:

```text
Alert 1: Word launched PowerShell
Alert 2: PowerShell used encoded command
Alert 3: Unknown executable downloaded
```

Individually, each alert may be suspicious. Together, they may indicate malicious document execution.

## Possible Correlation

```text
Phishing attachment
→ Word execution
→ PowerShell command
→ Payload download
→ Malware execution
```

## Threat Intelligence Enrichment

The downloaded file hash is unknown. The domain was registered two days ago. Other internal hosts have not contacted it before.

## Possible Decision

```text
Escalate to incident response
Isolate endpoint if evidence strengthens
Preserve logs
Collect the document and downloaded file
Search for similar activity across other hosts
```

---

# 15. Case Study 3: Threat Intelligence False Confidence

## Scenario

A SOC alert shows a connection to an IP address. Threat intelligence says the IP was malicious six months ago.

## Questions

- Is the IP still malicious?
- Is the IP shared by a cloud provider?
- Has ownership changed?
- Are there other supporting indicators?
- Does the internal host behaviour look suspicious?

## Lesson

Threat intelligence must be interpreted. A threat feed match is evidence, not proof.

---

# 16. Common Failures in AI-Assisted Security Operations

| Failure | Explanation |
|---|---|
| Alert flooding | AI generates too many alerts |
| Poor grouping | Unrelated alerts are grouped together |
| Missed correlation | Related signals are not connected |
| Context blindness | AI ignores business or user context |
| Threat-intel overreliance | AI treats feed matches as proof |
| Poor explainability | Analysts cannot understand the score |
| Unsafe automation | AI triggers disruptive actions |
| Stale models | Model no longer matches current environment |
| Feedback errors | Wrong analyst decisions are fed back into the system |

Important point:

> AI in security operations should reduce analyst burden, not create a new layer of unexplained noise.

---

# 17. Week 4 Summary

This week focused on AI for security operations and threat intelligence.

Key points:

```text
Security operations involves monitoring, triage, investigation, response, and learning.

SIEM supports collection, correlation, and alerting.

SOAR supports orchestration and automation.

Threat intelligence enriches evidence but should not be treated as proof.

AI can help group alerts, prioritise risk, summarise incidents, and recommend actions.

Weak signals can become strong evidence when correlated.

MITRE ATT&CK provides a shared language for mapping evidence to attacker behaviour.

Human approval is essential for high-impact response actions.

A useful AI-assisted security operations system must be explainable, proportionate, and accountable.
```

Final takeaway:

> AI should help analysts turn alerts into prioritised, explainable, and proportionate security decisions.

---

# 18. Lab Sheet 4: AI-Assisted Alert Triage and Threat Intelligence

## Lab Overview

In this lab, you will analyse a set of simplified security alerts, group related alerts into incidents, enrich them with threat intelligence, assign priority, and decide which actions should be automated or require human approval.

This lab focuses on security operations reasoning. No live malware, real attack execution, or active scanning is required.

---

## Lab Duration

Approximate duration: 90 minutes.

---

## Lab Mode

Individual work followed by small-group discussion.

---

## Lab Objectives

By completing this lab, you should be able to:

1. Distinguish events, alerts, and incidents.
2. Group related alerts into possible incidents.
3. Use context and threat intelligence to enrich evidence.
4. Prioritise incidents based on risk.
5. Map evidence to attacker behaviour.
6. Define safe and unsafe automation actions.
7. Produce an analyst-friendly incident summary.

---

# 19. Lab Dataset A: Security Alerts

Use the following simplified alert set.

| Alert ID | Source | Alert Description |
|---|---|---|
| A1 | Identity | User login from unusual country |
| A2 | Identity | MFA failed twice, then succeeded |
| A3 | Cloud | Same user accessed sensitive finance folder |
| A4 | Cloud | Same user downloaded 1.2 GB of files |
| A5 | Endpoint | Word launched PowerShell |
| A6 | Endpoint | PowerShell used encoded command |
| A7 | Endpoint | Unknown executable downloaded |
| A8 | DNS | Host queried rare domain repeatedly |
| A9 | Threat Intel | Domain associated with recent malware campaign |
| A10 | Firewall | Outbound connection to suspicious IP |
| A11 | HR System | User is confirmed to be travelling abroad |
| A12 | Asset Inventory | Affected host belongs to finance department |
| A13 | Vulnerability Scanner | Host is missing recent security patches |
| A14 | Helpdesk | User reports laptop is running slowly |
| A15 | Email Security | User received email with macro-enabled attachment |

---

# 20. Lab Task 1 — Classify Items as Event, Alert, Context, or Intelligence

Complete the table.

| Item ID | Event / Alert / Context / Threat Intelligence | Reason |
|---|---|---|
| A1 |  |  |
| A2 |  |  |
| A3 |  |  |
| A4 |  |  |
| A5 |  |  |
| A6 |  |  |
| A7 |  |  |
| A8 |  |  |
| A9 |  |  |
| A10 |  |  |
| A11 |  |  |
| A12 |  |  |
| A13 |  |  |
| A14 |  |  |
| A15 |  |  |

---

# 21. Lab Task 2 — Group Related Alerts into Incidents

Group the alerts into possible incidents.

Example incident groups may include:

```text
Possible account compromise
Possible malicious document execution
Possible malware command-and-control
Possible data exfiltration
Possible benign travel-related access
```

Complete the table.

| Incident Group | Related Alert IDs | Why They Belong Together |
|---|---|---|
|  |  |  |
|  |  |  |
|  |  |  |

---

# 22. Lab Task 3 — Add Context and Revise Interpretation

Some evidence increases risk. Some evidence reduces risk.

Complete the table.

| Evidence | Increases or Reduces Risk? | Explanation |
|---|---|---|
| User login from unusual country |  |  |
| User confirmed travelling abroad |  |  |
| MFA failed twice before success |  |  |
| Sensitive folder accessed |  |  |
| Large download |  |  |
| Word launched PowerShell |  |  |
| Threat-intel match on domain |  |  |
| Host missing patches |  |  |
| User reports laptop slow |  |  |

Then answer:

1. Which initial interpretation changed after adding context?
2. Which evidence remains concerning?
3. What additional evidence would you request?

---

# 23. Lab Task 4 — Map Evidence to Attacker Behaviour

Use the following attacker behaviour categories:

- Initial access
- Execution
- Persistence
- Credential access
- Discovery
- Lateral movement
- Command and control
- Exfiltration
- Impact
- Uncertain

Complete the table.

| Evidence | Possible Behaviour Category | Reason |
|---|---|---|
| Macro-enabled attachment |  |  |
| Word launched PowerShell |  |  |
| Encoded PowerShell command |  |  |
| Unknown executable downloaded |  |  |
| Repeated DNS queries to rare domain |  |  |
| Large download from finance folder |  |  |
| Outbound connection to suspicious IP |  |  |

---

# 24. Lab Task 5 — Prioritise the Incident

Design a simple prioritisation score.

Use 6–8 indicators, such as:

- Privileged user involved
- Sensitive data accessed
- Known threat intelligence match
- Endpoint suspicious behaviour
- Asset criticality
- Confirmed travel context
- Patch status
- User report
- Evidence confidence
- Possible business impact

Complete the table.

| Indicator | Score Contribution | Why It Matters |
|---|---:|---|
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |

Define thresholds.

| Score Range | Priority |
|---|---|
| 0–30 |  |
| 31–60 |  |
| 61–80 |  |
| 81–100 |  |

---

# 25. Lab Task 6 — Decide Response and Automation Boundaries

Choose suitable actions.

Possible actions:

```text
Monitor
Collect more logs
Query threat intelligence
Create incident ticket
Notify analyst
Ask user to confirm activity
Require step-up authentication
Revoke sessions
Isolate endpoint
Block domain
Block IP
Disable user account
Escalate to incident response
Preserve forensic evidence
```

Complete the table.

| Action | Automate? | Human Approval Required? | Reason |
|---|---|---|---|
| Query threat intelligence |  |  |  |
| Collect endpoint logs |  |  |  |
| Create incident ticket |  |  |  |
| Require step-up authentication |  |  |  |
| Block domain |  |  |  |
| Isolate endpoint |  |  |  |
| Disable user account |  |  |  |
| Escalate to incident response |  |  |  |

---

# 26. Lab Task 7 — Write an Analyst-Friendly Incident Summary

Rewrite the alert set into a short incident summary.

Your summary should include:

1. Incident title.
2. Main evidence.
3. Risk-increasing factors.
4. Risk-reducing factors.
5. Most likely interpretation.
6. Recommended next action.
7. Actions requiring human approval.
8. Missing evidence.

Avoid writing only:

```text
Risk score: 86
```

Instead, explain why the incident matters.

---

# 27. Lab Task 8 — Critique AI Support

Answer:

1. Which parts of this investigation could AI help with?
2. Which parts require human judgement?
3. What could go wrong if the AI grouped unrelated alerts?
4. What could go wrong if the AI ignored travel context?
5. What could go wrong if the AI automatically disabled the user account?
6. How should analyst feedback be used to improve the system?

---

# 28. Lab Deliverable

Submit a short worksheet containing:

1. Event/alert/context/intelligence classification.
2. Incident grouping table.
3. Context and risk interpretation table.
4. ATT&CK-style behaviour mapping.
5. Incident prioritisation score.
6. Response and automation boundary table.
7. Analyst-friendly incident summary.
8. Short critique of AI support.

Recommended length:

```text
1000–1500 words
```

---

# 29. Exercises

## Exercise 1 — Concept Check

Answer briefly.

1. What is the difference between an event and an alert?
2. What is the difference between an alert and an incident?
3. What is the role of a SIEM?
4. What is the role of SOAR?
5. What is threat intelligence?
6. Why is threat intelligence not proof?
7. What is alert triage?
8. Why is alert grouping useful?
9. Why is explainability important in security operations?
10. Give two examples of response actions that should require human approval.

---

## Exercise 2 — Short Analytical Answer

Write 250–300 words.

**Question:**  
Why should AI in security operations be treated as decision support rather than full replacement for human analysts?

Your answer should discuss at least four of the following:

- Context
- False positives
- False negatives
- Threat intelligence limitations
- Business impact
- Unsafe automation
- Explainability
- Human accountability
- Legal or regulatory implications

---

## Exercise 3 — Threat Intelligence Analysis

A domain appears in a threat-intelligence feed.

Answer:

1. What questions should an analyst ask before treating it as malicious?
2. What additional evidence would strengthen the case?
3. What evidence might reduce the risk?
4. Why might a domain appear in a feed but no longer be malicious?
5. What response would be proportionate?

---

## Exercise 4 — Alert Grouping

Given these alerts:

```text
Alert 1: User received suspicious email
Alert 2: Word launched PowerShell
Alert 3: PowerShell downloaded executable
Alert 4: DNS query to rare domain
Alert 5: Outbound connection to suspicious IP
```

Answer:

1. Should these alerts be grouped into one incident?
2. What is the likely attack chain?
3. What evidence is missing?
4. Which response actions are appropriate?
5. Which actions require approval?

---

## Exercise 5 — Automation Reflection

Read the statement:

```text
If an AI system assigns an incident a high risk score, containment should be automatic.
```

Do you agree or disagree?

Write 200–300 words. Discuss:

- Reversibility
- Business impact
- Confidence
- Evidence quality
- Human approval
- Automation boundaries

---

## Exercise 6 — Explainability Practice

Rewrite this poor incident output into an analyst-friendly explanation.

Poor output:

```text
Incident probability: 91%
Recommended action: Disable account
```

Your improved explanation should include:

- Risk-increasing evidence
- Risk-reducing evidence
- Threat intelligence
- Missing evidence
- Recommended next action
- Whether human approval is required

---

# 30. Further Reading

## Core Reading

1. **NIST SP 800-61 Rev. 3: Incident Response Recommendations and Considerations for Cybersecurity Risk Management**  
   Useful for understanding incident response as part of cybersecurity risk management, including preparation, detection, response, and recovery.  
   <https://csrc.nist.gov/pubs/sp/800/61/r3/final>

2. **CISA: Cybersecurity Incident and Vulnerability Response Playbooks**  
   Useful for practical response guidance, incident coordination, remediation, recovery, and tracking.  
   <https://www.cisa.gov/planning-response-recovery>

3. **MITRE ATT&CK Enterprise Matrix**  
   Useful for mapping evidence to adversary tactics and techniques.  
   <https://attack.mitre.org/matrices/enterprise/>

4. **MITRE ATT&CK Enterprise Techniques**  
   Useful for exploring specific adversary techniques and associated behaviours.  
   <https://attack.mitre.org/techniques/enterprise/>

5. **Microsoft Sentinel Documentation**  
   Useful for understanding practical SIEM/SOAR concepts, analytics, incidents, hunting, and response.  
   <https://learn.microsoft.com/en-us/azure/sentinel/>

6. **Microsoft Sentinel Automation Rules**  
   Useful for understanding how automation rules can orchestrate response actions under defined triggers and conditions.  
   <https://learn.microsoft.com/en-us/azure/sentinel/create-manage-use-automation-rules>

---

## Suggested Search Topics

Search for recent academic or technical material on:

- AI-assisted alert triage
- SIEM analytics
- SOAR automation
- Threat intelligence enrichment
- Alert correlation
- Incident prioritisation
- MITRE ATT&CK mapping
- Human-in-the-loop security operations
- LLMs for SOC analysts
- Explainable AI for security operations
- Analyst feedback loops
- Automation risk in cybersecurity

---

# 31. Week 4 Summary

This week focused on AI for security operations and threat intelligence.

The most important lessons are:

```text
Security operations is about turning evidence into action.

SIEM collects, correlates, and analyses security events.

SOAR coordinates and automates response workflows.

Threat intelligence enriches evidence but does not prove maliciousness by itself.

AI can help with grouping, prioritisation, enrichment, summarisation, and recommendation.

Weak signals can become strong evidence when correlated.

MITRE ATT&CK helps map evidence to attacker behaviour.

Human oversight is essential for high-impact response decisions.

Useful AI in security operations must be explainable, proportionate, and accountable.
```

Final takeaway:

> AI should help security analysts make better decisions, not simply generate more alerts.
