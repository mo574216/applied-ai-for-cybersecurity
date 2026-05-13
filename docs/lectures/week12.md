---
title: "Week 12: SecMLOps, Deployment, Monitoring, and Final Integration"
layout: default
permalink: /lectures/week12/
---

# Week 12: SecMLOps, Deployment, Monitoring, and Final Integration
## From Model Prototype to Governed Security System

Welcome to Week 12 of **Applied AI for Cybersecurity**.

This final week brings the course together. Across the course, we studied AI for intrusion detection, DDoS detection, malware and phishing detection, security operations, vulnerability management, cloud and IoT security, LLM-assisted security, explainability, and adversarial risk.

This week asks:

> How do we deploy, monitor, maintain, secure, and govern AI-based cybersecurity systems in practice?

The central lesson is:

> An AI cybersecurity model is not finished when it achieves a good test score. It must be deployed as part of a secure, monitored, auditable, and governable system.

---

# 1. Learning Objectives

By the end of this week, you should be able to:

1. Explain the difference between model development and operational deployment.
2. Describe MLOps and SecMLOps.
3. Identify security risks in the ML lifecycle.
4. Explain model versioning, dataset versioning, and feature pipeline management.
5. Define monitoring metrics for AI cybersecurity systems.
6. Explain data drift, concept drift, and model degradation.
7. Design a rollback plan for faulty model deployment.
8. Explain how human feedback loops should be governed.
9. Prepare a deployment readiness review for an AI cybersecurity system.
10. Integrate data, model, explanation, monitoring, and governance into a final design.

---

# 2. From ML Prototype to Security System

A prototype model usually focuses on:

```text
dataset
features
model
metrics
```

An operational AI security system must also include:

```text
data pipeline
feature pipeline
model versioning
threshold management
alert workflow
explanation
human approval
monitoring
audit logs
drift detection
rollback
security controls
governance
```

A model may perform well in a notebook but fail in production because live data differs from training data, logs are missing, feature extraction changes, labels are delayed, analysts do not trust outputs, false positives overload the SOC, or attackers adapt.

---

# 3. MLOps and SecMLOps

MLOps applies engineering discipline to the machine learning lifecycle.

It includes:

- data versioning
- model versioning
- automated testing
- deployment pipelines
- monitoring
- retraining
- rollback
- documentation
- governance

SecMLOps extends this with security controls:

- trusted training data
- secured feature pipeline
- protected model artefacts
- threshold-change approval
- feedback poisoning controls
- audit logs
- rollback procedures
- adversarial testing
- privacy controls
- human approval for high-impact actions

---

# 4. AI Cybersecurity System Lifecycle

A mature lifecycle may look like:

```text
1. Problem definition
2. Threat model
3. Data collection
4. Data engineering
5. Feature design
6. Model development
7. Evaluation
8. Explainability review
9. Adversarial testing
10. Deployment approval
11. Production monitoring
12. Feedback collection
13. Retraining governance
14. Rollback and incident response
```

NIST AI RMF is useful for thinking about AI risk management across the lifecycle.

---

# 5. Deployment Risks

| Risk | Example |
|---|---|
| Data pipeline failure | Endpoint logs stop arriving |
| Feature mismatch | Production feature differs from training feature |
| Model drift | New attack patterns appear |
| Concept drift | Normal user behaviour changes |
| Threshold error | Too many false positives |
| Unsafe automation | Model isolates production server wrongly |
| Feedback poisoning | Wrong analyst labels affect retraining |
| Privacy leakage | Sensitive logs exposed in model outputs |
| Model theft | API queries reveal model behaviour |
| Supply-chain risk | Untrusted library or model artefact compromised |

---

# 6. Versioning

## 6.1 Dataset Versioning

Track:

- data source
- collection period
- preprocessing logic
- labels
- exclusions
- class distribution
- privacy handling
- known limitations

## 6.2 Feature Versioning

Track:

- feature definitions
- aggregation windows
- encoding rules
- missing-value handling
- enrichment sources
- threat intelligence timestamp

## 6.3 Model Versioning

Track:

- model type
- hyperparameters
- training dataset
- evaluation results
- threshold
- explanation method
- deployment date
- approved owner
- rollback version

A production alert should be traceable:

```text
Which model version produced this decision?
Which data and feature pipeline were used?
Which threshold was active?
What explanation was shown?
Who approved the action?
```

---

# 7. Monitoring

## 7.1 Model Performance Monitoring

Monitor:

- precision
- recall
- false positive rate
- false negative rate
- alert volume
- detection latency
- analyst override rate
- incident confirmation rate
- missed attack reports
- model confidence distribution

