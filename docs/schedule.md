---
title: "Schedule"
layout: default
nav_order: 3
permalink: "/schedule/"
---

# Course Schedule

## Applied AI for Cybersecurity

This page provides the week-by-week structure for the module.

---

## Weekly Schedule

| Week | Topic | Main Focus | Practical / Academic Emphasis | Lecture Notes |
|---|---|---|---|---|
| 1 | Foundations of Applied AI for Cybersecurity | AI in cyber defence, security data, common use cases, problem framing, strengths and limitations of AI | Building a shared conceptual foundation for the rest of the module | [Week 1](../lectures/week1.html) |
| 2 | Data, Features, and Classical Machine Learning for Security Analytics | Cyber datasets, preprocessing, feature engineering, supervised learning, anomaly detection, and evaluation metrics | Developing evidence-based model selection and interpretation skills | [Week 2](../lectures/week2.html) |
| 3 | Deep Learning and Generative AI in Cybersecurity | Deep learning for cyber data, NLP for threat analysis, LLMs in SOC workflows, benefits and risks of GenAI | Exploring modern AI-enabled cyber workflows with critical awareness | [Week 3](../lectures/week3.html) |
| 4 | Attacking and Defending AI Systems | Adversarial ML, evasion, poisoning, inference attacks, model misuse, prompt injection, and secure design principles | Understanding AI systems as security-critical and attackable assets | [Week 4](../lectures/week4.html) |
| 5 | Trustworthy Deployment, Governance, and Capstone Case Study | Explainability, robustness, privacy, ethics, governance, assurance, and integrated case-based evaluation | Bringing together technical analysis with operational and professional judgement | [Week 5](../lectures/week5.html) |

---

## Weekly Breakdown

### Week 1 — Foundations of Applied AI for Cybersecurity

**Lecture focus**
- What AI means in the context of cybersecurity
- AI, machine learning, deep learning, and generative AI
- Cybersecurity tasks that can be framed as data-driven problems
- Security telemetry, logs, flows, alerts, malware features, and threat intelligence
- Strengths, weaknesses, and common misconceptions about AI in cyber defence

**Lab / workshop**
- Explore a small cybersecurity dataset
- Inspect features, labels, class balance, and missing values
- Build a very simple baseline workflow in Python

**Independent study**
- Review core concepts of AI for security analytics
- Reflect on where AI should and should not be trusted in cyber workflows

---

### Week 2 — Data, Features, and Classical Machine Learning for Security Analytics

**Lecture focus**
- Preprocessing and cleaning cyber data
- Feature engineering for security problems
- Supervised classification and unsupervised anomaly detection
- Data leakage, imbalance, noisy labels, and validation pitfalls
- Metrics for security evaluation: precision, recall, F1, ROC-AUC, false positives

**Lab / workshop**
- Train and compare classical models on a security dataset
- Evaluate model behaviour using confusion matrices and core metrics
- Interpret results from an operational perspective rather than accuracy alone

**Independent study**
- Read about the challenges of evaluating detection models in realistic environments
- Prepare short notes comparing at least two modelling approaches

---

### Week 3 — Deep Learning and Generative AI in Cybersecurity

**Lecture focus**
- When deep learning is useful for cyber data
- Sequence and representation learning for traffic, logs, and malware-related tasks
- NLP for phishing detection, report analysis, and threat intelligence
- LLMs for analyst support, summarisation, rule drafting, and secure coding assistance
- Risks of hallucination, overconfidence, and poor prompt design

**Lab / workshop**
- Use a guided AI-assisted workflow for alert or text-based security analysis
- Compare AI-supported outputs with simpler non-AI methods
- Critique reliability, usefulness, and failure modes

**Independent study**
- Reflect on appropriate and inappropriate uses of LLMs in cybersecurity operations
- Record examples of productivity gains versus security risks

---

### Week 4 — Attacking and Defending AI Systems

**Lecture focus**
- Threat models for AI-based systems
- Adversarial examples and evasion attacks
- Data poisoning and backdoor risks
- Inference attacks, model extraction, and privacy leakage
- Prompt injection and insecure output handling in LLM applications
- Defensive principles for safer AI deployment

**Lab / workshop**
- Analyse a simplified adversarial or prompt injection case
- Identify assets, attack surfaces, impacts, and mitigations
- Produce a short threat model for an AI-enabled cyber tool

**Independent study**
- Review common AI attack patterns
- Prepare a brief mitigation summary for a selected threat scenario

---

### Week 5 — Trustworthy Deployment, Governance, and Capstone Case Study

**Lecture focus**
- Why accuracy alone is not enough
- Robustness, explainability, privacy, and fairness
- Model drift, monitoring, assurance, and incident response
- Governance and policy questions for AI in security
- Integrated case study: should an AI-enabled security system be deployed?

**Lab / workshop**
- Evaluate a case-based deployment scenario
- Produce technical and managerial recommendations
- Discuss whether the system should be adopted, revised, or rejected

**Independent study**
- Consolidate weekly learning into a final critical perspective
- Use findings to support the final report or portfolio submission

---

## Suggested Study Rhythm

A typical week may follow this pattern:

- **Before class:** short reading and concept preparation
- **Lecture:** core technical and conceptual material
- **Lab:** practical exercise and guided analysis
- **Seminar / discussion:** critique, reflection, and interpretation
- **After class:** notebook completion and short reflective notes

---

## Assessment Mapping by Week

| Week | Learning Contribution | Assessment Relevance |
|---|---|---|
| 1 | Problem framing, context, and data awareness | Portfolio foundation |
| 2 | Data preparation, modelling, and evaluation | Portfolio and final report |
| 3 | Advanced applications and GenAI critique | Portfolio and final report |
| 4 | AI security threats and mitigations | Final report and case analysis |
| 5 | Trustworthy deployment and integrated judgement | Final report conclusion and recommendations |

---

## Notes for Course Website Development

This schedule page is designed to work well with a GitHub Pages course site. A natural next step is to create:

- `lectures/week1.md`
- `lectures/week2.md`
- `lectures/week3.md`
- `lectures/week4.md`
- `lectures/week5.md`

You can also add companion pages such as:

- `labs.md`
- `assessment.md`
- `references.md`
- `project.md`

These additions would give the course website a fuller teaching structure and make the module easier for students to navigate.
