---
title: "References"
layout: default
nav_order: 4
permalink: "/references/"
---

# References

## Applied AI for Cybersecurity

This page provides a curated reading list for the **12-week Applied AI for Cybersecurity** module. The emphasis is on **authoritative**, **reliable**, and **teaching-friendly** sources that support a Level 6 course in applied AI, cybersecurity analytics, trustworthy AI, adversarial machine learning, security operations, LLM security, secure software engineering, cloud security, IoT security, cyber-physical security, and SecMLOps.

The readings are grouped into:

- core curriculum and guidance references;
- week-by-week recommended readings;
- recommended books;
- datasets and practical resources;
- journals and venues for advanced reading;
- suggested referencing practice.

---

# 1. Core Curriculum and Guidance References

These sources help frame the module academically and professionally.

1. **QAA Subject Benchmark Statement: Computing**  
   A key UK reference for academic expectations in computing programmes. Useful for grounding level, breadth, criticality, and professional orientation.  
   <https://www.qaa.ac.uk/the-quality-code/subject-benchmark-statements/computing>

2. **CyBOK Topic Guide: AI for Security**  
   A strong conceptual guide to how AI techniques are used in cybersecurity contexts.  
   <https://www.cybok.org/wp-content/uploads/AI_for_Security_TG_v1.0.0.pdf>

3. **CyBOK Knowledge Guide: Security and Privacy of AI**  
   A foundational source for adversarial machine learning, privacy attacks, model security, and AI system risk.  
   <https://www.cybok.org/wp-content/uploads/Security_Privacy_AI_KG_v1.0.0.pdf>

4. **NIST AI Risk Management Framework**  
   A central reference for trustworthy AI, AI risk governance, validity, reliability, security, resilience, explainability, privacy, transparency, and accountability.  
   <https://www.nist.gov/itl/ai-risk-management-framework>

5. **NIST AI RMF Resources**  
   Useful for more detailed material on AI risk management, trustworthiness characteristics, and practical implementation resources.  
   <https://airc.nist.gov/airmf-resources/airmf/>

6. **NIST AI 100-2e2025: Adversarial Machine Learning — A Taxonomy and Terminology**  
   A reliable source for terminology and structured understanding of attacks and mitigations in adversarial machine learning.  
   <https://csrc.nist.gov/pubs/ai/100/2/e2025/final>

7. **MITRE ATLAS**  
   A knowledge base of adversary tactics and techniques against AI-enabled systems. Useful for adversarial AI and AI threat modelling.  
   <https://atlas.mitre.org/>

8. **OWASP Machine Learning Security Top 10**  
   A practical security-oriented reference for common risks in machine learning systems.  
   <https://owasp.org/www-project-machine-learning-security-top-10/>

9. **OWASP Top 10 for Large Language Model Applications**  
   A widely used practical guide to LLM application risks such as prompt injection, insecure output handling, sensitive information disclosure, and excessive agency.  
   <https://owasp.org/www-project-top-10-for-large-language-model-applications/>

10. **NCSC: AI and Cyber Security — What You Need to Know**  
   A concise and trustworthy UK-focused reference on the opportunities and risks of AI in cybersecurity.  
   <https://www.ncsc.gov.uk/guidance/ai-and-cyber-security-what-you-need-to-know>

11. **NCSC: Guidelines for Secure AI System Development**  
   Useful for secure design, development, deployment, and operation of AI systems.  
   <https://www.ncsc.gov.uk/files/Guidelines-for-secure-AI-system-development.pdf>

12. **ENISA: Artificial Intelligence and Cybersecurity Research**  
   A European perspective on both AI for cybersecurity and cybersecurity of AI.  
   <https://www.enisa.europa.eu/publications/artificial-intelligence-and-cybersecurity-research>

---

# 2. Week-by-Week Recommended Readings

---

## Week 1 — Introduction to Applied AI for Cybersecurity

### Core reading

1. **CyBOK: AI for Security**  
   Useful for understanding where AI fits within cybersecurity tasks.  
   <https://www.cybok.org/wp-content/uploads/AI_for_Security_TG_v1.0.0.pdf>

2. **NCSC: AI and Cyber Security — What You Need to Know**  
   Useful for a high-level view of AI opportunities and cyber risks.  
   <https://www.ncsc.gov.uk/guidance/ai-and-cyber-security-what-you-need-to-know>

