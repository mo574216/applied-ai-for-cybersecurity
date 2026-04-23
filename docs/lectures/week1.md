---
title: "Week 1 — Foundations of Applied AI for Cybersecurity"
layout: default
permalink: /lectures/week1/
---

# Week 1 — Foundations of Applied AI for Cybersecurity

## Overview

This first week sets the intellectual foundation for the whole module. It addresses a central question:

> **Why has AI become so important in cybersecurity, and why must security professionals use it carefully rather than uncritically?**

Students are often exposed to exaggerated claims about AI in cyber defence. Some believe AI can replace analysts. Others assume AI is just another buzzword with little practical value. The purpose of this session is to move beyond both extremes.

This week shows that AI matters in cybersecurity because modern digital systems generate large amounts of heterogeneous, noisy, and time-sensitive data, while defenders must make decisions under uncertainty and adversarial pressure. AI can help with detection, triage, prioritisation, clustering, summarisation, and pattern extraction. At the same time, AI systems can be brittle, misleading, overtrusted, badly evaluated, or poorly aligned with operational needs.

This is therefore not a lecture about “AI magic.” It is a lecture about **where AI fits, where it fails, and how cybersecurity problems should be framed before any model is chosen**.

---

## Teaching Position of This Lecture in the Module

This session is the conceptual entry point for the full course.

It prepares students for later weeks by establishing:

- the vocabulary of AI in cybersecurity;
- the difference between AI, machine learning, deep learning, and generative AI;
- the kinds of cyber data used in AI-enabled workflows;
- the importance of problem framing;
- the reasons many AI-for-cyber projects fail despite promising demos;
- the idea that AI systems must be evaluated operationally, not just computationally.

This week is intentionally broad, because later weeks will go deeper into:

- datasets and classical machine learning;
- deep learning and generative AI;
- attacks against AI systems;
- trustworthy deployment, governance, and judgement.

---

## Learning Outcomes

By the end of this week, students should be able to:

1. explain the difference between AI, machine learning, deep learning, and generative AI in a cybersecurity context;
2. identify common cybersecurity tasks that can be framed as data-driven problems;
3. describe major categories of cybersecurity data used in AI-enabled workflows;
4. explain why problem framing, data quality, and evaluation often matter more than model novelty;
5. discuss major strengths and limitations of AI-based cybersecurity systems;
6. distinguish between technical performance and operational usefulness;
7. participate in classroom discussion about where AI should and should not be trusted in security practice.

---

## Indicative Session Plan for Classroom Delivery

This file is designed for a live classroom session of approximately **2 hours**, but it can also be adapted.

### Suggested lecture rhythm

- **Part 1:** Motivation and framing — 20 minutes
- **Part 2:** AI vocabulary and distinctions — 20 minutes
- **Part 3:** Cybersecurity data and workflows — 20 minutes
- **Part 4:** Framing cyber problems as AI tasks — 20 minutes
- **Part 5:** Why AI-for-cyber projects fail — 20 minutes
- **Part 6:** Strengths, limits, and discussion — 15 minutes
- **Part 7:** Wrap-up and transition to lab — 5 minutes

### Suggested interactive rhythm

Include:
- 2 quick show-of-hands polls;
- 2 think-pair-share activities;
- 1 mini case discussion;
- 1 short end-of-class reflection.

---

# Part 1 — Why AI Matters in Cybersecurity

## 1.1 Opening hook for the classroom

Start the session with a question such as:

> If an organisation gives its SOC an AI assistant tomorrow, what exactly should improve first?

Write student answers on the board. Likely answers:
- faster detection;
- fewer alerts;
- better prioritisation;
- less analyst workload;
- faster reporting;
- improved accuracy.

Then ask the follow-up:

> Which of these improvements are actually guaranteed by “adding AI”?

This usually surfaces an important teaching point immediately:
**AI is not a direct synonym for improvement.**

---

## 1.2 Why cybersecurity is an attractive domain for AI

Cybersecurity is a natural area for AI because it combines five difficult properties:

- **data-rich:** large volumes of logs, events, packets, telemetry, and text;
- **time-sensitive:** defenders often need to act quickly;
- **noisy:** security data contains irrelevant, duplicated, incomplete, and misleading signals;
- **adversarial:** attackers adapt in response to defensive behaviour;
- **operationally constrained:** analysts have limited time, imperfect visibility, and incomplete context.

