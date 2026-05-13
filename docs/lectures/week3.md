---
title: "Week 3: AI for Network Intrusion and DDoS Detection"
layout: default
permalink: /lectures/week3/
---

# Week 3: AI for Network Intrusion and DDoS Detection  
## From Network Traffic to Attack Detection



Welcome to Week 3 of **Applied AI for Cybersecurity**.

In Week 1, we studied how cybersecurity problems can be converted into AI problems. We discussed security data, features, labels, models, predictions, decisions, and evaluation metrics.

This week applies those ideas to one of the most important areas of cybersecurity:

> **Network intrusion and DDoS detection**

The main question for this week is:

> How can AI help us detect malicious network behaviour, and why is this difficult in real environments?

---

# 1. Learning Objectives

By the end of this week, you should be able to:

1. Explain the purpose of network intrusion detection.
2. Distinguish between signature-based, anomaly-based, and ML-based intrusion detection.
3. Describe common types of network attacks.
4. Explain what DDoS attacks are and why they are difficult to detect.
5. Identify useful features for network intrusion and DDoS detection.
6. Explain the difference between packet-level, flow-level, and log-level data.
7. Describe how supervised learning and anomaly detection can be used for intrusion detection.
8. Explain why network intrusion datasets may not fully represent real-world traffic.
9. Evaluate intrusion detection models using security-aware metrics.
10. Discuss false positives, false negatives, class imbalance, concept drift, and adversarial adaptation in network security.

---

# 2. Why Network Intrusion Detection Matters

A network intrusion is an unauthorised, suspicious, or malicious activity affecting a network, system, or service.

Examples include:

- Port scanning
- Brute-force login attempts
- Malware communication
- Botnet command-and-control traffic
- Data exfiltration
- Denial-of-service attacks
- Lateral movement
- Exploitation attempts
- Suspicious DNS activity
- Abnormal traffic from compromised devices

A network intrusion detection system, or **NIDS**, monitors network activity to identify suspicious or malicious behaviour.

Traditional intrusion detection relied heavily on signatures and rules. Modern systems increasingly use machine learning to detect patterns that may not be captured by static rules.

---

# 3. Intrusion Detection Approaches

## 3.1 Signature-Based Detection

Signature-based detection uses known patterns of malicious behaviour.

Example:

```text
If packet payload matches known exploit pattern,
generate alert.
```

Advantages:

- Good for known attacks
- Easy to explain
- Low false positive rate when signatures are precise

Limitations:

- Poor at detecting new or modified attacks
- Requires regular signature updates
- Can be evaded by small changes in attack behaviour

Example:

```text
A known malware family always connects to a specific command-and-control domain.
A signature can detect traffic to that domain.
```

But if the malware changes the domain, the signature may fail.

---

## 3.2 Anomaly-Based Detection

Anomaly-based detection learns what normal behaviour looks like and flags deviations.

Example:

```text
Normal traffic to a web server: 300 requests/minute
Current traffic: 30,000 requests/minute
Alert: traffic anomaly
```

Advantages:

- Can detect unknown attacks
- Useful when labelled attack data is limited
- Suitable for behavioural monitoring

Limitations:

- Anomaly does not always mean attack
- High false positives are common
- Requires good understanding of normal behaviour
- Normal behaviour changes over time

Example:

A traffic spike may indicate a DDoS attack. But it may also be caused by a legitimate event, such as course registration, ticket sales, or a marketing campaign.

---

## 3.3 Machine-Learning-Based Detection

Machine learning can be used for both classification and anomaly detection.

Examples:

```text
Input: network flow features
Output: benign or attack
```

or:

```text
Input: traffic behaviour
Output: normal or anomalous
```

Common ML methods include:

- Decision trees
- Random forests
- Support vector machines
- k-nearest neighbours
- Logistic regression
- Naive Bayes
- Neural networks
- Autoencoders
- Clustering methods
- Isolation forest

ML-based detection can improve flexibility, but it also introduces new challenges:

- Model generalisation
- Data quality
- Class imbalance
- Feature selection
- Explainability
- Adversarial evasion
- Dataset bias

---

# 4. Network Data Types