3. **NIST AI Risk Management Framework**  
   Useful for introducing students to AI risk and trustworthy AI from the start.  
   <https://www.nist.gov/itl/ai-risk-management-framework>

### Why these matter

These readings establish the vocabulary of AI in cybersecurity and help students understand the distinction between model prediction and security decision-making.

### Suggested follow-up

- QAA Computing Benchmark Statement  
  <https://www.qaa.ac.uk/the-quality-code/subject-benchmark-statements/computing>

- Warwick module example: Artificial Intelligence for Cyber Security  
  <https://courses.warwick.ac.uk/modules/2025/WM9PH-15>

---

## Week 2 — Cybersecurity Data Engineering and Feature Design

### Core reading

1. **NIST SP 800-92: Guide to Computer Security Log Management**  
   Useful for understanding why security logging, log management, and reliable data collection matter.  
   <https://csrc.nist.gov/pubs/sp/800/92/final>

2. **MITRE ATT&CK Data Sources**  
   Useful for connecting detection ideas to collectable security data sources and data components.  
   <https://attack.mitre.org/datasources/>

3. **MITRE ATT&CK Enterprise Matrix**  
   Useful for relating telemetry and features to adversary tactics and techniques.  
   <https://attack.mitre.org/matrices/enterprise/>

4. **scikit-learn: train_test_split Documentation**  
   Useful for introducing train/test splitting, while also discussing why random splitting may be unsuitable for time-dependent security data.  
   <https://scikit-learn.org/stable/modules/generated/sklearn.model_selection.train_test_split.html>

### Suggested focus

Students should focus on the practical data pipeline: raw logs, parsing, normalisation, feature extraction, labelling, missing values, class imbalance, data leakage, and realistic evaluation splitting.

---

## Week 3 — AI for Network Intrusion and DDoS Detection

### Core reading

1. **MITRE ATT&CK: Network Denial of Service**  
   Useful for understanding denial-of-service behaviour as an adversary technique.  
   <https://attack.mitre.org/techniques/T1498/>

2. **MITRE ATT&CK: Direct Network Flood**  
   Useful for direct flood behaviour.  
   <https://attack.mitre.org/techniques/T1498/001/>

3. **MITRE ATT&CK: Reflection Amplification**  
   Useful for reflection and amplification attacks.  
   <https://attack.mitre.org/techniques/T1498/002/>

4. **CIC-IDS2017 Dataset**  
   Useful for labelled intrusion detection data with PCAPs and extracted flow features.  
   <https://www.unb.ca/cic/datasets/ids-2017.html>

5. **CSE-CIC-IDS2018 Dataset**  
   Useful for modern labelled intrusion detection scenarios and flow features.  
   <https://www.unb.ca/cic/datasets/ids-2018.html>

6. **UNSW-NB15 Dataset**  
   Useful for network intrusion detection data with multiple attack categories.  
   <https://research.unsw.edu.au/projects/unsw-nb15-dataset>

7. **CICFlowMeter**  
   Useful for understanding extraction of network flow features from packet captures.  
   <https://www.unb.ca/cic/research/applications.html>

### Suggested focus

Students should use these references to understand network flow features, DDoS categories, IDS datasets, and the limitations of benchmark-based evaluation.

---

## Week 4 — AI for Malware, Phishing, and Malicious URL Detection

### Core reading

1. **MITRE ATT&CK: Phishing, T1566**  
   Useful for understanding phishing as an adversary technique.  
   <https://attack.mitre.org/techniques/T1566/>

2. **EMBER Dataset Repository**  
   Useful for static malware detection research using Windows PE-file features.  
   <https://github.com/elastic/ember>

3. **PhishTank**  
   Useful for studying phishing URLs and community-supported phishing intelligence.  
   <https://www.phishtank.net/>

4. **PhishTank Developer Information**  
   Useful for understanding access to PhishTank data and API expectations.  
   <https://www.phishtank.net/developer_info.php>

5. **URLhaus by abuse.ch**  
   Useful for malicious URL intelligence related to malware distribution.  
   <https://urlhaus.abuse.ch/>

6. **abuse.ch Threat Intelligence Projects**  
   Useful for exploring URLhaus, ThreatFox, MalwareBazaar, and YARAify.  
   <https://abuse.ch/>

### Suggested focus

