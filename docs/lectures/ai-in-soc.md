---
title: "AI in the Security Operations Center"
layout: default
nav_order: 6
permalink: /lectures/ai-in-soc/
---

# AI in the Security Operations Center

## From Noisy Alerts to Threat Decisions

**Teaching Assessment: Applied AI for Cybersecurity**

# Purpose of the Revised Lecture

This revised version strengthens the lecture for a Level 6 undergraduate audience in cybersecurity. The original version introduced useful ideas, but the opening example, mini-case study, and activity were too similar. They all focused on the same pattern: unusual login, file download, and campus login. This made the lecture repetitive and reduced the technical depth.

The revised design separates the teaching functions clearly:

- The **opening hook** is now only a short two-slide triage puzzle.

- The **main lecture body** explains SOC telemetry, AI pipelines, risk scoring, and limitations at a deeper level.

- The **mini-case study** is now a higher-level multi-stage ransomware and cloud-exfiltration scenario.

- The **interactive activity** asks students to build a threat hypothesis and justify a proportionate response.

> **Teaching Point**
>
> The central message is not simply that “AI detects anomalies”. The stronger Level 6 message is that AI helps the SOC convert heterogeneous telemetry into evidence-based, explainable, and proportionate threat decisions.

# Lecture Overview

A Security Operations Center, or **SOC**, monitors security telemetry, investigates suspicious activity, and coordinates incident response. Modern SOCs receive data from firewalls, identity systems, endpoints, cloud platforms, email gateways, vulnerability scanners, threat intelligence feeds, and network sensors.

The challenge is not only that organizations face attacks. The operational challenge is that defenders must make decisions under:

- **high volume**: thousands or millions of events per day;

- **high uncertainty**: incomplete and sometimes contradictory evidence;

- **high speed**: attackers may move from initial access to impact in minutes or hours;

- **high consequence**: both missed attacks and unnecessary containment can harm the organization.

AI is therefore used not as a magic detector, but as a decision-support layer that helps analysts prioritize, correlate, enrich, explain, and respond.

# Learning Objectives

By the end of this lecture, students should be able to:

1.  Explain why AI is used in modern SOC environments.

2.  Distinguish between raw telemetry, features, alerts, incidents, and response decisions.

3.  Map SOC telemetry to adversary behaviour using a framework such as MITRE ATT&CK.

4.  Explain how AI-based systems perform alert prioritization, anomaly detection, event correlation, and risk scoring.

5.  Analyse why accuracy alone is a poor evaluation measure for SOC models.

6.  Construct a threat hypothesis from incomplete evidence in a multi-stage attack scenario.

7.  Evaluate when response should be automated and when human approval is required.

# Opening Hook: Which Alert Deserves Human Attention?

## Slide 1: The Triage Problem

It is **02:17 a.m.**. The SOC dashboard shows **1,248 alerts**. A human analyst cannot investigate all of them manually.

The practical SOC question is not:

> Can we detect every suspicious event?

The practical SOC question is:

> Which few events deserve human attention now?

Consider three alerts:

| Alert | Description | First Impression |
|:------|:------------|:-----------------|
| A | 300 failed logins from one external IP address | Very noisy and suspicious |
| B | One successful login from a new country, followed by unusual access to cloud storage | Less noisy but potentially more damaging |
| C | Malware signature detected on a quarantined test machine | Serious, but already contained |

> **In-Class Question**
>
> **Question to students:** Which alert should the SOC analyst investigate first, and why?

## Slide 2: The Teaching Point

Alert B should probably be investigated first because it combines several risk factors:

- the access was successful;

- the location is unusual;

- the account reached cloud storage;

- the potential impact may involve data exposure.

Alert A may be a blocked brute-force attempt. Alert C may sound serious, but the machine has already been quarantined. Alert B is dangerous because the attacker may already be inside.

> **Teaching Point**
>
> A SOC is not only an alert detector. A SOC is a decision system. AI is useful when it helps analysts decide which weak signals combine into a credible threat.

# Why AI Is Used in the SOC

AI is used because the SOC faces a mismatch between the scale of machine-generated telemetry and the limited attention of human analysts.

