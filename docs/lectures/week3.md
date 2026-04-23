---
title: "Week 3 — Deep Learning and Generative AI in Cybersecurity"
layout: default
permalink: "/docs/lectures/week3.html"
---

# Week 3 — Deep Learning and Generative AI in Cybersecurity

## Overview

This week examines two major developments in modern cybersecurity analytics:

1. the use of deep learning for complex cyber data;
2. the use of generative AI and large language models in cyber workflows.

Deep learning is useful when data is high-dimensional, sequential, or difficult to represent using a small set of hand-engineered features. Generative AI is useful when the task involves language, code, explanation, summarisation, or conversational support.

These technologies are powerful, but they should not be treated as automatic upgrades over classical methods. Their value depends on the task, the data, and the deployment context.

---

## Learning Outcomes

By the end of this week, students should be able to:

1. explain why deep learning may be useful for certain cybersecurity data types;
2. identify common cyber use cases for neural networks and representation learning;
3. describe practical uses of generative AI and LLMs in security operations;
4. evaluate the benefits and weaknesses of GenAI-supported cyber workflows;
5. discuss risks such as hallucination, overconfidence, and unsafe automation.

---

## 1. Why deep learning entered cybersecurity

Classical machine learning often depends on engineered features. Deep learning became attractive because it can learn internal representations from raw or semi-structured data.

This matters in cybersecurity because many cyber artefacts are:

- sequential;
- variable in length;
- high-dimensional;
- partly unstructured;
- context-sensitive.

Examples include:

- packet or flow sequences;
- command histories;
- process trees;
- log streams;
- malware byte sequences or API call traces;
- phishing message text;
- threat intelligence reports.

Deep learning is especially useful when the relationships in the data are complex and not easy to express as a small manual feature set.

---

## 2. Neural network ideas in simple terms

A neural network takes input data and transforms it through layers to learn increasingly useful representations.

For this module, the important intuition is not heavy mathematics but the following:

- early layers may learn local or low-level patterns;
- deeper layers may capture more abstract structure;
- the network learns these patterns from examples rather than from hand-written rules.

### Practical implication

If the data contains rich structure, deep learning may discover patterns that manual feature engineering misses.

### Practical warning

If the data is small, biased, noisy, or unrealistic, deep learning may simply learn these problems more efficiently.

---

## 3. Deep learning use cases in cybersecurity

### 3.1 Malware analysis

Possible inputs:
- byte sequences;
- opcode sequences;
- API call traces;
- behavioural event streams.

Possible outputs:
- benign vs malicious;
- malware family classification;
- behavioural clustering.

### 3.2 Network and traffic analysis

Possible inputs:
- packet timing;
- flow sequences;
- encrypted traffic metadata;
- session patterns.

Possible tasks:
- intrusion detection;
- DDoS detection;
- application classification;
- anomaly detection.

### 3.3 Log and event sequence analysis

Deep learning may be useful for:
- detecting unusual sequences of system events;
- modelling normal behaviour and finding deviations;
- supporting incident timeline interpretation.

### 3.4 Phishing and text analysis

Possible tasks:
- classifying phishing text;
- detecting social-engineering cues;
- extracting threat intelligence entities;
- clustering related campaigns.

---

## 4. Representation learning and embeddings

A representation is a transformed version of the input that captures useful structure.

Embeddings are numerical vector representations that place related items closer together in a learned space.

In cybersecurity, embeddings can help with:

- clustering similar alerts;
- comparing related malware samples;
- grouping similar domains or URLs;
- mapping textual reports into searchable vector spaces.

This is important because security analysts often care not only about yes/no decisions, but also about similarity, relationship, and context.

---

## 5. Where deep learning helps and where it does not

### Deep learning may help when:
- there is a large volume of relevant data;
- the data has rich internal structure;
- manual features are hard to design;
- the task benefits from learned representations.

### Deep learning may not help when:
- the dataset is small or low-quality;
- the operational question is simple;
- interpretability is critical;
- a classical baseline already performs well;
- deployment constraints make deep models too costly or too opaque.

Students should resist the idea that deep learning is inherently superior. The right question is whether it improves the actual security workflow.

---

## 6. Generative AI and LLMs in cybersecurity

Large language models are increasingly used because much security work involves language:

- alerts;
- analyst notes;
- incident tickets;
- threat reports;
- vulnerability descriptions;
- detection rules;
- code snippets;
- security guidance.

### Potential LLM-supported tasks

