---
title: "Labs"
layout: default
nav_order: 5
permalink: "/docs/labs/"
---

# Labs

## Applied AI for Cybersecurity

This page outlines the practical lab component of the module. The labs are designed to help students move from conceptual understanding to applied technical judgement.

The emphasis is on:

- realistic workflows;
- careful evaluation;
- reflective interpretation;
- awareness of limitations;
- responsible use of AI tools.

---

## Lab Philosophy

The labs in this module are not intended to turn students into instant machine-learning specialists. Instead, they are designed to help students:

1. understand how cybersecurity problems are framed as AI tasks;
2. work with security-relevant datasets and workflows;
3. compare methods critically rather than blindly;
4. recognise failure modes and deployment risks;
5. communicate technical findings clearly.

Students should treat every lab as both a technical exercise and a critical evaluation exercise.

---

## Practical Environment

Indicative tools and platforms include:

- Python
- Jupyter Notebook
- pandas
- scikit-learn
- matplotlib
- NumPy
- optionally Wireshark-derived data or packet/flow datasets
- selected public cybersecurity datasets
- optional LLM interfaces or instructor-controlled AI tools for safe classroom use

Students should not run offensive tools or unauthorised scans as part of this module unless explicitly instructed in a safe and approved environment.

---

## Weekly Lab Plan

## Week 1 Lab — Exploring Cybersecurity Data and Building a Baseline

### Aim
To introduce students to the structure, messiness, and limitations of cybersecurity data.

### Learning focus
- understanding the dataset;
- identifying labels and feature types;
- spotting class imbalance and missing data;
- building a trivial baseline.

### Suggested tasks
1. load a small cybersecurity dataset;
2. inspect shape, columns, labels, and feature types;
3. identify missing values, duplicates, or suspicious variables;
4. visualise class distribution;
5. create a very simple baseline model or majority-class baseline;
6. write a short reflection on what the dataset represents and what it does not represent.

### Deliverable
A short notebook or worksheet containing:
- initial observations;
- one basic baseline result;
- a brief reflection on dataset realism.

### Main lesson
Before building models, students must understand the data and the decision context.

---

## Week 2 Lab — Classical Machine Learning for Security Analytics

### Aim
To apply and compare classical machine-learning methods on a cybersecurity task.

### Learning focus
- preprocessing;
- feature engineering;
- model comparison;
- security-relevant metrics.

### Suggested tasks
1. preprocess the chosen dataset;
2. split the data carefully into training and test sets;
3. train at least two classical models;
4. compare precision, recall, F1-score, and confusion matrices;
5. interpret the operational meaning of false positives and false negatives.

### Possible datasets
- phishing classification;
- malicious URL detection;
- simplified intrusion detection;
- email or message classification.

### Deliverable
A notebook and short summary containing:
- preprocessing steps;
- model comparison;
- metric interpretation;
- one paragraph on deployment limitations.

### Main lesson
Model comparison in cybersecurity must focus on operational usefulness, not accuracy alone.

---

## Week 3 Lab — Deep Learning or AI-Assisted Cyber Workflow

### Aim
To expose students to more advanced AI-enabled workflows while maintaining critical judgement.

### Two possible versions

### Option A — Deep-learning-flavoured lab
Students explore a prepared notebook demonstrating:
- simple neural classification;
- sequence or text-based inputs;
- comparison with a classical baseline.

### Option B — Generative-AI-assisted lab
Students use a controlled LLM workflow to:
- summarise alerts or security text;
- classify suspicious content;
- extract entities or investigation clues;
- compare AI-supported outputs with a manual baseline.

### Suggested tasks
1. review a prepared workflow;
2. run a guided analysis;
3. compare output quality with a simpler baseline;
4. identify errors, omissions, or hallucinations;
5. reflect on whether the approach is safe and useful in practice.

### Deliverable
A notebook or structured worksheet with:
- screenshots or outputs;
- comparative observations;
- critical reflection on reliability and trust.

### Main lesson
More advanced AI does not remove the need for human evaluation.

---

## Week 4 Lab — Threat Modelling an AI-Enabled Security System

### Aim
To help students analyse the attack surface of an AI-based cybersecurity workflow.

### Learning focus
- adversarial thinking;
- AI attack surfaces;
- prompt injection;
- poisoning and evasion concepts;
- mitigation design.

### Suggested tasks
1. choose an AI-enabled cyber tool or case;
2. identify assets, trust boundaries, users, and data flows;
3. identify likely attack scenarios;
4. map each scenario to impact and mitigation;
5. produce a short deployment risk judgement.

### Example systems
- phishing analysis assistant;
- alert triage assistant;
- AI-supported SOC summarisation tool;
- ML-based network anomaly detector.

### Deliverable
A one-page threat model or short slide set.

### Main lesson
An AI system must be analysed as a security-critical system, not just as a model.

---

## Week 5 Lab — Deployment Review and Recommendation

### Aim
To bring together the whole module through a structured judgement task.

### Learning focus
- trustworthy deployment;
- explainability;
- privacy;
- governance;
- operational fit;
- recommendation writing.

### Suggested tasks
1. review a capstone case-study brief;
2. assess data, model choice, risks, controls, and monitoring needs;
3. decide whether the proposed system should be:
   - deployed;
   - deployed with restrictions;
   - revised before deployment;
   - rejected;
4. justify the recommendation in both technical and organisational terms.

### Deliverable
A short written review or mini-presentation.

### Main lesson
The most important professional skill is not only building AI, but deciding whether it deserves to be trusted.

---

## Suggested Datasets

The exact datasets may vary depending on teaching preference and licensing, but suitable public or classroom-ready options may include:

- phishing or email classification datasets;
- malicious URL datasets;
- selected intrusion detection datasets;
- simplified network flow datasets;
- selected security text corpora;
- instructor-created toy datasets for safe evaluation.

Students should be reminded that benchmark datasets may be cleaner and less realistic than live operational data.

---

## Submission Style for Labs

Depending on the final assessment design, labs may be submitted as:

- Jupyter notebooks;
- short markdown reports;
- PDF exports of notebooks;
- worksheets with structured answers.

A consistent and simple submission format is recommended across all five weeks.

---

## What Good Lab Work Looks Like

Strong lab work will usually show:

- clear understanding of the problem being solved;
- sensible preprocessing and modelling choices;
- correct use of metrics;
- careful interpretation of results;
- honest discussion of limitations;
- awareness of security and deployment implications.

Weak lab work often shows:

- blind trust in model outputs;
- overfocus on accuracy only;
- missing discussion of false positives and false negatives;
- no reflection on data quality;
- no discussion of realism or risk.

---

## Responsible Practice

Students must:

- use only approved data and tools;
- avoid offensive or intrusive activity outside authorised environments;
- document any use of AI assistance appropriately;
- remain accountable for all submitted work and conclusions.

---

## Suggested Extensions

For stronger students or optional mini-projects, you may add:

- hyperparameter comparison tasks;
- interpretability analysis;
- time-based train/test splits;
- drift discussion using simulated data change;
- comparison between AI-assisted and non-AI workflows;
- short peer review of another group’s deployment judgement.

---

## Summary

The lab component is designed to make the module practical, current, and professionally relevant. It supports technical skill development, but its deeper goal is to help students become **critical users and evaluators** of AI in cybersecurity.
