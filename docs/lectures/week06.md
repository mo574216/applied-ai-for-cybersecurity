---
title: "Week 06: Explainable AI for Cybersecurity"
layout: default
permalink: /lectures/week06/
---

# Week 06: Explainable AI for Cybersecurity  
## From Model Scores to Analyst-Ready Evidence

Welcome to Week 6 of **Applied AI for Cybersecurity**.

In previous weeks, we studied how AI can be applied to cybersecurity data, network intrusion detection, DDoS detection, malware detection, phishing detection, malicious URL detection, and deep learning for cybersecurity.

This week focuses on a critical question:

> If an AI system says something is malicious, how can a security analyst understand, trust, challenge, and act on that result?

This is the role of **Explainable AI**, often abbreviated as **XAI**.

The central lesson this week is:

> In cybersecurity, an explanation is not only a technical add-on. It is part of the security decision process.

A prediction such as:

```text
Malicious probability: 94%
```

is not enough for most security decisions. Analysts need to know:

- What evidence increased the risk?
- What evidence reduced the risk?
- What context is missing?
- How confident is the model?
- What action is proportionate?
- Could the explanation itself help an attacker evade detection?

---

# 1. Learning Objectives

By the end of this week, you should be able to:

1. Explain why explainability matters in cybersecurity.
2. Distinguish between interpretability, explainability, transparency, and accountability.
3. Explain the difference between local and global explanations.
4. Describe common explanation methods, including feature importance, surrogate models, LIME, SHAP, counterfactual explanations, and rule-based explanations.
5. Explain how explanations support analysts in phishing, malware, intrusion detection, and SOC triage.
6. Identify what makes an explanation useful or misleading.
7. Discuss the security risks of explanations, including information leakage and evasion support.
8. Design analyst-friendly explanations for AI cybersecurity outputs.
9. Evaluate explanation quality using cybersecurity criteria.
10. Explain why explainability must be connected to human oversight and response decisions.

---

# 2. Why Explainability Matters in Cybersecurity

AI systems in cybersecurity may influence decisions such as:

- Blocking a URL
- Quarantining an email
- Isolating a host
- Escalating an incident
- Prioritising a vulnerability
- Marking a user as high risk
- Flagging a file as malware
- Classifying traffic as DDoS
- Assigning a SOC alert priority

These decisions can affect users, services, business operations, privacy, and legal responsibility.

A black-box prediction may be technically impressive but operationally weak.

Example:

```text
Prediction: malicious
Confidence: 96%
```

This output does not tell the analyst:

- Why the model thinks the sample is malicious
- Whether the evidence is strong or weak
- Whether important context is missing
- Whether a false positive would be costly
- Whether the action should be automatic or require human approval

A better AI output would be:

```text
Prediction: suspicious endpoint behaviour
Confidence: medium-high

Risk increased because:
- winword.exe launched powershell.exe
- PowerShell used an encoded command
- The process contacted a newly registered domain
- A new scheduled task was created

Risk reduced because:
- The endpoint belongs to the IT administration team
- Some PowerShell activity is expected on this host

Missing evidence:
- Sandbox result for downloaded file
- User confirmation
- Threat intelligence status of the domain

Recommended action:
- Preserve logs
- Submit file to sandbox
- Escalate for analyst review
- Do not isolate automatically unless further evidence appears
```

The second output supports investigation and decision-making.

---

# 3. Interpretability, Explainability, Transparency, and Accountability

These terms are related but not identical.

| Term | Meaning | Cybersecurity Example |
|---|---|---|
| Interpretability | The model itself is understandable | A small decision tree for phishing detection |
| Explainability | The system provides reasons for an output | “Flagged because URL is newly registered and contains login keywords” |
| Transparency | Information is available about data, model, and process | Documentation of features, training data, and limitations |
| Accountability | Humans or organisations remain responsible for decisions | Analyst approval required before isolating a production server |

## 3.1 Interpretable Model

Some models are easier to understand by design.

Examples:

- Decision trees
- Logistic regression
- Rule lists
- Small scoring models

Example rule:

```text
IF domain_age < 7 days
AND URL contains "login"
AND sender domain does not match claimed organisation
THEN phishing risk = high
```

This is interpretable because the reasoning is visible.