A modern organisation may generate:

- firewall logs;
- endpoint telemetry;
- DNS and proxy logs;
- authentication records;
- cloud audit trails;
- vulnerability scan outputs;
- IDS/IPS alerts;
- email metadata;
- incident tickets;
- analyst notes;
- packet captures;
- flow summaries.

The human challenge is obvious: **no team can inspect all raw signals manually at scale**.

This makes AI attractive for tasks such as:

- classification of suspicious activity;
- anomaly detection in traffic or behaviour;
- ranking and prioritisation of alerts;
- clustering related incidents;
- phishing and malicious URL detection;
- malware family analysis;
- summarisation of reports and alerts;
- support for rule writing and analyst workflows.

---

## 1.3 Important caution

At this point, make the distinction explicit:

> **Attractive does not mean appropriate.**

Some cyber problems are genuinely suited to AI.
Others are better solved with:

- deterministic rules;
- careful engineering;
- better visibility;
- better logging;
- stronger processes;
- simpler statistical methods.

A recurring theme in this module is:

> **Do not ask, “Can we apply AI here?” before asking, “What problem are we actually trying to solve?”**

---

## In-class Q&A prompt 1

Ask students:

1. Why does having more security data not automatically mean better security?
2. If a SOC is overloaded with alerts, is AI always the first thing that should be added?
3. What are examples of cyber problems where a simple rule might outperform a learned model?

---

## Quick classroom activity 1 — Two-minute poll

Ask students to vote on the following:

> Which of the following is the most realistic short-term use of AI in a SOC?

Options:
- replacing analysts entirely;
- automatically responding to every alert;
- helping prioritise and summarise alerts;
- eliminating the need for logs.

Expected direction: students should see that **triage and support** are more realistic than full automation.

---

# Part 2 — AI, Machine Learning, Deep Learning, and Generative AI

## 2.1 Why this distinction matters

Students often use these terms interchangeably. In classroom teaching, this causes confusion later, especially when moving from classical models to LLMs.

Clarify the hierarchy early.

---

## 2.2 Artificial Intelligence

Artificial intelligence is the broad umbrella term.

In this module, AI refers to computational techniques that support tasks associated with intelligent behaviour, such as:

- prediction;
- ranking;
- recognition;
- classification;
- summarisation;
- recommendation;
- limited reasoning or assistance.

Important note for students:
AI does **not** necessarily imply consciousness, general intelligence, or human-like understanding.

In cybersecurity, AI is often simply a practical label for systems that assist detection and decision-making.

---

## 2.3 Machine Learning

Machine learning is a subset of AI in which systems learn patterns from data instead of depending only on hand-written logic.

Examples in cybersecurity:

- classifying emails as phishing or benign;
- predicting whether a flow is malicious;
- identifying likely false positives;
- grouping related incidents;
- learning risk scores from past examples.

Key teaching point:

> Machine learning is powerful when patterns exist in data and when we can define a useful output target or behavioural notion of normality.

---

## 2.4 Deep Learning

Deep learning is a subset of machine learning based on multi-layer neural networks.

It becomes useful when data is:

- high-dimensional;
- sequential;
- unstructured or semi-structured;
- difficult to describe with simple hand-engineered features.

Examples in cybersecurity:

- sequence modelling for logs;
- traffic classification from flow sequences;
- learned representations of malware behaviour;
- text models for phishing or threat intelligence.

Key classroom warning:
Deep learning is **not automatically better**. It usually requires more data, more computation, and more careful evaluation.

---

## 2.5 Generative AI

Generative AI refers to models that create or transform content such as:

- text;
- code;
- images;
- structured summaries;
- responses to prompts.

In cybersecurity, the most visible examples are large language models.

Possible uses include:

- summarising alerts;
- explaining logs or incidents;
- drafting detection rules;
- assisting analysts with investigations;
- helping developers reason about secure coding issues.

But generative AI introduces major risks:

- hallucination;
- overconfidence;
- leakage of sensitive data;
- unsafe integration into operational pipelines;
- prompt-based manipulation.

---

## Mini-contrast table