AI-based network detection can use different levels of network data.

## 4.1 Packet-Level Data

Packet-level data contains detailed information about individual packets.

Examples:

- Source IP
- Destination IP
- Source port
- Destination port
- Protocol
- Packet size
- Flags
- Payload content
- Timestamp

Packet-level analysis can be detailed, but it may be expensive and privacy-sensitive.

Example:

```text
192.168.1.10 → 10.0.0.5
Protocol: TCP
Destination port: 443
Packet size: 1,500 bytes
TCP flags: SYN
```

---

## 4.2 Flow-Level Data

Flow-level data summarises a sequence of packets between two endpoints.

A flow is usually identified by:

```text
Source IP
Destination IP
Source port
Destination port
Protocol
Time window
```

Flow-level features may include:

- Flow duration
- Total packets
- Total bytes
- Average packet size
- Packet rate
- Byte rate
- Forward packets
- Backward packets
- Inter-arrival time
- TCP flags
- Flow direction

Flow-level data is commonly used in ML-based intrusion detection because it is more compact than raw packet data and less privacy-sensitive than payload inspection.

---

## 4.3 Log-Level Data

Log-level data comes from systems, firewalls, routers, web servers, DNS servers, authentication systems, and security tools.

Examples:

```text
Firewall log:
src_ip, dst_ip, port, action, timestamp

Web server log:
client_ip, URL, status_code, response_size, user_agent

DNS log:
host, queried_domain, query_type, response_ip, timestamp
```

Log-level data is useful when combined with flow-level data.

---

# 5. Common Network Attack Categories

Network intrusion detection may target many attack types.

| Attack Type | Description |
|---|---|
| Port scanning | Attacker probes systems to discover open ports and services |
| Brute-force attack | Repeated attempts to guess credentials |
| DoS | One source attempts to disrupt availability |
| DDoS | Many sources attempt to disrupt availability |
| Botnet traffic | Compromised hosts communicate with attacker infrastructure |
| Exploitation | Attacker sends traffic to exploit a vulnerability |
| Data exfiltration | Data is transferred out of the organisation |
| Lateral movement | Attacker moves between internal systems |
| Command and control | Malware communicates with attacker-controlled servers |
| Web attack | Attacks such as SQL injection, XSS, or path traversal |

---

# 6. DDoS Detection

## 6.1 What Is a DDoS Attack?

A Distributed Denial-of-Service attack attempts to make a service unavailable by overwhelming resources.

The target may be:

- A website
- A DNS service
- An API endpoint
- A database-backed web application
- A cloud service
- A university portal
- An authentication service
- A payment service

DDoS attacks affect **availability**, one of the three core goals of cybersecurity: confidentiality, integrity, and availability.

MITRE ATT&CK describes Network Denial of Service as activity where adversaries attempt to degrade or block the availability of target resources.

Further reading:

- MITRE ATT&CK: Network Denial of Service  
  <https://attack.mitre.org/techniques/T1498/>

---

## 6.2 Types of DDoS Attacks

| Type | Description | Example |
|---|---|---|
| Volumetric attack | Consumes network bandwidth | UDP flood |
| Protocol attack | Exploits protocol behaviour | SYN flood |
| Application-layer attack | Exhausts application resources | HTTP GET flood |
| Reflection/amplification attack | Uses third-party reflectors to amplify traffic | DNS amplification |
| Low-and-slow attack | Sends traffic slowly to avoid thresholds | Slowloris-like behaviour |

---

## 6.3 DDoS Detection Features

Useful DDoS detection features may include:

| Feature | Meaning |
|---|---|
| Request rate | Number of requests per time window |
| Packet rate | Number of packets per second |
| Byte rate | Volume of bytes per second |
| Source IP diversity | Number of distinct source IPs |
| Destination concentration | Whether many requests target one service |
| Protocol distribution | TCP, UDP, ICMP, HTTP, DNS |
| SYN/ACK ratio | Useful for SYN flood detection |
| Error rate | Server errors, timeouts, dropped connections |
| Response latency | Service slowdown |
| User-agent diversity | Whether clients look similar or automated |
| Session completion rate | Whether users follow normal application behaviour |
| Geo-distribution | Regional distribution of traffic |
| Endpoint concentration | Whether traffic targets expensive endpoints |
| Historical baseline | Normal traffic for comparison |

