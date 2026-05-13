---
title: "Week 04: AI for Malware, Phishing, and Malicious URL Detection"
layout: default
permalink: /lectures/week04/
---

# Week 04: AI for Malware, Phishing, and Malicious URL Detection  
## From Digital Artefacts to Threat Classification

Welcome to Week 4 of **Applied AI for Cybersecurity**.

In Week 1, we studied the foundations of applying AI to cybersecurity problems. In Week 2, we focused on network intrusion and DDoS detection. This week moves from network traffic to another major area of cyber defence:

> **Detecting malicious artefacts such as phishing emails, malicious URLs, and malware samples.**

The main question for this week is:

> How can AI help us classify suspicious files, emails, URLs, and behaviours, and what are the limitations of this approach?

---

# 1. Learning Objectives

By the end of this week, you should be able to:

1. Explain how AI is used for malware, phishing, and malicious URL detection.
2. Distinguish between static, dynamic, and behavioural malware analysis.
3. Identify useful features for malware detection.
4. Identify useful features for phishing email detection.
5. Identify useful features for malicious URL detection.
6. Explain how classification models can be used for artefact-based threat detection.
7. Explain why feature engineering is important in malware and phishing detection.
8. Discuss why attackers can evade AI-based detection.
9. Evaluate malware and phishing detectors using suitable metrics.
10. Explain the limitations of public malware and phishing datasets.

---

# 2. Why This Topic Matters

Many cyberattacks begin with a malicious artefact.

Examples include:

- A phishing email that steals credentials
- A malicious URL that leads to a fake login page
- A file attachment that installs malware
- A macro-enabled document that downloads a payload
- A trojanised software installer
- A script that runs encoded commands
- A malware sample that communicates with command-and-control infrastructure

AI is useful because defenders must analyse large numbers of emails, URLs, files, and behaviours. Manual inspection does not scale.

However, AI-based detection is difficult because attackers actively change their artefacts to bypass detection.

---

# 3. Malware, Phishing, and Malicious URLs

## 3.1 Malware

Malware is software designed to perform unauthorised or harmful actions.

Common malware types include:

| Malware Type | Description |
|---|---|
| Virus | Attaches to other files and spreads when executed |
| Worm | Self-propagates across systems or networks |
| Trojan | Pretends to be legitimate software |
| Ransomware | Encrypts or blocks access to data and demands payment |
| Spyware | Steals information from a system |
| Keylogger | Records keystrokes |
| Bot | Turns a host into part of a botnet |
| Rootkit | Hides malicious activity and maintains privileged access |
| Downloader | Downloads additional malicious payloads |
| Backdoor | Provides hidden access to the attacker |

Malware detection may use file properties, code structure, imported libraries, strings, system calls, network behaviour, and runtime actions.

---

## 3.2 Phishing

Phishing is a social engineering attack where the attacker sends a deceptive message to trick the victim into revealing information, clicking a link, opening an attachment, or performing an unsafe action.

