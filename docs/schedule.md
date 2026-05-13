---
title: "Schedule"
layout: default
nav_order: 3
permalink: "/schedule/"
---

# Course Schedule

## Applied AI for Cybersecurity

This page provides the week-by-week structure for the module.

The module is organised as a **12-week Level 6 course**. It begins with foundations and cybersecurity data engineering, moves through applied AI use cases, and then develops toward explainability, LLMs, trustworthy AI, adversarial risk, deployment, monitoring, and governance.

---

## Weekly Schedule

| Week | Topic | Main Focus | Practical / Academic Emphasis | Lecture Notes |
|---:|---|---|---|---|
| 1 | Introduction to Applied AI for Cybersecurity | Security data, features, labels, models, predictions, decisions, and evaluation | Building a shared conceptual foundation for the module | [Week 1](../lectures/week01/) |
| 2 | Cybersecurity Data Engineering and Feature Design | Raw logs, normalisation, cleaning, enrichment, feature extraction, labels, leakage, splitting | Preparing AI-ready cybersecurity datasets | [Week 2](../lectures/week02/) |
| 3 | AI for Network Intrusion and DDoS Detection | Flow data, packet data, IDS, anomaly detection, DDoS, botnet traffic, port scanning | Applying AI to network attack detection and availability threats | [Week 3](../lectures/week03/) |
| 4 | AI for Malware, Phishing, and Malicious URL Detection | Static, dynamic, behavioural, email, URL, file, and artefact-based detection | Classifying malicious artefacts and analysing feature evidence | [Week 4](../lectures/week04/) |
| 5 | Deep Learning for Cybersecurity | MLPs, CNNs, sequence models, autoencoders, transformers, embeddings, GNNs | Matching cybersecurity data types to deep learning architectures | [Week 5](../lectures/week05/) |
| 6 | Explainable AI for Cybersecurity | Local/global explanations, feature importance, LIME, SHAP, counterfactuals, explanation risk | Turning model outputs into analyst-ready explanations | [Week 6](../lectures/week06/) |
| 7 | AI for Security Operations and Threat Intelligence | SIEM, SOAR, alert triage, incident prioritisation, threat intelligence, ATT&CK mapping | Moving from alerts to prioritised security decisions | [Week 7](../lectures/week07/) |
| 8 | Large Language Models for Cybersecurity | LLM-assisted analysis, RAG, alert summarisation, threat intelligence, prompt injection, safe prompting | Using LLMs as constrained analyst-support tools | [Week 8](../lectures/week08/) |
| 9 | AI for Vulnerability Management and Secure Software Engineering | CVE, CVSS, exploitability, asset risk, secure code review, dependency and supply-chain risk | Prioritising remediation and supporting secure development | [Week 9](../lectures/week09/) |
| 10 | AI for Cloud, IoT, and Cyber-Physical Security | Cloud IAM/API logs, IoT anomaly detection, edge detection, OT/CPS safety-aware monitoring | Applying AI in distributed and safety-critical environments | [Week 10](../lectures/week10/) |
| 11 | Trustworthy and Adversarial AI for Cybersecurity | Evasion, poisoning, backdoors, extraction, privacy attacks, federated learning, differential privacy | Securing AI systems used for cyber defence | [Week 11](../lectures/week11/) |
| 12 | SecMLOps, Deployment, Monitoring, and Final Integration | MLOps, SecMLOps, versioning, drift, feedback loops, rollback, governance | Moving from model prototype to governed security system | [Week 12](../lectures/week12/) |

---

## Weekly Breakdown

### Week 1 — Introduction to Applied AI for Cybersecurity

**Lecture focus**

- What “Applied AI for Cybersecurity” means
- Cybersecurity tasks that can be framed as data-driven problems
- Security data, features, labels, models, predictions, and decisions
- Classification, anomaly detection, and risk scoring
- False positives, false negatives, precision, recall, F1-score, and accuracy limitations
- Why AI predictions are not the same as security decisions

**Lab / workshop**

- Identify cybersecurity domains from simplified security observations
- Extract possible features from events, emails, URLs, files, and logs
- Assign tentative labels and discuss uncertainty
- Calculate basic evaluation metrics
- Reflect on why accuracy alone is not enough

**Independent study**

