---
title: "Week 1: Introduction to Applied AI for Cybersecurity"
layout: default
permalink: /lectures/week1/
---

# Week 1: Introduction to Applied AI for Cybersecurity  
## From Security Data to AI-Driven Decisions

Welcome to Week 1 of **Applied AI for Cybersecurity**.

This week introduces the main idea of the course: artificial intelligence can support cybersecurity, but it must be used carefully. AI is not a magic detector of attacks. It is a set of methods that can help us analyse security data, detect suspicious patterns, prioritise risks, and support security decisions.

The key question for this week is:

> How do we convert a cybersecurity problem into an AI problem without losing the security meaning?

---

# 1. Why This Week Matters

Cybersecurity is now a data-intensive field. Modern systems generate large volumes of data from networks, endpoints, cloud platforms, authentication systems, email systems, web applications, and security tools.

Security professionals need to answer questions such as:

- Is this network traffic normal or malicious?
- Is this email phishing or legitimate?
- Is this file malware or benign software?
- Is this login suspicious or expected?
- Is this traffic spike a DDoS attack or a legitimate flash crowd?
- Is this alert important enough for an analyst to investigate?
- Should the system automatically block, quarantine, or escalate?

AI can help with these questions, but only when the problem is defined correctly, the data is meaningful, the model is evaluated properly, and the final decision is interpreted in context.

---

# 2. Learning Objectives

By the end of this week, you should be able to:

1. Explain the role of AI in modern cybersecurity.
2. Identify major cybersecurity use cases for AI.
3. Distinguish between security data, features, labels, models, predictions, and decisions.
4. Explain the difference between classification, anomaly detection, and risk scoring.
5. Define false positives, false negatives, precision, recall, and F1-score in cybersecurity terms.
6. Explain why accuracy alone is not enough for security evaluation.
7. Discuss why AI for cybersecurity is difficult because of adversarial behaviour, class imbalance, noisy data, poor labels, and concept drift.
8. Apply basic reasoning to classify a security observation as benign, suspicious, malicious, or uncertain.

---

# 3. What Does “Applied AI for Cybersecurity” Mean?

Applied AI for cybersecurity means using AI and machine learning techniques to support cyber defence tasks.

It does **not** only mean building a model. It means designing a complete decision-support process:

```text
Security problem
→ observable behaviour
→ telemetry
→ features
→ labels or assumptions
→ model
→ prediction
→ interpretation
→ security decision
```

For example, suppose we want to detect phishing emails.

A weak way to describe the problem is:

```text
Train an AI model to detect phishing.
```

A stronger way is:

```text
Use email metadata, sender reputation, URL features, text patterns, and attachment indicators to estimate whether an email is likely to be phishing, then decide whether to deliver, warn, quarantine, or escalate it.
```

The second version is better because it connects the model to the real security decision.

---

# 4. Why AI Is Used in Cybersecurity

AI is used in cybersecurity because cyber defence is often:

- Data-rich
- Time-sensitive
- Pattern-based
- Uncertain
- Adversarial

Human analysts cannot manually inspect all logs, packets, files, emails, alerts, or cloud events. AI can help detect patterns that would be difficult to identify manually.

However, AI does not remove the need for human expertise. In many cases, the model output is only a recommendation. A security professional still needs to interpret the output, consider context, and decide what action is appropriate.

---

# 5. Main Cybersecurity Use Cases for AI

| Cybersecurity Area | Example AI Task |
|---|---|
| Network intrusion detection | Classify network flows as benign or malicious |
| DDoS detection | Detect abnormal traffic surges or resource exhaustion |
| Malware detection | Classify files or behaviours as malicious |
| Phishing detection | Identify suspicious emails, links, or attachments |
| Malicious URL detection | Classify URLs based on lexical and reputation features |
| Account compromise detection | Detect abnormal login or access behaviour |
| Insider threat detection | Identify abnormal behaviour by trusted users |
| Cloud security | Detect abnormal API calls, storage access, or misconfiguration |
| IoT security | Detect compromised or abnormal devices |
| Vulnerability prioritisation | Rank vulnerabilities by exploitability and asset impact |
| SOC alert triage | Prioritise alerts for analyst investigation |
| Threat intelligence | Cluster indicators, summarise reports, and map behaviours |

