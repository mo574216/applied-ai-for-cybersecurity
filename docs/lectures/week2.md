---
title: "Week 2: Cybersecurity Data Engineering and Feature Design"
layout: default
permalink: /lectures/week2/
---

# Week 2: Cybersecurity Data Engineering and Feature Design  
## From Raw Security Evidence to AI-Ready Data

Welcome to Week 2 of **Applied AI for Cybersecurity**.

In Week 1, we introduced the basic idea of applying AI to cybersecurity. We discussed security data, features, labels, models, predictions, decisions, and evaluation.

This week focuses on the stage that often determines whether an AI cybersecurity system succeeds or fails:

> **Data engineering and feature design**

Before we train any model, we need to answer several practical questions:

- What data do we need?
- Where does the data come from?
- Is the data complete?
- Is the data reliable?
- How should we clean it?
- How should we transform it?
- What features should we extract?
- How should we label it?
- How should we split it for training and testing?
- What could go wrong before the model is even trained?

The central lesson this week is:

> Most AI failures in cybersecurity are not caused only by weak algorithms. They often start with poor data, weak labels, misleading features, or unrealistic evaluation design.

---

# 1. Learning Objectives

By the end of this week, you should be able to:

1. Explain why data engineering is critical for AI-based cybersecurity.
2. Identify common security data sources used in AI systems.
3. Distinguish between raw data, normalised data, features, labels, and datasets.
4. Explain the difference between packet-level, flow-level, log-level, artefact-level, and context-level data.
5. Describe common data quality problems in cybersecurity.
6. Explain why labels are difficult to obtain and maintain in security datasets.
7. Design useful features for common cybersecurity tasks.
8. Explain the risks of data leakage and unrealistic train/test splitting.
9. Discuss class imbalance and sampling in security datasets.
10. Prepare a simple AI-ready feature table from raw security observations.

---

# 2. Why Data Engineering Matters in Cybersecurity AI

A machine learning model can only learn from the data provided to it.

If the data is incomplete, biased, incorrectly labelled, or poorly structured, even a sophisticated model may produce unreliable results.

In cybersecurity, data is especially difficult because it is often:

- Noisy
- Incomplete
- High-volume
- Time-dependent
- Distributed across many systems
- Privacy-sensitive
- Labelled imperfectly
- Affected by attacker behaviour
- Different from one organisation to another

For example, an intrusion detection model may perform well on a clean public dataset, but fail in a real enterprise network because the real environment contains encrypted traffic, missing logs, different user behaviour, and new applications.

---

# 3. The Cybersecurity AI Data Pipeline

A simplified data pipeline for AI-based cybersecurity is:

```text
Raw security data
→ collection
→ parsing
→ normalisation
→ cleaning
→ enrichment
→ feature extraction
→ labelling
→ dataset construction
→ train/validation/test splitting
→ model training
→ evaluation
→ deployment monitoring
```

Each step matters.

If any step is weak, the final model may be misleading.

---

# 4. Security Data Sources

Security AI systems may use many types of data.

| Data Source | Example | Possible Use |
|---|---|---|
| Network packets | Packet headers, payloads, timestamps | Protocol analysis, intrusion detection |
| Network flows | Source IP, destination IP, ports, bytes, duration | IDS, DDoS detection, anomaly detection |
| Firewall logs | Allowed or blocked connections | Network policy monitoring |
| DNS logs | Queried domains, response IPs, query frequency | Botnet and C2 detection |
| Authentication logs | Login time, user, device, location, MFA result | Account compromise detection |
| Endpoint logs | Process creation, command line, parent process | Malware and suspicious behaviour detection |
| Email logs | Sender, subject, URL, attachment metadata | Phishing detection |
| Web server logs | URL path, status code, user agent, IP address | Web attack detection |
| Cloud logs | API calls, IAM changes, storage access | Cloud security monitoring |
| Vulnerability scan data | CVE, CVSS, asset exposure | Vulnerability prioritisation |
| Threat intelligence | Malicious IPs, domains, hashes, campaigns | Alert enrichment |
| Asset inventory | Host role, owner, criticality, business function | Context-aware risk scoring |

