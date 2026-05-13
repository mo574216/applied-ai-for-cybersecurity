---
title: "Week 10: AI for Cloud, IoT, and Cyber-Physical Security"
layout: default
permalink: /lectures/week10/
---

# Week 10: AI for Cloud, IoT, and Cyber-Physical Security
## From Distributed Telemetry to Context-Aware Detection

Welcome to Week 10 of **Applied AI for Cybersecurity**.

This week focuses on environments where cybersecurity data is distributed, heterogeneous, resource-constrained, and sometimes tied to physical processes:

- cloud platforms
- Internet of Things devices
- edge systems
- operational technology
- industrial control systems
- cyber-physical systems

The main question is:

> How can AI support security in distributed, cloud-connected, resource-constrained, and safety-critical environments?

The central lesson is:

> AI-based security in cloud, IoT, and cyber-physical systems must consider context, resource constraints, safety, privacy, and operational continuity.

---

# 1. Learning Objectives

By the end of this week, you should be able to:

1. Identify cloud, IoT, and cyber-physical security data sources.
2. Explain how AI can detect abnormal cloud IAM, API, and storage activity.
3. Design useful features for IoT anomaly detection.
4. Distinguish cyberattacks from device faults and operational changes.
5. Explain why cyber-physical systems require safety-aware security decisions.
6. Discuss edge-based and federated detection.
7. Explain why resource constraints matter for IoT security AI.
8. Identify risks of false positives and false negatives in cloud, IoT, and CPS.
9. Apply ATT&CK or ATT&CK for ICS concepts to detection reasoning.
10. Design a responsible AI-based monitoring approach for a cloud, IoT, or CPS scenario.

---

# 2. Why These Domains Matter

Cloud, IoT, and CPS environments change the security problem.

Cloud systems involve API-driven infrastructure, identity and access management, storage permissions, virtual machines, containers, and serverless functions.

IoT systems involve sensors, constrained devices, firmware, gateways, wireless communication, and cloud backends.

Cyber-physical systems connect digital control with physical processes. Examples include power systems, water treatment plants, manufacturing systems, smart buildings, transport systems, and medical devices.

In these environments, AI errors can have operational or physical consequences.

---

# 3. AI for Cloud Security

Cloud platforms generate rich telemetry.

| Cloud Data Source | Example |
|---|---|
| IAM logs | user, role, permission, login event |
| API logs | create VM, delete object, change policy |
| Storage logs | bucket access, file download, policy change |
| Network logs | flow logs, security group changes |
| Container logs | image pull, privilege use, container start |
| Serverless logs | function invocation and errors |
| Configuration data | public bucket, open port, weak policy |
| Asset inventory | service owner, region, criticality |

Common cloud threats:

- compromised access keys
- excessive permissions
- public storage exposure
- unusual region usage
- suspicious IAM policy changes
- data exfiltration from storage
- cryptomining in cloud instances
- container misuse
- insecure API usage
- misconfigured security groups

Useful features:

| Feature | Security Use |
|---|---|
| new_region_flag | unusual location or region |
| api_call_frequency | abnormal automation |
| privilege_escalation_action | risky IAM behaviour |
| public_bucket_flag | storage exposure |
| storage_download_volume | possible exfiltration |
| unusual_service_creation | cryptomining or misuse |
| access_key_age | stale or risky credential |
| failed_api_call_rate | probing or misuse |
| role_change_count | privilege manipulation |
| baseline_deviation_score | behavioural anomaly |

---

# 4. Case Study 1: Suspicious Cloud Access Key

## Scenario

```text
02:30 — access key used from new region
02:32 — list storage buckets
02:34 — change bucket policy
02:38 — download 12 GB from sensitive bucket
02:40 — create new compute instance
```

## Security Question

Is this legitimate administration or compromised credential activity?

Risk-increasing evidence:

- new region
- unusual time
- sensitive bucket download
- policy change
- new compute instance
- high data volume