| Term | Main idea | Cyber examples | Typical risk |
|---|---|---|---|
| AI | Broad umbrella | triage support, alert ranking | vague overclaiming |
| ML | learns patterns from data | phishing classification, anomaly scoring | data quality dependence |
| Deep Learning | neural learning from complex data | log sequences, malware representations | opacity and resource cost |
| Generative AI | generates content | alert summaries, query drafting, analyst support | hallucination and unsafe outputs |

---

## In-class Q&A prompt 2

1. Is every AI system in cybersecurity a machine-learning system?
2. Is every deep-learning system generative?
3. Why might an organisation use classical ML instead of deep learning?
4. Why does an LLM sounding fluent not guarantee that it is correct?

---

## Misconceptions to address explicitly

### Misconception 1
**“AI means the system understands the attack.”**  
Correction: many AI systems detect statistical patterns, not causal intent.

### Misconception 2
**“Deep learning is always more advanced and therefore better.”**  
Correction: sometimes a simpler and more interpretable model is preferable.

### Misconception 3
**“Generative AI can replace analysts because it explains things well.”**  
Correction: explanation quality and factual correctness are not the same.

---

# Part 3 — Where AI Fits in the Security Workflow

## 3.1 Cybersecurity as a workflow, not a single tool

It is a mistake to think of cyber defence as “the model.” Security is an end-to-end process.

A simplified defensive workflow includes:

1. **data collection**  
   gathering logs, telemetry, packets, endpoint signals, and threat intelligence;

2. **normalisation and preprocessing**  
   cleaning, deduplicating, structuring, and aligning data;

3. **analysis and detection**  
   rules, correlation, machine learning, anomaly detection, or hybrid methods;

4. **prioritisation and triage**  
   deciding what deserves analyst attention first;

5. **investigation and interpretation**  
   understanding what happened and why;

6. **response and recovery**  
   containment, eradication, communication, and post-incident learning.

AI usually supports only part of this process.

---

## 3.2 Where AI is most useful

AI is often most useful in:

- detection support;
- ranking and triage;
- clustering similar events;
- text-heavy analyst assistance;
- identifying patterns that humans would miss at scale.

It is usually less trustworthy when used blindly for:

- automatic irreversible response;
- high-stakes decisions without human oversight;
- contexts with poor labels or rapidly changing attacker behaviour.

---

## 3.3 Why notebook success does not equal operational success

A model that looks impressive in a notebook may fail in practice if:

- the data is delayed or incomplete;
- labels are noisy or inconsistent;
- the environment changes after deployment;
- analysts cannot interpret the output;
- false positives overwhelm the team;
- the model is solving the wrong problem.

Key classroom phrase:

> **A high-performing model in isolation may still be a low-value system in operation.**

---

## Short think-pair-share activity

Ask students to work in pairs for 3 minutes:

> Imagine a phishing detection model with 98% accuracy. Why might a real SOC still dislike it?

Expected answers:
- poor precision;
- too many false positives;
- no explanation;
- weak adaptation to new campaigns;
- not aligned with workflow;
- difficult integration into email systems.

Then debrief with the full class.

---

# Part 4 — Types of Cybersecurity Data

## 4.1 Why “cyber data” is not one thing

Cybersecurity draws on many data sources with different structures, timing properties, quality levels, and meanings.

Students must understand that model design depends strongly on data type.

---

## 4.2 Network traffic and flow data

Examples:
- packet captures;
- NetFlow/IPFIX-style summaries;
- session metadata;
- protocol features.

Use cases:
- intrusion detection;
- DDoS detection;
- scanning detection;
- protocol misuse detection;
- anomaly detection;
- encrypted traffic inference from metadata.

Teaching note:
Packet data is rich but expensive. Flow data is lighter but less detailed.

---

## 4.3 Log data

Examples:
- authentication logs;
- operating system logs;
- server logs;
- application logs;
- firewall and proxy logs;
- cloud audit trails.

Use cases:
- suspicious login detection;
- privilege misuse;
- lateral movement patterns;
- incident reconstruction;
- behavioural analysis.

Teaching note:
Logs often look structured, but they are messy in practice: missing fields, inconsistent formats, duplicated records, and context gaps are common.

---

## 4.4 Endpoint and host telemetry

Examples:
- process creation;
- registry modifications;
- file operations;
- memory-related indicators;
- EDR telemetry.

Use cases:
- malware detection;
- behavioural analysis;
- insider-threat indicators;
- persistence detection.

Teaching note:
Host data can be very informative but may raise privacy, storage, and deployment issues.