NIST SP 800-92 provides guidance on computer security log management and describes the importance of developing, implementing, and maintaining effective log management practices across an enterprise. Further reading: [NIST SP 800-92: Guide to Computer Security Log Management](https://csrc.nist.gov/pubs/sp/800/92/final).

MITRE ATT&CK also provides a useful view of defensive data sources. MITRE describes data sources as information that can be collected from sensors or logs, with data components representing specific properties relevant to detecting techniques. Further reading: [MITRE ATT&CK Data Sources](https://attack.mitre.org/datasources/).

---

# 5. Raw Data, Normalised Data, and Features

## 5.1 Raw Data

Raw data is the original data collected from systems.

Example firewall log:

```text
2026-02-10T10:03:12Z ALLOW TCP 192.168.1.20:51522 -> 10.0.0.5:443 bytes=1542
```

Raw logs are often inconsistent. Different tools use different names, formats, and timestamp conventions.

---

## 5.2 Normalised Data

Normalisation converts raw data into a consistent format.

Example normalised record:

| Field | Value |
|---|---|
| timestamp | 2026-02-10 10:03:12 |
| action | allow |
| protocol | TCP |
| source_ip | 192.168.1.20 |
| source_port | 51522 |
| destination_ip | 10.0.0.5 |
| destination_port | 443 |
| bytes | 1542 |

Normalisation allows records from different systems to be compared and combined.

---

## 5.3 Features

Features are measurable inputs used by a model.

From the normalised log above, possible features include:

| Feature | Meaning |
|---|---|
| destination_port | Target service |
| bytes | Traffic size |
| protocol | TCP, UDP, ICMP |
| is_external_destination | Whether destination is outside organisation |
| is_common_service_port | Whether the port is common |
| connection_count_5min | Number of connections in a 5-minute window |
| bytes_out_5min | Total outbound bytes in a 5-minute window |

Feature design is where security knowledge becomes model input.

---

# 6. Types of Cybersecurity Data

## 6.1 Packet-Level Data

Packet-level data contains detailed information about individual packets.

Examples:

- Source IP
- Destination IP
- Source port
- Destination port
- Protocol
- Flags
- Packet size
- Timestamp
- Payload

Advantages:

- Detailed
- Useful for protocol-level analysis
- Can support deep inspection

Limitations:

- Large volume
- Privacy-sensitive
- Expensive to store and process
- Encrypted payloads limit visibility

---

## 6.2 Flow-Level Data

Flow-level data summarises communication between two endpoints.

A flow is often defined by:

```text
source IP
destination IP
source port
destination port
protocol
time window
```

Example flow features:

- Flow duration
- Total packets
- Total bytes
- Average packet size
- Packets per second
- Bytes per second
- Forward packets
- Backward packets
- Inter-arrival time
- TCP flag counts

Flow-level data is widely used for intrusion and DDoS detection because it is more compact than packet captures.

---

## 6.3 Log-Level Data

Log-level data comes from applications, operating systems, identity providers, firewalls, cloud services, and security tools.

Example authentication log:

```text
timestamp=2026-02-10T09:12:44Z
user=alice
device=laptop-17
location=London
mfa_result=success
```

Possible features:

- Login time
- Country
- Device reputation
- MFA result
- Failed login count
- Previous login location
- Impossible travel indicator

---

## 6.4 Artefact-Level Data

Artefact-level data describes files, URLs, emails, or documents.

Examples:

| Artefact | Possible Features |
|---|---|
| Executable file | entropy, imports, file size, digital signature |
| URL | length, domain age, entropy, redirect count |
| Email | sender, subject, links, attachment type |
| Document | macros, embedded links, metadata |

---

## 6.5 Context-Level Data

Context-level data provides business or organisational meaning.

Examples:

- Asset criticality
- User role
- Department
- Business calendar
- Maintenance window
- Data sensitivity
- Known travel
- Approved vulnerability scanning
- Change ticket
- Threat intelligence match

Context often changes the interpretation of the same event.

Example:

```text
A server scan from an approved scanner may be benign.
The same scan from an unknown workstation may be suspicious.
```

---

# 7. Data Quality Problems in Cybersecurity

Cybersecurity data is rarely clean.

Common problems include:

| Problem | Example | Consequence |
|---|---|---|
| Missing fields | Location missing in login logs | Model cannot use geo-anomaly features |
| Duplicate logs | Same alert repeated many times | Model overweights repeated events |
| Inconsistent formats | Different timestamp formats | Incorrect event ordering |
| Clock drift | Endpoint time is wrong | False sequence reconstruction |
| Noisy labels | Alert marked benign without investigation | Wrong training signal |
| Incomplete visibility | Endpoint logs missing | Attack chain appears incomplete |
| Encrypted traffic | Payload not visible | Must rely on metadata |
| Log volume spikes | Too much data during incidents | Pipeline delay |
| Tool changes | New EDR format | Feature extraction breaks |
| Imbalanced classes | Few attacks, many benign events | Model biased toward benign class |

A data pipeline should include checks for completeness, consistency, and validity.

---

# 8. Data Cleaning

Data cleaning prepares raw data for analysis.

Common cleaning actions include:

- Removing duplicate records
- Standardising timestamps
- Handling missing values
- Converting categorical values
- Removing impossible values
- Filtering irrelevant records
- Correcting inconsistent field names
- Validating IP address and port formats
- Removing corrupted records
- Checking whether labels match expected values

## Example

Raw log entries:

```text
10/02/26 10:03:12 ALLOW TCP src=192.168.1.20 dst=10.0.0.5 port=443
2026-02-10T10:03:12Z allow tcp source=192.168.1.20 destination=10.0.0.5 dport=443
```

These logs contain similar information but use different formats.

A normalised schema should make them consistent.

---

# 9. Handling Missing Values

Missing data is common in cybersecurity.

Examples:

| Missing Field | Possible Cause |
|---|---|
| user_id | Network log has no authenticated user |
| geo_location | IP location service unavailable |
| file_hash | File not captured |
| process_parent | Endpoint tool did not record parent process |
| threat_intel_score | Indicator not found in feed |
| mfa_result | System does not use MFA |

Possible strategies:

| Strategy | When Useful |
|---|---|
| Remove record | If record is unusable and low value |
| Fill with “unknown” | For categorical fields |
| Use default value | If meaningful and documented |
| Impute value | For numerical fields, with caution |
| Add missingness indicator | When missing itself may be meaningful |
| Request better logging | If missing field is critical |

Example:

```text
mfa_result = unknown
mfa_result_missing = 1
```

Sometimes missingness is itself useful. For example, absence of expected endpoint telemetry may indicate a disabled agent.

---

# 10. Time Windows and Aggregation

Many cyber behaviours are meaningful only over time.

A single login failure may not be suspicious. Fifty failures in two minutes may be suspicious.

Time-window aggregation converts individual events into behavioural features.

Examples:

| Raw Events | Aggregated Feature |
|---|---|
| Multiple failed logins | failed_login_count_5min |
| Many DNS queries | dns_query_rate_10min |
| Repeated connections | connection_count_1min |
| Large upload | bytes_out_30min |
| Many destination ports | unique_dst_ports_5min |
| Multiple endpoints contacted | unique_dst_ips_10min |

## Example: Brute Force Detection

Raw events:

```text
10:00:01 failed login
10:00:08 failed login
10:00:14 failed login
10:00:21 failed login
```

Feature:

```text
failed_login_count_1min = 4
```

With more events:

```text
failed_login_count_1min = 40
```

The second case is more suspicious.

---

# 11. Feature Engineering

Feature engineering is the process of designing model inputs from raw data.

Good features should be:

- Relevant to the security problem
- Computable from available data
- Stable enough for deployment
- Harder for attackers to manipulate
- Interpretable where possible
- Tested for leakage
- Useful beyond one dataset

---

## 11.1 Network Security Features

| Feature | Use |
|---|---|
| request_rate | DDoS detection |
| packet_rate | Flood detection |
| bytes_out | Exfiltration detection |
| unique_dst_ports | Port scanning |
| syn_ack_ratio | SYN flood detection |
| flow_duration | Traffic behaviour |
| dns_query_rate | DNS anomaly detection |
| domain_entropy | DGA or suspicious domain detection |
| unique_src_ips | Distributed attack detection |
| endpoint_concentration | Application-layer DDoS |

---

## 11.2 Authentication Features

| Feature | Use |
|---|---|
| failed_login_count | Brute force detection |
| login_hour | Unusual time detection |
| login_country | Geo-anomaly detection |
| impossible_travel_flag | Account compromise detection |
| mfa_failure_count | MFA abuse detection |
| new_device_flag | Account risk scoring |
| privilege_level | Risk prioritisation |
| previous_successful_login_country | Contextual comparison |

---

## 11.3 Endpoint Features

| Feature | Use |
|---|---|
| process_name | Process classification |
| parent_process | Suspicious process chain |
| command_line_length | Obfuscation indicator |
| encoded_command_flag | Suspicious scripting |
| file_hash | Known malware matching |
| unsigned_binary_flag | Static risk indicator |
| network_connection_count | Runtime behaviour |
| persistence_indicator | Malware behaviour |
| suspicious_import_count | Static malware analysis |

---

## 11.4 Email and URL Features

| Feature | Use |
|---|---|
| sender_domain_reputation | Phishing detection |
| spf_dkim_dmarc_result | Email authentication |
| urgency_keyword_flag | Phishing signal |
| attachment_type | Malware delivery risk |
| url_length | Malicious URL detection |
| domain_age | Newly registered domain detection |
| redirect_count | URL obfuscation |
| brand_impersonation_score | Phishing detection |
| url_entropy | Random-looking URL detection |

---

## 11.5 Cloud Security Features

| Feature | Use |
|---|---|
| api_call_type | Cloud activity classification |
| unusual_region_flag | Cloud account compromise |
| storage_download_volume | Exfiltration detection |
| iam_policy_change_flag | Privilege misuse |
| new_access_key_created | Persistence or misuse |
| public_bucket_flag | Misconfiguration detection |
| unusual_admin_action | Cloud security risk |
| service_account_used | Automation or abuse context |

---

# 12. Labels and Ground Truth

A label is the expected output used for training or evaluation.

Examples:

```text
benign
malware
phishing
DDoS
port scan
suspicious
true positive
false positive
```

Labels are difficult in cybersecurity.

## 12.1 Why Labels Are Hard

| Problem | Explanation |
|---|---|
| Attack labels may be unknown | Some attacks are never detected |
| Labels may be delayed | An incident may be confirmed weeks later |
| Analyst labels may be inconsistent | Different analysts may disagree |
| “Benign” may mean “not yet known malicious” | Absence of evidence is not proof |
| Multi-stage attacks complicate labels | Early events may look benign |
| Labels may change over time | A domain may become malicious later |
| Context affects labels | Same behaviour may be benign in one environment |

## 12.2 Weak Labels

A weak label is an imperfect label.

Examples:

- An antivirus detection label
- A threat-intelligence feed match
- An analyst closure reason
- A sandbox score
- A user report
- A public blacklist result

Weak labels are useful but should be treated carefully.

---

# 13. Class Imbalance

Cybersecurity datasets are often imbalanced.

Example:

```text
1,000,000 network flows
995,000 benign
5,000 attack
```

A model can appear accurate by predicting most events as benign.

## 13.1 Why Imbalance Matters

Class imbalance can cause:

- Low recall for attacks
- Misleading accuracy
- Poor minority-class performance
- Unstable evaluation
- Overconfidence in benign predictions

## 13.2 Common Strategies

| Strategy | Description |
|---|---|
| Use precision, recall, F1 | Better than accuracy alone |
| Stratified splitting | Preserve class proportions |
| Resampling | Over-sample minority or under-sample majority |
| Class weighting | Penalise minority-class errors more |
| Threshold adjustment | Tune decision threshold |
| Anomaly detection | Useful when attacks are rare |
| Cost-sensitive learning | Consider operational cost of errors |

No method is perfect. The choice depends on the security task and operational cost.

---

# 14. Train, Validation, and Test Splitting

A dataset is usually divided into:

| Split | Purpose |
|---|---|
| Training set | Used to train the model |
| Validation set | Used to tune model settings and thresholds |
| Test set | Used for final evaluation |

Scikit-learn’s `train_test_split` is a common utility for splitting arrays or matrices into random train and test subsets. Further reading: [scikit-learn train_test_split documentation](https://scikit-learn.org/stable/modules/generated/sklearn.model_selection.train_test_split.html).

However, random splitting is not always appropriate for cybersecurity.

---

# 15. Why Random Splitting Can Be Misleading

In security datasets, events are often time-dependent.

Example:

```text
Day 1: normal traffic
Day 2: attack starts
Day 3: attack continues
```

If we randomly split rows, very similar attack samples may appear in both training and test sets. The model may appear to perform well because it has already seen almost identical examples.

This is a form of unrealistic evaluation.

## Better Splitting Strategies

| Strategy | When Useful |
|---|---|
| Time-based split | Train on earlier data, test on later data |
| Host-based split | Test on hosts not seen during training |
| Campaign-based split | Test on unseen attack campaigns |
| Family-based split | For malware families |
| Organisation-based split | Test on different environments |
| Stratified split | Preserve class proportions |

A realistic test set should represent the situation the model will face after deployment.

---

# 16. Data Leakage

Data leakage occurs when information unavailable at prediction time is accidentally included in training or evaluation.

Leakage makes model performance look better than it really is.

## Examples of Data Leakage

| Leakage Type | Example |
|---|---|
| Future information | Using labels or events from after the prediction time |
| Duplicate samples | Same or near-identical records in train and test |
| Dataset artefact | Attack class encoded in file name |
| Post-incident field | Using analyst decision as input feature |
| Threat feed timestamp issue | Using future threat-intel labels |
| Session leakage | Same user session split across train and test |
| Campaign leakage | Same attack campaign appears in both train and test |

## Example

A dataset includes a field:

```text
incident_status = confirmed_malware
```

If this field is used as a feature, the model will perform extremely well. But in real deployment, this field is not available before detection.

That is data leakage.

---

# 17. Dataset Documentation

Every AI cybersecurity dataset should be documented.

A useful dataset description should include:

- Data source
- Collection period
- Environment
- Logging tools
- Features
- Labels
- Label method
- Class distribution
- Missing fields
- Known limitations
- Privacy handling
- Splitting strategy
- Intended use
- Not intended use

This helps future users understand whether the dataset is suitable for their task.

---

# 18. Case Study 1: From Login Logs to Account Risk Features

## Raw Events

```text
09:00 user=alice device=laptop-1 country=UK mfa=success
09:10 user=alice device=laptop-1 country=UK mfa=success
03:15 user=alice device=unknown country=RU mfa=failed
03:16 user=alice device=unknown country=RU mfa=failed
03:18 user=alice device=unknown country=RU mfa=success
```

## Possible Features

| Feature | Value |
|---|---|
| login_hour | 03 |
| new_device_flag | 1 |
| unusual_country_flag | 1 |
| mfa_failure_count_5min | 2 |
| mfa_success_after_failures | 1 |
| previous_country | UK |
| impossible_travel_flag | depends on timing and distance |
| account_privilege_level | required context |

## Possible Label

```text
suspicious
```

## Additional Context Needed

- Is Alice travelling?
- Is the device registered?
- Is there a VPN?
- Is the IP associated with known abuse?
- Did Alice access sensitive resources after login?

## Lesson

Feature design requires both data and security reasoning.

---

# 19. Case Study 2: From Web Logs to DDoS Features

## Raw Events

```text
10:00 registration opens
10:03 request rate increases from 300/min to 4,800/min
10:05 API latency increases from 200 ms to 3.5 s
10:06 payment gateway timeouts begin
10:07 many requests hit /check-seat-availability
```

## Possible Features

| Feature | Meaning |
|---|---|
| request_rate_1min | Current traffic intensity |
| request_rate_ratio_baseline | Increase compared with normal |
| endpoint_concentration | Whether traffic targets one endpoint |
| expensive_endpoint_flag | Whether endpoint is resource-heavy |
| error_rate | Application failure indicator |
| latency_p95 | Service degradation |
| known_business_event_flag | Registration opened |
| session_completion_rate | Whether users complete normal flow |

## Possible Interpretation

This may be:

```text
legitimate flash crowd
application-layer DDoS
API abuse
mixed availability incident
```

## Lesson

The same traffic feature can mean different things depending on business context.

---

# 20. Case Study 3: Dataset Leakage in Malware Detection

## Scenario

A malware dataset contains the following fields:

```text
file_hash
file_size
entropy
imported_apis
source_folder
label
```

The `source_folder` values are:

```text
/malware_samples/
/benign_samples/
```

If the model uses `source_folder` as a feature, it may learn:

```text
source_folder contains "malware" → malicious
source_folder contains "benign" → benign
```

The model may show excellent accuracy but fail on real files.

## Lesson

Not every available field should be used as a feature.

---

# 21. Week 2 Summary

This week focused on cybersecurity data engineering and feature design.

Key points:

```text
AI cybersecurity systems depend heavily on data quality.

Raw logs must be parsed, normalised, cleaned, enriched, and transformed.

Features should represent meaningful security behaviour.

Labels in cybersecurity are often delayed, noisy, incomplete, or uncertain.

Class imbalance is common and can make accuracy misleading.

Random train/test splitting can produce unrealistic evaluation.

Data leakage can make models look far better than they really are.

Context is often essential for interpreting security data.

A strong AI system starts with a strong data pipeline.
```

Final takeaway:

> In cybersecurity AI, the dataset is not just an input to the model.  
> It is part of the security system.

---

# 22. Lab Sheet 2: Building AI-Ready Cybersecurity Data

## Lab Overview

In this lab, you will convert simplified raw security observations into an AI-ready feature table. You will identify data sources, normalise fields, propose features, discuss labels, detect possible data leakage, and design an evaluation split.

This lab is conceptual and analytical. No live attack data or real user data is required.

---

## Lab Duration

Approximate duration: 90 minutes.

---

## Lab Mode

Individual work followed by small-group discussion.

---

## Lab Objectives

By completing this lab, you should be able to:

1. Identify security data sources.
2. Convert raw observations into normalised fields.
3. Propose useful features for AI-based security detection.
4. Discuss missing values and context requirements.
5. Assign tentative labels and label confidence.
6. Identify class imbalance and data leakage risks.
7. Choose a suitable train/test splitting strategy.
8. Produce a simple dataset documentation note.

---

# 23. Lab Dataset A: Raw Security Observations

Use the following simplified observations.

| ID | Raw Observation |
|---|---|
| R1 | `2026-02-10 09:01 user=bob login success country=UK device=laptop-7 mfa=success` |
| R2 | `2026-02-10 02:14 user=bob login failed country=BR device=unknown mfa=failed` |
| R3 | `2026-02-10 02:15 user=bob login failed country=BR device=unknown mfa=failed` |
| R4 | `2026-02-10 02:17 user=bob login success country=BR device=unknown mfa=success` |
| R5 | `2026-02-10 02:25 user=bob downloaded 1.5GB from finance folder` |
| R6 | `2026-02-10 10:00 course registration opens` |
| R7 | `2026-02-10 10:04 web requests increase from 300/min to 6000/min` |
| R8 | `2026-02-10 10:05 API latency increases to 4.1 seconds` |
| R9 | `2026-02-10 10:06 repeated calls to /check-seat-availability` |
| R10 | `2026-02-10 10:08 payment gateway timeout errors begin` |
| R11 | `2026-02-10 11:12 winword.exe launches powershell.exe with encoded command` |
| R12 | `2026-02-10 11:14 powershell.exe downloads update.exe from unknown domain` |
| R13 | `2026-02-10 11:16 update.exe creates scheduled task` |
| R14 | `2026-02-10 11:18 host queries rare domain every 60 seconds` |
| R15 | `2026-02-10 12:00 approved vulnerability scanner scans internal subnet` |

---

# 24. Lab Task 1 — Identify Data Source and Security Domain

Complete the table.

| ID | Data Source | Security Domain | Reason |
|---|---|---|---|
| R1 |  |  |  |
| R2 |  |  |  |
| R3 |  |  |  |
| R4 |  |  |  |
| R5 |  |  |  |
| R6 |  |  |  |
| R7 |  |  |  |
| R8 |  |  |  |
| R9 |  |  |  |
| R10 |  |  |  |
| R11 |  |  |  |
| R12 |  |  |  |
| R13 |  |  |  |
| R14 |  |  |  |
| R15 |  |  |  |

Possible data sources include:

```text
authentication log
cloud storage log
business calendar
web server log
application monitoring
payment gateway log
endpoint log
DNS log
vulnerability scanner log
asset inventory
```

Possible security domains include:

```text
account compromise
cloud data access
DDoS / availability
endpoint malware behaviour
DNS / command-and-control
vulnerability scanning
benign context
```

---

# 25. Lab Task 2 — Normalise Selected Events

Choose six events and convert them into structured fields.

Example fields:

```text
timestamp
user
host
source_country
device
event_type
resource
process_name
parent_process
domain
bytes
endpoint
status
```

Complete the table.

| ID | timestamp | entity | event_type | key_field_1 | key_field_2 | key_field_3 |
|---|---|---|---|---|---|---|
|  |  |  |  |  |  |  |
|  |  |  |  |  |  |  |
|  |  |  |  |  |  |  |
|  |  |  |  |  |  |  |
|  |  |  |  |  |  |  |
|  |  |  |  |  |  |  |

---

# 26. Lab Task 3 — Design Features

Design features for three detection tasks:

1. Account compromise detection
2. DDoS or API abuse detection
3. Endpoint malware behaviour detection

Complete the tables.

## Account Compromise Features

| Feature | Description | Required Data |
|---|---|---|
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |

## DDoS / API Abuse Features

| Feature | Description | Required Data |
|---|---|---|
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |

## Endpoint Malware Behaviour Features

| Feature | Description | Required Data |
|---|---|---|
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |

---

# 27. Lab Task 4 — Handle Missing Values

For each missing-value problem, propose a strategy.

| Missing Field | Possible Impact | Handling Strategy |
|---|---|---|
| user_id missing in network log |  |  |
| country missing in login log |  |  |
| parent_process missing in endpoint log |  |  |
| threat intelligence score missing |  |  |
| business calendar context missing |  |  |
| file hash missing |  |  |

Possible strategies:

```text
remove record
fill with unknown
add missingness indicator
request additional log source
use alternative feature
delay decision until context is available
```

---

# 28. Lab Task 5 — Assign Tentative Labels and Confidence

Assign tentative labels to selected event groups.

Suggested event groups:

| Group | Related IDs |
|---|---|
| G1 | R1–R5 |
| G2 | R6–R10 |
| G3 | R11–R14 |
| G4 | R15 |

Complete the table.

| Group | Tentative Label | Confidence | Evidence | Additional Context Needed |
|---|---|---:|---|---|
| G1 |  |  |  |  |
| G2 |  |  |  |  |
| G3 |  |  |  |  |
| G4 |  |  |  |  |

Possible labels:

```text
benign
suspicious
malicious
uncertain
mixed incident
```

---

# 29. Lab Task 6 — Identify Data Leakage Risks

Review the following potential features.

| Candidate Feature | Use or Exclude? | Leakage Risk? | Reason |
|---|---|---|---|
| incident_status_after_investigation |  |  |  |
| analyst_final_decision |  |  |  |
| source_folder_name |  |  |  |
| detection_rule_name |  |  |  |
| login_country |  |  |  |
| failed_login_count_5min |  |  |  |
| file_path_contains_malware |  |  |  |
| endpoint_process_name |  |  |  |
| threat_intel_label_added_next_week |  |  |  |
| bytes_downloaded_10min |  |  |  |

Answer:

1. Which features should be excluded?
2. Which features are safe?
3. Which features require careful timestamp handling?
4. Why is data leakage dangerous?

---

# 30. Lab Task 7 — Choose a Train/Test Split Strategy

For each scenario, choose a suitable split strategy.

| Scenario | Suitable Split Strategy | Reason |
|---|---|---|
| Phishing emails collected over 12 months |  |  |
| Malware samples from different families |  |  |
| Network logs from one week of attacks |  |  |
| User login behaviour across departments |  |  |
| DDoS traffic from several campaigns |  |  |
| Cloud logs from multiple organisations |  |  |

Possible strategies:

```text
random split
stratified split
time-based split
host-based split
family-based split
campaign-based split
organisation-based split
```

---

# 31. Lab Task 8 — Write a Dataset Documentation Note

Write a short dataset documentation note for the lab dataset.

Your note should include:

1. What data sources are included?
2. What security tasks could this dataset support?
3. What labels are available or missing?
4. What important context is missing?
5. What privacy concerns might exist?
6. What leakage risks should be avoided?
7. What split strategy would you recommend?
8. What is the dataset not suitable for?

---

# 32. Lab Deliverable

Submit a short worksheet containing:

1. Data source and security domain table.
2. Normalised event table.
3. Feature design tables.
4. Missing-value handling table.
5. Tentative labels and confidence table.
6. Data leakage analysis.
7. Train/test split strategy.
8. Dataset documentation note.

Recommended length:

```text
1000–1500 words
```

---

# 33. Exercises

## Exercise 1 — Concept Check

Answer briefly.

1. What is the difference between raw data and a feature?
2. What is normalisation?
3. Why are timestamps important in cybersecurity data?
4. What is a weak label?
5. Why are labels difficult in cybersecurity?
6. What is class imbalance?
7. Why can random train/test splitting be misleading?
8. What is data leakage?
9. Why is context-level data important?
10. Why should every dataset be documented?

---

## Exercise 2 — Short Analytical Answer

Write 250–300 words.

**Question:**  
Why is cybersecurity data engineering often more difficult than data engineering for ordinary business prediction tasks?

Your answer should discuss at least four of the following:

- Noisy logs
- Missing fields
- Time dependency
- Adversarial behaviour
- Poor labels
- Class imbalance
- Privacy
- Context dependence
- Dataset leakage
- Concept drift

---

## Exercise 3 — Feature Design

For each task, propose five useful features.

| Task | Feature 1 | Feature 2 | Feature 3 | Feature 4 | Feature 5 |
|---|---|---|---|---|---|
| Account compromise detection |  |  |  |  |  |
| DDoS detection |  |  |  |  |  |
| Malware behaviour detection |  |  |  |  |  |
| Phishing detection |  |  |  |  |  |
| Cloud misuse detection |  |  |  |  |  |

---

## Exercise 4 — Leakage Analysis

A dataset for malware detection includes these fields:

```text
file_hash
file_size
entropy
imported_apis
file_collection_source
analyst_final_label
date_label_confirmed
label
```

Answer:

1. Which fields are safe as features?
2. Which fields may cause leakage?
3. Which fields are labels rather than features?
4. Which fields require timestamp checks?
5. What would happen if leakage features were used during training?

---

## Exercise 5 — Split Strategy Reflection

A network intrusion dataset contains five days of traffic:

```text
Day 1: mostly benign traffic
Day 2: port scanning
Day 3: brute-force attacks
Day 4: DDoS attack
Day 5: mixed traffic
```

Answer:

1. Why might random splitting be misleading?
2. What split would you use?
3. What would the test set represent?
4. What limitations would remain?
5. How would you improve the dataset?

---

## Exercise 6 — Dataset Documentation

Choose a cybersecurity dataset from a public source or from a hypothetical scenario.

Write a short dataset card including:

- Purpose
- Data sources
- Features
- Labels
- Collection period
- Known limitations
- Privacy concerns
- Recommended split strategy
- Intended use
- Not intended use

---

# 34. Further Reading

## Core Reading

1. **NIST SP 800-92: Guide to Computer Security Log Management**  
   Useful for understanding why log management matters and how organisations should collect, manage, and use security logs.  
   <https://csrc.nist.gov/pubs/sp/800/92/final>

2. **MITRE ATT&CK Data Sources**  
   Useful for understanding security data sources and data components that can support detection of adversary techniques.  
   <https://attack.mitre.org/datasources/>

3. **MITRE ATT&CK Enterprise Matrix**  
   Useful for connecting data sources and detection logic to adversary techniques.  
   <https://attack.mitre.org/matrices/enterprise/>

4. **scikit-learn: train_test_split Documentation**  
   Useful for understanding basic train/test splitting, while remembering that random splitting may not always be suitable for cybersecurity datasets.  
   <https://scikit-learn.org/stable/modules/generated/sklearn.model_selection.train_test_split.html>

5. **NIST AI Risk Management Framework**  
   Useful for understanding AI risk across the AI lifecycle, including mapping, measuring, managing, and governing AI systems.  
   <https://www.nist.gov/itl/ai-risk-management-framework>

---

## Suggested Search Topics

Search for recent academic or technical material on:

- Cybersecurity data engineering
- Feature engineering for intrusion detection
- Log normalisation for SIEM
- Data leakage in machine learning
- Dataset bias in cybersecurity
- Class imbalance in intrusion detection
- Weak labels in security datasets
- Time-based splitting for security data
- Concept drift in cybersecurity datasets
- Dataset cards for machine learning
- Privacy-preserving security analytics
- Security telemetry pipelines

---

# 35. Week 2 Summary

This week focused on the data layer of Applied AI for Cybersecurity.

The most important lessons are:

```text
Security AI begins before model training.

Raw security data must be collected, parsed, normalised, cleaned, enriched, and transformed.

Good features represent meaningful security behaviour.

Labels in cybersecurity are often incomplete, delayed, noisy, or uncertain.

Class imbalance makes accuracy misleading.

Random splitting may produce unrealistic evaluation.

Data leakage can make a weak model look excellent.

Context-level data is essential for interpreting many security events.

Every dataset should be documented with its sources, labels, limitations, risks, and intended use.
```

Final takeaway:

> A cybersecurity AI model is only as reliable as the data pipeline that feeds it.