## 3.2 Explainable Black-Box Model

A black-box model may be difficult to understand internally, but explanation methods can estimate why it produced a specific output.

Examples:

- SHAP explanations
- LIME explanations
- Feature importance
- Counterfactual explanations
- Attention visualisation
- Example-based explanations

SHAP describes itself as a game-theoretic approach for explaining the output of machine learning models. It connects local explanations with Shapley values from cooperative game theory. Further reading: [SHAP documentation](https://shap.readthedocs.io/).

LIME is designed to explain predictions of black-box classifiers by learning interpretable local surrogate models around individual predictions. Further reading: [LIME documentation](https://lime-ml.readthedocs.io/) and [LIME GitHub repository](https://github.com/marcotcr/lime).

---

# 4. What Makes Cybersecurity Explanations Different?

Explainability in cybersecurity has special requirements.

In ordinary classification, an explanation may answer:

```text
Why did the model classify this image as a cat?
```

In cybersecurity, an explanation must often support an operational decision:

```text
Should this host be isolated?
Should this email be blocked?
Should this alert be escalated?
Should this user session be revoked?
```

Therefore, cybersecurity explanations must be:

- Evidence-based
- Actionable
- Context-aware
- Uncertainty-aware
- Analyst-readable
- Risk-sensitive
- Operationally relevant
- Safe to disclose

## Important Difference

A technically correct explanation may still be operationally poor.

Example:

```text
The model classified the URL as malicious because token_17 had high weight.
```

This may be mathematically accurate but not useful to an analyst.

Better:

```text
The URL is suspicious because it uses a newly registered domain, contains login-related terms, impersonates a university service, and redirects through two unrelated domains.
```

---

# 5. Local and Global Explanations

## 5.1 Local Explanation

A local explanation explains one prediction.

Example:

```text
Why was this specific email classified as phishing?
```

Useful for:

- Analyst review
- Incident investigation
- User warning banners
- Explaining individual alerts
- Deciding whether to override a model

Example:

```text
This email was flagged because:
- sender domain does not match university domain
- message contains urgent password reset language
- link points to a newly registered domain
- greeting is generic
```

## 5.2 Global Explanation

A global explanation explains how the model generally behaves.

Example:

```text
Which features usually influence this phishing detector?
```

Useful for:

- Model validation
- Governance
- Audit
- Debugging
- Bias detection
- Feature review
- Security risk analysis

Example:

```text
The phishing detector generally relies on:
1. Domain reputation
2. URL age
3. Sender authentication result
4. Link mismatch
5. Urgency keywords
```

## 5.3 Why Both Are Needed

Local explanations help with individual decisions.

Global explanations help with model governance.

A security team needs both.

---

# 6. Feature Importance

Feature importance describes which input features most influence model predictions.

Example for malicious URL detection:

| Feature | Importance |
|---|---:|
| domain_age_days | High |
| url_entropy | High |
| redirect_count | Medium |
| suspicious_keyword_count | Medium |
| https_present | Low |
| url_length | Medium |

Feature importance can help analysts understand general model behaviour.

## Limitations

Feature importance may be misleading if:

- Features are correlated
- The model learned dataset artefacts
- Importance is global but the analyst needs local explanation
- The feature is not meaningful to analysts
- The model relies on unstable features
- Attackers can easily manipulate important features

Example:

If a malware model relies heavily on `source_folder_name`, it may indicate data leakage rather than real malware behaviour.

---

# 7. Surrogate Models

A surrogate model is a simpler model trained to approximate a more complex model.

Example:

```text
Complex model: deep neural network
Surrogate model: small decision tree
```

The surrogate model is not the original model. It is an approximation.

## Use Case

A SOC team may use a complex model for alert prioritisation. A surrogate decision tree may help explain the general behaviour:

```text
IF asset criticality is high
AND threat intelligence match exists
AND endpoint suspicious behaviour is present
THEN incident priority is high
```

## Limitations

- The surrogate may not perfectly match the original model.
- It may hide important complexity.
- It can create false confidence.
- It should be validated for fidelity.

Fidelity means:

```text
How well does the explanation model approximate the original model?
```

---

# 8. LIME

LIME stands for **Local Interpretable Model-Agnostic Explanations**.

The basic idea is:

```text
Take one prediction
Perturb the input nearby
Observe how the black-box model changes
Train a simple local model
Use that local model as the explanation
```

In simpler terms:

> LIME tries to explain one decision by approximating the model near that specific input.

## Example: Phishing Email

Suppose a phishing detector flags an email.

LIME may identify influential words or features:

```text
"urgent" → increases phishing risk
"verify" → increases phishing risk
unknown sender domain → increases phishing risk
official university domain absent → increases phishing risk
```

## Strengths

- Model-agnostic
- Useful for individual predictions
- Can be applied to text and tabular data
- Often easier to understand than deep model internals

## Limitations

- Local explanations can be unstable
- Results depend on perturbation strategy
- May not reflect true model reasoning globally
- Can be misleading if features are poorly designed
- Analysts may overtrust the explanation

Further reading:

- LIME documentation:  
  <https://lime-ml.readthedocs.io/>
- LIME GitHub repository:  
  <https://github.com/marcotcr/lime>

---

# 9. SHAP

SHAP stands for **SHapley Additive exPlanations**.

SHAP is based on Shapley values from cooperative game theory. The idea is to assign each feature a contribution to the model output.

For one prediction, SHAP can show:

```text
Feature A increased the risk by +0.20
Feature B reduced the risk by -0.05
Feature C increased the risk by +0.15
```

## Example: Malicious URL Detection

Prediction:

```text
URL risk score: 0.86
```

SHAP-style explanation:

| Feature | Contribution |
|---|---:|
| domain_age_days = 2 | +0.24 |
| url_contains_login = yes | +0.18 |
| redirect_count = 3 | +0.13 |
| domain_reputation = unknown | +0.10 |
| https_present = yes | -0.03 |

This tells the analyst what increased and reduced the score.

## Strengths

- Strong theoretical foundation
- Supports local and global explanations
- Useful for feature contribution analysis
- Works with many model types

## Limitations

- Can be computationally expensive
- Explanations depend on background data
- Correlated features can complicate interpretation
- Feature contributions may still be hard for analysts to understand
- Explanations can expose model behaviour to attackers

Further reading:

- SHAP documentation:  
  <https://shap.readthedocs.io/>
- Introduction to explainable AI with Shapley values:  
  <https://shap.readthedocs.io/en/latest/example_notebooks/overviews/An%20introduction%20to%20explainable%20AI%20with%20Shapley%20values.html>

---

# 10. Counterfactual Explanations

A counterfactual explanation answers:

> What minimum change would alter the model decision?

Example:

```text
This URL would no longer be classified as high risk if:
- the domain were older than 180 days
- no login-related terms were present
- redirect count were zero
```

Counterfactuals can help analysts understand decision boundaries.

## Cybersecurity Use

Counterfactual explanations may be useful for:

- Debugging models
- Understanding thresholds
- Explaining why a vulnerability was prioritised
- Understanding why a URL was blocked
- Finding fragile model behaviour

## Security Risk

Counterfactuals can also help attackers.

Example:

```text
To avoid detection, remove "verify", reduce URL entropy, and use an older domain.
```

Therefore, counterfactual explanations should be handled carefully.

The level of explanation shown to internal analysts may be different from the explanation shown to external users.

---

# 11. Rule-Based Explanations

Rule-based explanations express model logic as human-readable rules.

Example:

```text
IF failed_login_count_5min > 10
AND login_country is new
AND device is unknown
THEN account risk = high
```

Rule-based explanations are useful because security teams already use rules and policies.

## Advantages

- Easy to communicate
- Good for audit
- Compatible with security playbooks
- Useful for analyst training
- Good for simple risk scoring

## Limitations

- May oversimplify complex model behaviour
- Can be brittle
- Attackers may evade known rules
- Hard to cover all variations of malicious behaviour

---

# 12. Example-Based Explanations

Example-based explanations show similar past cases.

Example:

```text
This alert resembles previous confirmed phishing cases because:
- similar sender spoofing pattern
- similar domain structure
- similar urgent language
- similar fake login page
```

Useful for:

- Analyst training
- Case comparison
- Malware family similarity
- Phishing campaign clustering
- Threat intelligence enrichment

## Risks

- Similarity may be superficial
- Past labels may be wrong
- Old attacks may not represent current attacks
- Similar examples may reveal sensitive incident data

---

# 13. Explanations for Different Cybersecurity Tasks

## 13.1 Phishing Detection

Poor output:

```text
Phishing probability: 91%
```

Better explanation:

```text
Risk increased because:
- sender domain does not match the claimed university identity
- the email asks for password verification
- the message uses urgent language
- the link points to a newly registered domain
- the greeting is generic

Risk reduced because:
- no attachment is present
- sender IP is not on a known blocklist

Recommended action:
- quarantine the message
- submit URL for analysis
- search for similar emails
```

---

## 13.2 Malware Detection

Poor output:

```text
Malware probability: 96%
```

Better explanation:

```text
Risk increased because:
- file is unsigned
- entropy is high
- imports include process injection APIs
- file contains suspicious command strings
- runtime behaviour created persistence

Missing evidence:
- sandbox report
- file origin
- user download context

Recommended action:
- block execution
- submit file to sandbox
- search for the hash across endpoints
```

---

## 13.3 Network Intrusion Detection

Poor output:

```text
Attack probability: 88%
```

Better explanation:

```text
Risk increased because:
- one host connected to 200 destination ports in 30 seconds
- most connections failed
- destination host is business-critical
- source host has no approved scanning role

Risk reduced because:
- no known malicious IP was involved
- no exploitation payload was observed

Recommended action:
- verify whether source host is an approved scanner
- check recent vulnerability scanning schedule
- escalate if not approved
```

---

## 13.4 DDoS Detection

Poor output:

```text
DDoS probability: 84%
```

Better explanation:

```text
Risk increased because:
- request rate increased 20x within five minutes
- API latency increased from 200 ms to 4 seconds
- repeated requests targeted an expensive endpoint
- payment gateway timeouts started

Risk reduced because:
- course registration opened at the same time
- traffic countries match expected student audience

Recommended action:
- rate-limit the expensive endpoint
- challenge suspicious sessions
- avoid broad country blocking unless stronger evidence appears
```

---

## 13.5 SOC Alert Triage

Poor output:

```text
Incident priority: high
```

Better explanation:

```text
Priority is high because:
- sensitive finance folder was accessed
- large download occurred
- endpoint executed encoded PowerShell
- related domain appears in threat intelligence
- host belongs to finance department

Context reducing certainty:
- user is travelling
- some finance access may be expected

Recommended action:
- preserve logs
- confirm user activity
- isolate endpoint only after analyst approval
```

---

# 14. Evaluating Explanation Quality

An explanation should be evaluated, not accepted automatically.

## Useful Criteria

| Criterion | Question |
|---|---|
| Correctness | Does the explanation reflect the model’s actual behaviour? |
| Fidelity | Does it approximate the model accurately? |
| Usefulness | Does it help the analyst make a decision? |
| Clarity | Is it understandable without ML expertise? |
| Completeness | Does it include key evidence and missing context? |
| Actionability | Does it suggest appropriate next steps? |
| Uncertainty | Does it show confidence and limitations? |
| Context-awareness | Does it include business/security context? |
| Safety | Could the explanation help attackers evade detection? |
| Consistency | Are similar cases explained similarly? |

## Analyst-Centred Question

The most important question is:

> Does this explanation help a security analyst decide what to do next?

If not, the explanation is insufficient.

---

# 15. Explanation Failure Modes

Explanations can fail.

| Failure Mode | Example |
|---|---|
| Too technical | “Feature 42 contributed +0.31” |
| Too vague | “Suspicious behaviour detected” |
| Misleading | Explanation highlights irrelevant feature |
| Unstable | Similar inputs produce very different explanations |
| Incomplete | Missing risk-reducing evidence |
| Overconfident | No uncertainty shown |
| Unsafe | Reveals exact evasion thresholds |
| Not actionable | No recommended next step |
| Context-blind | Ignores user role, asset value, or business event |

## Example of Poor Explanation

```text
Risk high because model confidence is high.
```

This is circular and unhelpful.

## Better Explanation

```text
Risk is high because the host contacted a rare domain, downloaded an unknown executable, and created a scheduled task. The domain has no known reputation score, so confidence is medium rather than high.
```

---

# 16. Explanation Risks and Security Trade-Offs

Explainability has security benefits, but it also creates risks.

## 16.1 Benefits

- Helps analysts investigate
- Reduces blind trust
- Supports auditing
- Improves model debugging
- Helps identify data leakage
- Supports human accountability
- Improves incident documentation

## 16.2 Risks

- Attackers may learn evasion strategies
- Explanations may expose sensitive features
- Internal detection logic may leak
- Users may overtrust explanations
- Poor explanations may mislead analysts
- Explanations may reveal confidential incident data

## 16.3 Internal vs External Explanation

Different audiences need different levels of detail.

| Audience | Explanation Level |
|---|---|
| SOC analyst | Detailed evidence and context |
| End user | Simple warning and safe action |
| Manager | Business impact and priority |
| Auditor | Governance and decision trail |
| External party | Limited explanation to avoid leakage |

Example:

Internal analyst explanation:

```text
Flagged because URL contains login keyword, domain age is 2 days, redirect count is 4, and page similarity to known university login page is high.
```

End-user warning:

```text
This link appears suspicious and may impersonate a trusted service. Do not enter your password.
```

---

# 17. XAI and Trustworthy AI

Explainability is one property of trustworthy AI, but it is not enough by itself.

A model can be explainable but still:

- inaccurate
- biased
- insecure
- privacy-invasive
- poorly monitored
- operationally unsafe

NIST’s AI Risk Management Framework lists explainable and interpretable as part of trustworthy AI, alongside other characteristics such as validity, reliability, safety, security and resilience, accountability and transparency, privacy enhancement, and fairness with harmful bias managed. Further reading: [NIST AI Risk Management Framework](https://www.nist.gov/itl/ai-risk-management-framework).

DARPA’s Explainable AI programme aimed to create machine learning techniques that produce more explainable models while maintaining strong learning performance, and to help users understand, appropriately trust, and effectively manage AI systems. Further reading: [DARPA Explainable AI](https://www.darpa.mil/research/programs/explainable-artificial-intelligence).

---

# 18. Case Study 1: Explaining a Phishing Detector

## Scenario

A phishing detector flags the following email:

```text
Subject: Immediate mailbox verification required

Dear user,

Your university account will be disabled unless you verify your mailbox today.

Click here:
http://university-login-secure.example-reset.net/verify

IT Support
```

Model output:

```text
Phishing probability: 93%
```

## Possible Explanation

Risk-increasing evidence:

```text
urgent language
generic greeting
password/account verification request
non-university domain
login-related URL terms
new or unknown domain
```

Risk-reducing evidence:

```text
no attachment
no known malware URL match
```

Missing context:

```text
official IT campaign status
sender authentication result
whether other users received similar messages
```

Recommended action:

```text
quarantine email
analyse URL safely
search for similar messages
warn affected users if campaign is confirmed
```

## Main Lesson

A phishing explanation should combine text, sender, URL, and organisational context.

---

# 19. Case Study 2: Explaining a Malware Classifier

## Scenario

A malware classifier flags a file:

```text
filename: invoice_viewer.exe
signature: unsigned
entropy: high
imports: VirtualAlloc, WriteProcessMemory, CreateRemoteThread
strings: powershell -enc, http://unknown-domain.example/update.bin
```

Model output:

```text
Malware probability: 96%
```

## Possible Explanation

Risk-increasing evidence:

```text
file is unsigned
high entropy suggests packing or encryption
imports are associated with process injection
contains encoded PowerShell string
contains unknown download URL
```

Risk-reducing evidence:

```text
no sandbox result yet
file origin unknown
some administrative tools may use similar APIs
```

Recommended action:

```text
block execution temporarily
submit to sandbox
check whether file exists on other endpoints
verify download source
```

## Main Lesson

A good malware explanation should distinguish between suspicious indicators and proof of maliciousness.

---

# 20. Case Study 3: Explanation Risk

## Scenario

A malicious URL detection service shows external users this explanation:

```text
Blocked because:
- URL entropy > 4.2
- domain age < 7 days
- redirect count > 2
- login keyword present
```

## Security Question

Could this explanation help attackers?

## Discussion

Yes. The explanation reveals thresholds and feature logic that attackers may use to adjust URLs.

Possible attacker changes:

```text
reduce entropy
wait for domain age to increase
reduce redirects
avoid login keyword
```

## Safer External Explanation

```text
This link appears suspicious because it has characteristics commonly associated with credential theft. Do not enter your password.
```

## Main Lesson

Explainability must be balanced with security. Internal analyst explanations can be detailed; external explanations may need to be limited.

---

# 21. Week 6 Summary

This week focused on Explainable AI for Cybersecurity.

Key points:

```text
Cybersecurity decisions require reasons, not only scores.

Interpretability, explainability, transparency, and accountability are related but different.

Local explanations explain one prediction.

Global explanations explain general model behaviour.

Feature importance, surrogate models, LIME, SHAP, counterfactuals, rules, and examples can all support explanation.

Explanations must be useful to analysts, not only technically correct.

Good explanations include risk-increasing evidence, risk-reducing evidence, missing context, uncertainty, and recommended next steps.

Explanations can also create security risks by revealing detection logic or helping attackers evade models.

Explainability is part of trustworthy AI, but it does not replace accuracy, robustness, privacy, monitoring, or governance.
```

Final takeaway:

> A good cybersecurity explanation helps the analyst understand the evidence, judge uncertainty, and choose a proportionate response.

---

# 22. Lab Sheet 6: Designing Analyst-Friendly Explanations

## Lab Overview

In this lab, you will improve poor AI outputs by turning them into analyst-friendly explanations. You will identify evidence, uncertainty, missing context, and appropriate next steps.

This lab focuses on explanation quality, not model training.

---

## Lab Duration

Approximate duration: 90 minutes.

---

## Lab Mode

Individual work followed by small-group discussion.

---

## Lab Objectives

By completing this lab, you should be able to:

1. Distinguish poor explanations from useful explanations.
2. Identify risk-increasing and risk-reducing evidence.
3. Add missing context and uncertainty.
4. Design local explanations for individual cybersecurity predictions.
5. Identify when explanations may create security risks.
6. Produce analyst-ready explanations for phishing, malware, IDS, DDoS, and SOC triage cases.

---

# 23. Lab Dataset A: Poor AI Outputs

Use the following simplified AI outputs.

| ID | AI Output | Context |
|---|---|---|
| X1 | `Phishing probability: 94%` | Email contains urgent account verification language and non-university URL |
| X2 | `Malware probability: 96%` | File is unsigned, high entropy, imports process injection APIs |
| X3 | `Attack probability: 88%` | Host connects to 150 ports in 40 seconds |
| X4 | `DDoS probability: 84%` | Traffic increased sharply during official course registration |
| X5 | `Incident priority: high` | Sensitive folder accessed, large download, user is confirmed travelling |
| X6 | `URL risk: 91%` | URL uses newly registered domain and redirects twice |
| X7 | `Account risk: 87%` | Login from new country, unknown device, MFA succeeded |
| X8 | `Endpoint risk: 90%` | Word launched PowerShell and downloaded executable |
| X9 | `Vulnerability priority: critical` | High CVSS, internet-facing server, patch available |
| X10 | `Cloud activity risk: 82%` | Admin created access key outside normal hours |

---

# 24. Lab Task 1 — Identify Why the Explanation Is Poor

For each output, explain what is missing.

Complete the table.

| ID | What Is Missing From the Explanation? |
|---|---|
| X1 |  |
| X2 |  |
| X3 |  |
| X4 |  |
| X5 |  |
| X6 |  |
| X7 |  |
| X8 |  |
| X9 |  |
| X10 |  |

Possible missing elements:

```text
risk-increasing evidence
risk-reducing evidence
missing context
uncertainty
recommended action
false positive cost
false negative cost
human approval requirement
business impact
threat intelligence status
```

---

# 25. Lab Task 2 — Build an Analyst-Friendly Explanation

Choose five outputs from Dataset A.

For each one, complete the template.

| ID | Prediction | Risk-Increasing Evidence | Risk-Reducing Evidence | Missing Context | Recommended Next Step |
|---|---|---|---|---|---|
|  |  |  |  |  |  |
|  |  |  |  |  |  |
|  |  |  |  |  |  |
|  |  |  |  |  |  |
|  |  |  |  |  |  |

Your explanations should be clear enough for a security analyst to use.

---

# 26. Lab Task 3 — Local or Global Explanation?

For each explanation need, decide whether a local or global explanation is more appropriate.

| Explanation Need | Local / Global / Both | Reason |
|---|---|---|
| Why was this email flagged? |  |  |
| Which features usually influence the phishing model? |  |  |
| Why was this host assigned high risk? |  |  |
| Does the model rely too much on domain age? |  |  |
| Why was this specific URL blocked? |  |  |
| What kinds of traffic does the IDS usually misclassify? |  |  |
| Why did the model miss this attack? |  |  |
| Which features should be reviewed for leakage? |  |  |

---

# 27. Lab Task 4 — Explanation Quality Evaluation

Evaluate three explanations using the criteria below.

| Criterion | Score 1–5 | Notes |
|---|---:|---|
| Clear |  |  |
| Evidence-based |  |  |
| Context-aware |  |  |
| Shows uncertainty |  |  |
| Actionable |  |  |
| Safe to disclose |  |  |
| Supports analyst decision |  |  |

Use this table for three selected explanations.

---

# 28. Lab Task 5 — Explanation Risk Analysis

Some explanations may help attackers.

For each explanation, decide whether it is safe for:

```text
internal SOC analyst
end user
external public message
attacker-facing API
```

Complete the table.

| Explanation Detail | Internal Analyst | End User | Public Message | Attacker-Facing API | Risk |
|---|---|---|---|---|---|
| Exact threshold values |  |  |  |  |  |
| Main suspicious features |  |  |  |  |  |
| Full model feature weights |  |  |  |  |  |
| General safety warning |  |  |  |  |  |
| Detailed detection rule |  |  |  |  |  |
| Recommended user action |  |  |  |  |  |
| Known malicious indicator |  |  |  |  |  |

---

# 29. Lab Task 6 — Counterfactual Explanation

Choose one case from Dataset A.

Write a counterfactual explanation:

```text
This prediction would change if...
```

Then answer:

1. Would this explanation help an analyst?
2. Could it help an attacker?
3. Should it be shown internally, externally, or not at all?
4. What safer version could be shown to an end user?

---

# 30. Lab Task 7 — Explanation Template Design

Design an explanation template for one of the following systems:

```text
phishing detector
malware classifier
IDS alert system
DDoS detector
SOC triage model
vulnerability prioritisation system
cloud risk scoring system
```

Your template should include:

1. Prediction
2. Confidence
3. Risk-increasing evidence
4. Risk-reducing evidence
5. Missing context
6. Recommended action
7. Human approval requirement
8. Explanation safety level

---

# 31. Lab Deliverable

Submit a short worksheet containing:

1. Missing-elements analysis for poor AI outputs.
2. Five analyst-friendly explanations.
3. Local/global explanation classification.
4. Explanation quality evaluation.
5. Explanation risk analysis.
6. One counterfactual explanation.
7. One reusable explanation template.

Recommended length:

```text
1200–1800 words
```

---

# 32. Exercises

## Exercise 1 — Concept Check

Answer briefly.

1. What is the difference between interpretability and explainability?
2. What is a local explanation?
3. What is a global explanation?
4. What is feature importance?
5. What is a surrogate model?
6. What is LIME?
7. What is SHAP?
8. What is a counterfactual explanation?
9. Why can explanations help analysts?
10. Why can explanations help attackers?

---

## Exercise 2 — Short Analytical Answer

Write 250–300 words.

**Question:**  
Why is explainability especially important in cybersecurity AI?

Your answer should discuss at least four of the following:

- Human decision-making
- False positives
- False negatives
- Incident response
- Analyst trust
- Auditability
- High-impact actions
- Threat investigation
- Explanation risks
- Accountability

---

## Exercise 3 — Explanation Rewriting

Rewrite the following poor output:

```text
Prediction: malicious
Confidence: 95%
Recommended action: block
```

Assume the case is a suspicious URL.

Your improved explanation should include:

- Risk-increasing evidence
- Risk-reducing evidence
- Missing context
- Suggested next step
- Whether automatic blocking is justified

---

## Exercise 4 — Local vs Global

For each question, state whether it needs a local explanation, global explanation, or both.

| Question | Local / Global / Both | Reason |
|---|---|---|
| Why was this specific file flagged as malware? |  |  |
| Which features does the malware model usually rely on? |  |  |
| Why did the IDS miss this specific attack? |  |  |
| Does the phishing model overuse domain age? |  |  |
| Why was this user session assigned high risk? |  |  |
| Is the model learning dataset artefacts? |  |  |

---

## Exercise 5 — Explanation Risk

Read the explanation:

```text
The URL was blocked because its entropy score was above 4.2,
the domain age was below 7 days,
and the redirect count was above 3.
```

Answer:

1. Why is this explanation useful?
2. Why might it be risky?
3. Who should be allowed to see this level of detail?
4. How would you rewrite it for an end user?
5. How would you rewrite it for a SOC analyst?

---

## Exercise 6 — XAI Method Selection

Choose a suitable explanation method for each situation.

| Situation | Suitable Method | Reason |
|---|---|---|
| Explain one phishing prediction |  |  |
| Understand overall IDS feature behaviour |  |  |
| Approximate a complex malware model with simple rules |  |  |
| Show what change would reduce a risk score |  |  |
| Explain similar past phishing campaigns |  |  |
| Audit whether a model relies on leaked features |  |  |

Possible methods:

```text
feature importance
LIME
SHAP
surrogate model
counterfactual explanation
rule-based explanation
example-based explanation
global model audit
```

---

## Exercise 7 — Critical Reflection

Write 200–300 words.

**Question:**  
Can explainability make cybersecurity AI less secure?

Discuss:

- Model leakage
- Evasion
- External explanations
- Internal analyst needs
- Safe explanation design
- Difference between public and internal explanations

---

# 33. Further Reading

## Core Reading

1. **SHAP Documentation**  
   Useful for understanding SHAP as a game-theoretic approach to explaining machine learning model outputs.  
   <https://shap.readthedocs.io/>

2. **SHAP: Introduction to Explainable AI with Shapley Values**  
   Useful for a practical introduction to Shapley-value-based explanations.  
   <https://shap.readthedocs.io/en/latest/example_notebooks/overviews/An%20introduction%20to%20explainable%20AI%20with%20Shapley%20values.html>

3. **LIME Documentation**  
   Useful for understanding Local Interpretable Model-Agnostic Explanations.  
   <https://lime-ml.readthedocs.io/>

4. **LIME GitHub Repository**  
   Useful for examples and implementation details.  
   <https://github.com/marcotcr/lime>

5. **NIST AI Risk Management Framework**  
   Useful for connecting explainability and interpretability to broader trustworthy AI risk management.  
   <https://www.nist.gov/itl/ai-risk-management-framework>

6. **DARPA Explainable Artificial Intelligence Programme**  
   Useful for understanding the original motivation behind XAI: helping users understand, appropriately trust, and manage AI systems.  
   <https://www.darpa.mil/research/programs/explainable-artificial-intelligence>

---

## Suggested Search Topics

Search for recent academic or technical material on:

- Explainable AI for cybersecurity
- XAI for intrusion detection
- SHAP for malware detection
- LIME for phishing detection
- Counterfactual explanations in cybersecurity
- Explainable deep learning for security
- Analyst-centred explanations
- Explanation risks in cybersecurity
- Model leakage through explanations
- Explainable AI for SOC triage
- Explainability and adversarial evasion
- Human trust in AI-based cybersecurity systems

---

# 34. Week 6 Summary

This week focused on Explainable AI for Cybersecurity.

The most important lessons are:

```text
Cybersecurity AI needs reasons, not only predictions.

Interpretability, explainability, transparency, and accountability are related but different.

Local explanations explain individual predictions.

Global explanations explain overall model behaviour.

LIME and SHAP are common model-agnostic explanation approaches.

Counterfactual explanations show what changes could alter a decision.

Explanations must be clear, evidence-based, context-aware, actionable, and uncertainty-aware.

Explanations can also create security risks if they expose detection logic.

Different audiences need different levels of explanation.

Explainability is part of trustworthy AI, but it does not replace robustness, monitoring, privacy, or governance.
```

Final takeaway:

> The best explanation is not the most mathematically detailed one.  
> The best explanation is the one that helps a security analyst make a better, safer, and more proportionate decision.