---

## 4.5 Email and web data

Examples:
- headers;
- subject lines;
- URLs;
- attachment metadata;
- domain properties;
- webpage features.

Use cases:
- phishing detection;
- malicious URL detection;
- spam filtering;
- campaign grouping.

Teaching note:
This is a very accessible teaching domain because students understand email and phishing intuitively.

---

## 4.6 Textual and intelligence data

Examples:
- threat reports;
- analyst notes;
- vulnerability descriptions;
- tickets;
- incident summaries.

Use cases:
- summarisation;
- entity extraction;
- relationship mapping;
- analyst assistance;
- threat intelligence support.

Teaching note:
This is where generative AI becomes especially visible, but also especially risky.

---

## In-class Q&A prompt 3

1. Which of these data types is likely to be most structured?
2. Which is likely to be richest in context?
3. Which is likely to be easiest to collect but hardest to trust?
4. Why might the same attack look different in network data and host data?

---

## Mini activity — Match data to task

Give the class a quick matching exercise:

| Task | Most relevant data source |
|---|---|
| DDoS detection | network flow data |
| suspicious admin login | authentication logs |
| phishing detection | email metadata + text + URLs |
| malware behaviour analysis | endpoint telemetry |
| report summarisation | textual threat intelligence |

Then ask:
> Could any of these tasks be solved with only one data source?

This opens discussion about multimodal and partial visibility.

---

# Part 5 — Framing Cybersecurity Problems as AI Problems

## 5.1 Why framing matters more than students expect

One of the deepest skills in applied AI is not coding the model. It is **defining the problem correctly**.

A badly framed problem leads to:

- the wrong data;
- the wrong labels;
- the wrong metrics;
- the wrong deployment choice;
- the wrong expectations.

---

## 5.2 Example: suspicious login detection

Suppose a university wants help detecting suspicious logins.

This can be framed in multiple ways.

### Framing A — Binary classification
Question: is this login suspicious or benign?

### Framing B — Anomaly detection
Question: how unusual is this login relative to typical behaviour?

### Framing C — Ranking
Question: which logins should analysts inspect first?

### Framing D — Clustering
Question: are several suspicious logins part of the same campaign?

### Framing E — Summarisation
Question: can the system produce a short explanation to help the analyst?

Each framing changes:

- what data is needed;
- how labels are defined;
- what outputs are produced;
- how performance is measured;
- what the human user expects.

---

## 5.3 The five problem-framing questions

Before choosing an algorithm, ask:

1. **What is the operational question?**  
   Not “build an AI model,” but “support which decision?”

2. **Who will use the output?**  
   Analyst, manager, developer, incident responder, end user?

3. **What data is actually available at decision time?**  
   Not later, not after investigation, but at the moment of need.

4. **Which mistakes are most costly?**  
   False positives? False negatives? Delay? Opaqueness?

5. **What does success mean operationally?**  
   Fewer misses? Faster triage? Reduced analyst workload? Better consistency?

---

## Instructor board-work idea

Draw the following on the board:

```text
Cyber problem → Framing choice → Data choice → Model choice → Metric choice → Deployment role
```

Then walk through a phishing example live.

This helps students see that the model is only one component in a longer chain of decisions.

---

## In-class Q&A prompt 4

1. Can the same cyber problem be framed as both classification and anomaly detection?
2. Why might ranking be more useful than hard yes/no classification?
3. If analysts are overloaded, is perfect recall always the best goal?
4. What happens if the model is trained on information unavailable at decision time?

---

# Part 6 — Why Many AI-for-Cyber Projects Fail

## 6.1 Students often think failure begins with the wrong algorithm

In reality, many projects fail before modelling even begins.

---

## 6.2 Failure mode 1 — Poor problem definition

Teams may say:
> “We want AI for threat detection.”

But that statement is incomplete unless they define:

- what threat;
- which decision point;
- which user;
- which time constraint;
- which success criterion;
- which tolerance for false alarms.

Without this, even a good model may solve the wrong problem.

---

## 6.3 Failure mode 2 — Bad or unrealistic data

Common issues:
- missing values;
- inconsistent labels;
- over-cleaned benchmark datasets;
- unrealistic simulation data;
- hidden leakage;
- historical bias in labels;
- stale or unrepresentative data.