| **SOC Problem**           | **Why It Is Difficult**                    | **How AI Can Help**                                                      |
|:--------------------------|:-------------------------------------------|:-------------------------------------------------------------------------|
| Alert fatigue             | Many alerts are low quality or duplicated  | Cluster, suppress, deduplicate, and prioritize alerts                    |
| Multi-stage attacks       | One event may look harmless in isolation   | Correlate weak signals across time, users, devices, and services         |
| Changing normal behaviour | Static rules become outdated               | Learn behavioural baselines and detect deviations                        |
| Subtle attacker behaviour | Attackers avoid obvious signatures         | Detect rare sequences, low-and-slow activity, and abnormal relationships |
| Heterogeneous evidence    | Logs come from different tools and formats | Normalize, enrich, and connect evidence                                  |
| Operational risk          | Wrong response can disrupt business        | Support proportionate response using risk and confidence                 |

## Rules Are Necessary but Not Sufficient

A traditional rule might be:

```text
IF failed_login_count > 100 THEN create_alert
```

This can detect brute-force attacks, but it may miss more realistic attacks where the adversary already has valid credentials:

```text
Successful login from unusual infrastructure
+ abnormal cloud API calls
+ rare process execution on endpoint
+ unusual SMB access to file server
+ staged archive uploaded to external service
= possible hands-on-keyboard intrusion
```

> **Level 6 Depth Point**
>
> At Level 6, students should see the difference between **event detection** and **threat reasoning**. SOC work is not only classification; it is evidence construction under uncertainty.

# What AI Actually Sees

AI does not directly see attackers, motives, or intentions. It sees traces left in telemetry.

## SOC Telemetry Sources

| **Data Source**     | **Examples of Evidence**                                                                   |
|:--------------------|:-------------------------------------------------------------------------------------------|
| Identity logs       | login time, source IP, device, MFA result, privilege changes, impossible travel            |
| Endpoint telemetry  | process execution, parent-child process relationship, command-line arguments, file changes |
| Network logs        | flows, ports, protocols, traffic volume, east-west movement, unusual destinations          |
| DNS logs            | rare domains, newly registered domains, domain generation patterns                         |
| Email logs          | sender reputation, attachments, URLs, user clicks, phishing indicators                     |
| Cloud audit logs    | API calls, object storage access, token use, VM creation, IAM changes                      |
| Proxy and web logs  | external uploads, downloads, category of destination service                               |
| Threat intelligence | known malicious IPs, domains, hashes, adversary infrastructure                             |
| Asset inventory     | criticality of server, owner, business function, exposure, patch level                     |
| Vulnerability data  | known exploitable weaknesses and missing controls                                          |

## From Events to Entities and Relationships

A mature AI-assisted SOC should not treat logs as disconnected rows. It should connect entities:

```text
User  -> logs into -> Cloud service
User  -> uses      -> Device
Device -> connects to -> File server
Process -> spawns -> PowerShell
Device -> uploads to -> External service
IP address -> associated with -> VPN provider or threat infrastructure
```

This creates an **entity graph**. Graph-based reasoning can help detect suspicious relationships that are not obvious from one log line.

> **Teaching Point**
>
> A single event asks: “Is this log line suspicious?” A graph asks: “Does this relationship between user, device, process, resource, and destination make sense?”

## Context Changes Meaning

| **Event**                       | **Context**                                     | **Interpretation** |
|:--------------------------------|:------------------------------------------------|:-------------------|
| Large data transfer at midnight | Backup server                                   | Possibly normal    |
| Large data transfer at midnight | HR laptop                                       | Suspicious         |
| PowerShell execution            | System administrator workstation                | Possibly normal    |
| PowerShell execution            | Reception desk computer                         | Suspicious         |
| Login from new country          | User is travelling and uses managed device      | Possibly normal    |
| Login from new country          | User is active locally at the same time         | Highly suspicious  |
| OAuth consent grant             | Approved enterprise app                         | Possibly normal    |
| OAuth consent grant             | Unknown app asking for mailbox and files access | Suspicious         |

# From Raw Logs to Threat Decisions

The AI-assisted SOC pipeline can be represented as follows:

```text
Raw telemetry
  -> Collection and normalization
  -> Enrichment with asset, identity, vulnerability, and threat intelligence context
  -> Feature extraction and representation
  -> Detection models
  -> Correlation and risk scoring
  -> Incident generation
  -> Analyst investigation
  -> Response decision
  -> Feedback and model improvement
```

## Step 1: Collection and Normalization

Logs arrive in different formats. A firewall event, an identity event, an endpoint event, and a cloud API event do not look the same.