Students should focus on static, dynamic, and behavioural artefact analysis; phishing and malicious URL features; dataset limitations; and the cost of false positives and false negatives.

---

## Week 5 — Deep Learning for Cybersecurity

### Core reading

1. **PyTorch Tutorials: Learn the Basics**  
   Useful for understanding basic workflows for data, models, optimisation, and model saving.  
   <https://docs.pytorch.org/tutorials/beginner/basics/intro.html>

2. **PyTorch Neural Networks Tutorial**  
   Useful for understanding neural network modules, loss functions, and neural network building blocks.  
   <https://docs.pytorch.org/tutorials/beginner/blitz/neural_networks_tutorial.html>

3. **TensorFlow: Basic Classification Tutorial**  
   Useful for seeing a complete neural-network classification workflow.  
   <https://www.tensorflow.org/tutorials/keras/classification>

4. **TensorFlow: Convolutional Neural Network Tutorial**  
   Useful for understanding CNNs through a practical image-classification example.  
   <https://www.tensorflow.org/tutorials/images/cnn>

5. **scikit-learn MLPClassifier Documentation**  
   Useful for understanding a basic multi-layer perceptron classifier for structured feature data.  
   <https://scikit-learn.org/stable/modules/generated/sklearn.neural_network.MLPClassifier.html>

6. **MITRE ATLAS**  
   Useful for linking deep learning deployment to adversarial AI risks.  
   <https://atlas.mitre.org/>

### Suggested focus

Students should focus on matching data types to architectures: structured features, byte sequences, event sequences, text, logs, and graphs. Deep learning should be evaluated against simpler baselines.

---

## Week 6 — Explainable AI for Cybersecurity

### Core reading

1. **SHAP Documentation**  
   Useful for understanding SHAP as a game-theoretic approach to explaining model outputs.  
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
   Useful for connecting explainability and interpretability to trustworthy AI risk management.  
   <https://www.nist.gov/itl/ai-risk-management-framework>

6. **DARPA Explainable Artificial Intelligence Programme**  
   Useful for understanding the original motivation behind XAI: helping users understand, appropriately trust, and manage AI systems.  
   <https://www.darpa.mil/research/programs/explainable-artificial-intelligence>

### Suggested focus

Students should focus on local and global explanations, analyst-friendly explanation design, explanation quality, and explanation risk.

---

## Week 7 — AI for Security Operations and Threat Intelligence

### Core reading

1. **NIST SP 800-61 Rev. 3: Incident Response Recommendations and Considerations for Cybersecurity Risk Management**  
   Useful for understanding preparation, detection, response, and recovery.  
   <https://csrc.nist.gov/pubs/sp/800/61/r3/final>

2. **CISA: Cybersecurity Incident and Vulnerability Response Playbooks**  
   Useful for practical response guidance, coordination, remediation, recovery, and tracking.  
   <https://www.cisa.gov/planning-response-recovery>

3. **MITRE ATT&CK Enterprise Matrix**  
   Useful for mapping evidence to adversary tactics and techniques.  
   <https://attack.mitre.org/matrices/enterprise/>

4. **MITRE ATT&CK Enterprise Techniques**  
   Useful for exploring specific adversary techniques and associated behaviours.  
   <https://attack.mitre.org/techniques/enterprise/>

5. **Microsoft Sentinel Documentation**  
   Useful for SIEM/SOAR concepts, analytics, incidents, hunting, and response workflows.  
   <https://learn.microsoft.com/en-us/azure/sentinel/>

6. **Microsoft Sentinel Automation Rules**  
   Useful for understanding orchestration and automation under defined triggers and conditions.  
   <https://learn.microsoft.com/en-us/azure/sentinel/create-manage-use-automation-rules>

### Suggested focus

Students should use these readings to connect alert triage, incident response, threat intelligence, MITRE ATT&CK mapping, and automation boundaries.

---

## Week 8 — Large Language Models for Cybersecurity

### Core reading

1. **OWASP Top 10 for Large Language Model Applications**  
   Useful for understanding LLM application risks across development, deployment, and operation.  
   <https://owasp.org/www-project-top-10-for-large-language-model-applications/>

2. **OWASP LLM01: Prompt Injection**  
   Useful for understanding direct and indirect prompt injection risk.  
   <https://genai.owasp.org/llmrisk/llm01-prompt-injection/>