Key point:
**Garbage in, impressive-looking garbage out.**

---

## 6.4 Failure mode 3 — Weak evaluation

A model can have high accuracy and still be operationally poor.

If malicious events are rare, a model can appear excellent while missing the attacks that matter.

Important metrics in security may include:
- precision;
- recall;
- F1-score;
- false-positive burden;
- false-negative cost;
- analyst time saved;
- triage quality.

---

## 6.5 Failure mode 4 — Distribution shift and drift

The environment changes:
- attackers adapt;
- users change behaviour;
- infrastructure changes;
- software versions change;
- logging quality shifts.

A model trained in one context may become unreliable later.

---

## 6.6 Failure mode 5 — Lack of trust and interpretability

A model may technically work, but still fail organisationally if:

- analysts do not trust it;
- outputs are too opaque;
- explanations are weak;
- workflow integration is poor;
- the system adds burden instead of reducing it.

---

## Interactive case pause

Ask:

> Which is worse: a model with modest performance that analysts trust and use, or a technically stronger model that analysts ignore?

Let students argue both sides for 4 minutes.

Then conclude:
Technical strength without adoption may produce little operational value.

---

# Part 7 — Strengths and Limitations of AI in Cybersecurity

## 7.1 Strengths

AI can be very useful for:

- scaling analysis to large data volumes;
- surfacing subtle patterns;
- handling repetitive triage tasks;
- prioritising likely-important cases;
- assisting with text-heavy security work;
- learning from historical examples;
- supporting, though not replacing, security teams.

---

## 7.2 Limitations

AI struggles when:

- high-quality labels do not exist;
- attacker behaviour changes rapidly;
- systems require strong causal understanding;
- costs of false positives are severe;
- models are deployed without human oversight;
- environments are dynamic but monitoring is weak;
- students or practitioners confuse benchmark performance with operational success.

---

## 7.3 The balanced position

State this clearly in class:

> AI is neither a miracle nor a gimmick.  
> It is a family of techniques that can help cybersecurity when the problem, data, metrics, workflow, and deployment assumptions are aligned.

This balanced position is the intellectual foundation for the rest of the module.

---

# Part 8 — Guided Case Discussion: AI for Phishing Detection

## 8.1 Scenario

A university wants to reduce phishing incidents.

It is considering an AI-enabled system to flag suspicious emails before users click on them.

---

## 8.2 Possible data

- sender domain;
- SPF/DKIM/DMARC status;
- URL features;
- message structure;
- attachment type;
- lexical cues;
- prior reports from users;
- historical outcomes.

---

## 8.3 Possible approaches

- rule-based filtering;
- engineered-feature machine learning;
- anomaly detection;
- NLP-based classification;
- LLM-assisted explanation for analysts.

---

## 8.4 Questions for classroom discussion

1. Is the goal blocking, triage, or analyst support?
2. What is the cost of a false positive in a university setting?
3. How might attackers adapt once the model is deployed?
4. Should the system explain its output to analysts?
5. Should the university allow auto-quarantine based on model confidence alone?
6. What happens if the LLM gives a fluent but wrong explanation?

---

## Small group task

Break the class into small groups.

Ask each group to recommend one of the following:

- rule-based only;
- ML-assisted triage;
- full AI-based filtering;
- hybrid rule + ML + human review.

Each group must justify:
- what problem is being solved;
- what mistakes matter most;
- what level of human oversight is needed.

This makes the lecture genuinely interactive and prepares students for later assessment logic.

---

# Part 9 — Classroom Checks for Understanding

## Concept check questions

Use these during the lecture:

1. Why is cybersecurity particularly attractive for AI applications?
2. Why is AI not automatically the correct solution?
3. What is the difference between machine learning and generative AI?
4. Why is a detection model not the same thing as a security workflow?
5. Why can a model with high accuracy still be operationally poor?
6. Why must cyber tasks be framed carefully before model selection?
7. Why is trust by analysts an important part of system success?

---

## Short-answer in-class quiz

You can end the lecture with 5 quick questions:

1. Name two differences between machine learning and generative AI.
2. Give two examples of cybersecurity data sources.
3. Explain one reason an AI-for-cyber project may fail before deployment.
4. Give one example of a cyber task that may be better solved by ranking than classification.
5. Explain in one sentence why notebook performance is not enough.

---

# Part 10 — Lecturer Notes and Teaching Advice