```text
Firewall log:
src_ip, dst_ip, port, protocol, action
```

```text
Identity log:
user_id, login_time, source_ip, MFA_result, device_id
```

```text
Endpoint log:
host_id, process_name, parent_process, command_line, file_hash
```

```text
Cloud audit log:
user_id, API_call, resource_name, object_id, access_time
```

Normalization converts this heterogeneous data into a consistent structure so that it can be searched, correlated, and modelled.

## Step 2: Enrichment

Raw events rarely contain enough meaning. The SOC enriches them:

```text
IP address -> known malicious, residential VPN, Tor exit, cloud provider, normal country?
User -> role, normal working hours, usual device, privilege level?
Device -> managed or unmanaged, criticality, patch level, EDR status?
File or resource -> public, internal, confidential, regulated?
Process -> signed binary, admin tool, suspicious command line?
Cloud API call -> common for this user or rare and high-impact?
```

## Step 3: Feature Extraction

AI models usually do not operate directly on raw log text. They need measurable features.

| **Feature Type** | **Example Feature**                    | **Why It Matters**                 |
|:-----------------|:---------------------------------------|:-----------------------------------|
| Frequency        | failed logins per minute               | Brute force or credential stuffing |
| Rarity           | process rarity score for this host     | Unusual execution behaviour        |
| Temporal         | activity outside user baseline         | Suspicious time pattern            |
| Geo-spatial      | distance from usual login region       | Possible impossible travel         |
| Sequence         | login then discovery then exfiltration | Multi-stage attack pattern         |
| Graph-based      | unusual edge between user and resource | Abnormal relationship              |
| Semantic         | suspicious command-line tokens         | Malicious use of legitimate tools  |
| Contextual       | asset criticality and data sensitivity | Business impact                    |

## Step 4: Detection Models

Different AI methods support different SOC tasks.

| **Method**                     | **Typical SOC Use**                                  | **Main Risk**                           |
|:-------------------------------|:-----------------------------------------------------|:----------------------------------------|
| Supervised learning            | Classify known malicious and benign examples         | Poor generalization to new attacks      |
| Unsupervised anomaly detection | Detect rare behaviour without many labels            | Many false positives                    |
| Semi-supervised learning       | Learn normal behaviour, flag deviations              | Concept drift                           |
| Graph analytics                | Detect suspicious entity relationships               | Data integration complexity             |
| Sequence models                | Detect abnormal order of events                      | Requires good temporal data             |
| LLMs                           | Summarize incidents, explain evidence, assist triage | Hallucination and over-trust            |
| Reinforcement learning         | Support adaptive response policies                   | Unsafe exploration in real environments |

## Step 5: Correlation and Risk Scoring

A mature SOC should not treat each event as independent. It should ask:

> Do multiple weak signals combine into a strong threat hypothesis?

A simplified risk score can be expressed as:

$$\text{Risk} = f(\text{likelihood}, \text{confidence}, \text{asset criticality}, \text{data sensitivity}, \text{attack stage})$$

For teaching purposes, this can be simplified:

$$\text{Risk Score} = 0.35A + 0.25B + 0.20C + 0.20D$$

where:

- $A$ = anomaly strength;

- $B$ = confidence in evidence;

- $C$ = asset or data criticality;

- $D$ = attack-stage severity.

> **Level 6 Depth Point**
>
> The model score is not the decision. The decision also depends on business impact, legal context, operational risk, and confidence in the evidence.

# Why Accuracy Alone Is Not Enough

A common beginner mistake is to say: “The model is 95% accurate, so it is good.” In a SOC, this can be misleading because real attacks are rare.

Assume a SOC processes **100,000 events** in one day. Suppose only **100** of them are truly malicious. A model has:

- 95% true positive rate;

- 1% false positive rate.

Then:

| **Measure**     | **Result**                                          |
|:----------------|:----------------------------------------------------|
| True positives  | 95 malicious events detected                        |
| False negatives | 5 malicious events missed                           |
| False positives | approximately 999 benign events incorrectly alerted |
| Precision       | $95 / (95 + 999) \approx 8.7\%$                     |

> **In-Class Question**
>
> **Question to students:** Why can a model with a low false positive rate still overwhelm the SOC?
>
> **Expected answer:** Because benign events are far more common than malicious events. Even a small false positive rate can generate many false alerts.