3. **NIST AI Risk Management Framework**  
   Useful for grounding LLM use in broader AI risk management.  
   <https://www.nist.gov/itl/ai-risk-management-framework>

4. **MITRE ATLAS**  
   Useful for adversarial risks affecting AI-enabled systems, including LLM-enabled workflows.  
   <https://atlas.mitre.org/>

5. **Microsoft Azure OpenAI Service Documentation**  
   Useful as a practical source for enterprise LLM deployment concepts and safety considerations.  
   <https://learn.microsoft.com/en-us/azure/ai-services/openai/>

### Suggested focus

Students should focus on LLM-assisted cybersecurity analysis, RAG, prompt safety, hallucination, data leakage, insecure output handling, and human validation.

---

## Week 9 — AI for Vulnerability Management and Secure Software Engineering

### Core reading

1. **NIST SP 800-218: Secure Software Development Framework**  
   Useful for secure software development practices and mitigating software vulnerability risk.  
   <https://csrc.nist.gov/pubs/sp/800/218/final>

2. **CISA Secure by Design**  
   Useful for understanding security as a core software product responsibility.  
   <https://www.cisa.gov/securebydesign>

3. **CISA Known Exploited Vulnerabilities Catalog**  
   Useful for prioritising vulnerabilities known to be exploited in the wild.  
   <https://www.cisa.gov/known-exploited-vulnerabilities-catalog>

4. **CVE Program**  
   Useful for understanding vulnerability identifiers and public vulnerability records.  
   <https://www.cve.org/>

5. **CVSS by FIRST**  
   Useful for understanding technical severity scoring.  
   <https://www.first.org/cvss/>

6. **OWASP Top 10 Web Application Security Risks**  
   Useful for common web application security weaknesses.  
   <https://owasp.org/www-project-top-ten/>

### Suggested focus

Students should distinguish severity from risk, learn why CVSS alone is insufficient, and understand how AI can support but not replace secure engineering practice.

---

## Week 10 — AI for Cloud, IoT, and Cyber-Physical Security

### Core reading

1. **NIST Cybersecurity for IoT Program**  
   Useful for understanding IoT cybersecurity guidance, tools, and standards.  
   <https://www.nist.gov/itl/applied-cybersecurity/nist-cybersecurity-iot-program>

2. **NISTIR 8259 Series: IoT Cybersecurity Guidance**  
   Useful for IoT device cybersecurity capability guidance.  
   <https://www.nist.gov/itl/applied-cybersecurity/nist-cybersecurity-iot-program/nistir-8259-series>

3. **NIST SP 800-82 Rev. 3: Guide to Operational Technology Security**  
   Useful for securing OT systems while addressing performance, reliability, and safety requirements.  
   <https://csrc.nist.gov/pubs/sp/800/82/r3/final>

4. **MITRE ATT&CK for ICS Matrix**  
   Useful for understanding adversary behaviour in industrial control system environments.  
   <https://attack.mitre.org/matrices/ics/>

5. **MITRE ATT&CK Enterprise Matrix**  
   Useful for enterprise cloud and identity-related adversary behaviours.  
   <https://attack.mitre.org/matrices/enterprise/>

6. **NIST SP 800-204C: DevSecOps for Cloud-Native Applications**  
   Useful for cloud-native DevSecOps and deployment security considerations.  
   <https://csrc.nist.gov/pubs/sp/800/204/c/final>

### Suggested focus

Students should focus on cloud telemetry, IoT constraints, edge detection, federated detection, OT/CPS safety, and the distinction between attack, fault, and operational change.

---

## Week 11 — Trustworthy and Adversarial AI for Cybersecurity

### Core reading

1. **NIST AI Risk Management Framework**  
   Useful for understanding AI risk management and trustworthiness across the AI lifecycle.  
   <https://www.nist.gov/itl/ai-risk-management-framework>

2. **NIST AI RMF Resources: AI Risks and Trustworthiness**  
   Useful for studying trustworthy AI characteristics such as validity, reliability, security, resilience, explainability, privacy, and accountability.  
   <https://airc.nist.gov/airmf-resources/airmf/3-sec-characteristics/>

3. **NIST AI 100-2e2025: Adversarial Machine Learning — A Taxonomy and Terminology**  
   Useful for adversarial machine-learning terminology, taxonomy, and mitigation concepts.  
   <https://csrc.nist.gov/pubs/ai/100/2/e2025/final>