Risk-reducing evidence may include:

- approved maintenance window
- known administrator
- valid change ticket
- expected migration or backup

AI framing:

```text
risk scoring
anomaly detection
sequence modelling
human-in-the-loop review
```

---

# 5. AI for IoT Security

IoT devices are often limited in CPU, memory, power, storage, and logging capability. They may also be difficult to patch.

AI can support:

- device anomaly detection
- botnet detection
- abnormal traffic detection
- firmware behaviour monitoring
- compromised device identification
- gateway-level detection
- edge-based monitoring

NIST’s Cybersecurity for IoT program supports standards, guidance, and tools for improving cybersecurity of IoT systems, connected products, and their environments.

---

# 6. IoT Data and Features

| Data Source | Example Features |
|---|---|
| Device traffic | packet rate, byte rate, destination count |
| Device behaviour | reporting interval, firmware version |
| Sensor readings | temperature, pressure, vibration |
| Gateway logs | device ID, connection time, protocol |
| Firmware metadata | version, signature, update time |
| Authentication logs | failed authentication, device identity |
| Cloud backend logs | API calls, message rate, topic usage |

Example features:

```text
message_rate
connection_interval
unique_destination_count
firmware_version
failed_auth_count
protocol_type
sensor_value_deviation
battery_drain_rate
reboot_frequency
```

---

# 7. Case Study 2: Compromised IoT Camera

## Scenario

A smart camera normally sends small periodic messages to a cloud service.

Observed behaviour:

```text
traffic volume increases
connections to many external IPs
DNS queries to rare domains
device reboots frequently
firmware version is outdated
```

Possible interpretations:

- compromised device
- firmware bug
- failed update
- misconfiguration
- botnet participation
- network change

AI framing:

```text
anomaly detection
risk scoring
gateway-level monitoring
```

Main lesson:

> IoT anomaly detection must distinguish attack behaviour from faults, updates, and environmental changes.

---

# 8. Edge-Based and Federated Detection

IoT and edge environments may not be able to send all raw data to a central cloud.

Reasons:

- bandwidth limits
- latency constraints
- privacy concerns
- intermittent connectivity
- local autonomy
- regulatory constraints

Approaches:

| Approach | Description |
|---|---|
| Edge inference | Run detection model near devices |
| Cloud training | Train centrally, deploy to edge |
| Federated learning | Train collaboratively without sharing raw data |
| Gateway aggregation | Collect local device telemetry |
| Hybrid detection | Local detection plus cloud correlation |

Federated learning may help privacy, but it also introduces risks such as poisoned updates, heterogeneous devices, and communication cost.

---

# 9. AI for Cyber-Physical and OT Security

Operational Technology, or OT, includes systems that monitor or control physical processes. NIST SP 800-82 Rev. 3 provides guidance for securing OT while addressing performance, reliability, and safety requirements.

Examples:

- water treatment control
- power distribution
- manufacturing line
- building management
- industrial robots
- traffic control
- smart grid
- medical systems

Cyber-physical systems are different because cybersecurity decisions may affect safety.

A false positive may stop production or interrupt a critical process. A false negative may allow sabotage or unsafe operation.

---

# 10. CPS Data and Features

| Data Source | Example Features |
|---|---|
| Sensor readings | pressure, temperature, flow rate |
| Actuator commands | open valve, close valve, set speed |
| PLC logs | control logic events |
| Network traffic | protocol, timing, source, destination |
| Process historian | historical process values |
| Alarm logs | triggered alarms |
| Maintenance schedule | planned changes |
| Operator actions | manual overrides |

Important distinction:

```text
A sensor anomaly may be an attack, a sensor fault, maintenance, process disturbance, or environmental change.
```

---

# 11. Case Study 3: Water Treatment Anomaly

## Scenario

A water treatment plant observes:

```text
chlorine sensor readings change sharply
pump command sequence changes
network traffic to PLC increases
maintenance is scheduled later, not now
operator did not approve change
```

Possible explanations:

- sensor fault
- process disturbance
- unauthorised control command
- compromised engineering workstation
- malicious manipulation

AI framing:

```text
multivariate anomaly detection
sequence modelling
risk scoring
human-in-the-loop safety review
```

Main lesson:

> In CPS, AI detection must be connected to safety procedures and operator validation.

---

# 12. MITRE ATT&CK for ICS

MITRE ATT&CK for ICS provides tactics and techniques representing adversary behaviour in industrial control system environments.

Examples of ICS-relevant tactics include:

- initial access
- execution
- persistence
- evasion
- discovery
- lateral movement
- collection
- command and control
- inhibit response function
- impair process control
- impact

Mapping evidence to adversary behaviour can help analysts explain suspicious activity.

---

# 13. AI Risks in Cloud, IoT, and CPS

| Risk | Explanation |
|---|---|
| False positives | May disrupt services or physical processes |
| False negatives | May allow compromise or unsafe operation |
| Resource constraints | IoT devices may not support heavy models |
| Data gaps | Devices may have limited logging |
| Privacy | Sensor and location data may be sensitive |
| Concept drift | Device behaviour changes after updates |
| Safety impact | CPS responses can affect physical world |
| Heterogeneity | Devices and cloud services differ widely |
| Adversarial manipulation | Attackers may mimic normal behaviour |
| Governance | Multiple teams may own different components |

---

# 14. Week 10 Summary

```text
Cloud security AI uses IAM, API, storage, configuration, and network telemetry.
IoT security AI must handle constrained devices, limited logging, and device heterogeneity.
CPS and OT security require safety-aware decision-making.
Anomaly does not automatically mean attack.
Context is essential for distinguishing faults, maintenance, and malicious activity.
Edge and federated detection may reduce data movement but introduce new risks.
Human oversight is essential when AI outputs may affect physical processes or critical services.
```

Final takeaway:

> AI for cloud, IoT, and CPS security must be context-aware, safety-aware, resource-aware, and operationally responsible.

---

# 15. Lab Sheet 10: AI-Based Anomaly Detection in Cloud, IoT, and CPS

## Lab Overview

In this lab, you will analyse cloud, IoT, and CPS scenarios, design features, identify possible explanations, and define safe response boundaries.

## Lab Dataset A: Distributed Security Scenarios

| ID | Scenario |
|---|---|
| C1 | Cloud access key used from new region and downloads 12 GB |
| C2 | Cloud admin creates new privileged role outside working hours |
| C3 | IoT camera connects to many external IPs |
| C4 | Smart meter reports abnormal usage every 30 seconds |
| C5 | Sensor readings change sharply after firmware update |
| C6 | PLC receives commands from unusual workstation |
| C7 | Gateway observes repeated failed authentication from IoT devices |
| C8 | Public storage bucket is created accidentally |
| C9 | Industrial pump command sequence changes unexpectedly |
| C10 | Edge device stops sending telemetry |

## Lab Task 1 — Domain and Data Source

| ID | Domain | Data Sources Needed | Reason |
|---|---|---|---|
| C1 |  |  |  |
| C2 |  |  |  |
| C3 |  |  |  |
| C4 |  |  |  |
| C5 |  |  |  |
| C6 |  |  |  |
| C7 |  |  |  |
| C8 |  |  |  |
| C9 |  |  |  |
| C10 |  |  |  |

## Lab Task 2 — Feature Design

For three scenarios, design features.

| Scenario ID | Feature 1 | Feature 2 | Feature 3 | Feature 4 | Feature 5 |
|---|---|---|---|---|---|
|  |  |  |  |  |  |
|  |  |  |  |  |  |
|  |  |  |  |  |  |

## Lab Task 3 — Attack, Fault, or Operational Change?

