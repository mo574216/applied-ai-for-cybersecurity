---
title: "Week 6: Trustworthy, Adversarial, and Responsible AI in Cybersecurity"
layout: default
permalink: /lectures/week6/
---

# Week 6: Trustworthy, Adversarial, and Responsible AI in Cybersecurity  
## Securing AI Systems and Using AI Responsibly in Cyber Defence

Welcome to Week 6 of **Applied AI for Cybersecurity**.

In previous weeks, we studied how AI can support cybersecurity tasks such as intrusion detection, DDoS detection, phishing detection, malware detection, alert triage, and threat intelligence. This week asks a more critical question:

> What happens when the AI system itself becomes a target, a source of risk, or a poorly governed security decision-maker?

This week is the capstone of the course. It brings together the technical, operational, and ethical issues involved in deploying AI for cybersecurity.

The main message is:

> AI can improve cyber defence, but AI systems must themselves be secured, evaluated, monitored, explained, and governed.

---

# 1. Learning Objectives

By the end of this week, you should be able to:

1. Explain what trustworthy AI means in a cybersecurity context.
2. Describe why AI systems used in security can become attack targets.
3. Distinguish between adversarial examples, evasion attacks, poisoning attacks, model extraction, and model inversion.
4. Explain how attackers may manipulate AI-based phishing, malware, intrusion, or SOC systems.
5. Discuss the risks of over-reliance on AI in security operations.
6. Explain why explainability, robustness, privacy, accountability, and human oversight matter.
7. Apply adversarial thinking to evaluate an AI-based cybersecurity system.
8. Design basic controls for safer AI deployment in cybersecurity.
9. Critically assess whether an AI security system is ready for operational deployment.
10. Produce a responsible deployment checklist for an AI-based cyber defence use case.

---

# 2. Why Trustworthy AI Matters in Cybersecurity

AI systems used in cybersecurity can influence important decisions:

- Which email is blocked?
- Which file is quarantined?
- Which network flow is treated as malicious?
- Which user is investigated?
- Which alert is escalated?
- Which host is isolated?
- Which vulnerability is prioritised?
- Which incident is treated as critical?

These decisions can affect users, business processes, legal responsibilities, and organisational trust.

A poorly designed AI security system may:

- Miss real attacks
- Produce too many false alarms
- Block legitimate activity
- Disrupt business operations
- Leak sensitive information
- Be manipulated by attackers
- Produce explanations that mislead analysts
- Encourage analysts to trust predictions without evidence

This is why trustworthy AI is not an optional topic. In cybersecurity, the AI system becomes part of the defence surface.

---

# 3. From “Using AI for Security” to “Securing AI for Security”

So far, most of the course has focused on using AI to improve cyber defence.

Examples:

```text
AI for phishing detection
AI for malware classification
AI for DDoS detection
AI for SOC alert triage
AI for threat intelligence enrichment
```

Week 5 changes the viewpoint:

```text
How can attackers manipulate these AI systems?
How can defenders evaluate whether the AI is safe enough to deploy?
How should human analysts use AI outputs responsibly?
```

This shift is important because an AI model is not just a tool. It is also a system that can be attacked, misused, misunderstood, or overtrusted.

---

# 4. What Is Trustworthy AI?

Trustworthy AI means that an AI system can be relied on within its intended context of use.

In cybersecurity, trustworthy AI should be:

| Property | Meaning in Cybersecurity |
|---|---|
| Valid | It measures or predicts what it claims to predict |
| Reliable | It behaves consistently under expected conditions |
| Robust | It resists small changes, noise, and manipulation |
| Secure | It is protected from attacks on the model, data, and pipeline |
| Explainable | Analysts can understand the reasons behind outputs |
| Accountable | Humans and organisations remain responsible for decisions |
| Privacy-preserving | Sensitive data is protected |
| Fair and appropriate | It avoids unjustified harm to users or groups |
| Monitored | It is observed after deployment |
| Governed | It is managed through policies, roles, and controls |

