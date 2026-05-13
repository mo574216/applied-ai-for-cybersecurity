---
title: "Syllabus"
layout: default
nav_order: 2
permalink: "/syllabus/"
---

# Applied AI for Cybersecurity

## Module Overview

This module introduces final-year undergraduate students to the practical, critical, and responsible use of artificial intelligence in cybersecurity. It focuses on how AI and machine learning can support real cyber defence tasks such as security data analysis, intrusion detection, DDoS detection, phishing detection, malware analysis, malicious URL detection, alert triage, threat intelligence, vulnerability prioritisation, secure software engineering, cloud security, IoT security, and cyber-physical system monitoring.

The module also examines the risks of using AI in cybersecurity. These include adversarial attacks against machine learning models, data poisoning, model evasion, model extraction, privacy leakage, prompt injection, unsafe automation, weak explainability, concept drift, and governance failures.

The module is designed as an applied and critical course rather than a purely theoretical machine learning course. Students will learn how to frame cybersecurity problems as data-driven tasks, prepare and evaluate cybersecurity datasets, design features, select appropriate AI methods, interpret model outputs, assess operational risk, and judge whether an AI-based cybersecurity solution is trustworthy enough for real deployment.

The course is suitable for Level 6 students with prior knowledge of basic cybersecurity, computer networking, and introductory programming.

---

## Module Aims

The module aims to:

1. develop students’ understanding of how AI is used in modern cybersecurity practice;
2. build practical skills in preparing, analysing, and modelling cybersecurity data;
3. enable students to apply and evaluate AI techniques for realistic cyber defence tasks;
4. develop students’ ability to design meaningful security features from raw cyber evidence;
5. introduce AI applications across network security, malware detection, phishing detection, security operations, vulnerability management, cloud security, IoT security, and cyber-physical security;
6. examine the security, privacy, reliability, and governance risks of AI-enabled cybersecurity systems;
7. strengthen students’ critical judgement on the responsible, explainable, and trustworthy deployment of AI in cybersecurity contexts.

---

## Learning Outcomes

By the end of the module, students should be able to:

1. **Explain** the main ways in which AI techniques are applied to cybersecurity problems.
2. **Prepare and analyse** cybersecurity datasets using appropriate preprocessing, feature design, labelling, and evaluation methods.
3. **Apply and compare** suitable AI or machine learning approaches for defined cybersecurity tasks.
4. **Evaluate critically** the effectiveness, limitations, and operational risks of AI-based cybersecurity systems.
5. **Explain and assess** attacks against AI systems, including evasion, poisoning, backdoors, model extraction, privacy attacks, and prompt injection.
6. **Design** explainable and human-in-the-loop AI-supported security workflows.
7. **Assess** the deployment readiness of AI-based cybersecurity systems using monitoring, governance, rollback, and risk-management criteria.
8. **Communicate** technical findings and deployment recommendations clearly in written, analytical, and practical forms.

---

## Indicative Prior Knowledge

Students are expected to have:

- basic knowledge of computer networks and cybersecurity concepts;
- introductory Python programming skills;
- familiarity with common data structures and basic statistics;
- basic understanding of security threats such as malware, phishing, network attacks, and access misuse;
- willingness to engage with practical lab activities, short technical readings, and critical discussion.

---

## Teaching Strategy

The module is delivered over **twelve teaching weeks** and combines:

- lectures for concepts, methods, case studies, and guided explanation;
- lab sessions for applied analysis, design tasks, model evaluation, and workflow critique;
- seminar-style discussion for critical analysis of tools, results, risks, and deployment decisions;
- directed independent study using readings, notebooks, datasets, security scenarios, and structured tasks.

The teaching approach emphasises applied understanding, evidence-based evaluation, and professional judgement rather than algorithm memorisation alone.

Students are expected to move progressively from foundational concepts to applied cybersecurity use cases, and then toward explainability, trustworthiness, deployment, monitoring, and governance.

---

## Assessment Strategy

A coursework-led assessment pattern is recommended for this module.

### Assessment 1 — Lab Portfolio and Reflective Notes (40%)

Students complete practical weekly tasks and submit a structured portfolio containing selected lab outputs, feature design tables, model evaluation results, risk analyses, explanations, and reflective comments.

The emphasis is on:

- correct problem framing;
- sound data and feature reasoning;
- appropriate use of evaluation metrics;
- interpretation of false positives and false negatives;
- awareness of uncertainty, context, and operational limitations;
- responsible use of AI-supported analysis.

### Assessment 2 — Applied AI Cybersecurity Case Study Report (60%)

Students produce an individual report in which they analyse a cybersecurity problem, design or evaluate an AI-enabled solution, discuss data and feature requirements, select appropriate methods, interpret results, assess adversarial and privacy risks, and make justified recommendations for deployment or improvement.

The report should include:

1. security problem definition;
2. threat model;
3. data sources and feature design;
4. AI method selection;
5. evaluation metrics;
6. false positive and false negative analysis;
7. explainability plan;
8. adversarial risk analysis;
9. privacy considerations;
10. human oversight and automation boundaries;
11. deployment and monitoring recommendations;
12. rollback or failure-handling considerations.

---

## Weekly Structure

The module is organised around twelve themes.

### Week 1 — Introduction to Applied AI for Cybersecurity

This week introduces the foundations of applying AI to cybersecurity. Students study how security problems are translated into AI problems, including security data, features, labels, models, predictions, decisions, and evaluation. The week also introduces core concepts such as classification, anomaly detection, risk scoring, false positives, false negatives, precision, recall, F1-score, and the limitations of accuracy.

**Main focus:** from security data to AI-driven decisions.

---

### Week 2 — Cybersecurity Data Engineering and Feature Design

This week focuses on the data layer of AI-based cybersecurity. Students study security data sources, raw logs, normalisation, cleaning, enrichment, feature extraction, missing values, labels, weak labels, class imbalance, time-window aggregation, train/test splitting, and data leakage.

**Main focus:** from raw security evidence to AI-ready data.

---

### Week 3 — AI for Network Intrusion and DDoS Detection

This week applies AI to network security. Students study packet-level, flow-level, and log-level data; signature-based and anomaly-based intrusion detection; port scanning; brute-force attacks; botnet communication; DDoS and application-layer DDoS; network flow features; and evaluation of intrusion detection systems.

**Main focus:** from network traffic to attack detection.

---

### Week 4 — AI for Malware, Phishing, and Malicious URL Detection

This week focuses on malicious artefact detection. Students study malware types, static analysis, dynamic analysis, behavioural analysis, phishing detection, malicious URL detection, URL lexical features, domain features, email features, file features, obfuscation, packing, redirects, and dataset limitations.

**Main focus:** from digital artefacts to threat classification.

---

### Week 5 — Deep Learning for Cybersecurity

This week introduces deep learning methods for cybersecurity. Students study multi-layer perceptrons, convolutional neural networks, sequence models, LSTMs, GRUs, autoencoders, transformers, embeddings, and graph neural networks. The week emphasises when deep learning is justified and when classical machine learning may be more appropriate.

**Main focus:** from handcrafted features to learned representations.

---

### Week 6 — Explainable AI for Cybersecurity

This week focuses on explainability and analyst-ready evidence. Students study interpretability, explainability, transparency, accountability, local and global explanations, feature importance, surrogate models, LIME, SHAP, counterfactual explanations, rule-based explanations, example-based explanations, and explanation risks.

**Main focus:** from model scores to analyst-ready explanations.

---

### Week 7 — AI for Security Operations and Threat Intelligence

This week focuses on operational cybersecurity. Students study events, alerts, incidents, cases, SIEM, SOAR, alert triage, alert grouping, incident prioritisation, weak signal correlation, threat intelligence enrichment, MITRE ATT&CK mapping, and human-in-the-loop response.

**Main focus:** from alerts to prioritised security decisions.

---

### Week 8 — Large Language Models for Cybersecurity

This week examines LLM applications and risks in cybersecurity. Students study LLM-assisted alert summarisation, threat intelligence summarisation, phishing analysis, secure code review, query generation, retrieval-augmented generation, hallucination, prompt injection, sensitive data leakage, insecure output handling, excessive agency, and safe prompting.

**Main focus:** from security text to assisted cyber defence.

---

### Week 9 — AI for Vulnerability Management and Secure Software Engineering

This week applies AI to vulnerability management and secure software development. Students study vulnerability prioritisation, CVE, CVSS, exploitability, asset criticality, known exploited vulnerabilities, secure code review, dependency risk, software supply-chain security, Secure by Design, and the Secure Software Development Framework.

**Main focus:** from vulnerability lists to risk-based remediation.

---

### Week 10 — AI for Cloud, IoT, and Cyber-Physical Security

This week focuses on distributed, resource-constrained, and safety-critical environments. Students study cloud IAM and API telemetry, cloud anomaly detection, IoT device behaviour, edge detection, federated detection, cyber-physical systems, operational technology, industrial control systems, sensor anomalies, safety-aware response, and MITRE ATT&CK for ICS.

**Main focus:** from distributed telemetry to context-aware detection.

---

### Week 11 — Trustworthy and Adversarial AI for Cybersecurity

This week focuses on how AI-based cybersecurity systems can fail or be attacked. Students study trustworthy AI, threat modelling for AI systems, evasion attacks, adversarial examples, poisoning attacks, backdoors, model extraction, model inversion, membership inference, prompt injection, privacy-preserving AI, federated learning, differential privacy, secure aggregation, robustness, and governance.

**Main focus:** securing AI systems used for cyber defence.

---

### Week 12 — SecMLOps, Deployment, Monitoring, and Final Integration