---

# 6. Security Data, Features, Labels, Models, and Decisions

A common mistake is to jump directly from “data” to “AI model”. In cybersecurity, we need to understand each stage.

| Concept | Meaning | Cybersecurity Example |
|---|---|---|
| Security data | Raw recorded information | Network logs, emails, files, login records |
| Feature | Measurable input used by a model | Request rate, URL length, failed login count |
| Label | Known class used for training or evaluation | Benign, phishing, malware, DDoS |
| Model | AI method that learns patterns | Decision tree, random forest, neural network |
| Prediction | Model output | “Phishing probability = 0.87” |
| Decision | Security action based on prediction | Warn user, quarantine email, escalate alert |

Important distinction:

> A prediction is not the same as a security decision.

A model may predict that an event is suspicious. The organisation still needs to decide whether to block, monitor, escalate, quarantine, or ignore.

---

# 7. Security Data Types

Different cybersecurity tasks use different data.

| Data Type | Example | Possible AI Use |
|---|---|---|
| Network flows | Source IP, destination IP, bytes, duration | Intrusion and DDoS detection |
| Packet captures | Packet headers and payloads | Protocol analysis and malware traffic detection |
| Authentication logs | Login time, user, location, MFA result | Account compromise detection |
| Endpoint logs | Process name, parent process, command line | Malware and suspicious behaviour detection |
| Executable files | PE headers, imported libraries, strings | Malware classification |
| Emails | Sender, subject, links, attachments, body text | Phishing detection |
| URLs | Domain age, length, entropy, redirects | Malicious URL detection |
| DNS logs | Queried domains, frequency, entropy | Botnet and command-and-control detection |
| Cloud logs | API calls, storage access, identity activity | Cloud threat detection |
| Vulnerability data | CVSS score, exploit availability, asset criticality | Vulnerability prioritisation |
| Security alerts | Alert type, severity, source, related events | SOC triage and alert prioritisation |

---

# 8. From Raw Data to Features

AI models usually need structured features. A feature is a measurable representation of behaviour.

| Raw Security Observation | Possible Feature |
|---|---|
| 50 failed logins in 2 minutes | `failed_login_rate` |
| Download from unknown domain | `domain_reputation_score` |
| Large outbound transfer | `outbound_bytes` |
| Many requests to one server | `request_rate` |
| Email contains urgent password reset link | `urgency_keyword_flag` |
| URL contains random-looking characters | `url_entropy` |
| PowerShell runs encoded command | `encoded_command_flag` |
| Executable imports suspicious APIs | `suspicious_import_count` |
| DNS query repeats every 60 seconds | `dns_periodicity_score` |
| User logs in from unusual country | `geo_anomaly_score` |

Key point:

> Feature engineering is where cybersecurity knowledge meets machine learning.

---

# 9. Main AI Problem Types in Cybersecurity

## 9.1 Classification

Classification is used when we have labelled examples.

Example:

```text
Input: email features
Output: phishing or benign
```

Used for:

- Phishing detection
- Malware classification
- Intrusion classification
- Malicious URL detection

Example features for phishing classification:

| Feature | Meaning |
|---|---|
| Sender reputation | Whether the sender has a suspicious history |
| URL mismatch | Link text and actual URL differ |
| Domain age | Recently registered domains may be suspicious |
| Urgency keywords | Words such as “urgent”, “verify”, “password” |
| Attachment type | Executable or macro-enabled attachment |

---

## 9.2 Anomaly Detection

Anomaly detection is used when we do not have enough labelled attack examples. The model learns what normal behaviour looks like and flags deviations.

Example:

```text
Input: user login behaviour
Output: normal or anomalous
```