The NIST AI Risk Management Framework is a useful reference for thinking about trustworthy AI. NIST describes the AI RMF as a framework developed to help manage risks to individuals, organisations, and society associated with AI. Further reading: [NIST AI Risk Management Framework](https://www.nist.gov/itl/ai-risk-management-framework).

---

# 5. AI Risk in the Cybersecurity Lifecycle

An AI-based cybersecurity system has several stages.

```text
Problem definition
→ Data collection
→ Data labelling
→ Feature engineering
→ Model training
→ Model evaluation
→ Deployment
→ Monitoring
→ Response integration
→ Feedback and retraining
```

Each stage introduces risks.

| Stage | Possible Risk |
|---|---|
| Problem definition | The wrong security question is modelled |
| Data collection | Data is incomplete, biased, or sensitive |
| Labelling | Labels are wrong or inconsistent |
| Feature engineering | Features leak shortcuts or miss attacker behaviour |
| Training | Model overfits to a dataset |
| Evaluation | Metrics do not reflect operational risk |
| Deployment | Model faces different traffic or users |
| Monitoring | Concept drift is not detected |
| Response integration | AI output triggers unsafe automation |
| Feedback | Wrong analyst feedback corrupts future learning |

A trustworthy system must manage risks across the whole lifecycle, not only during model training.

---

# 6. Adversarial Machine Learning

Adversarial machine learning studies how attackers can manipulate AI systems.

In normal machine learning, we often assume that data comes from a stable distribution. In cybersecurity, this assumption is weak because attackers actively adapt.

Examples:

```text
A malware author modifies a file to avoid detection.
A phisher changes wording to bypass an email classifier.
A botnet mimics normal traffic to avoid anomaly detection.
An attacker poisons training data to weaken future detection.
An attacker queries a model repeatedly to infer how it works.
```

MITRE ATLAS is a useful framework for studying adversary tactics and techniques against AI-enabled systems. MITRE describes ATLAS as a globally accessible knowledge base of adversary tactics and techniques against AI-enabled systems based on real-world attack observations. Further reading: [MITRE ATLAS](https://atlas.mitre.org/).

---

# 7. Main Attack Types Against AI Systems

## 7.1 Evasion Attacks

An evasion attack happens at inference time. The attacker modifies the input so that the model makes a wrong prediction.

Example:

```text
Original malware: detected as malicious
Modified malware: detected as benign
```

The attacker may change the file without changing its harmful function.

Examples in cybersecurity:

| Detection System | Evasion Example |
|---|---|
| Malware detector | Add benign-looking strings or pack the binary |
| Phishing detector | Change wording, use images instead of text |
| URL detector | Use redirects or trusted hosting platforms |
| DDoS detector | Slow down traffic below thresholds |
| IDS | Split attack traffic across time or sources |
| SOC risk scoring | Avoid actions that strongly increase risk score |

Important point:

> Evasion attacks exploit the difference between what the model measures and what the attacker is actually doing.

---

## 7.2 Adversarial Examples

An adversarial example is an input intentionally modified to cause a model error.

In image classification, adversarial examples are often small pixel changes. In cybersecurity, adversarial examples may look different:

- Adding unused sections to a PE file
- Changing domain names or URL paths
- Rewording phishing emails
- Padding network flows
- Splitting activity across sessions
- Changing command syntax
- Reordering harmless operations

Example:

```text
A phishing email still asks the user to verify credentials,
but it avoids known suspicious keywords.
```

The security meaning remains malicious, but the model may no longer detect it.

---

## 7.3 Poisoning Attacks

A poisoning attack targets the training data.

The attacker attempts to influence the model during training or retraining.

Example:

```text
An attacker injects malicious examples labelled as benign into the training data.
The model later learns that similar malicious behaviour is normal.
```

Possible poisoning targets:

- Training datasets
- Analyst feedback
- User reports
- Threat intelligence feeds
- Crowdsourced labels
- Federated learning updates
- Auto-retraining pipelines

Cybersecurity example:

```text
A spammer repeatedly reports phishing emails as legitimate.
If the system learns from this feedback without validation, future phishing detection may weaken.
```

---

## 7.4 Backdoor Attacks

A backdoor attack inserts hidden behaviour into a model.

The model behaves normally on most inputs, but misclassifies inputs containing a specific trigger.

Example:

```text
A malware detector works normally,
except files containing a special harmless-looking string are classified as benign.
```

Backdoors are dangerous because normal evaluation may not reveal them.

Potential sources:

- Compromised training data
- Untrusted pretrained models
- Malicious third-party libraries
- Poisoned model updates
- Supply chain attacks

---

## 7.5 Model Extraction

Model extraction occurs when an attacker tries to copy or approximate a model by querying it repeatedly.

Example:

```text
The attacker submits many URLs to a malicious URL detector.
By observing outputs, the attacker learns which features increase or reduce risk.
```

Why this matters:

- The attacker can build a substitute model.
- The attacker can test evasion strategies.
- The attacker can infer decision boundaries.
- The attacker can reduce the cost of bypassing detection.

Possible controls:

- Rate limiting
- Query monitoring
- Output restriction
- Authentication
- Abuse detection
- Returning coarse-grained outputs rather than detailed scores

---

## 7.6 Model Inversion and Membership Inference

Model inversion attempts to infer sensitive information about training data.

Membership inference attempts to determine whether a specific record was included in the training data.

Why this matters in cybersecurity:

- Security datasets may contain sensitive logs.
- Email datasets may contain private content.
- Authentication records may expose user behaviour.
- Malware analysis datasets may include proprietary samples.
- Incident data may contain confidential organisational details.

Privacy protection is important when using real security data.

---

## 7.7 Prompt Injection and LLM-Specific Risks

If large language models are used in security operations, they introduce additional risks.

Examples:

- A malicious email contains text that instructs the LLM to ignore previous instructions.
- A threat report contains misleading content that affects summarisation.
- A user asks the LLM to generate unsafe commands.
- The LLM produces an incorrect incident summary.
- The LLM overstates confidence.
- The LLM leaks sensitive information from context.

OWASP maintains a Top 10 list for Large Language Model Applications. The 2025 OWASP Top 10 for LLMs includes risks such as prompt injection and other risks across the development, deployment, and management lifecycle. Further reading: [OWASP Top 10 for LLM Applications](https://genai.owasp.org/llm-top-10/).

---

# 8. Threat Model for AI-Based Cybersecurity Systems

A threat model asks:

> What are we protecting, from whom, and how might they attack it?

For an AI-based cybersecurity system, we should consider:

## 8.1 Assets

| Asset | Example |
|---|---|
| Model | Malware classifier, IDS model, phishing detector |
| Training data | Labelled emails, network flows, malware features |
| Feature pipeline | Scripts extracting features from logs or files |
| Labels | Analyst decisions, ground truth, threat intelligence |
| Model outputs | Risk scores, classifications, explanations |
| Feedback loop | Analyst feedback used for retraining |
| Deployment environment | API, SIEM integration, endpoint agent |
| Response actions | Blocking, quarantine, isolation, escalation |

## 8.2 Adversaries

Possible adversaries include:

- Malware authors
- Phishing operators
- Botnet operators
- Insider threats
- External attackers
- Malicious data contributors
- Compromised users
- Supply-chain attackers
- Competitors or model thieves

## 8.3 Attack Goals

Attackers may want to:

- Avoid detection
- Cause false alarms
- Weaken the model over time
- Extract the model
- Infer sensitive training data
- Trigger unsafe automation
- Reduce analyst trust
- Overload the SOC
- Hide malicious behaviour inside normal patterns

---

# 9. Case Study 1: Evasion Against a Phishing Detector

## Scenario

A phishing detector uses features such as:

```text
urgency keywords
password-related words
known suspicious domains
URL length
sender reputation
brand impersonation keywords
```

The attacker modifies the phishing email:

```text
Original phrase: "Your password will expire today."
Modified phrase: "Your access needs a quick review."

Original link: suspicious-login-example.com
Modified link: cloud-docs.example-hosting.com/shared/file
```

The goal is to reduce the model score while still tricking the user.

## Security Question

Is the modified email less malicious, or only less detectable?

## Discussion

The email may still be malicious even if the model score decreases. This shows why defenders should evaluate whether features capture the true security behaviour or only surface patterns.

## Main Lesson

> A lower model score does not necessarily mean lower real-world risk.

---

# 10. Case Study 2: Poisoning Through Analyst Feedback

## Scenario

A SOC system learns from analyst feedback.

Analysts can mark alerts as:

```text
True positive
False positive
Benign
Needs investigation
```

An attacker compromises several low-privilege accounts and generates suspicious but low-impact activity. The attacker then causes many alerts to be marked as false positives because analysts become used to seeing similar noisy behaviour.

Later, the attacker uses similar behaviour for a real attack.

## Security Question

Can feedback become an attack surface?

## Discussion

Yes. If feedback is used for retraining without validation, the model may learn that suspicious behaviour is benign.

## Possible Controls

- Validate feedback before retraining
- Separate training labels from operational closure reasons
- Weight feedback by analyst confidence
- Monitor for label distribution changes
- Audit retraining data
- Keep human-reviewed gold-standard datasets
- Use delayed retraining rather than immediate learning

## Main Lesson

> Feedback loops improve AI systems, but they can also become poisoning channels.

---

# 11. Case Study 3: Unsafe Automation in SOC Response

## Scenario

An AI-assisted SOC system assigns:

```text
Incident risk score: 94/100
Recommendation: isolate server immediately
```

The server is a production database used by hospital staff.

The evidence includes:

```text
unusual outbound connection
unusual process execution
high data transfer
unknown destination
```

But the model lacks context:

```text
The hospital is performing an emergency data migration.
The activity is approved but not recorded in the security calendar.
```

## Security Question

Should the system automatically isolate the server?

## Discussion

Automatic isolation could interrupt a critical service. High-risk scores should not automatically trigger high-impact actions without human approval and operational context.

## Main Lesson

> The higher the impact of a response, the stronger the requirement for human approval, evidence quality, and context.

---

# 12. Case Study 4: Model Extraction Against a Malicious URL Detector

## Scenario

A malicious URL detection API returns detailed outputs:

```text
Risk score: 86/100
Reasons:
- domain age: high risk
- URL length: medium risk
- suspicious keyword: high risk
- reputation: unknown
```

An attacker submits thousands of test URLs and observes the outputs.

## Security Question

What can the attacker learn?

## Possible Attacker Knowledge

- Which keywords increase risk
- Which URL lengths trigger alerts
- Which domain ages are risky
- Whether reputation matters
- How to modify URLs to reduce score
- Whether the detector uses lexical or reputation features

## Possible Controls

- Limit query rate
- Monitor suspicious query patterns
- Reduce output detail for untrusted users
- Use authentication
- Randomise or smooth outputs where appropriate
- Avoid exposing internal feature weights
- Separate user-facing explanations from internal model reasoning

## Main Lesson

> Explainability is important, but too much detail exposed to adversaries can help evasion.

---

# 13. Responsible Deployment of AI in Cybersecurity

A model should not be deployed only because it has good benchmark performance.

Before deployment, ask:

## 13.1 Security Fit

- What security problem does the model solve?
- Does the model output support a real decision?
- What are the possible decisions after the prediction?
- Who is responsible for the decision?
- What is the cost of being wrong?

## 13.2 Data Quality

- Where did the data come from?
- Are labels reliable?
- Is the data representative of the target environment?
- Is sensitive information protected?
- Is the dataset balanced enough?
- Are there known blind spots?

## 13.3 Evaluation

- Which metrics were used?
- Were false positives and false negatives analysed?
- Was the model tested on recent data?
- Was the model tested on out-of-distribution examples?
- Was adversarial evaluation performed?
- Was detection latency measured?
- Was analyst workload considered?

## 13.4 Explainability

- Can analysts understand the output?
- Does the explanation show useful evidence?
- Does the explanation include uncertainty?
- Does the explanation show risk-increasing and risk-reducing factors?
- Could the explanation leak too much information to attackers?

## 13.5 Monitoring

- How will model drift be detected?
- How will false positives be tracked?
- How will missed attacks be analysed?
- How often will the model be reviewed?
- Who approves retraining?
- What logs are kept for audit?

## 13.6 Governance

- Who owns the model?
- Who approves deployment?
- Who can change thresholds?
- Who reviews high-impact actions?
- What is the rollback plan?
- How is privacy protected?
- How are incidents involving the AI system handled?

---

# 14. Human Oversight and Automation Boundaries

Not every AI-supported action should be automated.

## 14.1 Lower-Risk Automation

Often suitable for automation:

- Enrich alerts with threat intelligence
- Retrieve related logs
- Generate incident summaries
- Create investigation tickets
- Group duplicate alerts
- Recommend next steps
- Apply temporary low-impact rate limits
- Send low-risk notifications

## 14.2 High-Risk Actions

Usually require human approval:

- Disable a user account
- Isolate a production server
- Block a country or major cloud provider
- Delete files
- Terminate cloud workloads
- Revoke privileged access
- Publicly disclose an incident
- Notify regulators
- Trigger ransomware recovery procedures

## 14.3 Rule of Thumb

```text
The more irreversible, disruptive, or legally significant the action,
the stronger the requirement for human approval.
```

---

# 15. Explainability and Analyst Trust

Explainability should help analysts understand the evidence.

Poor explanation:

```text
Prediction: malicious
Confidence: 93%
```

Better explanation:

```text
Risk increased because:
- The file is unsigned.
- The file has high entropy.
- It imports process injection APIs.
- It contacted a newly registered domain.
- Similar behaviour was seen in previous malware cases.

Risk reduced because:
- The file was downloaded from an internal software repository.
- The host is used by the IT administration team.

Recommended action:
- Send to sandbox analysis.
- Do not delete automatically.
- Escalate if runtime behaviour confirms persistence or C2.
```

Good explanations should include:

- Evidence used
- Confidence
- Uncertainty
- Missing context
- Risk-increasing factors
- Risk-reducing factors
- Recommended action
- Automation boundary

---

# 16. Privacy and Data Protection

Cybersecurity data can contain sensitive information.

Examples:

- Usernames
- Email contents
- IP addresses
- Locations
- Device identifiers
- File names
- URLs visited
- Login behaviour
- Cloud access logs
- Incident notes
- Analyst comments

Privacy risks include:

- Over-collection
- Unnecessary retention
- Unauthorised access
- Model memorisation
- Sensitive data leakage through explanations
- Re-identification
- Misuse of monitoring data

Responsible design should apply:

- Data minimisation
- Access control
- Retention limits
- Anonymisation or pseudonymisation where possible
- Audit logging
- Clear purpose limitation
- Secure storage
- Legal and organisational review

---

# 17. Monitoring and Drift Management

AI systems must be monitored after deployment.

## 17.1 What to Monitor

| Monitoring Target | Why It Matters |
|---|---|
| False positive rate | Analyst workload and disruption |
| False negative reports | Missed attacks |
| Alert volume | Operational load |
| Detection latency | Speed of response |
| Feature distribution | Concept drift |
| Model confidence | Overconfidence or uncertainty |
| Analyst overrides | Trust and disagreement |
| Threat landscape | New attacker behaviour |
| Data pipeline health | Missing or broken logs |
| Response outcomes | Whether actions worked |

## 17.2 Drift Examples

```text
A university introduces a new cloud platform.
Login patterns change.
A model trained on old identity logs flags many normal events as suspicious.
```

```text
Attackers change phishing templates.
A phishing detector trained on old keywords misses new campaigns.
```

```text
Encrypted traffic increases.
A network IDS relying on payload features becomes less useful.
```

## Main Lesson

> Deployment is not the end of the AI lifecycle. It is the beginning of operational monitoring.

---

# 18. Course Integration: What We Have Learned

This course has covered five connected ideas.

| Week | Main Idea |
|---|---|
| Week 1 | Security problems must be translated carefully into AI problems |
| Week 2 | Network intrusion and DDoS detection require context and robust evaluation |
| Week 3 | Malware, phishing, and URL detection need meaningful features and adversarial awareness |
| Week 4 | Security operations require alert correlation, prioritisation, and human oversight |
| Week 5 | AI systems used in security must themselves be trustworthy, secure, monitored, and governed |

The final skill is not just “using AI”.

The final skill is:

```text
Designing, evaluating, and governing AI-supported cybersecurity decisions.
```

---

# 19. Week 5 Summary

This week focused on trustworthy, adversarial, and responsible AI in cybersecurity.

Key points:

```text
AI systems used in cybersecurity can themselves become attack targets.

Attackers can evade, poison, extract, or manipulate AI models.

Prompt injection and LLM-specific risks matter when LLMs are used in security workflows.

Trustworthy AI requires validity, reliability, robustness, security, explainability, privacy, monitoring, and accountability.

Human oversight is essential for high-impact cybersecurity decisions.

Feedback loops must be protected from poisoning and misuse.

Good benchmark performance is not enough for real-world deployment.

Responsible deployment requires data quality checks, adversarial evaluation, monitoring, governance, and rollback planning.
```

Final takeaway:

> AI can strengthen cyber defence only when it is itself secured, monitored, explainable, and governed.

---

# 20. Lab Sheet 5: Adversarial and Responsible AI for Cybersecurity

## Lab Overview

In this lab, you will evaluate the trustworthiness and deployment readiness of AI-based cybersecurity systems. You will identify possible attacks against AI models, propose defensive controls, define automation boundaries, and prepare a responsible deployment checklist.

This lab is conceptual and analytical. It does not require attacking real systems or generating malicious artefacts.

---

## Lab Safety Notice

Do not attempt to attack real AI systems, bypass real detection tools, upload malicious files, or test evasion against public services.

All scenarios are simplified for learning purposes.

---

## Lab Duration

Approximate duration: 90 minutes.

---

## Lab Mode

Individual work followed by small-group discussion.

---

## Lab Objectives

By completing this lab, you should be able to:

1. Identify possible adversarial attacks against AI-based cybersecurity tools.
2. Distinguish evasion, poisoning, extraction, inversion, and unsafe automation risks.
3. Assess whether an AI-based security system is ready for deployment.
4. Propose controls for safer AI use in cybersecurity.
5. Define human approval requirements for high-impact actions.
6. Produce an explainable and responsible deployment checklist.

---

# 21. Lab Dataset A: AI Security System Scenarios

Use the following simplified scenarios.

| ID | AI System | Scenario |
|---|---|---|
| S1 | Phishing detector | Attackers change wording and use image-based text to avoid keyword detection |
| S2 | Malware classifier | Malware authors add benign-looking strings and pack the binary |
| S3 | DDoS detector | Botnet sends slower traffic below detection threshold |
| S4 | SOC alert triage | Model learns from analyst feedback, but many noisy malicious-like alerts are marked false positive |
| S5 | URL detector API | Public API returns detailed risk reasons for submitted URLs |
| S6 | IDS model | Model trained on public dataset performs poorly on encrypted enterprise traffic |
| S7 | LLM SOC assistant | Malicious email contains instructions that manipulate the assistant’s summary |
| S8 | Vulnerability prioritisation model | Model prioritises internet-facing assets but ignores internal crown-jewel systems |
| S9 | Endpoint response system | High model score automatically isolates a production server |
| S10 | Threat intelligence summariser | LLM summary omits uncertainty and overstates confidence |

---

# 22. Lab Task 1 — Identify the AI Risk Type

For each scenario, identify the most relevant risk type.

Possible risk types:

```text
Evasion
Poisoning
Backdoor
Model extraction
Model inversion / membership inference
Prompt injection
Concept drift
Dataset bias
Unsafe automation
Poor explainability
Privacy risk
Governance failure
```

Complete the table:

| ID | Risk Type | Reason |
|---|---|---|
| S1 |  |  |
| S2 |  |  |
| S3 |  |  |
| S4 |  |  |
| S5 |  |  |
| S6 |  |  |
| S7 |  |  |
| S8 |  |  |
| S9 |  |  |
| S10 |  |  |

---

# 23. Lab Task 2 — Analyse the Attacker Goal

For each scenario, identify what the attacker or failure mode is trying to achieve.

Possible goals:

```text
Avoid detection
Cause false positives
Poison future learning
Extract model behaviour
Trigger unsafe response
Hide uncertainty
Reduce analyst trust
Steal sensitive information
Manipulate explanation
Exploit deployment mismatch
```

Complete the table:

| ID | Attacker or Failure Goal | Possible Impact |
|---|---|---|
| S1 |  |  |
| S2 |  |  |
| S3 |  |  |
| S4 |  |  |
| S5 |  |  |
| S6 |  |  |
| S7 |  |  |
| S8 |  |  |
| S9 |  |  |
| S10 |  |  |

---

# 24. Lab Task 3 — Propose Defensive Controls

For each scenario, propose at least two controls.

Possible controls include:

```text
Adversarial testing
Rate limiting
Query monitoring
Output restriction
Human approval
Feedback validation
Drift monitoring
Retraining governance
Sandboxing
Data validation
Threat modelling
Explainability review
Access control
Audit logging
Rollback plan
Independent evaluation
```

Complete the table:

| ID | Control 1 | Control 2 | Additional Notes |
|---|---|---|---|
| S1 |  |  |  |
| S2 |  |  |  |
| S3 |  |  |  |
| S4 |  |  |  |
| S5 |  |  |  |
| S6 |  |  |  |
| S7 |  |  |  |
| S8 |  |  |  |
| S9 |  |  |  |
| S10 |  |  |  |

---

# 25. Lab Task 4 — Define Automation Boundaries

For each action, decide whether it should be automated, require approval, or be prohibited.

| Action | Automate / Approval / Prohibit | Reason |
|---|---|---|
| Enrich alert with threat intelligence |  |  |
| Generate analyst summary |  |  |
| Quarantine suspicious email |  |  |
| Delete suspicious file |  |  |
| Isolate production server |  |  |
| Disable administrator account |  |  |
| Apply temporary low-impact rate limit |  |  |
| Block entire country |  |  |
| Submit unknown file to sandbox |  |  |
| Retrain model using analyst feedback |  |  |

Consider:

- Reversibility
- Business impact
- Confidence level
- Evidence quality
- Legal or privacy implications
- Human accountability

---

# 26. Lab Task 5 — Deployment Readiness Checklist

Choose one AI cybersecurity system:

```text
Phishing detector
Malware classifier
DDoS detector
SOC alert prioritisation model
Vulnerability prioritisation model
LLM SOC assistant
```

Prepare a deployment readiness checklist.

Your checklist should include at least 12 items across these categories:

| Category | Example Questions |
|---|---|
| Problem definition | What decision does the model support? |
| Data quality | Is the training data representative? |
| Labels | Are labels reliable? |
| Evaluation | Were precision, recall, F1, and false positive rates checked? |
| Adversarial testing | Was evasion or poisoning considered? |
| Explainability | Can analysts understand the output? |
| Privacy | Does the system process sensitive data? |
| Monitoring | How will drift be detected? |
| Human oversight | Which actions require approval? |
| Governance | Who owns thresholds and retraining? |
| Rollback | Can deployment be reversed? |
| Audit | Are decisions logged? |

---

# 27. Lab Task 6 — Explainability Review

Review this poor AI output:

```text
Risk score: 97/100
Action: isolate host
```

Rewrite it as an analyst-friendly output.

Your improved output should include:

1. Risk-increasing evidence.
2. Risk-reducing evidence.
3. Missing evidence.
4. Confidence level.
5. Recommended next step.
6. Whether isolation requires human approval.
7. Possible business impact.
8. Suggested monitoring or follow-up.

---

# 28. Lab Task 7 — Final Critical Reflection

Write a short reflection answering:

1. What is the biggest risk of using AI in cybersecurity?
2. What is the biggest benefit?
3. Which AI security risk is most difficult to manage?
4. Which response actions should never be fully automated?
5. What should be monitored after deployment?
6. What would make you trust an AI-based cybersecurity system?

---

# 29. Lab Deliverable

Submit a short worksheet containing:

1. AI risk type classification.
2. Attacker/failure goal analysis.
3. Defensive controls table.
4. Automation boundary table.
5. Deployment readiness checklist.
6. Improved analyst-friendly AI output.
7. Final critical reflection.

Recommended length:

```text
1200–1800 words
```

---

# 30. Exercises

## Exercise 1 — Concept Check

Answer briefly.

1. What is trustworthy AI?
2. Why can AI systems used in cybersecurity become targets?
3. What is an evasion attack?
4. What is a poisoning attack?
5. What is model extraction?
6. What is membership inference?
7. What is prompt injection?
8. Why can feedback loops be dangerous?
9. Why is explainability important in security operations?
10. Why should high-impact response actions require human approval?

---

## Exercise 2 — Short Analytical Answer

Write 250–300 words.

**Question:**  
Why is adversarial machine learning especially important in cybersecurity?

Your answer should discuss at least four of the following:

- Attackers adapt to defenders
- Evasion
- Poisoning
- Model extraction
- Concept drift
- False positives and false negatives
- Operational impact
- Human oversight
- Deployment monitoring

---

## Exercise 3 — Threat Modelling

Choose one AI cybersecurity system:

```text
Malware classifier
Phishing detector
DDoS detector
SOC triage model
LLM SOC assistant
```

Answer:

1. What are the main assets?
2. Who are the likely adversaries?
3. What are the possible attack goals?
4. How could the system be attacked?
5. What controls would reduce the risk?
6. What monitoring would be required after deployment?

---

## Exercise 4 — Evasion Analysis

Read the case:

```text
A phishing classifier relies heavily on urgency keywords and known suspicious domains.
Attackers start using neutral language, image-based text, and trusted cloud-hosted pages.
Detection performance drops sharply.
```

Answer:

1. What type of adversarial behaviour is this?
2. Which features failed?
3. What additional features could help?
4. What evaluation should be performed?
5. How should the model be updated?
6. What human review process is needed?

---

## Exercise 5 — Responsible Automation

Read the statement:

```text
If an AI system is 99% confident that a host is compromised, it should automatically isolate the host.
```

Do you agree or disagree?

Write 250–300 words. Discuss:

- Confidence versus evidence
- Business impact
- Asset criticality
- Reversibility
- Human approval
- False positive cost
- Incident urgency
- Auditability

---

## Exercise 6 — LLM Security Reflection

A SOC uses an LLM to summarise alerts and recommend next steps.

Answer:

1. What could go wrong?
2. How could prompt injection occur?
3. What sensitive data might be exposed?
4. Why might analysts overtrust the output?
5. What controls should be in place?
6. Should the LLM be allowed to trigger response actions directly?

---

## Exercise 7 — Deployment Checklist

Create a responsible deployment checklist for one of the following:

```text
AI phishing detector
AI malware detector
AI DDoS detector
AI vulnerability prioritisation system
AI SOC assistant
```

Your checklist should cover:

- Data
- Labels
- Metrics
- Adversarial testing
- Explainability
- Privacy
- Human oversight
- Monitoring
- Governance
- Rollback

---

# 31. Further Reading

## Core Reading

1. **NIST AI Risk Management Framework**  
   Useful for understanding trustworthy AI, AI risk, governance, validity, reliability, safety, security, resilience, accountability, transparency, explainability, interpretability, and privacy.  
   <https://www.nist.gov/itl/ai-risk-management-framework>

2. **NIST AI RMF Resources**  
   Useful for additional AI RMF material, playbook resources, and trustworthiness considerations.  
   <https://airc.nist.gov/airmf-resources/airmf/>

3. **MITRE ATLAS**  
   Useful for understanding adversary tactics and techniques against AI-enabled systems.  
   <https://atlas.mitre.org/>

4. **OWASP Machine Learning Security Top 10**  
   Useful for understanding common security risks in machine learning systems.  
   <https://owasp.org/www-project-machine-learning-security-top-10/>

5. **OWASP Top 10 for Large Language Model Applications**  
   Useful for understanding LLM-specific security risks such as prompt injection and risks across the development, deployment, and management lifecycle.  
   <https://genai.owasp.org/llm-top-10/>

6. **MITRE SAFE-AI: A Framework for Securing AI-Enabled Systems**  
   Useful for defensive thinking about securing enterprise systems that use AI.  
   <https://atlas.mitre.org/pdf-files/SAFEAI_Full_Report.pdf>

---

## Suggested Search Topics

Search for recent academic or technical material on:

- Adversarial machine learning in cybersecurity
- Evasion attacks against malware classifiers
- Poisoning attacks against intrusion detection
- Prompt injection in security operations
- Model extraction attacks
- Model inversion and membership inference
- Explainable AI for cybersecurity
- Privacy-preserving security analytics
- Secure ML pipelines
- Human-in-the-loop AI for cyber defence
- AI governance for cybersecurity
- Robust malware detection
- Robust phishing detection
- Drift monitoring for security models
- AI red teaming
- Secure deployment of machine learning models

---

# 32. Week 5 Summary and Course Wrap-Up

This week completed the course by focusing on the risks of AI itself.

The most important lessons are:

```text
AI systems used in cybersecurity are themselves part of the attack surface.

Attackers can evade, poison, extract, or manipulate AI models.

LLM-based security tools introduce risks such as prompt injection and overreliance.

Trustworthy AI requires security, robustness, explainability, privacy, monitoring, governance, and accountability.

High benchmark performance does not guarantee safe deployment.

Human oversight is essential for high-impact cybersecurity decisions.

Responsible AI deployment requires threat modelling, adversarial testing, monitoring, and rollback planning.
```

Across the course, the central lesson is:

```text
AI should not be treated as an automatic security authority.
AI should be treated as a decision-support technology that must be evaluated, explained, monitored, and governed.
```

Final takeaway:

> Applied AI for Cybersecurity is not only about detecting threats with models.  
> It is about designing AI-supported security decisions that are technically sound, operationally useful, adversarially robust, and responsibly governed.