## 7.2 Data Monitoring

Monitor:

- missing fields
- schema changes
- feature distribution changes
- data volume
- delayed logs
- duplicate events
- enrichment failures
- threat-intelligence feed failures

## 7.3 Operational Monitoring

Monitor:

- analyst workload
- response time
- number of escalations
- number of automatic actions
- rollback events
- user complaints
- business disruption
- incident outcomes

---

# 8. Drift

## 8.1 Data Drift

Data drift means input data changes.

Example:

```text
A new cloud service changes normal API patterns.
```

## 8.2 Concept Drift

Concept drift means the relationship between features and labels changes.

Example:

```text
Attackers change phishing templates.
```

## 8.3 Detection Drift

Detection drift means operational detection quality changes.

Example:

```text
Recall drops because attackers adopt low-and-slow behaviour.
```

Drift should trigger review, not automatic retraining without governance.

---

# 9. Retraining Governance

Retraining can improve models, but it can also introduce risk.

Questions:

- Who approves retraining?
- What data is included?
- Are labels validated?
- Is poisoning considered?
- Is previous performance compared?
- Is rollback possible?
- Are thresholds recalibrated?
- Are explanations reviewed?

Unsafe retraining:

```text
Automatically retrain every night on all analyst feedback.
```

Safer retraining:

```text
collect feedback
validate labels
review drift
test candidate model
compare with current model
perform adversarial checks
approve deployment
monitor after release
```

---

# 10. Human Feedback Loops

Analyst feedback can improve AI systems.

Useful feedback:

- true positive
- false positive
- false negative
- duplicate alert
- benign but noisy
- needs more context
- action taken
- outcome confirmed

Feedback should be stored with:

- analyst role
- timestamp
- confidence
- evidence
- closure reason
- final incident outcome

Feedback can be wrong, inconsistent, or manipulated. It must be governed.

---

# 11. Rollback Planning

Rollback may be needed if:

- false positives increase sharply
- critical attacks are missed
- feature pipeline breaks
- model behaves unexpectedly
- analysts reject outputs
- automation causes disruption
- drift is detected
- adversarial weakness is found

A rollback plan should specify:

- previous stable model
- rollback trigger
- approval authority
- communication process
- data preservation
- post-rollback review

---

# 12. Case Study 1: IDS Model Deployment Failure

## Scenario

An IDS model performs well on test data. After deployment, alert volume increases by 500%.

Cause:

```text
New backup system creates traffic not present in training data.
```

Lessons:

- training data did not include new normal behaviour
- monitoring should detect feature distribution change
- threshold review may be needed
- analysts need a way to mark benign operational changes
- rollback may be required

---

# 13. Case Study 2: Phishing Model Drift

## Scenario

A phishing detector relies heavily on urgency keywords. Attackers shift to neutral language and QR-code phishing.

Result:

```text
Recall drops.
More phishing emails reach inboxes.
```

Lessons:

- attackers adapt
- model needs drift monitoring
- feature set may need update
- new data sources may be needed
- human reports are important feedback

---

# 14. Case Study 3: Unsafe Automation

## Scenario

A model assigns high risk to cloud activity and automatically revokes an administrator account. The activity was part of approved emergency maintenance.

Impact:

```text
service recovery delayed
critical system remains unavailable
incident response slowed
```

Lessons:

- high-impact actions need approval
- business calendar context matters
- automation boundaries must be defined
- model confidence is not enough

---

# 15. Deployment Readiness Checklist

Before deployment, answer:

## Problem and Decision

- What decision does the model support?
- What action follows each output?
- Who is responsible?

## Data

- Are data sources reliable?
- Are labels validated?
- Is privacy protected?
- Is data representative?

## Model

- What baselines were compared?
- What metrics were used?
- Was class imbalance considered?
- Was adversarial testing performed?

## Explainability

- Can analysts understand the output?
- Does explanation show evidence and uncertainty?
- Is explanation safe to disclose?

## Operations

- What is the alert workflow?
- What requires human approval?
- What is the rollback plan?
- What will be monitored?

## Governance

- Who owns the model?
- Who approves threshold changes?
- Who approves retraining?
- How are decisions audited?

---

# 16. Final Project Integration

A strong final project should include:

1. Security problem definition
2. Threat model
3. Data sources
4. Feature design
5. AI method choice
6. Evaluation metrics
7. False positive and false negative analysis
8. Explainability plan
9. Adversarial risk analysis
10. Privacy considerations
11. Human oversight boundaries
12. Deployment plan
13. Monitoring plan
14. Rollback plan
15. References