---

## 6.4 High Traffic Is Not Always DDoS

A traffic spike may be caused by a DDoS attack, but it may also be legitimate.

Examples of benign traffic spikes:

- Course registration opens
- Product launch
- Exam results released
- Ticket sales
- News event
- Marketing campaign
- Software update
- Public announcement

Therefore, a good detection system should consider context.

Example:

```text
Traffic increased 20x in five minutes.
```

Possible interpretations:

```text
DDoS attack
Legitimate flash crowd
Crawler activity
Broken client retry loop
API misuse
```

Key point:

> DDoS detection is not only a traffic-volume problem. It is a resource-exhaustion and behaviour-analysis problem.

---

# 7. AI Problem Framing for Network Intrusion Detection

## 7.1 Binary Classification

Binary classification separates traffic into two classes:

```text
Benign
Attack
```

Example:

```text
Input: flow features
Output: benign or malicious
```

Advantages:

- Simple problem definition
- Easy to evaluate
- Useful for first IDS models

Limitations:

- Does not distinguish attack types
- May hide important operational differences
- Requires labelled data

---

## 7.2 Multi-Class Classification

Multi-class classification predicts specific attack categories.

Example:

```text
Benign
Port scan
DDoS
Botnet
Brute force
Web attack
Infiltration
```

Advantages:

- More informative than binary classification
- Helps analysts understand attack type

Limitations:

- Harder than binary classification
- Requires reliable labels for each attack type
- Some attacks may overlap

---

## 7.3 Anomaly Detection

Anomaly detection identifies deviations from normal behaviour.

Example:

```text
Normal traffic baseline:
300 requests/minute

Observed:
30,000 requests/minute

Output:
anomalous
```

Advantages:

- Can detect unknown attacks
- Useful when labelled data is limited

Limitations:

- High false positives
- Legitimate unusual behaviour may be flagged
- Requires a stable definition of normal

---

## 7.4 Risk Scoring

Risk scoring assigns a severity score based on multiple indicators.

Example:

```text
Traffic spike: +20
Repeated API calls: +25
Error rate increase: +15
Known business event: -20
Known malicious IPs: +30
Final risk score: 70/100
```

Advantages:

- Supports analyst prioritisation
- Can combine model output with context
- More flexible than a binary decision

Limitations:

- Scores can be subjective
- Requires careful calibration
- Needs explainability

---

# 8. Feature Engineering for Network Intrusion Detection

Feature engineering is the process of converting raw network data into useful model inputs.

## 8.1 Basic Flow Features

| Feature | Description |
|---|---|
| `duration` | Length of the flow |
| `total_fwd_packets` | Packets from source to destination |
| `total_bwd_packets` | Packets from destination to source |
| `total_length_fwd_packets` | Bytes sent forward |
| `total_length_bwd_packets` | Bytes sent backward |
| `flow_bytes_per_sec` | Byte rate |
| `flow_packets_per_sec` | Packet rate |
| `packet_length_mean` | Average packet size |
| `packet_length_std` | Packet size variation |
| `flow_iat_mean` | Mean inter-arrival time |

---

## 8.2 TCP and Protocol Features

| Feature | Description |
|---|---|
| `syn_flag_count` | Number of SYN flags |
| `ack_flag_count` | Number of ACK flags |
| `rst_flag_count` | Number of reset flags |
| `fin_flag_count` | Number of FIN flags |
| `protocol` | TCP, UDP, ICMP, etc. |
| `destination_port` | Target service port |
| `source_port` | Source port |

These features are useful for detecting scans, floods, and abnormal protocol behaviour.

---

## 8.3 Application-Level Features

| Feature | Description |
|---|---|
| `http_request_rate` | Number of HTTP requests per time window |
| `url_path_frequency` | Frequency of requested paths |
| `status_code_distribution` | HTTP response code patterns |
| `user_agent_entropy` | Diversity of user-agent strings |
| `session_completion_rate` | Whether users complete expected workflows |
| `expensive_endpoint_hits` | Calls to costly API endpoints |