> **Teaching Point**
>
> For SOC evaluation, students should consider precision, recall, false positive cost, false negative cost, time-to-detect, time-to-triage, explainability, and response impact.

# Higher-Level Mini-Case: Multi-Stage Ransomware and Cloud Exfiltration

> **Case Focus**
>
> This case is intentionally different from the short opening hook. The opening hook teaches prioritization. This mini-case teaches multi-stage reasoning, telemetry fusion, adversary tactics, and response trade-offs.

## Scenario

A university department is targeted by an attacker. The attacker begins with phishing, obtains valid credentials, abuses cloud access, moves laterally through the network, stages sensitive research data, and then prepares for ransomware impact.

This scenario is more advanced than a simple unusual-login case because it requires students to reason across identity, email, endpoint, network, and cloud evidence.

## Timeline of Evidence

| **Time** | **Observed Evidence**                                                        | **Telemetry Source**                  | **SOC Interpretation**                                    |
|:---------|:-----------------------------------------------------------------------------|:--------------------------------------|:----------------------------------------------------------|
| 09:12    | Staff member clicks a link in a delivery-themed email                        | Email security gateway and click logs | Possible phishing entry point                             |
| 09:18    | Successful login from residential VPN infrastructure using valid credentials | Identity logs                         | Valid account misuse; not enough alone, but suspicious    |
| 09:21    | Unknown OAuth application requests access to mailbox and cloud files         | Cloud audit logs                      | Possible token abuse or persistence through consent grant |
| 09:42    | Endpoint runs PowerShell with encoded command after browser activity         | EDR telemetry                         | Suspicious execution pattern                              |
| 10:05    | Device connects to multiple file shares it rarely accesses                   | Network and file server logs          | Discovery or lateral movement                             |
| 10:26    | Large archive file is created and uploaded to an external storage service    | Endpoint, proxy, and cloud logs       | Data staging and possible exfiltration                    |
| 10:40    | Attempts to disable backups and delete shadow copies                         | EDR and Windows event logs            | Ransomware preparation or impact phase                    |

## Mapping to Adversary Behaviour

Students should not only list events. They should map evidence to attacker objectives.

| **Adversary Objective**    | **Evidence in the Case**                | **Relevant SOC Question**                                         |
|:---------------------------|:----------------------------------------|:------------------------------------------------------------------|
| Initial access             | Phishing link click and credential use  | Was the user phished, and were credentials captured?              |
| Persistence or token abuse | Unknown OAuth consent grant             | Can the attacker continue access even after password reset?       |
| Execution                  | Encoded PowerShell execution            | Is this legitimate administration or malicious command execution? |
| Discovery and collection   | Rare file share access and data archive | What data was accessed and staged?                                |
| Exfiltration               | Upload to external storage service      | Was sensitive data transferred outside the organization?          |
| Impact                     | Backup deletion attempts                | Is ransomware deployment imminent?                                |

> **Teaching Point**
>
> This case encourages students to think in terms of a threat hypothesis: “The attacker is moving from valid account access toward data theft and ransomware impact.”

## What the AI System Does

The AI-assisted SOC does not simply say “malicious” or “benign”. It supports investigation by combining evidence.

```text
Evidence cluster:
- Phishing click by same user
- Successful login from unusual infrastructure
- Unknown OAuth consent grant
- Encoded PowerShell on managed endpoint
- Rare access to file shares
- Archive creation and external upload
- Backup deletion attempts
```

```text
Threat hypothesis:
Possible hands-on-keyboard intrusion progressing toward data exfiltration and ransomware impact.
```

```text
Risk level:
Critical
```

```text
Recommended immediate actions:
1. Revoke cloud sessions and OAuth tokens.
2. Isolate the endpoint from the network.
3. Disable or reset the affected account after preserving evidence.
4. Block the external upload destination temporarily.
5. Check whether other users clicked the same phishing link.
6. Preserve logs and start incident response procedures.
```

## What the Human Analyst Must Validate

The analyst should validate:

1.  Was the OAuth application approved by IT or by the user?

2.  Is PowerShell execution normal for this role and device?

3.  Which files were accessed, archived, and uploaded?

4.  Was the external destination personal cloud storage, attacker infrastructure, or a legitimate service?

5.  Are backup deletion attempts confirmed, or are they false positives?

6.  Are other users affected by the same phishing campaign?

7.  What containment action is proportionate to the evidence and business impact?