- summarising long alerts or reports;
- explaining suspicious events in plain language;
- drafting detection rules or queries;
- assisting with documentation;
- helping analysts triage cases;
- supporting secure coding review;
- transforming natural language requests into search or investigation steps.

### Example

A SOC analyst may receive a large, messy alert with multiple IPs, processes, and timestamps. An LLM could help produce:

- a concise narrative summary;
- a list of key indicators;
- candidate next investigation steps;
- a note for escalation.

---

## 7. Benefits of GenAI in cyber workflows

### 7.1 Speed
Generative models can reduce time spent on repetitive reading and drafting.

### 7.2 Accessibility
They can help junior analysts understand unfamiliar outputs or concepts.

### 7.3 Natural language interaction
They allow human-friendly interfaces over complex data and tooling.

### 7.4 Support for documentation and communication
They can assist with incident summaries, playbook drafting, or explanation for mixed audiences.

---

## 8. Limitations and risks of GenAI

Students must treat LLMs critically.

### 8.1 Hallucination
The model may produce plausible but false information.

### 8.2 Overconfidence
The tone may sound certain even when the content is weak or fabricated.

### 8.3 Prompt sensitivity
Small wording changes may alter outputs significantly.

### 8.4 Context limitations
The model may misunderstand the environment, missing technical detail or organisational nuance.

### 8.5 Privacy and confidentiality
Sensitive logs, code, or incident details may be exposed if handled unsafely.

### 8.6 Unsafe automation
If an LLM is allowed to trigger actions directly, the risk increases significantly.

---

## 9. Human-in-the-loop design

A good operational design often keeps humans responsible for interpretation and action.

### Safer pattern
- model assists;
- analyst reviews;
- analyst decides.

### Riskier pattern
- model interprets;
- model acts automatically;
- humans review only after impact.

In many cyber contexts, LLMs are best used first as **support tools**, not autonomous agents.

---

## 10. Case discussion: LLM support in a SOC

Suppose a SOC wants to deploy an LLM assistant.

### Candidate tasks
- explain SIEM alerts;
- summarise incident tickets;
- suggest investigation questions;
- map plain-language requests to security queries.

### Benefits
- reduced triage time;
- better support for junior analysts;
- improved documentation quality.

### Risks
- fabricated explanations;
- misleading recommendations;
- leakage of sensitive case data;
- prompt manipulation;
- analyst overreliance.

### Key design questions
- What data can the model see?
- What output is the analyst allowed to trust?
- Can the model issue actions or only suggestions?
- How are outputs logged and reviewed?
- What happens when the model is wrong?

---

## 11. Deep learning and GenAI are not the same thing

Students should keep the distinction clear.

### Deep learning in analytics
Often used for:
- classification;
- detection;
- representation learning;
- pattern recognition.

### Generative AI
Often used for:
- text generation;
- summarisation;
- code assistance;
- conversational support.

A large language model is usually based on deep learning, but not all deep learning in cybersecurity is generative.

---

## 12. Lab guidance

### Suggested lab theme
**AI-assisted alert analysis and critical evaluation**

### Suggested tasks
1. take a short set of alert or security text examples;
2. use a guided AI workflow or simulation to summarise or classify them;
3. compare AI-supported outputs with a manual or non-AI baseline;
4. record strengths, weaknesses, and failure cases;
5. reflect on whether the workflow is safe enough for operational use.

### Suggested reflection questions
- Did the model save time?
- Did it miss important technical detail?
- Did it invent anything?
- Would you allow it to influence response actions?
- What controls would you require before deployment?

---

## 13. Discussion questions

1. When is deep learning justified in cybersecurity, and when is it unnecessary?
2. Should LLMs be allowed to draft detection rules for production use?
3. What is more dangerous in practice: hallucination or analyst overtrust?
4. Which cyber tasks benefit most from natural-language models?
5. Can generative AI improve security while also increasing security risk?

---

## 14. Key terms

- Neural Network
- Representation Learning
- Embedding
- Sequence Modelling
- Malware Classification
- NLP
- Large Language Model
- Hallucination
- Human-in-the-Loop
- AI-assisted Triage

---

## 15. Week summary

This week introduced modern AI capabilities beyond classical machine learning.

Students should now understand:

- why deep learning is useful for complex cyber data;
- how learned representations can help classification, clustering, and analysis;
- where LLMs can support security work;
- why GenAI must be used critically rather than blindly;
- why human oversight remains central in security operations.

The next week turns the focus around: instead of asking how AI can help cybersecurity, it asks how AI systems themselves can be attacked and how they should be defended.