Application-layer DDoS detection often needs application-level features, not only network-level features.

---

# 9. Case Study 1: Port Scanning

## Scenario

A host sends connection attempts to many ports on a server within a short time.

```text
Source: 192.168.1.50
Destination: 10.0.0.20
Ports contacted: 21, 22, 23, 25, 53, 80, 443, 445, 3389
Time window: 30 seconds
```

## Security Question

Is this normal administration, vulnerability scanning, or attacker reconnaissance?

## Useful Features

| Feature | Why It Matters |
|---|---|
| Number of destination ports | Many ports suggest scanning |
| Time window | Rapid attempts are more suspicious |
| Connection success rate | Failed connections may indicate probing |
| Source host role | Scanner or ordinary workstation? |
| Destination host criticality | Critical servers deserve higher priority |
| Historical behaviour | Has this source scanned before? |

## Possible AI Framing

```text
Classification
Anomaly detection
Risk scoring
```

## Discussion

The same behaviour may be legitimate if it comes from an approved vulnerability scanner. It is more suspicious if it comes from an ordinary user workstation.

---

# 10. Case Study 2: DDoS or Flash Crowd?

## Scenario

A university opens online registration for a popular short course.

At 10:00, registration opens.

By 10:05:

```text
Requests increase from 300/minute to 4,800/minute
API latency increases from 200 ms to 3.5 seconds
Payment timeouts begin
Traffic mainly comes from three countries
Many requests use similar user-agent strings
```

## Security Question

Is this a legitimate flash crowd, DDoS attack, or mixed incident?

## Evidence Supporting Legitimate Demand

- Registration opened at 10:00.
- The course may be popular.
- Traffic increase happened immediately after opening.
- The main countries may match the target audience.

## Evidence Supporting DDoS or Abuse

- Request volume increased sharply.
- API latency degraded.
- Payment errors started.
- Similar user-agent strings may suggest automation.
- Repeated requests may target expensive endpoints.
- Real users may be unable to complete registration.

## AI Framing

```text
Anomaly detection
Risk scoring
Application-layer DDoS classification
```

## Main Lesson

Do not classify based only on traffic volume. Consider business context, session behaviour, endpoint concentration, and service impact.

---

# 11. Case Study 3: Botnet Command-and-Control Traffic

## Scenario

An internal host sends DNS queries to a rare domain every 60 seconds.

```text
Host: 10.0.5.23
Domain: xj29sda-control-example.net
Frequency: every 60 seconds
Duration: 4 hours
Normal user activity: none
```

## Security Question

Is this normal DNS activity or possible botnet command-and-control traffic?

## Useful Features

| Feature | Why It Matters |
|---|---|
| Query periodicity | Regular beaconing may indicate malware |
| Domain rarity | Rare domains are more suspicious |
| Domain age | Newly registered domains may be suspicious |
| Domain entropy | Random-looking domains may indicate DGA |
| Host role | Server, workstation, IoT device |
| Query duration | Long repeated activity increases suspicion |

## AI Framing

```text
Anomaly detection
Classification
Clustering of similar DNS behaviour
```

## Main Lesson

Botnet detection may require temporal features, not only single-event features.

---

# 12. Dataset Awareness

Network intrusion detection often uses public datasets. These are useful for learning and benchmarking, but they have limitations.

## 12.1 CIC-IDS2017

CIC-IDS2017 is a widely used dataset for intrusion detection research. It includes benign traffic and common attack scenarios. It provides PCAP files and labelled flow CSV files generated using CICFlowMeter.

Further reading:

- CIC-IDS2017 official page:  
  <https://www.unb.ca/cic/datasets/ids-2017.html>

## 12.2 CSE-CIC-IDS2018

CSE-CIC-IDS2018 includes several attack scenarios, including brute force, Heartbleed, botnet, DoS, DDoS, web attacks, and infiltration. It also includes extracted flow features.

Further reading:

- CSE-CIC-IDS2018 official page:  
  <https://www.unb.ca/cic/datasets/ids-2018.html>

## 12.3 UNSW-NB15