Used for:

- Insider threat detection
- DDoS detection
- User behaviour analytics
- IoT anomaly detection
- Cloud account misuse

Important warning:

> An anomaly is not automatically an attack.

For example, a user logging in from a new country may be suspicious. But it may also be normal if the user is travelling.

---

## 9.3 Risk Scoring

Risk scoring assigns a risk value to an event, user, file, URL, vulnerability, or incident.

Example:

```text
Input: login location + device + time + file access
Output: risk score = 78/100
```

Used for:

- SOC alert triage
- Vulnerability prioritisation
- Fraud detection
- Access risk assessment
- Incident prioritisation

A risk score should normally be explainable. Analysts need to know why the system assigned a high score.

---

# 10. Case Study 1: Phishing Email Detection

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

Is this email legitimate or phishing?

## Possible Features

| Feature | Value | Interpretation |
|---|---|---|
| Urgency keywords | Present | Suspicious |
| Password request | Present | Suspicious |
| Sender identity | Unknown | Suspicious |
| URL domain | Not official university domain | Suspicious |
| Link text | Claims university support | Suspicious |
| Attachment | None | Neutral |
| Personalisation | Generic “Dear user” | Suspicious |

## AI Framing

This can be framed as a classification problem:

```text
Input: email features
Output: phishing or benign
```

## Security Decision

Possible decisions:

| Model Output | Possible Decision |
|---|---|
| Low phishing risk | Deliver normally |
| Medium phishing risk | Deliver with warning banner |
| High phishing risk | Quarantine and alert user |
| Very high phishing risk | Block and report to security team |

## Discussion

A phishing detector should not be evaluated only by accuracy. Missing a phishing email may lead to credential theft. Blocking too many legitimate emails may disrupt communication.

---

# 11. Case Study 2: DDoS Detection

## Scenario

A university web service receives a sudden traffic surge.

```text
Normal rate: 300 requests/minute
Current rate: 30,000 requests/minute
API latency: increased from 200 ms to 4 seconds
Failed logins: increased by 8x
Payment errors: increasing
```

## Security Question

Is this a DDoS attack?

## Possible Features

| Feature | Meaning |
|---|---|
| Request rate | Number of requests per minute |
| Source IP diversity | Number of unique IP addresses |
| User-agent diversity | Variety of browser/client identifiers |
| Endpoint distribution | Whether traffic targets one endpoint or many |
| Session completion rate | Whether users follow normal behaviour |
| Error rate | Application failures and timeouts |
| Geo-distribution | Countries or regions of traffic sources |
| Historical baseline | Normal traffic for this service |

## AI Framing

This may be framed as:

```text
Anomaly detection
```

or:

```text
Classification if labelled DDoS and benign traffic examples are available
```

## Important Distinction

High traffic is not automatically DDoS.

It could be:

- A legitimate flash crowd
- A marketing campaign
- A course registration opening
- A broken client retrying requests
- A bot attack
- An application-layer DDoS

## Security Decision

Possible responses:

- Monitor
- Scale infrastructure
- Rate-limit suspicious endpoints
- Apply bot challenge
- Block malicious IPs
- Escalate to incident response
- Avoid broad blocking unless necessary

---

# 12. Case Study 3: Malware Detection from Endpoint Behaviour

## Scenario

An endpoint monitoring system records the following behaviour:

```text
Process: powershell.exe
Command: encoded command
Network: connects to unknown domain
Action: downloads executable file
Parent process: winword.exe
```

## Security Question

Is this malicious behaviour?

## Possible Features

| Feature | Interpretation |
|---|---|
| PowerShell execution | May be legitimate or suspicious |
| Encoded command | Suspicious |
| Parent process is Word | Suspicious |
| Download from unknown domain | Suspicious |
| Executable download | Suspicious |
| Domain reputation unknown | Suspicious or uncertain |

## AI Framing

This may be framed as:

```text
Endpoint behaviour classification
```