> **Level 6 Depth Point**
>
> This is the correct depth for Level 6: students should connect technical evidence, attacker behaviour, model output, and operational response.

# Interactive Activity: Build a Threat Hypothesis

## Activity Goal

Students practise SOC reasoning by constructing a threat hypothesis from incomplete evidence. They must avoid two weak answers:

- **Overreaction:** “Disable everything immediately.”

- **Underreaction:** “It is only one suspicious login.”

## Student Task

Working in pairs, students answer the following:

1.  Which evidence items are weak signals, and which are strong signals?

2.  Which events map to initial access, execution, collection, exfiltration, and impact?

3.  What is the most plausible threat hypothesis?

4.  Which immediate containment actions are justified?

5.  Which actions should require human approval?

6.  What additional evidence would reduce uncertainty?

## Expected High-Quality Student Answer

A strong answer should say something like:

> The case suggests a multi-stage intrusion rather than a single anomalous login. The phishing click and valid login are early signals. The OAuth consent grant increases concern because token access may survive password reset. Encoded PowerShell, rare file share access, archive creation, external upload, and backup deletion attempts together support a high-confidence hypothesis of data theft followed by ransomware preparation. Immediate containment is justified, but destructive actions should be controlled and evidence should be preserved.

## Possible Risk-Scoring Exercise

Ask students to score the case from 0 to 5 for each dimension:

| **Dimension**          | **Score** | **Reason**                                                                 |
|:-----------------------|:----------|:---------------------------------------------------------------------------|
| Anomaly strength       | 5         | Multiple abnormal behaviours across identity, endpoint, network, and cloud |
| Evidence confidence    | 4         | Several independent telemetry sources confirm the pattern                  |
| Asset/data criticality | 4         | Research files and institutional data may be sensitive                     |
| Attack-stage severity  | 5         | Evidence reaches exfiltration and possible impact phase                    |

Using the simple formula:

$$\text{Risk Score} = 0.35A + 0.25B + 0.20C + 0.20D$$

we get:

$$0.35(5) + 0.25(4) + 0.20(4) + 0.20(5) = 4.55/5$$

This supports urgent escalation.

# Why AI Fails in SOC Environments

AI is useful, but it fails in predictable ways. A cybersecurity graduate should be able to explain these failure modes.

## Failure 1: Missing or Poor-Quality Data

If endpoint logs are missing, the AI system may see a suspicious login but not the execution that follows.

```text
Identity logs: suspicious login observed
Endpoint logs: missing
Cloud logs: delayed
Result: incomplete investigation picture
```

## Failure 2: Lack of Context

AI may treat legitimate maintenance as malicious if it does not know the user’s role or the maintenance window.

```text
PowerShell at midnight by domain administrator: possibly normal
PowerShell at midnight by HR laptop: suspicious
```

## Failure 3: Concept Drift

Normal behaviour changes over time.

```text
During exam registration, university systems may receive unusual traffic.
A model trained during a quiet period may generate many false positives.
```

## Failure 4: Base-Rate Problem

Even a model with a low false positive rate can overwhelm analysts because real attacks are rare. This is why precision and operational workload matter.

## Failure 5: Adversarial Adaptation

Attackers can change behaviour to avoid detection.

```text
Instead of uploading 5 GB at once,
the attacker uploads 50 MB every hour for several days.
```

This low-and-slow behaviour may evade simple threshold rules.

## Failure 6: Explainability Gap

A poor alert says:

```text
Risk score: 94%
```

A better alert says:

```text
Risk score: 94%
Main reasons:
- Unknown OAuth consent grant
- Encoded PowerShell execution
- Rare file-share access
- Archive creation
- External upload
- Backup deletion attempt
```

SOC analysts need reasons, not only scores.

## Failure 7: Automation Risk

Automated containment can cause damage.

```text
The AI system disables a critical administrator account.
The alert was a false positive.
A production outage cannot be fixed quickly.
```

> **Teaching Point**
>
> In cybersecurity, false negatives may allow attacks, but false positives can also disrupt the organization. Good SOC design must balance both.

# Human-in-the-Loop SOC

AI should support human analysts, not replace them completely.

## What AI Can Do Well

AI can support:

- alert grouping and deduplication;

- anomaly detection;

- entity correlation;

- behavioural baselining;

- threat intelligence enrichment;

- incident summarization;

- evidence ranking;