UNSW-NB15 contains normal traffic and several attack categories, including Fuzzers, Analysis, Backdoors, DoS, Exploits, Generic, Reconnaissance, Shellcode, and Worms.

Further reading:

- UNSW-NB15 official page:  
  <https://research.unsw.edu.au/projects/unsw-nb15-dataset>

---

# 13. Limitations of Network Intrusion Datasets

Public datasets are useful, but they are not perfect.

Common limitations include:

| Limitation | Explanation |
|---|---|
| Artificial traffic | Some datasets are generated in lab environments |
| Outdated attacks | Attack behaviours may not reflect current threats |
| Dataset bias | Models may learn dataset artefacts instead of attack behaviour |
| Label noise | Labels may be incomplete or inaccurate |
| Class imbalance | Some attack classes may be very rare |
| Lack of encryption realism | Modern traffic is often encrypted |
| Environment mismatch | A model trained on one network may fail in another |
| Overfitting | High dataset performance may not generalise |

Important point:

> A model that performs well on a benchmark dataset may still fail in a real network.

---

# 14. Model Evaluation for IDS

Evaluation should reflect security impact, not only statistical performance.

## 14.1 Key Metrics

| Metric | Meaning in IDS |
|---|---|
| Accuracy | Overall proportion of correct predictions |
| Precision | Of alerts raised, how many are real attacks? |
| Recall | Of real attacks, how many are detected? |
| F1-score | Balance between precision and recall |
| False positive rate | Benign traffic wrongly flagged |
| False negative rate | Attacks missed |
| Detection latency | How quickly the attack is detected |
| Throughput | Whether detection works at required traffic volume |
| Interpretability | Whether analysts understand the alert |
| Operational cost | Human and business impact of the detection |

---

## 14.2 Why Accuracy Can Mislead

Suppose a network dataset contains:

```text
99% benign traffic
1% attack traffic
```

A model that predicts everything as benign may achieve 99% accuracy while detecting no attacks.

Therefore, IDS evaluation must consider recall, precision, false positive rate, false negative rate, and operational impact.

---

## 14.3 False Positives in IDS

A false positive occurs when benign traffic is flagged as malicious.

Possible consequences:

- Analyst fatigue
- Wasted investigation time
- Blocked legitimate users
- Service disruption
- Loss of trust in the IDS

Example:

```text
A legitimate vulnerability scan from the internal security team is flagged as attacker reconnaissance.
```

---

## 14.4 False Negatives in IDS

A false negative occurs when malicious traffic is missed.

Possible consequences:

- Compromise remains undetected
- Malware spreads
- Data exfiltration continues
- DDoS attack disrupts service
- Attacker moves laterally

Example:

```text
Low-and-slow data exfiltration is treated as normal outbound traffic.
```

---

# 15. Why AI-Based IDS Is Difficult

## 15.1 Concept Drift

Normal network behaviour changes over time.

Examples:

- New applications are deployed.
- Users work remotely.
- Cloud services change traffic patterns.
- Software updates create new traffic.
- New business events cause traffic spikes.

A model trained on old traffic may become less effective.

---

## 15.2 Adversarial Adaptation

Attackers adapt to detection systems.

Examples:

- Slowing down scans
- Mimicking normal user-agent strings
- Using encrypted channels
- Splitting traffic across many sources
- Avoiding known malicious domains
- Sending traffic below thresholds

---

## 15.3 Encryption

Modern traffic is often encrypted.

This limits payload inspection and increases the importance of metadata and flow features.

Useful features may include:

- TLS version
- Certificate metadata
- Server name indication where available
- Flow duration
- Packet sizes
- Timing patterns
- Destination reputation

---

## 15.4 Deployment Constraints

IDS models must work under operational constraints.

Questions to ask:

- Can the model process traffic fast enough?
- Does it require packet payloads?
- Does it preserve privacy?
- Can analysts understand the alerts?
- How often must the model be retrained?
- What happens when the model is wrong?

---

# 16. Week 2 Summary

This week introduced AI for network intrusion and DDoS detection.

Key points:

```text
Network intrusion detection aims to identify suspicious or malicious network behaviour.

DDoS attacks target availability by exhausting network, protocol, or application resources.

Network detection can use packet-level, flow-level, and log-level data.

Machine learning can support classification, anomaly detection, and risk scoring.

Feature engineering is central to effective IDS design.

High traffic is not automatically DDoS.

Accuracy alone is not enough for IDS evaluation.

Public datasets are useful but may not represent real deployment conditions.

AI-based IDS must handle class imbalance, concept drift, encryption, and adversarial adaptation.
```

Final takeaway:

> AI can help detect network attacks, but effective intrusion detection requires security context, meaningful features, careful evaluation, and operational judgment.

---

# 17. Lab Sheet 2: Network Intrusion and DDoS Detection

## Lab Overview

In this lab, you will analyse simplified network security observations and design an AI-based approach for intrusion and DDoS detection.

This lab does not require advanced coding. It focuses on network security reasoning, feature design, AI problem framing, and evaluation.

---

## Lab Duration

Approximate duration: 90 minutes.

---

## Lab Mode

Individual work followed by small-group discussion.

---

## Lab Objectives

By completing this lab, you should be able to:

1. Interpret simplified network traffic observations.
2. Identify possible network attack categories.
3. Extract useful flow-level and application-level features.
4. Choose an appropriate AI framing for a network detection problem.
5. Distinguish DDoS attacks from legitimate traffic surges.
6. Discuss false positive and false negative costs in IDS.
7. Design a simple detection strategy for network attacks.

---

# 18. Lab Dataset A: Network Events

Use the following simplified network observations.

| Event ID | Observation |
|---|---|
| N1 | One internal host connects to 200 destination ports on one server within 30 seconds |
| N2 | Web traffic increases from 300 requests/minute to 30,000 requests/minute |
| N3 | A host sends DNS queries to a rare domain every 60 seconds for 4 hours |
| N4 | Repeated failed SSH login attempts are observed from one external IP |
| N5 | An internal database server sends 5 GB of outbound traffic to an unknown external IP |
| N6 | Many clients send SYN packets to one server, but few complete the TCP handshake |
| N7 | Traffic to one expensive API endpoint increases sharply after a public registration opens |
| N8 | A workstation communicates with an IP address listed in threat intelligence as malicious |
| N9 | A vulnerability scanner approved by IT scans the internal network |
| N10 | A small number of users repeatedly refresh a web page during exam result publication |

---

# 19. Lab Task 1 — Identify Possible Attack Type

For each event, identify the most likely category.

Possible categories:

- Benign activity
- Port scanning
- Brute-force attack
- DDoS
- Application-layer DDoS
- Botnet or command-and-control
- Data exfiltration
- Threat-intelligence match
- Vulnerability scanning
- Uncertain

Complete the table:

| Event ID | Possible Category | Reason |
|---|---|---|
| N1 |  |  |
| N2 |  |  |
| N3 |  |  |
| N4 |  |  |
| N5 |  |  |
| N6 |  |  |
| N7 |  |  |
| N8 |  |  |
| N9 |  |  |
| N10 |  |  |

---

# 20. Lab Task 2 — Extract Features

For each event, propose at least three features an AI-based IDS could use.

Examples:

```text
request_rate
source_ip_count
destination_port_count
syn_ack_ratio
flow_duration
bytes_out
dns_query_periodicity
domain_reputation_score
endpoint_path
user_agent_diversity
```

Complete the table:

| Event ID | Feature 1 | Feature 2 | Feature 3 |
|---|---|---|---|
| N1 |  |  |  |
| N2 |  |  |  |
| N3 |  |  |  |
| N4 |  |  |  |
| N5 |  |  |  |
| N6 |  |  |  |
| N7 |  |  |  |
| N8 |  |  |  |
| N9 |  |  |  |
| N10 |  |  |  |

---

# 21. Lab Task 3 — Choose AI Problem Framing

For each event, choose a suitable AI framing.

Possible framings:

```text
Binary classification
Multi-class classification
Anomaly detection
Risk scoring
Clustering
Rule-assisted ML
Human-in-the-loop review
```

Complete the table:

| Event ID | Suitable AI Framing | Reason |
|---|---|---|
| N1 |  |  |
| N2 |  |  |
| N3 |  |  |
| N4 |  |  |
| N5 |  |  |
| N6 |  |  |
| N7 |  |  |
| N8 |  |  |
| N9 |  |  |
| N10 |  |  |

---

# 22. Lab Task 4 — DDoS or Legitimate Traffic Surge?

Consider the following scenario:

```text
A university opens exam results at 10:00.

At 10:03:
- Traffic increases 15x.
- Many students repeatedly refresh the result page.
- The web server becomes slow.
- Most traffic comes from student residential networks.
- No known malicious IPs are observed.
- The same endpoint is repeatedly requested.
```

Answer:

1. What evidence suggests legitimate demand?
2. What evidence suggests possible DDoS or abuse?
3. What additional evidence would you request?
4. Would you classify this as benign, suspicious, malicious, or uncertain?
5. What would be a proportionate response?

---

# 23. Lab Task 5 — Design a Simple DDoS Risk Score

Design a simple DDoS risk score using 6–8 indicators.

Example indicators may include:

- Traffic increase compared with baseline
- Source IP diversity
- SYN/ACK ratio
- User-agent diversity
- Endpoint concentration
- Error rate
- Known business event
- Threat intelligence match
- Session completion rate
- Geo-distribution

Complete the table:

| Indicator | Score Contribution | Why It Matters |
|---|---:|---|
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |

Define your decision thresholds:

| Score Range | Decision |
|---|---|
| 0–30 |  |
| 31–60 |  |
| 61–80 |  |
| 81–100 |  |

---

# 24. Lab Task 6 — Evaluation Metrics for IDS

A network intrusion detector is tested on 5,000 network flows.

Dataset:

```text
4,500 benign flows
500 attack flows
```

Model output:

```text
420 attack flows correctly detected
80 attack flows missed
300 benign flows wrongly flagged as attacks
4,200 benign flows correctly ignored
```

Complete the confusion matrix:

|  | Predicted Attack | Predicted Benign |
|---|---:|---:|
| Actually Attack |  |  |
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

Do not only calculate the metrics. Also answer:

1. Is the model more concerning because of false positives or false negatives?
2. What would happen if this model were deployed in a real SOC?
3. What threshold adjustment might be needed?
4. What additional evaluation would you request?

---

# 25. Lab Task 7 — Dataset Critique

Choose one of the following datasets:

- CIC-IDS2017
- CSE-CIC-IDS2018
- UNSW-NB15

Answer:

1. What type of network data does the dataset provide?
2. What attack categories are included?
3. What are the strengths of the dataset?
4. What are possible limitations?
5. Why might a model trained on this dataset fail in a real enterprise network?

Use the official dataset links in the Further Reading section.

---

# 26. Lab Deliverable

Submit a short worksheet containing:

1. Attack category identification table.
2. Feature extraction table.
3. AI problem framing table.
4. DDoS versus legitimate traffic analysis.
5. Simple DDoS risk score.
6. IDS evaluation metrics.
7. Dataset critique.

Recommended length:

```text
1000–1500 words
```

---

# 27. Exercises

## Exercise 1 — Concept Check

Answer briefly.

1. What is a network intrusion detection system?
2. What is the difference between signature-based and anomaly-based detection?
3. Why is high traffic not automatically a DDoS attack?
4. What is a network flow?
5. Give three useful features for DDoS detection.
6. Give three useful features for port scan detection.
7. Why can false positives be costly in IDS?
8. Why can false negatives be dangerous in IDS?
9. Why is concept drift a problem for IDS?
10. Why may encrypted traffic make detection harder?

---

## Exercise 2 — Short Analytical Answer

Write 250–300 words.

**Question:**  
Why might a machine learning model trained on a public intrusion detection dataset perform poorly in a real enterprise network?

Your answer should discuss at least four of the following:

- Dataset bias
- Artificial traffic
- Outdated attack patterns
- Label noise
- Class imbalance
- Encrypted traffic
- Different network architecture
- Different user behaviour
- Concept drift
- Adversarial adaptation

---

## Exercise 3 — Feature Design