4. **MITRE ATLAS**  
   Useful for adversarial tactics and techniques against AI-enabled systems.  
   <https://atlas.mitre.org/>

5. **OWASP Machine Learning Security Top 10**  
   Useful for practical risks in machine learning systems.  
   <https://owasp.org/www-project-machine-learning-security-top-10/>

6. **NIST Privacy Framework**  
   Useful for privacy risk management in systems that process personal or sensitive data.  
   <https://www.nist.gov/privacy-framework>

7. **OWASP Top 10 for Large Language Model Applications**  
   Useful for LLM-specific risks, including prompt injection and insecure output handling.  
   <https://owasp.org/www-project-top-10-for-large-language-model-applications/>

### Suggested focus

Students should focus on evasion, poisoning, backdoors, model extraction, inversion, membership inference, privacy-preserving AI, federated learning, differential privacy, secure aggregation, and governance.

---

## Week 12 — SecMLOps, Deployment, Monitoring, and Final Integration

### Core reading

1. **NIST AI Risk Management Framework**  
   Useful for AI lifecycle risk management and deployment governance.  
   <https://www.nist.gov/itl/ai-risk-management-framework>

2. **NIST SP 800-204C: DevSecOps for Cloud-Native Applications**  
   Useful for secure deployment and DevSecOps thinking in cloud-native systems.  
   <https://csrc.nist.gov/pubs/sp/800/204/c/final>

3. **NIST SP 800-218: Secure Software Development Framework**  
   Useful for secure software development practices connected to AI system deployment.  
   <https://csrc.nist.gov/pubs/sp/800/218/final>

4. **MITRE ATLAS**  
   Useful for considering adversarial AI risk throughout deployment and monitoring.  
   <https://atlas.mitre.org/>

5. **OWASP Machine Learning Security Top 10**  
   Useful for secure ML lifecycle risk review.  
   <https://owasp.org/www-project-machine-learning-security-top-10/>

6. **MLflow Documentation**  
   Useful for understanding model tracking, model management, and practical MLOps concepts.  
   <https://mlflow.org/docs/latest/index.html>

### Suggested focus

Students should focus on model lifecycle management, versioning, monitoring, drift, retraining governance, rollback, audit logs, feedback loops, and deployment-readiness review.

---

# 3. Recommended Books

The following books are suitable as broader supporting references.

1. **Sarker, I. H.**  
   *AI-Driven Cybersecurity and Cyber Threat Intelligence*  
   Useful for connecting AI techniques with cybersecurity application areas.

2. **Géron, A.**  
   *Hands-On Machine Learning with Scikit-Learn, Keras, and TensorFlow*  
   Excellent for practical machine-learning workflows, preprocessing, model evaluation, and neural-network implementation.

3. **James, G., Witten, D., Hastie, T., Tibshirani, R.**  
   *An Introduction to Statistical Learning*  
   Very suitable for upper-level students who need a clear route into classification, validation, and model comparison.

4. **Bishop, C. M.**  
   *Pattern Recognition and Machine Learning*  
   Strong theoretical depth for students who want more formal foundations.

5. **Goodfellow, I., Bengio, Y., Courville, A.**  
   *Deep Learning*  
   Strong conceptual reference for neural networks and deep learning.

6. **Anderson, H. S. and Roth, P.**  
   *Machine Learning for Cybersecurity Cookbook*  
   A practical reference for students interested in hands-on security analytics examples.

7. **Saxe, J. and Sanders, H.**  
   *Malware Data Science*  
   Useful for malware analysis, feature extraction, and security data science workflows.

8. **Russell, S. and Norvig, P.**  
   *Artificial Intelligence: A Modern Approach*  
   Broad AI reference for students seeking wider conceptual background.

---

# 4. Datasets and Practical Resources

These resources can support labs, coursework, demonstrations, and independent study.

## Network and Intrusion Detection

1. **CIC-IDS2017**  
   <https://www.unb.ca/cic/datasets/ids-2017.html>

2. **CSE-CIC-IDS2018**  
   <https://www.unb.ca/cic/datasets/ids-2018.html>

3. **UNSW-NB15**  
   <https://research.unsw.edu.au/projects/unsw-nb15-dataset>