- Review the difference between data, features, labels, predictions, and decisions
- Prepare short notes on one cybersecurity task that could be supported by AI
- Reflect on where AI should and should not be trusted in cyber defence

---

### Week 2 — Cybersecurity Data Engineering and Feature Design

**Lecture focus**

- Security data sources: logs, flows, packets, emails, files, cloud logs, endpoint telemetry
- Raw data, normalised data, features, labels, and datasets
- Data cleaning, missing values, duplicate records, inconsistent formats, and timestamp issues
- Time-window aggregation and behavioural feature design
- Weak labels, noisy labels, delayed labels, and class imbalance
- Train/test splitting, time-based splitting, and dataset leakage
- Dataset documentation and responsible data handling

**Lab / workshop**

- Convert simplified raw security observations into normalised fields
- Design features for account compromise, DDoS/API abuse, and endpoint malware behaviour
- Identify missing values and propose handling strategies
- Assign tentative labels with confidence levels
- Identify data leakage risks
- Propose a suitable train/test split strategy

**Independent study**

- Read about security log management and security data sources
- Prepare a short dataset documentation note for a hypothetical cybersecurity dataset
- Review why data leakage can make model performance unrealistic

---

### Week 3 — AI for Network Intrusion and DDoS Detection

**Lecture focus**

- Network intrusion detection and network security monitoring
- Packet-level, flow-level, and log-level data
- Signature-based, anomaly-based, and ML-based detection
- Port scanning, brute-force attacks, botnet traffic, data exfiltration, and DDoS
- DDoS types: volumetric, protocol, application-layer, reflection/amplification, low-and-slow
- Network flow features and temporal features
- Public IDS datasets and their limitations
- IDS evaluation beyond accuracy

**Lab / workshop**

- Classify simplified network events by likely attack category
- Extract network and application-level features
- Choose appropriate AI framing: classification, anomaly detection, risk scoring, or review
- Analyse DDoS versus legitimate traffic surge
- Design a simple DDoS risk score
- Calculate IDS evaluation metrics and discuss operational impact

**Independent study**

- Review one public intrusion detection dataset
- Reflect on why high traffic is not automatically a DDoS attack
- Prepare short notes on false positives and false negatives in IDS

---

### Week 4 — AI for Malware, Phishing, and Malicious URL Detection

**Lecture focus**

- Malware types and common malicious artefacts
- Static, dynamic, and behavioural malware analysis
- File features: entropy, imports, strings, digital signatures, packers
- Phishing email features: sender, subject, body, links, attachments, urgency language
- Malicious URL features: lexical, host-based, content-based, reputation-based
- Obfuscation, packing, redirects, domain rotation, and evasion
- Public resources such as EMBER, PhishTank, and URLhaus
- Evaluation issues in artefact-based detection

**Lab / workshop**

- Analyse simplified suspicious emails, URLs, files, and endpoint behaviours
- Identify detection domain and extract features
- Assign tentative labels and identify uncertainty
- Choose suitable AI problem framing
- Design explainable risk scores
- Analyse false positive and false negative costs
- Critique malware/phishing/URL datasets

**Independent study**

- Read about phishing and malicious URL intelligence sources
- Prepare short notes on static versus dynamic analysis
- Reflect on why HTTPS does not prove that a website is safe

---

### Week 5 — Deep Learning for Cybersecurity

**Lecture focus**

- Difference between classical machine learning and deep learning
- Representation learning for cybersecurity data
- Multi-layer perceptrons for structured security features
- CNNs for malware images, byte sequences, and local patterns
- RNNs, LSTMs, and GRUs for event and system-call sequences
- Autoencoders for anomaly detection
- Transformers for logs, emails, sequences, and threat reports
- Embeddings for URLs, commands, files, users, hosts, and entities
- Graph neural networks for security relationships and alert correlation
- Overfitting, generalisation, explainability, and adversarial risks

**Lab / workshop**

- Match cybersecurity data types to suitable deep learning architectures
- Design input representations for URLs, logs, binaries, flows, and graphs
- Compare deep learning choices with classical ML baselines
- Identify risks such as overfitting, weak explainability, and adversarial evasion
- Design an evaluation plan for a deep learning cybersecurity use case

**Independent study**

- Review basic neural network concepts
- Compare one deep learning approach with a classical baseline for a cybersecurity task
- Reflect on when deep learning is justified and when it is unnecessary

