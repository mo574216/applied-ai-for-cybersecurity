---
title: "Week 1 — Foundations of Applied AI for Cybersecurity"
layout: default
permalink: /lectures/week1/
---

# Week 1 — Foundations of Applied AI for Cybersecurity

## Overview

This lecture introduces the module by answering a practical question:

**Why is AI now a serious topic in cybersecurity, and why should security professionals treat it carefully rather than enthusiastically by default?**

The short answer is that cybersecurity generates large volumes of data, many defensive tasks involve pattern recognition under time pressure, and analysts increasingly need support for prioritisation, detection, triage, and interpretation. AI can help with these tasks, but it can also create false confidence, operational fragility, and new attack surfaces.

This week establishes the shared foundation for the rest of the course. It explains where AI fits into security operations, what kinds of cybersecurity problems are suitable for AI, what kinds of data are available, and why badly framed AI projects often fail.

---

## Learning Outcomes

By the end of this week, students should be able to:

1. explain the difference between AI, machine learning, deep learning, and generative AI in a cybersecurity context;
2. identify common cybersecurity tasks that can be framed as data-driven problems;
3. describe major categories of cybersecurity data used in AI-enabled workflows;
4. explain why problem framing, data quality, and evaluation matter more than model novelty in many security settings;
5. discuss major limitations of AI-based cybersecurity systems.

---

## 1. Why AI matters in cybersecurity

Cybersecurity teams work in environments that are:

- data-rich;
- time-sensitive;
- noisy;
- adversarial;
- operationally constrained.

A modern organisation may generate firewall logs, endpoint events, DNS records, web proxy logs, authentication records, cloud activity logs, vulnerability scan outputs, IDS alerts, email metadata, packet captures, and analyst investigation notes. Human analysts cannot manually interpret all of this at scale.

AI becomes attractive because it can support:

- classification of suspicious activity;
- anomaly detection in traffic or behaviour;
- ranking and prioritisation of alerts;
- clustering of related incidents;
- phishing and spam detection;
- malware family analysis;
- summarisation of threat reports and alerts;
- assistance with rule writing, triage, and investigation.

However, attraction is not the same as suitability. Some problems are genuinely well-suited to AI. Others are better solved by simpler rules, engineered detections, good logging, or improved processes.

---

## 2. AI, machine learning, deep learning, and generative AI

These terms are related but not identical.

### 2.1 Artificial Intelligence

Artificial intelligence is the broadest term. In this module, it refers to computational methods that support tasks usually associated with intelligent decision-making, such as pattern recognition, prediction, ranking, summarisation, or limited reasoning.

### 2.2 Machine Learning

Machine learning is a subset of AI in which systems learn patterns from data instead of relying only on hand-written rules.

Examples in cybersecurity include:

- classifying emails as phishing or benign;
- predicting whether a network flow is malicious;
- identifying likely false-positive alerts;
- grouping similar incidents for analyst review.

### 2.3 Deep Learning

Deep learning is a subset of machine learning that uses multi-layer neural networks and is often useful when data is complex, high-dimensional, or sequential.

Examples include:

- sequence modelling for logs;
- representation learning for malware features;
- deep models for packet or flow analysis;
- text models for phishing content or threat intelligence.

### 2.4 Generative AI

Generative AI refers to models that generate or transform content such as text, code, images, or structured summaries. In cybersecurity, large language models are the most visible example.

Possible uses include:

- summarising alerts;
- explaining logs in natural language;
- drafting detection rules;
- assisting analysts with investigation steps;
- helping developers reason about secure coding issues.

But generative models can hallucinate, leak sensitive content, or behave unsafely when integrated into operational pipelines.

---

## 3. Where AI fits in the security workflow

It is useful to think of cybersecurity work as a pipeline rather than a collection of isolated tools.

A simplified defensive workflow often includes:

1. **data collection**  
   gathering logs, telemetry, packets, endpoint events, and intelligence;

2. **normalisation and preprocessing**  
   cleaning, structuring, deduplicating, and aligning data;

3. **analysis and detection**  
   rules, correlation, machine learning, anomaly detection, or hybrid methods;

4. **prioritisation and triage**  
   deciding what deserves analyst attention;

5. **investigation and interpretation**  
   understanding what happened, whether it is malicious, and what to do next;

6. **response and learning**  
   containment, recovery, reporting, and improvement of future detections.

AI can support several of these steps, especially steps 3 to 5. It should usually be treated as a component of the workflow, not the whole workflow.

A poor AI design often fails because it ignores the surrounding system. A model that performs well in a notebook may still be useless if:

- the data is not available in real time;
- labels are poor or inconsistent;
- false positives overwhelm analysts;
- the environment changes after deployment;
- the output is not interpretable enough for action.

---

## 4. Types of cybersecurity data

Students should understand that “cyber data” is not a single thing. Different sources have different structures, time properties, and limitations.

### 4.1 Network traffic and flow data

Examples:

- packet captures;
- NetFlow or IPFIX-style summaries;
- connection metadata;
- protocol features.

Common use cases:

- intrusion detection;
- DDoS detection;
- protocol misuse detection;
- anomaly detection;
- encrypted traffic analysis based on metadata.

### 4.2 Log data

Examples:

- authentication logs;
- operating system logs;
- server and application logs;
- firewall and proxy logs;
- cloud audit trails.

Common use cases:

- suspicious login detection;
- privilege misuse detection;
- incident reconstruction;
- attack sequence analysis.

### 4.3 Endpoint and host data

Examples:

- process creation events;
- registry changes;
- file access patterns;
- memory indicators;
- endpoint detection and response telemetry.

Common use cases:

- malware detection;
- lateral movement analysis;
- insider threat monitoring;
- endpoint anomaly detection.