| Scenario ID | Attack Explanation | Benign/Fault Explanation | Context Needed |
|---|---|---|---|
|  |  |  |  |
|  |  |  |  |
|  |  |  |  |

## Lab Task 4 — Choose AI Framing

Possible framings:

```text
classification
anomaly detection
risk scoring
sequence modelling
federated learning
edge inference
human-in-the-loop review
```

| Scenario ID | AI Framing | Reason |
|---|---|---|
| C1 |  |  |
| C2 |  |  |
| C3 |  |  |
| C4 |  |  |
| C5 |  |  |
| C6 |  |  |
| C7 |  |  |
| C8 |  |  |
| C9 |  |  |
| C10 |  |  |

## Lab Task 5 — Response Boundary

| Response Action | Automate / Approval / Prohibit | Reason |
|---|---|---|
| Send alert to analyst |  |  |
| Require cloud step-up authentication |  |  |
| Revoke cloud access key |  |  |
| Block IoT device network access |  |  |
| Shut down industrial pump |  |  |
| Trigger safety alarm |  |  |
| Collect more telemetry |  |  |
| Start incident ticket |  |  |

## Lab Task 6 — Safety-Aware Explanation

Rewrite this poor output:

```text
Anomaly detected. Stop process immediately.
```

Your improved explanation should include evidence, possible attack explanation, possible benign explanation, missing context, safety impact, recommended next step, and human approval requirement.

## Lab Deliverable

Submit a worksheet containing:

1. Domain and data source table.
2. Feature design table.
3. Attack/fault/operational-change analysis.
4. AI framing table.
5. Response boundary table.
6. Safety-aware explanation.

Recommended length:

```text
1200–1800 words
```

---

# 16. Exercises

## Exercise 1 — Concept Check

1. What makes cloud security data different from endpoint data?
2. Give five useful features for cloud anomaly detection.
3. Why are IoT devices difficult to monitor?
4. What is edge inference?
5. What is federated learning?
6. Why is CPS security safety-critical?
7. Why is anomaly not automatically attack?
8. What is MITRE ATT&CK for ICS?
9. Why can false positives be dangerous in OT?
10. Why is human approval essential in CPS response?

## Exercise 2 — Short Analytical Answer

Write 250–300 words:

**Question:** Why must AI-based security for cyber-physical systems consider safety as well as security?

## Exercise 3 — Feature Design

Propose features for:

- cloud account compromise
- IoT botnet detection
- sensor anomaly detection
- industrial control command anomaly
- public cloud storage exposure

## Exercise 4 — Case Analysis

Analyse a smart building system where HVAC sensor readings become abnormal after a software update. Discuss attack, fault, and benign explanations.

---

# 17. Further Reading

## Core Reading

1. **NIST Cybersecurity for IoT Program**  
   <https://www.nist.gov/itl/applied-cybersecurity/nist-cybersecurity-iot-program>

2. **NISTIR 8259 Series: IoT Cybersecurity Guidance**  
   <https://www.nist.gov/itl/applied-cybersecurity/nist-cybersecurity-iot-program/nistir-8259-series>

3. **NIST SP 800-82 Rev. 3: Guide to OT Security**  
   <https://csrc.nist.gov/pubs/sp/800/82/r3/final>

4. **MITRE ATT&CK for ICS Matrix**  
   <https://attack.mitre.org/matrices/ics/>

5. **MITRE ATT&CK Enterprise Matrix**  
   <https://attack.mitre.org/matrices/enterprise/>

6. **NIST SP 800-204C: DevSecOps for Cloud-Native Applications**  
   <https://csrc.nist.gov/pubs/sp/800/204/c/final>

## Suggested Search Topics

- AI for cloud security
- IAM anomaly detection
- AI for IoT botnet detection
- federated learning for IoT security
- AI for industrial control system security
- cyber-physical anomaly detection
- safety-aware cybersecurity
- edge AI for security monitoring