or:

```text
Anomaly detection
```

## Why Context Matters

PowerShell is not always malicious. System administrators use it legitimately. But PowerShell launched by a Word document with an encoded command and external download is much more suspicious.

---

# 13. Case Study 4: Cloud Account Activity

## Scenario

A cloud administrator creates a new virtual machine at 02:10.

At first glance, this may look suspicious. But the activity occurs during a scheduled maintenance window.

## Security Question

Should this be treated as malicious?

## Possible Interpretation

| Evidence | Interpretation |
|---|---|
| Admin creates VM at night | Suspicious without context |
| Maintenance window exists | Reduces suspicion |
| Admin account is known | Reduces suspicion |
| VM image is approved | Reduces suspicion |
| VM opens public ports | Increases suspicion |
| No change ticket exists | Increases suspicion |

## Main Lesson

The same event can be benign or suspicious depending on context.

---

# 14. Evaluation: The Most Important Week 1 Topic

In cybersecurity, evaluating AI is difficult because attacks are often rare and costly.

## Confusion Matrix

|  | Predicted Malicious | Predicted Benign |
|---|---|---|
| Actually Malicious | True Positive | False Negative |
| Actually Benign | False Positive | True Negative |

## Cybersecurity Meaning

| Term | Meaning |
|---|---|
| True Positive | Attack correctly detected |
| True Negative | Benign activity correctly ignored |
| False Positive | Benign activity wrongly flagged as attack |
| False Negative | Attack missed by the model |

---

# 15. Why Accuracy Alone Is Not Enough

Suppose a dataset contains 10,000 events:

```text
100 malicious events
9,900 benign events
```

A useless model predicts every event as benign.

Results:

```text
Correct benign predictions = 9,900
Missed attacks = 100
Accuracy = 9,900 / 10,000 = 99%
```

The model has 99% accuracy, but it detects no attacks.

Key lesson:

> High accuracy can hide poor security performance when attacks are rare.

---

# 16. Precision, Recall, and F1-Score

## Precision

Precision answers:

> Of everything the model flagged as malicious, how much was actually malicious?

```text
Precision = TP / (TP + FP)
```

High precision means fewer false alarms.

## Recall

Recall answers:

> Of all real malicious cases, how many did the model detect?

```text
Recall = TP / (TP + FN)
```

High recall means fewer missed attacks.

## F1-Score

F1-score balances precision and recall.

```text
F1 = 2 × (Precision × Recall) / (Precision + Recall)
```

## Security Interpretation

| Metric | Why It Matters |
|---|---|
| Precision | Analyst workload and alert fatigue |
| Recall | Ability to catch attacks |
| F1-score | Balance between false alarms and missed attacks |
| False positive rate | Operational disruption |
| False negative rate | Security exposure |

---

# 17. Why AI for Cybersecurity Is Difficult

| Challenge | Explanation |
|---|---|
| Class imbalance | Attacks are usually much rarer than benign events |
| Poor labels | Security labels may be missing, delayed, or wrong |
| Concept drift | Normal behaviour and attack behaviour change over time |
| Adversarial behaviour | Attackers deliberately adapt to evade detection |
| Noisy data | Logs may be incomplete, duplicated, or inconsistent |
| Context dependence | The same behaviour may be benign or malicious depending on context |
| Explainability | Analysts need reasons, not only predictions |
| Automation risk | Wrong automated actions can disrupt systems |
| Privacy | Security data may contain sensitive user information |
| Generalisation | Models trained in one environment may fail in another |

Core statement:

> Cybersecurity is an adversarial domain. Attackers react to defenders, so the data distribution is not stable.

---

# 18. Summary of Key Ideas

This week introduced the foundations of Applied AI for Cybersecurity.

Main points:

- AI can support cybersecurity, but it is not a magic solution.
- Security problems must be translated carefully into AI problems.
- Cybersecurity data must be converted into meaningful features.
- Predictions are not the same as decisions.
- Accuracy alone is not enough.
- False positives and false negatives have different security costs.
- Context is essential.
- AI systems can fail because attackers adapt.