MITRE ATT&CK describes phishing as electronically delivered social engineering, including mass phishing and targeted spearphishing. Phishing messages may be used to gain access to victim systems or deliver malware. Further reading: [MITRE ATT&CK: Phishing T1566](https://attack.mitre.org/techniques/T1566/).  

Phishing may occur through:

- Email
- SMS
- Social media
- Messaging platforms
- Collaboration tools
- Fake login pages
- Malicious attachments
- QR codes
- Cloud sharing links

---

## 3.3 Malicious URLs

A malicious URL is a web address used for harmful purposes.

Examples include URLs that lead to:

- Phishing pages
- Malware downloads
- Fake login pages
- Drive-by downloads
- Scam pages
- Command-and-control infrastructure
- Credential harvesting sites

Malicious URL detection can be based on:

- URL structure
- Domain reputation
- Domain age
- Redirect behaviour
- Hosting information
- Lexical patterns
- Page content
- Threat intelligence

URLhaus is an example of a threat-intelligence platform that shares malicious URLs used for malware distribution. Further reading: [URLhaus by abuse.ch](https://urlhaus.abuse.ch/).  

---

# 4. Static, Dynamic, and Behavioural Analysis

Malware and artefact detection can be approached in different ways.

## 4.1 Static Analysis

Static analysis examines an artefact without executing it.

For malware detection, this may include:

- File hash
- File size
- File type
- PE header fields
- Imported libraries
- Strings
- Byte sequences
- Opcodes
- Entropy
- Sections
- Digital signature information
- Packer indicators

Example:

```text
File: invoice_update.exe
Imported APIs: CreateRemoteThread, VirtualAlloc, WriteProcessMemory
Strings: http://unknown-domain.example/payload
Entropy: high
Digital signature: missing
```

Possible interpretation:

```text
The file may be suspicious because it imports APIs often associated with process injection, contains an unknown download URL, has high entropy, and is unsigned.
```

### Advantages of static analysis

- Fast
- Scalable
- Safe because the file is not executed
- Suitable for large-scale screening

### Limitations of static analysis

- Obfuscation can hide useful features
- Packers can change file structure
- Static features may not reveal runtime behaviour
- Benign software may share some suspicious features

---

## 4.2 Dynamic Analysis

Dynamic analysis observes an artefact while it runs in a controlled environment, such as a sandbox.

Dynamic analysis may record:

- Files created or modified
- Registry changes
- Processes launched
- Network connections
- DNS queries
- System calls
- Persistence mechanisms
- Command execution
- Attempts to disable security tools

Example:

```text
The file creates a scheduled task,
writes to a startup directory,
connects to an unknown IP address,
and downloads a second executable.
```

### Advantages of dynamic analysis

- Reveals actual behaviour
- Useful against some obfuscation
- Helps analysts understand attack chain

### Limitations of dynamic analysis

- More expensive than static analysis
- Malware may detect sandbox environments
- Behaviour may depend on time, user action, or network conditions
- Short analysis windows may miss delayed behaviour

---

## 4.3 Behavioural Analysis

Behavioural analysis focuses on what the artefact or user does, rather than only what the artefact looks like.

Examples:

- Word document launches PowerShell
- PowerShell downloads an executable
- Executable injects into another process
- Host queries rare domains periodically
- Browser visits credential-harvesting page
- User submits credentials to a suspicious domain

Behavioural analysis is important because attackers can change surface features, but harmful behaviour may still follow recognisable patterns.

---

# 5. AI Problem Framing

## 5.1 Malware Detection as Classification

Malware detection is often framed as binary classification:

```text
Input: file features
Output: benign or malware
```

It can also be framed as multi-class classification:

```text
Input: file features
Output: ransomware, trojan, worm, spyware, benign, etc.
```

Binary classification is simpler. Multi-class classification is more informative but harder.

---

## 5.2 Phishing Detection as Classification

Phishing detection is commonly framed as classification:

```text
Input: email, URL, sender, and content features
Output: phishing or legitimate
```

The model may analyse:

- Sender
- Subject line
- Body text
- Embedded links
- Attachment metadata
- Domain reputation
- Urgency language
- Login-page indicators

---

## 5.3 Malicious URL Detection

Malicious URL detection may use:

```text
Input: URL lexical features + domain features + reputation features
Output: benign, phishing, malware, suspicious, or unknown
```

The difficulty is that attackers can generate new domains quickly, use URL shorteners, compromise legitimate sites, or host phishing pages on trusted cloud platforms.

---

## 5.4 Risk Scoring

Some systems do not make a hard decision. Instead, they assign a risk score.

Example:

```text
URL risk score = 82/100
```

The risk score may consider:

- Domain age
- Domain reputation
- URL length
- Suspicious keywords
- Number of redirects
- Hosting provider
- Threat-intelligence matches
- Page similarity to known brands

A risk score should be explainable.

---

# 6. Feature Engineering for Malware Detection

## 6.1 Static Malware Features

| Feature | Why It Matters |
|---|---|
| File hash | Useful for known malware matching |
| File size | Extremely small or large files may be suspicious |
| File type | Executable, script, document, archive |
| PE header fields | Structure of Windows executable files |
| Imported APIs | May reveal suspicious capabilities |
| Strings | URLs, commands, registry paths, suspicious text |
| Entropy | High entropy may suggest packing or encryption |
| Section names | Unusual sections may indicate obfuscation |
| Digital signature | Unsigned or invalid signatures may be suspicious |
| Packer indicators | Packed malware may hide code |

---

## 6.2 Behavioural Malware Features

| Feature | Why It Matters |
|---|---|
| Process creation | Malware may launch suspicious child processes |
| File modification | Ransomware modifies many files |
| Registry changes | Persistence may involve registry keys |
| Network connections | Malware may contact C2 servers |
| DNS queries | Malware may use suspicious domains |
| Privilege escalation attempts | Malware may attempt higher privileges |
| Security tool tampering | Malware may disable protection tools |
| Persistence mechanisms | Malware may survive reboot |
| Injection behaviour | Malware may inject code into other processes |
| Encryption behaviour | Ransomware may encrypt many files |

---

## 6.3 Example: Static Feature Interpretation

Consider this file:

```text
Filename: invoice_viewer.exe
File type: Windows PE executable
Digital signature: missing
Entropy: high
Imported APIs:
- VirtualAlloc
- WriteProcessMemory
- CreateRemoteThread
Strings:
- http://45.77.x.x/update.bin
- powershell -enc
```

Possible interpretation:

```text
The file is suspicious because it is unsigned, has high entropy, imports APIs often associated with process injection, and contains a URL and encoded PowerShell command.
```

However, this is not proof of malware. Some legitimate tools may use similar APIs.

---

# 7. Feature Engineering for Phishing Detection

## 7.1 Email Header and Sender Features

| Feature | Why It Matters |
|---|---|
| Sender domain | May not match claimed organisation |
| Reply-to address | May differ from sender |
| SPF/DKIM/DMARC result | Indicates email authentication status |
| Display name mismatch | Sender name may impersonate trusted entity |
| Sending IP reputation | Suspicious infrastructure may be used |
| Time of sending | Some attacks occur outside normal patterns |

---

## 7.2 Email Content Features

| Feature | Why It Matters |
|---|---|
| Urgency language | Creates pressure |
| Credential request | Common phishing goal |
| Generic greeting | May indicate mass phishing |
| Grammar anomalies | May indicate suspicious origin |
| Brand impersonation | Attackers mimic trusted organisations |
| Attachment type | Macro documents or executables are risky |
| Link text mismatch | Displayed link differs from actual URL |
| Suspicious call to action | “Verify now”, “Reset immediately” |

---

## 7.3 URL Features in Phishing Emails

| Feature | Why It Matters |
|---|---|
| Domain age | New domains are often suspicious |
| URL length | Long URLs can hide intent |
| Number of subdomains | Used to impersonate brands |
| Use of IP address | Direct IP links can be suspicious |
| HTTPS presence | Useful but not sufficient |
| URL entropy | Random strings may indicate generated URLs |
| Redirect count | Multiple redirects can hide destination |
| Brand keywords | May indicate impersonation |

---

# 8. Feature Engineering for Malicious URL Detection

Malicious URL detection may use three major feature groups.

## 8.1 Lexical Features

Lexical features are extracted from the URL string itself.

Examples:

| Feature | Example |
|---|---|
| URL length | Very long URL |
| Number of dots | Many subdomains |
| Special characters | `@`, `%`, `-`, `_` |
| Suspicious keywords | login, verify, update, secure |
| Digit ratio | Many digits in domain or path |
| Entropy | Random-looking characters |
| Use of IP address | `http://192.0.2.10/login` |

---

## 8.2 Host-Based Features

Host-based features describe the domain or hosting environment.

Examples:

| Feature | Meaning |
|---|---|
| Domain age | Newly registered domain |
| Registrar | Suspicious or uncommon registrar |
| Hosting ASN | Hosting provider |
| WHOIS privacy | Ownership hidden |
| DNS records | A, MX, NS record patterns |
| Certificate age | Recently issued certificate |
| Reputation score | Known malicious or unknown |

---

## 8.3 Content-Based Features

Content-based features describe what the webpage contains.

Examples:

| Feature | Meaning |
|---|---|
| Login form | May collect credentials |
| Brand logo | May impersonate a known service |
| JavaScript behaviour | Obfuscated or suspicious scripts |
| External resources | Loads content from suspicious domains |
| Form action URL | Sends credentials to unknown server |
| Page similarity | Looks like a known brand page |

---

# 9. Case Study 1: Phishing Email

## Scenario

A student receives this email:

```text
Subject: URGENT: Verify your university account

Dear user,

Your university mailbox will be disabled today unless you verify your account.

Click here to confirm your password:
http://university-support-login.example-security-check.com

Regards,
IT Support Team
```

## Security Question

Is this legitimate or phishing?

## Possible Evidence

| Evidence | Interpretation |
|---|---|
| Urgency language | Suspicious |
| Generic greeting | Suspicious |
| Password verification request | Suspicious |
| Non-university domain | Suspicious |
| No attachment | Neutral |
| Claims to be IT Support | Possible impersonation |
| HTTP rather than HTTPS | Suspicious, but HTTPS alone would not prove safety |

## AI Framing

```text
Classification
Risk scoring
Human-in-the-loop review
```

## Main Lesson

Phishing detection often requires combining language, URL, sender, and context features.

---

# 10. Case Study 2: Malware-Like Endpoint Behaviour

## Scenario

An endpoint monitoring system records this sequence:

```text
winword.exe launches powershell.exe
powershell.exe runs an encoded command
powershell.exe connects to unknown-domain.example
powershell.exe downloads update.exe
update.exe writes to startup folder
```

## Security Question

Is this malware behaviour?

## Evidence

| Evidence | Interpretation |
|---|---|
| Word launches PowerShell | Suspicious |
| Encoded PowerShell command | Suspicious |
| Unknown domain | Suspicious |
| Executable download | Suspicious |
| Startup folder modification | Persistence attempt |

## AI Framing

```text
Behavioural malware classification
Anomaly detection
Risk scoring
```

## Main Lesson

A single event may not be enough, but a sequence of behaviours can strongly indicate malicious activity.

---

# 11. Case Study 3: Malicious URL or False Alarm?

## Scenario

A URL detector flags this link:

```text
https://secure-login-university.example-reset.com/account/verify
```

The model gives:

```text
Risk score: 84/100
```

## Risk-Increasing Evidence

| Evidence | Interpretation |
|---|---|
| Contains “secure”, “login”, “verify” | Common phishing terms |
| Contains “university” but not official domain | Possible impersonation |
| Recently registered domain | Suspicious |
| Login-related path | Credential-harvesting possibility |
| Similar to legitimate brand | Possible brand impersonation |

## Risk-Reducing Evidence

| Evidence | Interpretation |
|---|---|
| HTTPS is present | Slightly reduces risk, but does not prove safety |
| No known threat-intelligence match | Does not prove benign |
| No malware download observed | May still be phishing |

## Main Lesson

A malicious URL detector should explain why a URL is risky. A score alone is not enough.

---

# 12. Dataset Awareness

Datasets are important for learning and evaluation, but they have limitations.

## 12.1 EMBER Dataset

EMBER is a malware classification dataset based on features extracted from Windows Portable Executable files. The official repository describes EMBER as a collection of PE-file features designed as a benchmark dataset for researchers. Further reading: [EMBER dataset repository](https://github.com/elastic/ember).  

Use case:

```text
Static malware detection from PE features
```

Possible limitation:

```text
The dataset contains derived features, not raw malware binaries. It is useful for ML benchmarking, but it does not fully represent complete malware analysis.
```

---

## 12.2 PhishTank

PhishTank is a collaborative clearing house for phishing data and provides an API for developers and researchers. Further reading: [PhishTank](https://www.phishtank.net/) and [PhishTank Developer Information](https://www.phishtank.net/developer_info.php).  

Use case:

```text
Phishing URL detection and validation
```

Possible limitation:

```text
Phishing URLs change quickly. A dataset may become outdated, and confirmed phishing URLs may not represent all real-world phishing behaviour.
```

---

## 12.3 URLhaus

URLhaus is a platform from abuse.ch and Spamhaus for sharing malicious URLs used for malware distribution. Further reading: [URLhaus](https://urlhaus.abuse.ch/).  

Use case:

```text
Malware URL detection and threat intelligence enrichment
```

Possible limitation:

```text
URLhaus focuses on URLs associated with malware distribution. It may not cover all phishing, scam, or credential-harvesting URLs.
```

---

# 13. Dataset Limitations

Public datasets are useful, but they should be used carefully.

| Limitation | Explanation |
|---|---|
| Ageing | Malware and phishing tactics change quickly |
| Label noise | Labels may be incorrect, incomplete, or delayed |
| Sampling bias | Dataset may not represent real traffic or real users |
| Class imbalance | Malicious examples may be rarer than benign ones |
| Artefact leakage | Models may learn dataset-specific shortcuts |
| Lack of context | Datasets often remove organisational context |
| Adversarial change | Attackers adapt after detection methods become known |
| Legal and ethical restrictions | Malware samples cannot always be shared freely |
| Benign diversity | Benign software and legitimate emails are highly diverse |

Important point:

> A model that performs well on a public dataset may still fail in a real organisation.

---

# 14. Evaluation for Malware and Phishing Detection

Evaluation should consider operational impact.

## 14.1 Useful Metrics

| Metric | Meaning |
|---|---|
| Accuracy | Overall proportion of correct predictions |
| Precision | Of flagged items, how many are truly malicious? |
| Recall | Of all malicious items, how many were detected? |
| F1-score | Balance between precision and recall |
| False positive rate | Benign items wrongly flagged |
| False negative rate | Malicious items missed |
| Detection latency | Time needed to detect |
| Analyst review rate | How many items require human review |
| Explainability | Whether analysts understand the result |
| Evasion resistance | Whether attackers can easily bypass the model |

---

## 14.2 False Positives

A false positive occurs when a benign item is flagged as malicious.

Examples:

- Legitimate email is quarantined.
- Business file is blocked.
- Software installer is flagged as malware.
- Important URL is blocked.

Possible consequences:

- Lost productivity
- User frustration
- Analyst workload
- Business disruption
- Reduced trust in the security system

---

## 14.3 False Negatives

A false negative occurs when a malicious item is missed.

Examples:

- Phishing email reaches user inbox.
- Malware file is allowed to execute.
- Malicious URL is not blocked.
- Suspicious script is treated as benign.

Possible consequences:

- Credential theft
- Malware infection
- Data loss
- Ransomware
- Lateral movement
- Financial or reputational damage

---

# 15. Why AI-Based Malware and Phishing Detection Is Difficult

## 15.1 Attackers Adapt

Attackers can change:

- Email wording
- Sender domains
- URL structure
- Hosting providers
- File hashes
- Malware packing
- Command-and-control domains
- Attachment types
- Obfuscation methods

This means models must be updated and monitored.

---

## 15.2 Obfuscation

Obfuscation is the process of hiding the true purpose or structure of code or content.

Examples:

- Packed executables
- Encoded PowerShell
- Randomised variable names
- Encrypted strings
- URL encoding
- Redirect chains
- JavaScript obfuscation

Obfuscation can make static analysis harder.

---

## 15.3 Concept Drift

Concept drift occurs when the data distribution changes over time.

Examples:

- New phishing templates appear.
- New malware families emerge.
- Benign software updates change file features.
- Organisations adopt new cloud tools.
- Attackers change infrastructure.

A model trained on old examples may lose effectiveness.

---

## 15.4 Explainability

Security analysts need reasons.

Poor explanation:

```text
Malware probability: 92%
```

Better explanation:

```text
Risk increased because:
- File is unsigned.
- Entropy is high.
- Suspicious process injection APIs are imported.
- The file contains an unknown download URL.
- Behaviour includes persistence in startup folder.
```

Explainability helps analysts trust, validate, and challenge the model.

---

# 16. Week 3 Summary

This week focused on AI for malware, phishing, and malicious URL detection.

Key points:

```text
Malware, phishing, and malicious URLs are common entry points for cyberattacks.

Static analysis examines artefacts without executing them.

Dynamic analysis observes runtime behaviour.

Behavioural analysis focuses on what the artefact or user does.

Feature engineering is essential for AI-based artefact detection.

Phishing detection combines sender, content, URL, and context features.

Malicious URL detection uses lexical, host-based, reputation, and content features.

Accuracy alone is not enough.

Attackers adapt through obfuscation, domain changes, packing, and evasion.

A useful AI detector should be explainable and operationally meaningful.
```

Final takeaway:

> A strong AI-based malware or phishing detector is not simply the one with the highest benchmark score.  
> It is the one that helps defenders make reliable, explainable, and proportionate security decisions.

---

# 17. Lab Sheet 3: Malware, Phishing, and Malicious URL Detection

## Lab Overview

In this lab, you will analyse simplified examples of suspicious emails, URLs, files, and endpoint behaviours. You will identify features, choose suitable AI framings, discuss false positives and false negatives, and design an explainable detection approach.

This is a conceptual and analytical lab. No malware execution is required or allowed.

---

## Lab Safety Notice

Do not download, execute, or visit suspicious files or URLs during this lab.

All examples in this lab are simplified and should be treated as text-only learning artefacts.

---

## Lab Duration

Approximate duration: 90 minutes.

---

## Lab Mode

Individual work followed by small-group discussion.

---

## Lab Objectives

By completing this lab, you should be able to:

1. Identify phishing, malware, and malicious URL indicators.
2. Extract useful static, behavioural, and URL-based features.
3. Choose an appropriate AI problem framing.
4. Discuss uncertainty in classification.
5. Compare false positive and false negative costs.
6. Propose explainable AI outputs for analysts.
7. Critique public datasets for malware and phishing detection.

---

# 18. Lab Dataset A: Suspicious Artefacts

Use the following simplified observations.

| ID | Type | Observation |
|---|---|---|
| A1 | Email | Email says “Your account will be disabled today” and links to a non-university domain |
| A2 | URL | `http://login-security-update-example.net/verify/account` |
| A3 | File | Unsigned executable with high entropy and suspicious imports |
| A4 | Endpoint | `winword.exe` launches `powershell.exe` with encoded command |
| A5 | URL | Recently registered domain with random-looking path |
| A6 | Email | Message from known lecturer with normal university domain and no links |
| A7 | File | Signed software installer downloaded from official vendor website |
| A8 | Endpoint | Script creates scheduled task and connects to unknown IP |
| A9 | Email | Invoice attachment from unknown sender with macro-enabled document |
| A10 | URL | Shortened URL redirects through multiple domains before reaching login page |

---

# 19. Lab Task 1 — Identify the Detection Domain

For each artefact, identify the most relevant detection domain.

Possible domains:

- Phishing email detection
- Malicious URL detection
- Static malware detection
- Behavioural malware detection
- Endpoint anomaly detection
- Benign or low-risk artefact
- Uncertain

Complete the table:

| ID | Detection Domain | Reason |
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

---

# 20. Lab Task 2 — Extract Features

For each artefact, propose useful features.

Examples:

```text
domain_age
url_length
url_entropy
sender_reputation
urgency_keyword_flag
macro_enabled_attachment
file_entropy
digital_signature_status
suspicious_import_count
encoded_command_flag
redirect_count
```

Complete the table:

| ID | Feature 1 | Feature 2 | Feature 3 | Feature 4 |
|---|---|---|---|---|
| A1 |  |  |  |  |
| A2 |  |  |  |  |
| A3 |  |  |  |  |
| A4 |  |  |  |  |
| A5 |  |  |  |  |
| A6 |  |  |  |  |
| A7 |  |  |  |  |
| A8 |  |  |  |  |
| A9 |  |  |  |  |
| A10 |  |  |  |  |

---

# 21. Lab Task 3 — Assign a Tentative Label

Assign one of the following labels:

```text
Benign
Suspicious
Malicious
Uncertain
```

Complete the table:

| ID | Tentative Label | Reason | Additional Context Needed |
|---|---|---|---|
| A1 |  |  |  |
| A2 |  |  |  |
| A3 |  |  |  |
| A4 |  |  |  |
| A5 |  |  |  |
| A6 |  |  |  |
| A7 |  |  |  |
| A8 |  |  |  |
| A9 |  |  |  |
| A10 |  |  |  |

Remember:

> “Uncertain” is acceptable if you can explain what evidence is missing.

---

# 22. Lab Task 4 — Choose AI Problem Framing

For each detection problem, choose a suitable AI framing.

Possible framings:

```text
Binary classification
Multi-class classification
Anomaly detection
Risk scoring
Clustering
Human-in-the-loop review
Rule-assisted ML
```

Complete the table:

| Detection Problem | Suitable AI Framing | Reason |
|---|---|---|
| Phishing email detection |  |  |
| Malicious URL detection |  |  |
| Static malware detection |  |  |
| Behavioural malware detection |  |  |
| Endpoint anomaly detection |  |  |
| Malware family grouping |  |  |
| Attachment triage |  |  |
| High-risk email review |  |  |

---

# 23. Lab Task 5 — Design an Explainable Risk Score

Choose one of the following:

```text
Phishing email
Malicious URL
Malware file
Endpoint behaviour
```

Design a risk score using 6–8 indicators.

Complete the table:

| Indicator | Score Contribution | Why It Matters |
|---|---:|---|
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |

Define thresholds:

| Score Range | Decision |
|---|---|
| 0–30 |  |
| 31–60 |  |
| 61–80 |  |
| 81–100 |  |

Your score should be explainable. Avoid using a score without reasons.

---

# 24. Lab Task 6 — False Positive and False Negative Costs

Choose three artefacts from Lab Dataset A.

Complete the table:

| ID | False Positive Cost | False Negative Cost |
|---|---|---|
|  |  |  |
|  |  |  |
|  |  |  |

Consider:

- What happens if a benign item is wrongly blocked?
- What happens if a malicious item is wrongly allowed?
- Which error is more costly in this case?
- Should the decision be automated or reviewed by a human?

---

# 25. Lab Task 7 — Evaluation Metrics

A phishing detector is tested on 2,000 emails.

Dataset:

```text
300 phishing emails
1,700 benign emails
```

Model output:

```text
240 phishing emails correctly detected
60 phishing emails missed
170 benign emails wrongly flagged as phishing
1,530 benign emails correctly ignored
```

Complete the confusion matrix:

|  | Predicted Phishing | Predicted Benign |
|---|---:|---:|
| Actually Phishing |  |  |
| Actually Benign |  |  |

Then calculate:

```text
True positives =
False negatives =
False positives =
True negatives =
Precision =
Recall =
F1-score =
Accuracy =
False positive rate =
False negative rate =
```

Then answer:

1. Is the model more concerning because of false positives or false negatives?
2. What would happen if this model were deployed in a university email system?
3. Should the model automatically block emails, warn users, or send to human review?
4. What additional evaluation would you request?

---

# 26. Lab Task 8 — Dataset Critique

Choose one of the following resources:

- EMBER
- PhishTank
- URLhaus

Answer:

1. What type of data does the resource provide?
2. What security problem can it help study?
3. What are its strengths?
4. What are its limitations?
5. Why might a model trained using this data fail in a real organisation?

Use the official links in the Further Reading section.

---

# 27. Lab Deliverable

Submit a short worksheet containing:

1. Detection domain table.
2. Feature extraction table.
3. Tentative labels and uncertainty.
4. AI problem framing table.
5. Explainable risk score.
6. False positive and false negative cost discussion.
7. Evaluation metric calculations.
8. Dataset critique.

Recommended length:

```text
1000–1500 words
```

---

# 28. Exercises

## Exercise 1 — Concept Check

Answer briefly.

1. What is the difference between static and dynamic malware analysis?
2. What is behavioural malware analysis?
3. Why is phishing detection not only a text classification problem?
4. Give four useful features for malicious URL detection.
5. Why does HTTPS not prove that a website is safe?
6. What is file entropy, and why may high entropy be suspicious?
7. What is a false positive in malware detection?
8. What is a false negative in phishing detection?
9. Why can attackers evade hash-based detection?
10. Why is explainability important for malware and phishing detection?

---

## Exercise 2 — Short Analytical Answer

Write 250–300 words.

**Question:**  
Why is AI-based malware and phishing detection difficult in real-world environments?

Your answer should discuss at least four of the following:

- Obfuscation
- Packing
- URL changes
- Domain rotation
- Poor labels
- Concept drift
- False positives
- False negatives
- Human review
- Dataset limitations

---

## Exercise 3 — Feature Design

For each artefact type, propose four useful features.

| Artefact Type | Feature 1 | Feature 2 | Feature 3 | Feature 4 |
|---|---|---|---|---|
| Phishing email |  |  |  |  |
| Malicious URL |  |  |  |  |
| Windows executable |  |  |  |  |
| Macro-enabled document |  |  |  |  |
| Suspicious PowerShell command |  |  |  |  |

---

## Exercise 4 — Case Analysis

Read the case:

```text
An employee receives an email claiming to be from the finance department.
The email contains an invoice attachment.
The sender domain is similar to the company domain but not identical.
The attachment is a macro-enabled Word document.
The message says payment must be processed today.
```

Answer:

1. Which features are suspicious?
2. Which features would you extract for an AI model?
3. Would this be classification, anomaly detection, or risk scoring?
4. What additional context is needed?
5. What would be a proportionate response?
6. Should the system block the email automatically or send it for review?

---

## Exercise 5 — Evaluation Reflection

A malware detector has:

```text
Accuracy: 97%
Precision: 88%
Recall: 45%
```

Answer:

1. Why might this model be unacceptable?
2. What does low recall mean in this case?
3. What operational harm may result?
4. What could be adjusted to improve recall?
5. What trade-off might occur if recall improves?

---

## Exercise 6 — Explainability Practice

Rewrite the following poor alert into an analyst-friendly explanation.

Poor alert:

```text
Malware probability: 93%
Prediction: malicious
```

Your explanation should include:

- Risk-increasing evidence
- Risk-reducing evidence
- Missing evidence
- Suggested next step
- Whether automatic blocking is justified

---

# 29. Further Reading

## Core Reading

1. **MITRE ATT&CK: Phishing, T1566**  
   Useful for understanding phishing as an adversary technique.  
   <https://attack.mitre.org/techniques/T1566/>

2. **EMBER Dataset Repository**  
   Useful for static malware detection research using PE-file features.  
   <https://github.com/elastic/ember>

3. **PhishTank**  
   Useful for studying phishing URLs and phishing intelligence.  
   <https://www.phishtank.net/>

4. **PhishTank Developer Information**  
   Useful for understanding access to PhishTank data and API expectations.  
   <https://www.phishtank.net/developer_info.php>

5. **URLhaus by abuse.ch**  
   Useful for malicious URL intelligence related to malware distribution.  
   <https://urlhaus.abuse.ch/>

6. **abuse.ch Threat Intelligence Projects**  
   Useful for exploring URLhaus, ThreatFox, MalwareBazaar, and YARAify.  
   <https://abuse.ch/>

---

## Suggested Search Topics

Search for recent academic or technical material on:

- Machine learning for malware detection
- Static malware analysis
- Dynamic malware analysis
- Behavioural malware detection
- Phishing detection using NLP
- Malicious URL detection
- URL lexical features
- Explainable AI for malware detection
- Adversarial malware examples
- Malware packing and obfuscation
- Concept drift in phishing detection
- Human-in-the-loop phishing triage
- Dataset bias in malware detection

---

# 30. Week 3 Summary

This week focused on AI for malware, phishing, and malicious URL detection.

The most important lessons are:

```text
Malware and phishing are common entry points for attacks.

Static analysis examines artefacts without executing them.

Dynamic analysis observes runtime behaviour.

Behavioural analysis focuses on actions and sequences.

Phishing detection combines sender, content, URL, and context features.

Malicious URL detection uses lexical, host-based, content-based, and reputation features.

Accuracy alone is not enough.

Attackers adapt through obfuscation, packing, URL changes, and domain rotation.

Useful AI detectors should support explainable and proportionate security decisions.
```

Final takeaway:

> AI can help detect malicious artefacts, but effective detection requires meaningful features, careful evaluation, adversarial awareness, and security context.