4. **CICFlowMeter**  
   <https://www.unb.ca/cic/research/applications.html>

## Malware, Phishing, and URLs

1. **EMBER**  
   <https://github.com/elastic/ember>

2. **PhishTank**  
   <https://www.phishtank.net/>

3. **URLhaus**  
   <https://urlhaus.abuse.ch/>

4. **abuse.ch Projects**  
   <https://abuse.ch/>

## Explainability and ML Tooling

1. **SHAP**  
   <https://shap.readthedocs.io/>

2. **LIME**  
   <https://lime-ml.readthedocs.io/>

3. **scikit-learn**  
   <https://scikit-learn.org/>

4. **PyTorch Tutorials**  
   <https://docs.pytorch.org/tutorials/>

5. **TensorFlow Tutorials**  
   <https://www.tensorflow.org/tutorials>

6. **MLflow**  
   <https://mlflow.org/docs/latest/index.html>

---

# 5. Journals and Venues for Advanced Reading

Students who want to explore beyond the taught material may consult papers from:

- IEEE Transactions on Information Forensics and Security
- IEEE Transactions on Dependable and Secure Computing
- IEEE Transactions on Network and Service Management
- IEEE Internet of Things Journal
- IEEE Security & Privacy
- Computers & Security
- Computer Networks
- Journal of Network and Computer Applications
- ACM Transactions on Privacy and Security
- ACM CCS
- IEEE Symposium on Security and Privacy
- NDSS
- USENIX Security
- RAID
- ACSAC
- DIMVA
- AISec Workshop
- NeurIPS, ICML, and ICLR security/adversarial ML workshops

These are not required weekly readings, but they are useful for coursework, case studies, and independent research.

---

# 6. Suggested Referencing Practice for Students

Students should use a mix of:

- authoritative guidance documents;
- standards and cybersecurity body publications;
- peer-reviewed academic papers;
- official tool documentation;
- official dataset documentation;
- course notes and lab outputs where appropriate.

Students should avoid relying heavily on:

- anonymous blog posts;
- marketing material from vendors;
- unsourced AI-generated claims;
- outdated dataset summaries;
- low-quality summaries without evidence;
- claims generated by AI tools without verification.

For assessed work, students should be able to explain:

- why a source is reliable;
- what claim it supports;
- whether it is current enough for the topic;
- whether it is guidance, documentation, dataset description, or academic evidence.

---

# 7. Notes for This Course Website

Each weekly lecture page should include a short reading section linking back to the most relevant sources from this page.

Suggested mapping:

| Week | Reading Anchor |
|---:|---|
| 1 | CyBOK AI for Security, NCSC AI guidance, NIST AI RMF |
| 2 | NIST SP 800-92, MITRE ATT&CK Data Sources |
| 3 | MITRE Network DoS, CIC-IDS2017, CSE-CIC-IDS2018, UNSW-NB15 |
| 4 | MITRE Phishing, EMBER, PhishTank, URLhaus |
| 5 | PyTorch, TensorFlow, scikit-learn MLPClassifier, MITRE ATLAS |
| 6 | SHAP, LIME, NIST AI RMF, DARPA XAI |
| 7 | NIST SP 800-61, CISA playbooks, MITRE ATT&CK, Microsoft Sentinel |
| 8 | OWASP LLM Top 10, OWASP Prompt Injection, NIST AI RMF |
| 9 | NIST SSDF, CISA Secure by Design, CISA KEV, CVE, CVSS, OWASP Top 10 |
| 10 | NIST IoT, NIST SP 800-82, MITRE ATT&CK for ICS |
| 11 | NIST AML taxonomy, MITRE ATLAS, OWASP ML Security Top 10, NIST Privacy Framework |
| 12 | NIST AI RMF, NIST SP 800-204C, MLflow, OWASP ML Security Top 10 |

---

# Summary

The references in this module are intentionally selective. The aim is not to overwhelm students with reading, but to give them a **credible**, **current**, and **well-structured** reading backbone for applied AI in cybersecurity.

The reading list supports the full 12-week progression:

```text
Foundations
→ Data engineering
→ Applied detection tasks
→ Deep learning
→ Explainability
→ Security operations
→ LLMs
→ Vulnerability and software security
→ Cloud, IoT, and CPS
→ Trustworthy and adversarial AI
→ SecMLOps and deployment
```