---

# 19. Lab Sheet 1: From Security Data to AI Decisions

## Lab Overview

In this lab, you will practise turning security observations into AI-ready reasoning. You will identify security domains, propose features, assign tentative labels, discuss uncertainty, and evaluate model performance.

This is a conceptual and analytical lab. The aim is not advanced coding. The aim is to understand how AI-based cybersecurity systems are designed and evaluated.

---

## Lab Duration

Approximate duration: 90 minutes.

---

## Lab Mode

Individual work followed by small-group discussion.

---

## Lab Objectives

By completing this lab, you should be able to:

1. Identify the security domain of a given event.
2. Extract possible AI features from security observations.
3. Assign tentative labels and justify uncertainty.
4. Explain the cost of false positives and false negatives.
5. Select a suitable AI problem type.
6. Calculate basic evaluation metrics.
7. Explain why accuracy alone is not enough.

---

# 20. Lab Dataset

Use the following simplified security observations.

| Event ID | Source | Observation |
|---|---|---|
| E1 | Email | Message claims urgent password reset and links to unknown domain |
| E2 | Network | 30,000 requests in 2 minutes to one web endpoint |
| E3 | Login | User logs in from usual device and usual location |
| E4 | Endpoint | PowerShell executes encoded command and downloads a file |
| E5 | URL | Domain registered yesterday and contains random-looking characters |
| E6 | Cloud | Admin creates new VM during scheduled maintenance |
| E7 | DNS | Host repeatedly queries rare domain every 60 seconds |
| E8 | File | Executable imports functions often used for process injection |
| E9 | Web | Many failed login attempts from one IP address |
| E10 | Endpoint | Antivirus detects malware in already quarantined file |

---

# 21. Lab Task 1 — Identify the Security Domain

For each event, identify the most relevant cybersecurity domain.

| Event ID | Domain |
|---|---|
| E1 |  |
| E2 |  |
| E3 |  |
| E4 |  |
| E5 |  |
| E6 |  |
| E7 |  |
| E8 |  |
| E9 |  |
| E10 |  |

Possible domains include:

- Email security
- Phishing detection
- Network security
- DDoS detection
- Identity and access security
- Endpoint security
- Malware detection
- URL security
- DNS security
- Cloud security
- Web application security

---

# 22. Lab Task 2 — Extract Possible Features

For each event, propose at least two possible features that an AI system could use.

Example:

| Event ID | Possible Features |
|---|---|
| E1 | sender reputation, domain age, urgency keywords, URL mismatch |
| E2 | request rate, endpoint path, source IP diversity, user-agent diversity |

Complete the table:

| Event ID | Possible Features |
|---|---|
| E1 |  |
| E2 |  |
| E3 |  |
| E4 |  |
| E5 |  |
| E6 |  |
| E7 |  |
| E8 |  |
| E9 |  |
| E10 |  |

---

# 23. Lab Task 3 — Assign a Tentative Label

Assign one of the following labels to each event:

```text
Benign
Suspicious
Malicious
Uncertain
```

Complete the table:

| Event ID | Tentative Label | Reason |
|---|---|---|
| E1 |  |  |
| E2 |  |  |
| E3 |  |  |
| E4 |  |  |
| E5 |  |  |
| E6 |  |  |
| E7 |  |  |
| E8 |  |  |
| E9 |  |  |
| E10 |  |  |

Important:

> “Uncertain” is an acceptable answer if you can explain what additional context is needed.

---

# 24. Lab Task 4 — False Positive and False Negative Costs

Choose three events from the dataset.

For each event, describe the cost of a false positive and the cost of a false negative.

| Event ID | False Positive Cost | False Negative Cost |
|---|---|---|
|  |  |  |
|  |  |  |
|  |  |  |

Example:

| Event | False Positive Cost | False Negative Cost |
|---|---|---|
| Phishing email | Legitimate email blocked | User credentials stolen |
| DDoS traffic | Legitimate users blocked | Service unavailable |
| Malware execution | Business process interrupted | Host compromised |

Teaching point:

> The best detection threshold depends on the cost of being wrong.

---

# 25. Lab Task 5 — Choose the AI Problem Type

Map each cybersecurity problem to the most suitable AI framing.

Possible AI framings:

- Classification
- Anomaly detection
- Risk scoring
- Ranking
- Clustering
- Human-in-the-loop decision support

Complete the table:

| Problem | Suitable AI Framing | Reason |
|---|---|---|
| Phishing detection |  |  |
| Malware detection |  |  |
| DDoS detection |  |  |
| Insider behaviour detection |  |  |
| SOC alert prioritisation |  |  |
| Vulnerability prioritisation |  |  |
| Malicious URL detection |  |  |
| DNS botnet detection |  |  |

---

# 26. Lab Task 6 — Confusion Matrix Exercise

A phishing detector is tested on 1,000 emails.

Dataset:

```text
100 phishing emails
900 benign emails
```

Model output:

```text
80 phishing emails correctly detected
20 phishing emails missed
60 benign emails wrongly flagged
840 benign emails correctly ignored
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
```

Calculate:

```text
Precision =
Recall =
F1-score =
Accuracy =
```

---

## Worked Solution

```text
True positives = 80
False negatives = 20
False positives = 60
True negatives = 840
```

```text
Precision = TP / (TP + FP)
          = 80 / (80 + 60)
          = 80 / 140
          = 0.571
```

```text
Recall = TP / (TP + FN)
       = 80 / (80 + 20)
       = 80 / 100
       = 0.800
```

```text
F1-score = 2 × (Precision × Recall) / (Precision + Recall)
         = 2 × (0.571 × 0.800) / (0.571 + 0.800)
         ≈ 0.667
```

```text
Accuracy = (TP + TN) / Total
         = (80 + 840) / 1000
         = 920 / 1000
         = 0.920
```

Discussion question:

> Is 92% accuracy good enough?

Possible answer:

Not necessarily. The model still misses 20 phishing emails and wrongly flags 60 benign emails. Whether this is acceptable depends on operational cost.

---

# 27. Lab Deliverable

Submit a short worksheet containing:

1. Security domain classification.
2. Feature extraction table.
3. Tentative labels and reasons.
4. False positive / false negative cost discussion.
5. AI problem type mapping.
6. Confusion matrix calculations.
7. Short reflection: **Why is accuracy alone not enough in cybersecurity?**

Recommended length:

```text
800–1200 words
```

---

# 28. Exercises

## Exercise 1 — Concept Check

Answer briefly.

1. What is the difference between a security event and a security decision?
2. What is a feature?
3. What is a label?
4. Why are labels difficult in cybersecurity?
5. What is a false positive?
6. What is a false negative?
7. Why is class imbalance common in cybersecurity?
8. Why is anomaly not the same as attack?
9. Why does cybersecurity require context?
10. Give one example where an AI model prediction should not automatically trigger a response.

---

## Exercise 2 — Short Analytical Answer

Write 200–300 words.

**Question:**  
Why is applying AI to cybersecurity more difficult than applying AI to ordinary image or product classification?

Your answer should discuss at least four of the following:

- Adversarial behaviour
- Concept drift
- Class imbalance
- Noisy data
- Poor labels
- Context dependence
- High cost of errors
- Explainability
- Privacy

---

## Exercise 3 — Feature Design

For each problem, propose three useful features.

| Problem | Feature 1 | Feature 2 | Feature 3 |
|---|---|---|---|
| Phishing detection |  |  |  |
| DDoS detection |  |  |  |
| Malware detection |  |  |  |
| Account compromise |  |  |  |
| Malicious URL detection |  |  |  |
| DNS botnet detection |  |  |  |
| Cloud misuse detection |  |  |  |

---