This week brings the module together by focusing on deployment and lifecycle management. Students study MLOps, SecMLOps, secure ML pipelines, model versioning, dataset versioning, feature pipeline monitoring, data drift, concept drift, detection drift, feedback loops, retraining governance, rollback planning, audit logs, deployment readiness, and final project integration.

**Main focus:** from model prototype to governed security system.

---

## Indicative Weekly Learning Pattern

Each week may include:

- **Lecture:** 2 hours
- **Lab / Workshop:** 2 hours
- **Seminar / Discussion:** 1 hour
- **Independent Study:** directed reading, lab completion, practical follow-up, and short reflection

The balance of activities may vary depending on the topic. Some weeks are more concept-heavy, while others involve more applied lab work and scenario analysis.

---

## Indicative Lab Themes

The module includes structured weekly lab activities. Indicative lab themes include:

| Week | Lab Theme |
|---:|---|
| 1 | From Security Data to AI Decisions |
| 2 | Building AI-Ready Cybersecurity Data |
| 3 | Network Intrusion and DDoS Detection |
| 4 | Malware, Phishing, and Malicious URL Detection |
| 5 | Designing Deep Learning Pipelines for Cybersecurity |
| 6 | Designing Analyst-Friendly Explanations |
| 7 | AI-Assisted Alert Triage and Threat Intelligence |
| 8 | Safe LLM-Assisted Cybersecurity Analysis |
| 9 | AI-Assisted Vulnerability Prioritisation and Secure Code Review |
| 10 | AI-Based Anomaly Detection in Cloud, IoT, and CPS |
| 11 | Threat Modelling an AI-Based Cybersecurity System |
| 12 | AI Cybersecurity System Deployment Review |

---

## Indicative Reading Themes

Students will engage with material in the following areas:

- AI and machine learning for cybersecurity;
- cybersecurity data engineering and feature design;
- AI for intrusion detection and DDoS detection;
- AI-assisted phishing, malware, and malicious URL detection;
- deep learning for security analytics;
- explainable AI for cybersecurity;
- SIEM, SOAR, threat intelligence, and alert triage;
- large language models for cybersecurity;
- AI for vulnerability management and secure software engineering;
- AI for cloud, IoT, and cyber-physical security;
- adversarial machine learning;
- privacy-preserving AI and federated learning;
- SecMLOps, deployment, monitoring, governance, and rollback.

A separate references page should be provided in the course website for detailed weekly readings and recommended sources.

---

## Software and Practical Environment

Indicative tools for practical work may include:

- Python
- Jupyter Notebook
- pandas
- NumPy
- scikit-learn
- matplotlib
- selected PyTorch or TensorFlow examples
- SHAP or LIME for explainability demonstrations
- Wireshark or packet/flow-based sample data tools
- selected open security datasets
- safe simulated security logs and alerts
- optional LLM interfaces or simulated prompt-based workflows for controlled classroom exercises

The module does not require students to run live attacks, execute malware, or interact with real unsafe URLs. All security examples should use safe, simulated, sanitised, or educational data.

---

## Professional and Academic Skills Developed

This module supports the development of:

- technical problem framing;
- cybersecurity data analysis;
- feature design and interpretation;
- model evaluation and comparison;
- critical assessment of false positives and false negatives;
- security-aware explanation design;
- adversarial and privacy risk analysis;
- evidence-based decision making;
- responsible use of AI tools;
- concise technical reporting;
- deployment-readiness assessment;
- professional judgement in AI-enabled cyber defence.

---

## Employability Relevance

The module prepares students for roles and pathways related to:

- security operations and SOC analysis;
- cyber threat analysis;
- security analytics and anomaly detection;
- AI-assisted security engineering;
- vulnerability management and secure software engineering;
- cloud and IoT security monitoring;
- cyber-physical system security analysis;
- machine learning security engineering;
- responsible deployment of data-driven cyber defence tools;
- further study in AI, cybersecurity, or applied data science.

---

## Academic Integrity and Responsible Use of AI

Students are expected to use AI tools responsibly and transparently. Any use of AI-assisted coding, text generation, data analysis, or analytical support in assessed work must comply with university regulations and module guidance.

Students must remain accountable for:

- the correctness of submitted work;
- the originality of analysis and interpretation;
- the validity of technical claims;
- the ethical use of data and AI tools;
- correct acknowledgement of sources and assistance;
- safe handling of cybersecurity examples and datasets.

Students must not use the module to develop, test, deploy, or assist real cyberattacks. All practical work must remain within authorised, safe, educational environments.

---

## Summary

Applied AI for Cybersecurity gives students a realistic, current, and critical understanding of how AI can support cyber defence. The module balances practical experimentation with reflective judgement, helping students understand not only what AI can do in cybersecurity, but also where it fails, how it can be attacked, how it should be explained, and how it should be evaluated before deployment.

The module’s central message is:

> AI should not be treated as an automatic security authority.  
> It should be treated as a decision-support technology that must be designed, evaluated, explained, monitored, and governed responsibly.