---

# 17. Week 12 Summary

```text
A model is not a complete security system.
Deployment requires data pipelines, monitoring, governance, rollback, and human oversight.
Drift can affect data, concepts, and operational performance.
Feedback loops must be validated.
High-impact security actions require approval.
Every production model decision should be traceable.
SecMLOps helps secure the ML lifecycle itself.
```

Final takeaway:

> Applied AI for Cybersecurity ends not with model accuracy, but with responsible deployment, monitoring, and governance.

---

# 18. Lab Sheet 12: AI Cybersecurity System Deployment Review

## Lab Overview

In this lab, you will review an AI cybersecurity system for deployment readiness.

## Lab Dataset A: System Proposal

A university wants to deploy an AI phishing detector.

```text
Input: email headers, URL features, sender reputation, body text
Model: transformer-based classifier
Output: phishing probability
Action:
- score < 50: deliver
- score 50–80: warning banner
- score > 80: quarantine
- score > 95: block sender domain automatically
Feedback: users and analysts can mark emails as phishing or safe
Retraining: monthly automatic retraining
```

## Lab Task 1 — Deployment Risk Review

| Risk Area | Concern | Mitigation |
|---|---|---|
| Data quality |  |  |
| Labels |  |  |
| Privacy |  |  |
| Explainability |  |  |
| Adversarial evasion |  |  |
| Automation |  |  |
| Feedback poisoning |  |  |
| Drift |  |  |
| Rollback |  |  |
| Governance |  |  |

## Lab Task 2 — Monitoring Plan

| Monitoring Area | Metric | Why It Matters |
|---|---|---|
| Model performance |  |  |
| Data pipeline |  |  |
| Analyst workload |  |  |
| User impact |  |  |
| Drift |  |  |
| Automation safety |  |  |

## Lab Task 3 — Rollback Plan

Write a rollback plan including:

- rollback triggers
- previous model version
- approval authority
- communication plan
- evidence preservation
- post-rollback review

## Lab Task 4 — Human Oversight Boundaries

| Action | Automate / Approval / Prohibit | Reason |
|---|---|---|
| Add warning banner |  |  |
| Quarantine email |  |  |
| Block sender domain |  |  |
| Delete email from all inboxes |  |  |
| Notify user |  |  |
| Retrain model |  |  |
| Change threshold |  |  |

## Lab Task 5 — Final Deployment Recommendation

Write a short recommendation:

```text
deploy as proposed
deploy with changes
do not deploy yet
```

Justify your decision.

## Lab Deliverable

Submit a worksheet containing:

1. Deployment risk review.
2. Monitoring plan.
3. Rollback plan.
4. Human oversight boundary table.
5. Final deployment recommendation.

Recommended length:

```text
1200–1800 words
```

---

# 19. Exercises

## Exercise 1 — Concept Check

1. What is MLOps?
2. What is SecMLOps?
3. Why is model versioning important?
4. What is data drift?
5. What is concept drift?
6. Why can feedback loops be risky?
7. What is rollback?
8. Why should threshold changes be governed?
9. What should be monitored after deployment?
10. Why is a model not a complete security system?

## Exercise 2 — Short Analytical Answer

Write 250–300 words:

**Question:** Why is deployment monitoring essential for AI-based cybersecurity systems?

## Exercise 3 — Final Project Checklist

Create a 15-item checklist for deploying an AI malware detector, AI IDS model, or AI SOC triage model.

## Exercise 4 — Drift Scenario

A DDoS detector performs well for six months, then recall drops sharply. Explain possible causes and response actions.

---

# 20. Further Reading

## Core Reading

1. **NIST AI Risk Management Framework**  
   <https://www.nist.gov/itl/ai-risk-management-framework>

2. **NIST SP 800-204C: DevSecOps for Cloud-Native Applications**  
   <https://csrc.nist.gov/pubs/sp/800/204/c/final>

3. **NIST SP 800-218: Secure Software Development Framework**  
   <https://csrc.nist.gov/pubs/sp/800/218/final>

4. **MITRE ATLAS**  
   <https://atlas.mitre.org/>

5. **OWASP Machine Learning Security Top 10**  
   <https://owasp.org/www-project-machine-learning-security-top-10/>

6. **MLflow Documentation**  
   <https://mlflow.org/docs/latest/index.html>

## Suggested Search Topics

- SecMLOps
- secure ML pipelines
- model drift monitoring
- AI governance for cybersecurity
- machine learning model versioning
- adversarial ML deployment
- model rollback
- AI incident response
- ML monitoring dashboards