## Exercise 4 — Evaluation Reflection

A model has 98% accuracy on a cybersecurity dataset.

Answer:

1. Why might this still be a poor model?
2. What additional metrics would you request?
3. What would you ask about the dataset?
4. What would you ask about the cost of false positives and false negatives?
5. What would you ask before deploying the model?

---

## Exercise 5 — Case Analysis

Read the case below.

```text
A user logs in from a new country at 03:00.
The user successfully completes MFA.
The same user downloads 2 GB of files from cloud storage.
The user is a senior manager who is currently attending a conference abroad.
```

Answer:

1. Which observations are suspicious?
2. Which observations reduce suspicion?
3. What features could an AI model use?
4. What additional context is needed?
5. Should this be labelled benign, suspicious, malicious, or uncertain?
6. What would be a proportionate security response?

---

## Exercise 6 — Explainability Practice

Rewrite this poor AI output into an analyst-friendly explanation.

Poor output:

```text
Incident probability: 86%
Recommended action: Block traffic
```

Your improved explanation should include:

- Risk-increasing evidence
- Risk-reducing evidence
- Missing evidence
- Recommended next step
- Whether human approval is required

---

# 29. Further Reading

These readings support the main ideas introduced in Week 1.

## Core Reading

1. **NIST AI Risk Management Framework**  
   This framework explains how organisations can manage risks related to AI systems, including trustworthiness, accountability, transparency, reliability, safety, and governance.  
   <https://www.nist.gov/itl/ai-risk-management-framework>  
   NIST describes the AI RMF as a framework for managing risks to individuals, organisations, and society associated with AI. :contentReference[oaicite:0]{index=0}

2. **NIST SP 800-61 Rev. 3: Incident Response Recommendations and Considerations for Cybersecurity Risk Management**  
   This publication explains how organisations can improve incident detection, response, and recovery activities.  
   <https://csrc.nist.gov/pubs/sp/800/61/r3/final>  
   NIST states that SP 800-61 Rev. 3 helps organisations prepare for incident response, reduce incident impact, and improve detection, response, and recovery activities. :contentReference[oaicite:1]{index=1}

3. **MITRE ATT&CK Enterprise Matrix**  
   MITRE ATT&CK provides a structured way to describe adversary tactics and techniques. It is useful for connecting security evidence to attacker behaviour.  
   <https://attack.mitre.org/matrices/enterprise/>  
   The Enterprise Matrix covers platforms including Windows, macOS, Linux, SaaS, IaaS, identity providers, network devices, containers, and others. :contentReference[oaicite:2]{index=2}

4. **CISA Cybersecurity Incident and Vulnerability Response Playbooks**  
   These playbooks provide practical response guidance for cybersecurity incidents and vulnerabilities.  
   <https://www.cisa.gov/planning-response-recovery>  
   CISA describes these playbooks as guidance for incident response and vulnerability response. :contentReference[oaicite:3]{index=3}

---

## Suggested Topics to Explore

Search for recent academic or industry material on:

- Machine learning for intrusion detection
- Machine learning for DDoS detection
- Phishing detection using natural language processing
- Malware detection using static and dynamic analysis
- Explainable AI for cybersecurity
- Adversarial machine learning
- Concept drift in intrusion detection
- Human-in-the-loop cybersecurity
- AI risk management
- Security analytics and alert prioritisation

---

# 30. Week 1 Summary

This week introduced the foundation of Applied AI for Cybersecurity.

The most important lessons are:

```text
AI in cybersecurity starts with a security problem, not with a model.

Security data must be transformed into meaningful features.

Predictions are not the same as decisions.

Accuracy alone can be misleading.

False positives and false negatives have different operational costs.

Context is essential.

Cybersecurity is adversarial, so AI models must be evaluated and deployed carefully.
```

Final takeaway:

> A good AI-based cybersecurity system is not simply the one with the highest accuracy.  
> It is the one that supports reliable, explainable, and proportionate security decisions.