---

### Week 6 — Explainable AI for Cybersecurity

**Lecture focus**

- Why cybersecurity AI needs explanations, not only scores
- Interpretability, explainability, transparency, and accountability
- Local and global explanations
- Feature importance and surrogate models
- LIME and SHAP
- Counterfactual explanations
- Rule-based and example-based explanations
- Analyst-centred explanation design
- Explanation quality criteria
- Explanation risks and information leakage

**Lab / workshop**

- Analyse poor AI outputs and identify what is missing
- Rewrite AI outputs into analyst-friendly explanations
- Distinguish local and global explanation needs
- Evaluate explanation quality using security criteria
- Analyse when explanations may help attackers
- Design reusable explanation templates for security tools

**Independent study**

- Read introductory material on LIME, SHAP, and trustworthy AI
- Prepare short examples of good and poor cybersecurity explanations
- Reflect on why different audiences need different explanation levels

---

### Week 7 — AI for Security Operations and Threat Intelligence

**Lecture focus**

- Events, alerts, incidents, and cases
- SIEM and SOAR concepts
- Security operations workflow
- Alert triage, deduplication, grouping, and prioritisation
- Weak signal correlation
- Threat intelligence enrichment
- MITRE ATT&CK mapping
- Human-in-the-loop incident response
- Automation boundaries and operational risk

**Lab / workshop**

- Classify items as events, alerts, context, or threat intelligence
- Group related alerts into possible incidents
- Add context and revise interpretations
- Map evidence to attacker behaviour
- Design a simple incident prioritisation score
- Define response and automation boundaries
- Write analyst-friendly incident summaries

**Independent study**

- Review SIEM, SOAR, and MITRE ATT&CK concepts
- Prepare short notes on the difference between threat intelligence evidence and proof
- Reflect on which SOC actions should require human approval

---

### Week 8 — Large Language Models for Cybersecurity

**Lecture focus**

- LLM use cases in cybersecurity
- LLM-assisted alert summarisation
- Threat intelligence summarisation
- Phishing analysis
- Secure code review assistance
- Security query generation
- Retrieval-augmented generation for cybersecurity knowledge
- Hallucination, prompt injection, data leakage, insecure output handling, and excessive agency
- Safe prompting and human validation

**Lab / workshop**

- Identify LLM use cases and associated risks
- Design safe prompts for cybersecurity analysis
- Analyse a prompt-injection example
- Design a RAG workflow for an internal incident response assistant
- Define automation boundaries for LLM-supported actions
- Rewrite unsafe LLM output into safer analyst-facing output

**Independent study**

- Review OWASP guidance on LLM application risks
- Prepare a short safe-prompting checklist
- Reflect on why LLMs should assist analysts rather than act autonomously

---

### Week 9 — AI for Vulnerability Management and Secure Software Engineering

**Lecture focus**

- Vulnerability management and remediation prioritisation
- CVE, CVSS, exploitability, exposure, and asset criticality
- Known exploited vulnerabilities
- AI-assisted vulnerability ranking and exploit prediction
- Secure code review and AI-supported detection of insecure patterns
- Dependency risk and software supply-chain security
- Secure by Design and Secure Software Development Framework concepts
- False positives and false negatives in code security tools

**Lab / workshop**

- Prioritise vulnerabilities using severity, exposure, exploitability, and business context
- Design a risk-scoring model for remediation priority
- Analyse simplified secure code findings
- Discuss false positive and false negative costs
- Design an AI-assisted secure development workflow

**Independent study**

- Review CVE, CVSS, and known exploited vulnerability resources
- Prepare short notes on why CVSS alone is insufficient
- Reflect on how AI can support, but not replace, secure engineering practice

---

### Week 10 — AI for Cloud, IoT, and Cyber-Physical Security

**Lecture focus**

- Cloud security telemetry: IAM logs, API logs, storage logs, configuration data
- Cloud anomaly detection and cloud misuse scenarios
- IoT device monitoring and anomaly detection
- Edge inference and federated detection
- Cyber-physical systems and operational technology
- Sensor anomalies, actuator commands, PLC logs, and process data
- Safety-aware security decisions
- MITRE ATT&CK for ICS
- False positives and false negatives in safety-critical environments

**Lab / workshop**