## What to emphasise verbally

- The course is not anti-AI.
- The course is not uncritically pro-AI.
- The course is about professional judgement.
- Students must learn to ask better questions, not just run models.

## What students may struggle with

- distinguishing AI from ML and GenAI;
- understanding why “more advanced model” is not always better;
- appreciating operational metrics rather than abstract performance;
- grasping that data quality often dominates model quality.

## What to repeat more than once

- frame the problem first;
- data and labels matter;
- metrics must reflect operational reality;
- the workflow matters, not just the model;
- human trust and interpretability affect adoption.

---

# Part 11 — Suggested Slides Structure

If you turn this into slides, a good sequence is:

1. Title and central question
2. Why cybersecurity is attractive for AI
3. Why attraction does not equal suitability
4. AI vs ML vs DL vs GenAI
5. Cybersecurity workflow and where AI fits
6. Types of cybersecurity data
7. Mini polling question
8. Framing cyber problems correctly
9. Suspicious login example
10. Why AI-for-cyber projects fail
11. Strengths and limitations
12. Phishing case discussion
13. Concept check questions
14. Key terms
15. Summary and transition to next week

---

# Part 12 — Lab Guidance

## Lab theme
**Exploring a cybersecurity dataset and building a baseline**

## Purpose
The lab should reinforce the lecture’s main message:

> Before students try sophisticated models, they must understand the dataset, the task, and the meaning of the labels.

## Suggested tasks

1. load a small cybersecurity dataset;
2. inspect feature names, data types, and label balance;
3. identify missing values or suspicious columns;
4. visualise class imbalance or simple distributions;
5. create a trivial baseline, such as majority class or a simple decision tree;
6. write a short reflection on what the dataset does and does not represent.

## Reflection questions

- What decision is the dataset trying to support?
- What important context is missing?
- Is the dataset likely to generalise to a real environment?
- Which errors would be most dangerous?
- What would an analyst need beyond the model output?

---

# Part 13 — In-Class Q&A Bank

Use these selectively throughout the session.

## Session 1 Q&A
- Why is AI especially attractive in high-volume cyber environments?
- Can too much data make security worse rather than better?

## Session 2 Q&A
- Is generative AI a form of machine learning?
- Is every machine-learning system “intelligent” in a meaningful sense?

## Session 3 Q&A
- Why might logs and packet captures lead to different conclusions?
- Which data source would you trust most for insider-threat analysis?

## Session 4 Q&A
- Why is ranking sometimes more useful than classification?
- Can anomaly detection work well when the environment changes frequently?

## Session 5 Q&A
- Why can high accuracy be misleading in security?
- What is one operational metric you would care about more than accuracy?

## Session 6 Q&A
- When should AI outputs be advisory only?
- When, if ever, should AI be allowed to trigger automated action?

---

# Part 14 — Key Terms

- Artificial Intelligence
- Machine Learning
- Deep Learning
- Generative AI
- Classification
- Ranking
- Clustering
- Anomaly Detection
- Triage
- Telemetry
- Feature
- Label
- Drift
- False Positive
- False Negative
- Operationalisation
- Workflow
- Interpretability

---

# Part 15 — End-of-Class Summary

This week introduced the core idea of the module:

> **Applied AI for cybersecurity is not mainly about choosing impressive models. It is about aligning security problems, data, metrics, workflows, and operational judgement.**

Students should now understand:

- why AI matters in cybersecurity;
- how AI, ML, deep learning, and generative AI differ;
- what kinds of cyber data are commonly used;
- why problem framing is a foundational skill;
- why many AI-for-cyber projects fail before or after deployment;
- why AI should be treated as useful but fallible.

---

# Part 16 — Transition to Week 2

Next week moves from broad conceptual framing to practical modelling foundations.

Students will begin working more directly with:

- datasets;
- preprocessing;
- feature engineering;
- classical machine learning;
- evidence-based evaluation.

That transition is deliberate.

Week 1 asks:
> **What is the problem, and what would responsible AI use look like?**

Week 2 asks:
> **How do we actually prepare cyber data and evaluate models properly?**

---

# Optional homework / reflection

Write 250–400 words responding to the statement:

> “The hardest problem in AI for cybersecurity is not building a model. It is deciding how much to trust it.”

Support your answer with at least two ideas from today’s lecture.