For each attack type, propose four useful features.

| Attack Type | Feature 1 | Feature 2 | Feature 3 | Feature 4 |
|---|---|---|---|---|
| Port scan |  |  |  |  |
| SYN flood |  |  |  |  |
| Application-layer DDoS |  |  |  |  |
| Botnet C2 |  |  |  |  |
| Data exfiltration |  |  |  |  |

---

## Exercise 4 — Case Analysis

Read the case:

```text
An internal host sends 2 GB of outbound traffic to a new external IP address at 02:30.
The host is a database server.
The destination IP is not on a known malicious list.
No scheduled backup is recorded.
The traffic is encrypted.
```

Answer:

1. Which features would you extract?
2. What benign explanations are possible?
3. What malicious explanations are possible?
4. Which AI framing would you choose?
5. What additional context is needed?
6. What would be a proportionate response?

---

## Exercise 5 — Evaluation Reflection

A DDoS detector has:

```text
Accuracy: 98%
Recall: 52%
Precision: 91%
```

Answer:

1. Why might this model still be unacceptable?
2. What does low recall mean in this case?
3. What operational harm may result?
4. What could be adjusted to improve recall?
5. What trade-off might occur if recall is improved?

---

## Exercise 6 — Explainability Practice

Rewrite the following poor IDS alert into an analyst-friendly explanation.

Poor alert:

```text
Attack probability: 91%
Prediction: DDoS
```

Your explanation should include:

- Risk-increasing evidence
- Risk-reducing evidence
- Missing evidence
- Suggested next step
- Whether immediate blocking is justified

---

# 28. Further Reading

## Core Reading

1. **MITRE ATT&CK: Network Denial of Service**  
   Useful for understanding denial-of-service behaviour as an adversary technique.  
   <https://attack.mitre.org/techniques/T1498/>

2. **MITRE ATT&CK: Direct Network Flood**  
   Useful for understanding direct flood behaviour.  
   <https://attack.mitre.org/techniques/T1498/001/>

3. **MITRE ATT&CK: Reflection Amplification**  
   Useful for understanding reflection and amplification attacks.  
   <https://attack.mitre.org/techniques/T1498/002/>

4. **CIC-IDS2017 Dataset**  
   Useful for learning about labelled intrusion detection data with PCAPs and flow features.  
   <https://www.unb.ca/cic/datasets/ids-2017.html>

5. **CSE-CIC-IDS2018 Dataset**  
   Useful for studying modern labelled intrusion detection scenarios and extracted flow features.  
   <https://www.unb.ca/cic/datasets/ids-2018.html>

6. **UNSW-NB15 Dataset**  
   Useful for studying network intrusion detection data with multiple attack categories.  
   <https://research.unsw.edu.au/projects/unsw-nb15-dataset>

7. **CICFlowMeter**  
   Useful for understanding how network flows can be extracted from packet captures.  
   <https://www.unb.ca/cic/research/applications.html>

---

## Suggested Search Topics

Search for recent academic or technical material on:

- Machine learning for network intrusion detection
- DDoS detection using flow features
- Application-layer DDoS detection
- Botnet command-and-control detection
- Concept drift in intrusion detection systems
- Explainable AI for intrusion detection
- Adversarial machine learning for IDS
- Encrypted traffic classification
- Network flow feature engineering
- Dataset bias in intrusion detection

---

# 29. Week 2 Summary

This week focused on AI for network intrusion and DDoS detection.

The most important lessons are:

```text
Network intrusion detection is a security decision problem, not only a classification problem.

DDoS detection requires context, not only traffic volume.

Network data can be represented at packet, flow, and log levels.

Feature engineering is critical for IDS performance.

Classification, anomaly detection, and risk scoring are all useful framings.

Public datasets are useful for learning but limited for real-world deployment.

Evaluation must consider false positives, false negatives, detection latency, and operational cost.

Attackers adapt, so IDS models must be monitored, updated, and interpreted carefully.
```

Final takeaway:

> A strong AI-based IDS is not simply the model with the highest accuracy.  
> It is the system that detects meaningful threats, reduces operational noise, and supports timely, explainable, and proportionate security decisions.