- Analyse distributed security scenarios across cloud, IoT, and CPS
- Identify data sources and security domains
- Design features for selected scenarios
- Distinguish attack, fault, and operational-change explanations
- Choose appropriate AI framing
- Define safe response boundaries
- Write safety-aware explanations

**Independent study**

- Review NIST guidance on IoT and OT security
- Prepare short notes on why CPS security requires safety-aware AI
- Reflect on why anomaly does not automatically mean attack

---

### Week 11 — Trustworthy and Adversarial AI for Cybersecurity

**Lecture focus**

- Trustworthy AI in cybersecurity
- AI systems as attack surfaces
- Threat modelling for AI-based cyber defence
- Evasion attacks and adversarial examples
- Poisoning attacks and feedback-loop risks
- Backdoor attacks
- Model extraction
- Model inversion and membership inference
- Prompt injection as an LLM-specific adversarial risk
- Privacy-preserving AI, federated learning, differential privacy, and secure aggregation
- Robustness, governance, and human oversight

**Lab / workshop**

- Choose an AI cybersecurity system and identify assets
- Identify adversaries and attack goals
- Analyse evasion, poisoning, extraction, privacy, and automation risks
- Propose technical and governance controls
- Conduct a privacy review
- Define human oversight boundaries
- Write a trustworthy AI risk review summary

**Independent study**

- Review MITRE ATLAS, NIST AI RMF, and OWASP ML/LLM security resources
- Prepare short notes on one adversarial AI risk
- Reflect on whether a highly accurate model can still be untrustworthy

---

### Week 12 — SecMLOps, Deployment, Monitoring, and Final Integration

**Lecture focus**

- Difference between model prototype and operational security system
- MLOps and SecMLOps
- Secure ML lifecycle
- Dataset, feature, and model versioning
- Production monitoring and audit logs
- Data drift, concept drift, and detection drift
- Human feedback loops and retraining governance
- Rollback planning
- Deployment readiness review
- Final project integration

**Lab / workshop**

- Review an AI phishing detector deployment proposal
- Identify deployment risks and mitigations
- Design monitoring metrics
- Write a rollback plan
- Define human oversight boundaries
- Produce a final deployment recommendation

**Independent study**

- Consolidate final project or report
- Review deployment readiness and governance criteria
- Prepare final reflection on responsible AI-enabled cyber defence

---

## Suggested Study Rhythm

A typical week may follow this pattern:

- **Before class:** short reading and concept preparation
- **Lecture:** core technical and conceptual material
- **Lab:** practical exercise, case analysis, or guided design task
- **Seminar / discussion:** critique, reflection, and interpretation
- **After class:** worksheet completion, short reflection, and follow-up reading

---

## Assessment Mapping by Week

| Week | Learning Contribution | Assessment Relevance |
|---:|---|---|
| 1 | Problem framing, AI pipeline, and evaluation foundations | Portfolio foundation and report introduction |
| 2 | Data preparation, feature design, labelling, leakage, and splitting | Portfolio and data-methodology section |
| 3 | Network intrusion and DDoS detection | Portfolio and possible final case study |
| 4 | Malware, phishing, and malicious URL detection | Portfolio and possible final case study |
| 5 | Deep learning design choices and architecture selection | Method comparison and critical evaluation |
| 6 | Explainable AI and analyst-ready evidence | Explanation plan and deployment recommendation |
| 7 | Security operations, alert triage, and threat intelligence | SOC-oriented case analysis and workflow design |
| 8 | LLM-assisted cybersecurity and LLM-specific risks | Responsible AI and GenAI critique |
| 9 | Vulnerability management and secure software engineering | Secure development and remediation case study |
| 10 | Cloud, IoT, and cyber-physical security | Distributed and safety-critical AI analysis |
| 11 | Trustworthy and adversarial AI | Adversarial risk section and governance analysis |
| 12 | SecMLOps, monitoring, rollback, and final integration | Final deployment recommendation and conclusion |

---

## Notes for Course Website Development

This schedule page is designed to work with a GitHub Pages course site.

The recommended lecture file structure is:

```text
lectures/
├── week1.md
├── week2.md
├── week3.md
├── week4.md
├── week5.md
├── week6.md
├── week7.md
├── week8.md
├── week9.md
├── week10.md
├── week11.md
└── week12.md