- recommended next investigative steps.

## What Humans Still Do Better

Human analysts are needed for:

- understanding business impact;

- judging incomplete and conflicting evidence;

- communicating with users, managers, and legal teams;

- making high-impact containment decisions;

- understanding ethical and regulatory consequences;

- deciding whether response is proportionate.

## What Can Be Automated?

Low-risk and reversible actions are good candidates for automation:

```text
Collect related logs
Query threat intelligence
Group similar alerts
Enrich IP addresses and domains
Generate an incident summary
Create an investigation ticket
Trigger step-up authentication
```

## What Should Require Human Approval?

High-impact or irreversible actions should usually require approval:

```text
Disable administrator account
Isolate production server
Block business-critical traffic
Terminate cloud workloads
Delete files
Report breach externally
```

# In-Lecture Q&A Prompts

## Q1. Why is the most obvious alert not always the most dangerous alert?

**Expected answer:** Because a noisy alert may be blocked or contained, while a less obvious successful compromise may create greater risk.

## Q2. What is the difference between an alert and an incident?

**Expected answer:** An alert is usually a warning signal from one source. An incident is a correlated set of evidence that suggests a meaningful security problem requiring response.

## Q3. Why is an OAuth consent grant dangerous in the mini-case?

**Expected answer:** Because it may give an attacker persistent cloud access through tokens or application permissions, even if the user password is later changed.

## Q4. Why can a 95% accurate model still be operationally poor?

**Expected answer:** Because attacks are rare. A small false positive rate can still produce many false alerts and overwhelm analysts.

## Q5. Why should a SOC map evidence to attacker tactics?

**Expected answer:** It helps analysts understand attacker objectives, identify missing evidence, prioritize response, and communicate findings using a common language.

## Q6. What should be automated, and what should remain human-controlled?

**Expected answer:** Evidence collection, enrichment, alert grouping, and ticket creation can often be automated. High-impact containment actions should usually require human approval.

# Final Takeaway

AI in the SOC is not about replacing analysts. It is about improving the quality and speed of security decisions.

```text
AI in the SOC:
1. Sees telemetry, not intentions.
2. Converts raw events into features and relationships.
3. Correlates weak signals into threat hypotheses.
4. Prioritizes incidents under uncertainty.
5. Requires context, explainability, and human judgment.
6. Should support proportionate and accountable response.
```

> The best SOC is not the one with the most alerts. The best SOC is the one that turns telemetry into timely, explainable, and proportionate action.

# Suggested Reading

1.  NIST, *SP 800-61 Rev. 3: Incident Response Recommendations and Considerations for Cybersecurity Risk Management*.  
```text
<https://csrc.nist.gov/pubs/sp/800/61/r3/final>
```

2.  NIST, *Artificial Intelligence Risk Management Framework*.  
```text
<https://www.nist.gov/itl/ai-risk-management-framework>
```

3.  MITRE, *ATT&CK Enterprise Matrix*.  
```text
<https://attack.mitre.org/matrices/enterprise/>
```

4.  CISA, *Cybersecurity Incident and Vulnerability Response Playbooks*.  
```text
<https://www.cisa.gov/resources-tools/resources/federal-government-cybersecurity-incident-and-vulnerability-response-playbooks>
```

5.  Microsoft, *Microsoft Sentinel Documentation*.  
```text
<https://learn.microsoft.com/en-us/azure/sentinel/>
```

# Optional Instructor Notes for a 10–15 Minute Teaching Assessment

A possible timing is:

| **Section**                                              | **Time**  |
|:---------------------------------------------------------|:----------|
| Opening triage puzzle: two-slide hook                    | 2 minutes |
| Why AI is used in SOC and what AI sees                   | 2 minutes |
| Pipeline: telemetry to features to risk scoring          | 3 minutes |
| Mini-case: multi-stage ransomware and cloud exfiltration | 4 minutes |
| Interactive threat-hypothesis question                   | 2 minutes |
| Why AI fails and final takeaway                          | 2 minutes |

For a teaching assessment, do not try to present every table in detail. Use the tables as structured teaching material, but select the most important points verbally. The strongest delivery strategy is:

1.  Start with the short triage puzzle.

2.  Move quickly to the idea that SOC work is evidence construction.

3.  Use the ransomware mini-case as the main example.

4.  Ask students to justify a threat hypothesis.

5.  End with the human-in-the-loop principle.