### 4.4 Email and web data

Examples:

- email headers;
- URLs;
- message metadata;
- domain features;
- webpage characteristics.

Common use cases:

- phishing detection;
- malicious URL classification;
- spam filtering;
- campaign clustering.

### 4.5 Textual and intelligence data

Examples:

- analyst notes;
- threat reports;
- vulnerability descriptions;
- incident summaries;
- ticketing system content.

Common use cases:

- summarisation;
- information extraction;
- relation mapping;
- support for analyst decision-making.

---

## 5. Framing cyber tasks as AI problems

One of the most important skills in this module is not “coding a model” but **framing the problem correctly**.

A cybersecurity task can often be framed in different ways.

### Example: suspicious login detection

Possible framings:

- **binary classification**: suspicious vs benign;
- **anomaly detection**: how unusual is this login relative to normal behaviour?;
- **ranking**: which logins should analysts investigate first?;
- **clustering**: are several suspicious logins part of the same campaign?;
- **summarisation**: can the system produce a concise explanation for the analyst?

Each framing leads to different data needs, model choices, metrics, and risks.

### Key lesson

Before choosing an algorithm, ask:

- What is the actual operational question?
- Who will use the output?
- What data exists at decision time?
- What mistakes are most costly?
- What does success mean in practice?

---

## 6. Why many AI-for-cyber projects fail

Students often assume that the main challenge is choosing a sophisticated model. In reality, many failures come earlier.

### 6.1 Poor problem definition

Teams may say they want “AI for threat detection” without defining:

- the threat;
- the decision point;
- the available data;
- the required response time;
- the acceptable false-positive burden.

### 6.2 Bad or unrealistic data

Common issues include:

- missing values;
- inconsistent labels;
- synthetic datasets that do not match reality;
- over-cleaned benchmark datasets;
- train-test leakage;
- historical bias in labels.

### 6.3 Weak evaluation

A model can appear strong on accuracy and still be operationally poor.

For example, if attacks are rare, a model can have high accuracy while missing most malicious cases. Security evaluation usually needs metrics such as:

- precision;
- recall;
- F1-score;
- false-positive rate;
- false-negative cost;
- alert burden per analyst.

### 6.4 Distribution shift and drift

Attack patterns change. Users change. Infrastructure changes. Tools change. A model trained last semester may become unreliable after deployment.

### 6.5 Lack of trust and interpretability

Analysts may ignore a model that gives scores without useful context. A technically strong model can fail organisationally if its outputs are not actionable.

---

## 7. Strengths and limitations of AI in cybersecurity

### Strengths

AI can help with:

- scaling analysis across large datasets;
- surfacing patterns that are hard to see manually;
- handling repetitive triage work;
- prioritising alerts;
- supporting text-heavy analysis;
- learning from historical examples.

### Limitations

AI struggles when:

- good labelled data is unavailable;
- attacker behaviour changes rapidly;
- there is a need for strong causal explanation;
- outputs must be highly reliable with little tolerance for false positives;
- the system is deployed without monitoring and human oversight.

The most responsible view is this:

> AI is not a replacement for security engineering or analysts. It is a set of techniques that can support security work when the problem, data, evaluation, and deployment conditions are carefully managed.

---

## 8. Case discussion: AI for phishing detection

Consider a university email environment.

### Objective
Identify likely phishing emails before users click on them.

### Possible data
- sender domain;
- SPF/DKIM/DMARC results;
- URL features;
- message structure;
- attachment type;
- textual cues;
- historical reports from users.

### Possible methods
- rule-based detection;
- classical machine learning on engineered features;
- text classification;
- LLM-assisted explanation for analysts.

### Key questions
- Is the task classification, ranking, or triage support?
- What is the cost of a false positive?
- What happens if attackers adapt?
- Can the system explain why a message was flagged?
- Should the model block automatically or support human review?

This simple example shows why cyber AI is as much about system design and judgement as it is about modelling.

---

## 9. Lab guidance

### Suggested lab theme
**Exploring a cybersecurity dataset and building a baseline**

### Suggested tasks
1. load a small cyber dataset;
2. inspect feature names, data types, and label balance;
3. identify missing values or suspicious columns;
4. visualise class imbalance or basic distributions;
5. create a trivial baseline, such as majority class or a simple decision tree;
6. write a short reflection on what the dataset does and does not represent.

### Suggested reflection questions
- What decision is the dataset trying to support?
- What important contextual information is missing?
- Is the dataset likely to generalise to a real environment?
- What kinds of errors would be dangerous?

---

## 10. Discussion questions

1. In which cybersecurity tasks is AI most useful, and in which is it overused?
2. Why is “high accuracy” often a weak argument in security contexts?
3. Should AI outputs in a SOC be advisory or automated by default?
4. What kinds of cyber data are easiest to collect but hardest to trust?
5. What risks arise when organisations deploy AI because it is fashionable rather than necessary?

---

## 11. Key terms

- Artificial Intelligence
- Machine Learning
- Deep Learning
- Generative AI
- Classification
- Anomaly Detection
- Triage
- Telemetry
- Feature
- Label
- Distribution Shift
- False Positive
- False Negative
- Operationalisation

---

## 12. Week summary

This week introduced the central idea of the module:

**Applied AI for cybersecurity is not mainly about sophisticated models. It is about aligning security problems, data, evaluation, and operational use.**

Students should now understand:

- the main categories of AI used in cyber contexts;
- the kinds of data cyber systems generate;
- why problem framing is crucial;
- why data quality and evaluation are decisive;
- why AI should be treated as useful but fallible.

The next week moves from foundations to practice by focusing on datasets, features, classical machine learning, and evidence-based evaluation for security analytics.
