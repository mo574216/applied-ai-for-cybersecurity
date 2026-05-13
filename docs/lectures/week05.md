---
title: "Week 05: Deep Learning for Cybersecurity"
layout: default
permalink: /lectures/week5/
---

# Week 05: Deep Learning for Cybersecurity  
## From Handcrafted Features to Learned Representations

Welcome to Week 5 of **Applied AI for Cybersecurity**.

In previous weeks, we studied the foundations of AI for cybersecurity, data engineering, feature design, network intrusion detection, malware detection, phishing detection, and malicious URL detection.

This week introduces **deep learning** for cybersecurity.

The main question is:

> When do deep learning methods add value in cybersecurity, and when are they unnecessary or risky?

Deep learning is powerful because it can learn complex patterns from large datasets. However, deep learning is not automatically better than classical machine learning. In cybersecurity, deep learning models can be difficult to explain, expensive to train, vulnerable to adversarial manipulation, and dependent on high-quality data.

The central lesson this week is:

> Deep learning is useful when the data representation, task complexity, and operational setting justify it. It should not be used only because it sounds advanced.

---

# 1. Learning Objectives

By the end of this week, you should be able to:

1. Explain what deep learning means in a cybersecurity context.
2. Distinguish between classical machine learning and deep learning.
3. Explain why representation learning matters for security data.
4. Identify cybersecurity tasks where deep learning may be useful.
5. Describe the role of MLPs, CNNs, RNNs, LSTMs, autoencoders, transformers, and graph neural networks in cybersecurity.
6. Match different cybersecurity data types to suitable deep learning architectures.
7. Explain how embeddings can represent URLs, commands, logs, binaries, and entities.
8. Discuss the risks of overfitting, poor generalisation, weak explainability, and adversarial evasion.
9. Evaluate whether deep learning is justified for a given cybersecurity use case.
10. Design a conceptual deep learning pipeline for a cybersecurity problem.

---

# 2. Why Deep Learning in Cybersecurity?

Classical machine learning often depends heavily on handcrafted features.

For example, in malicious URL detection, we may manually design features such as:

```text
url_length
domain_age
number_of_dots
entropy
redirect_count
suspicious_keyword_flag
```

In malware detection, we may manually extract:

```text
file_entropy
imported_api_count
suspicious_import_count
section_count
digital_signature_status
```

Deep learning can reduce some manual feature engineering by learning internal representations from data.

For example:

| Security Data | Classical Approach | Deep Learning Approach |
|---|---|---|
| URL | Manually extract URL length, entropy, dots, keywords | Learn character-level or token-level URL representation |
| Email | Manually count suspicious words and URL features | Learn text representation using neural networks or transformers |
| Binary file | Extract PE headers and imported APIs | Learn from byte sequences or binary images |
| Network flow | Use manually engineered flow statistics | Learn temporal or sequential patterns |
| Logs | Extract event counts and rules | Learn event sequences or log embeddings |
| User-device graph | Handcraft relationship features | Learn graph representations |

Deep learning is useful when patterns are complex, high-dimensional, sequential, or difficult to capture manually.

---

# 3. Classical Machine Learning vs Deep Learning

## 3.1 Classical Machine Learning

Classical models include:

- Logistic regression
- Decision trees
- Random forests
- Support vector machines
- k-nearest neighbours
- Naive Bayes
- Gradient boosting

These models often work well when we have good structured features.

Example:

```text
Input features:
- request_rate
- failed_login_count
- url_entropy
- domain_age
- file_entropy

Model:
- Random forest

Output:
- benign or malicious
```

Advantages:

- Often easier to train
- Works with smaller datasets
- More interpretable than many deep models
- Faster to deploy
- Good baseline for many cybersecurity tasks

Limitations:

- Depends heavily on feature engineering
- May struggle with raw sequences, text, binaries, graphs, and high-dimensional data
- May not capture complex relationships automatically

---

## 3.2 Deep Learning

Deep learning models use multiple layers to learn increasingly abstract representations.

Example:

```text
Raw URL characters
→ character embeddings
→ neural layers
→ learned URL representation
→ phishing probability
```

Deep learning may learn patterns such as:

- Suspicious character combinations in URLs
- Sequential event patterns in logs
- Malware byte patterns
- Behavioural sequences in endpoint activity
- Relationships among users, hosts, IPs, and domains

Advantages:

- Can learn representations automatically
- Suitable for text, images, sequences, graphs, and high-dimensional data
- Useful when manual features are incomplete
- Can model complex nonlinear relationships

Limitations:

- Requires more data
- Can overfit
- Often harder to explain
- More computationally expensive
- Can be vulnerable to adversarial manipulation
- May fail when deployment data differs from training data

---

# 4. Core Deep Learning Concepts

## 4.1 Neural Network

A neural network is a model made of connected layers. Each layer transforms the input into a new representation.

A simple neural network may look like this:

```text
Input features
→ hidden layer
→ hidden layer
→ output layer
```

For example, a phishing detector may take URL and email features as input and output:

```text
phishing probability = 0.87
```

---

## 4.2 Neuron

A neuron computes a weighted combination of inputs and passes it through an activation function.

Simplified form:

```text
output = activation(w1*x1 + w2*x2 + ... + b)
```

In cybersecurity, inputs may be:

```text
url_length
domain_age
redirect_count
sender_reputation
attachment_type
```

---

## 4.3 Activation Function

Activation functions introduce nonlinearity.

Common activation functions include:

| Activation | Common Use |
|---|---|
| ReLU | Hidden layers |
| Sigmoid | Binary classification output |
| Softmax | Multi-class classification output |
| Tanh | Some sequence models |

Without nonlinear activation functions, a deep network would behave like a simpler linear model.

---

## 4.4 Loss Function

The loss function measures how wrong the model is.

Examples:

| Task | Common Loss |
|---|---|
| Binary classification | Binary cross-entropy |
| Multi-class classification | Categorical cross-entropy |
| Reconstruction anomaly detection | Mean squared error |
| Ranking | Ranking loss |

For a malware classifier, the loss measures the difference between predicted label and true label.

---

## 4.5 Backpropagation

Backpropagation is the process used to update neural network weights during training.

The model:

```text
makes prediction
calculates loss
propagates error backward
updates weights
repeats
```

This is how the model learns patterns from data.

---

## 4.6 Epoch, Batch, and Learning Rate

| Term | Meaning |
|---|---|
| Epoch | One full pass through the training data |
| Batch | A small group of samples processed together |
| Learning rate | How large each weight update is |

If the learning rate is too high, training may be unstable. If it is too low, training may be very slow.

---

# 5. Multi-Layer Perceptron for Structured Security Data

A **Multi-Layer Perceptron**, or MLP, is a basic feedforward neural network.

It is suitable for structured feature tables.

Example input:

| Feature | Value |
|---|---:|
| url_length | 74 |
| domain_age_days | 3 |
| redirect_count | 4 |
| suspicious_keyword_count | 2 |
| sender_reputation_score | 0.21 |

Possible task:

```text
Predict whether a URL is benign or malicious.
```

MLP pipeline:

```text
Structured features
→ input layer
→ hidden layers
→ output layer
→ prediction
```

## When MLPs Are Useful

MLPs can be useful for:

- Malicious URL detection from structured features
- Phishing detection from engineered features
- Flow-based intrusion detection
- Malware detection from extracted static features
- Vulnerability risk scoring

## When MLPs May Not Be Enough

MLPs may be weak when the data has strong sequential, spatial, textual, or graph structure.

For example:

- Event sequences may need sequence models.
- Text may benefit from language models.
- Binary byte patterns may benefit from CNNs or transformers.
- User-device relationships may benefit from graph neural networks.

Further reading:

- scikit-learn MLPClassifier documentation:  
  <https://scikit-learn.org/stable/modules/generated/sklearn.neural_network.MLPClassifier.html>

---

# 6. Convolutional Neural Networks for Cybersecurity

Convolutional Neural Networks, or CNNs, are commonly associated with image processing. However, they can also be used for some cybersecurity tasks.

## 6.1 CNNs for Malware Images

Some malware detection approaches convert binary files into image-like representations.

Example:

```text
binary bytes
→ grayscale image
→ CNN
→ malware family prediction
```

The idea is that malware families may show visual patterns when binary bytes are represented as images.

## 6.2 CNNs for Byte Sequences

CNNs can also detect local patterns in byte sequences.

Example:

```text
byte sequence from executable
→ convolutional filters
→ learned local patterns
→ malware classification
```

## 6.3 CNNs for Network Traffic

CNNs can sometimes be applied to structured traffic matrices or packet sequences.

Example:

```text
packet size sequence
packet direction sequence
time-window matrix
```

## Advantages

- Good at learning local patterns
- Useful for image-like or sequence-like representations
- Can reduce manual feature engineering

## Limitations

- Requires careful representation design
- May learn dataset artefacts
- Can be difficult to explain
- May not capture long-term dependencies well unless combined with other methods

Further reading:

- TensorFlow CNN tutorial:  
  <https://www.tensorflow.org/tutorials/images/cnn>

---

# 7. Sequence Models: RNN, LSTM, and GRU

Many cybersecurity behaviours are sequential.

Examples:

```text
login failure → login failure → login success → sensitive file access
```

```text
Word launches PowerShell → PowerShell downloads file → file creates scheduled task
```

```text
DNS query → connection to IP → download payload → beaconing
```

Sequence models are designed to process ordered data.

---

## 7.1 Recurrent Neural Networks

A Recurrent Neural Network, or RNN, processes data step by step.

Example:

```text
event_1 → event_2 → event_3 → event_4 → prediction
```

RNNs maintain a hidden state that carries information from previous steps.

## 7.2 LSTM and GRU

LSTMs and GRUs are improved sequence models designed to better handle longer dependencies.

They may be useful for:

- System call sequences
- Endpoint behaviour
- Authentication sequences
- Network event sequences
- Log event sequences
- User behaviour analytics

## Example: Endpoint Behaviour

Sequence:

```text
winword.exe starts
powershell.exe starts
encoded command runs
unknown executable downloaded
scheduled task created
```

A sequence model may learn that this order is suspicious.

## Limitations

- Requires ordered event data
- Sensitive to missing events
- Harder to interpret than simple models
- Long sequences can be computationally expensive
- Modern transformer models often outperform older RNN-based approaches for text and long sequences

---

# 8. Autoencoders for Anomaly Detection

An autoencoder is a neural network trained to reconstruct its input.

Pipeline:

```text
input
→ compressed representation
→ reconstructed input
```

The model learns normal patterns. If it cannot reconstruct a new sample well, the sample may be anomalous.

## Example: Network Anomaly Detection

Train an autoencoder on normal network flow features:

```text
duration
bytes
packets
packet_rate
flow_iat_mean
destination_port
```

During deployment:

```text
normal flow → low reconstruction error
unusual flow → high reconstruction error
```

A high reconstruction error may indicate anomaly.

## Important Warning

Anomaly does not automatically mean attack.

A high reconstruction error could mean:

- New application
- Legitimate traffic spike
- Configuration change
- Data collection error
- Attack
- Rare but benign behaviour

## Suitable Use Cases

Autoencoders may be useful for:

- Network anomaly detection
- IoT device anomaly detection
- User behaviour anomaly detection
- Cloud API anomaly detection
- Endpoint behaviour anomaly detection

## Limitations

- Can generate many false positives
- Requires representative normal training data
- May fail when normal behaviour changes
- Reconstruction error thresholds need careful tuning

---

# 9. Transformers for Cybersecurity

Transformers are neural network architectures that are especially effective for sequence and language-related tasks.

They are widely used in large language models, but they can also be applied to cybersecurity data.

## 9.1 Transformers for Text Security

Examples:

- Phishing email classification
- Threat report summarisation
- Security ticket classification
- Vulnerability description analysis
- Abuse report clustering

## 9.2 Transformers for Logs

Security logs are sequences of events.

Example:

```text
login_success
file_access
privilege_change
process_execution
network_connection
```

A transformer may learn relationships between events across longer contexts.

## 9.3 Transformers for Malware

Transformers may be applied to:

- API call sequences
- Opcode sequences
- Byte sequences
- Function call sequences

## Advantages

- Good at modelling long-range dependencies
- Useful for text and sequences
- Can use pretrained representations
- Flexible across many data types

## Limitations

- Data-hungry
- Computationally expensive
- Can hallucinate if used as generative systems
- Hard to explain
- Sensitive to training data quality
- Can introduce privacy and prompt-injection risks when used as LLMs

Large language models will be covered separately in Week 8.

---

# 10. Embeddings for Cybersecurity

An embedding is a numerical representation of an object.

The object may be:

- Word
- URL token
- Command
- Domain
- IP address
- File
- Process
- User
- Host
- Alert
- Malware sample

The goal is to represent similar objects close together in the embedding space.

## Example: URL Token Embeddings

URLs:

```text
login-secure-example.com/verify
university-password-reset.net/account
normal-university.edu/library
```

A model may learn representations that capture:

- login-related tokens
- security-related words
- suspicious domain structure
- impersonation patterns

## Example: Command Embeddings

Commands:

```text
powershell -enc ...
curl http://unknown-domain/payload
certutil -urlcache -split -f ...
```

Command embeddings may help detect suspicious command-line behaviour.

## Example: Entity Embeddings

In security operations, entities include:

```text
users
hosts
IP addresses
domains
files
processes
```

Embeddings can help represent relationships among entities.

---

# 11. Graph Neural Networks for Cybersecurity

Many cybersecurity problems are naturally graph-based.

Examples:

```text
user → logs into → host
host → connects to → IP
process → downloads → file
file → contacts → domain
domain → resolves to → IP
```

Graph Neural Networks, or GNNs, learn from nodes and edges.

## 11.1 Graph Components

| Graph Element | Cybersecurity Example |
|---|---|
| Node | User, host, process, domain, IP, file |
| Edge | Login, connection, download, execution |
| Node feature | User role, host type, file entropy |
| Edge feature | Timestamp, frequency, bytes, action |
| Label | Malicious node, suspicious edge, compromised host |

## 11.2 Use Cases

GNNs may be useful for:

- Attack graph analysis
- Lateral movement detection
- Fraud detection
- Botnet detection
- Entity relationship modelling
- Alert correlation
- Threat intelligence graph analysis
- User-host-IP-domain relationship analysis

## 11.3 Example

Graph evidence:

```text
user_A logs into host_1
host_1 connects to rare_domain
rare_domain resolves to suspicious_IP
host_1 downloads file_X
file_X appears on host_2
```

A graph model may help detect suspicious relationships that are not visible from one event alone.

## Limitations

- Graph construction is difficult
- Graphs can be large and dynamic
- Labels may be sparse
- Explanations are challenging
- Attackers may manipulate graph structure

---

# 12. Choosing the Right Deep Learning Architecture

Different data types require different modelling choices.

| Cybersecurity Data | Possible Architecture | Example Task |
|---|---|---|
| Structured feature table | MLP | Flow-based intrusion classification |
| URL characters | CNN, RNN, transformer | Malicious URL detection |
| Email text | Transformer | Phishing detection |
| Binary bytes | CNN, transformer | Malware detection |
| API call sequence | LSTM, GRU, transformer | Malware behaviour classification |
| Network time series | LSTM, GRU, autoencoder | DDoS anomaly detection |
| User behaviour sequence | LSTM, transformer | Account compromise detection |
| Entity relationships | GNN | Alert correlation or lateral movement |
| Logs | Transformer, LSTM, autoencoder | Log anomaly detection |
| Normal-only behaviour | Autoencoder | Anomaly detection |

## Main Decision Question

Before choosing deep learning, ask:

```text
Does the data structure justify a deep model?
```

If the data is a small structured table, a classical model may be better.

If the data is large, sequential, textual, graph-based, or high-dimensional, deep learning may add value.

---

# 13. Case Study 1: Deep Learning for Malicious URL Detection

## Scenario

A security team wants to detect malicious URLs.

Classical approach:

```text
Extract handcrafted features:
- URL length
- number of dots
- number of digits
- domain age
- entropy
- suspicious keywords
```

Deep learning approach:

```text
Input raw URL characters or tokens
→ embedding layer
→ sequence model or transformer
→ malicious URL probability
```

## Possible Advantages

- Learns suspicious token patterns automatically
- May detect previously unseen URL structures
- Can use character-level information
- Reduces reliance on manually selected keywords

## Possible Risks

- May overfit to dataset-specific domains
- May fail when attackers change patterns
- May be difficult to explain
- May require many labelled URLs
- May learn shortcuts such as specific domain names rather than general malicious behaviour

## Security Question

Should the model block URLs automatically?

A responsible answer depends on:

- Confidence
- Explanation quality
- False positive cost
- User impact
- Threat intelligence
- Whether the URL is already known malicious
- Whether human review is available

---

# 14. Case Study 2: Autoencoder for IoT Anomaly Detection

## Scenario

An organisation has many IoT devices. Each device normally sends small periodic traffic to a cloud service.

Normal features:

```text
packet_rate
byte_rate
destination_count
dns_query_count
flow_duration
connection_interval
```

A compromised device starts scanning the internal network.

Possible observed change:

```text
destination_count increases
unique_port_count increases
packet_rate changes
connection_interval becomes irregular
```

## Deep Learning Approach

Train an autoencoder on normal IoT device behaviour.

Deployment:

```text
normal behaviour → low reconstruction error
abnormal scanning behaviour → high reconstruction error
```

## Advantages

- Does not require many labelled attack samples
- Useful for device behaviour monitoring
- Can detect unusual patterns

## Risks

- New firmware updates may look anomalous
- Device maintenance may trigger false positives
- Compromised behaviour may be slow and subtle
- Reconstruction error does not explain the cause by itself

## Main Lesson

Autoencoders can help detect anomalies, but analysts still need context and explanation.

---

# 15. Case Study 3: Sequence Model for Endpoint Behaviour

## Scenario

An endpoint tool records process events.

Sequence A:

```text
explorer.exe → chrome.exe → download.pdf
```

Sequence B:

```text
winword.exe → powershell.exe → encoded command → download.exe → scheduled task
```

Sequence B is more suspicious because the order of events suggests possible malicious document execution.

## Deep Learning Approach

A sequence model may learn patterns of suspicious process chains.

Possible inputs:

```text
process names
parent-child relationships
command-line tokens
file creation events
network connections
timestamps
```

Possible outputs:

```text
benign
suspicious
malware-like behaviour
```

## Main Lesson

For endpoint detection, the sequence of actions often matters more than a single event.

---

# 16. Case Study 4: Graph-Based Alert Correlation

## Scenario

A SOC has many alerts involving:

```text
users
hosts
IP addresses
domains
processes
files
cloud accounts
```

Instead of analysing each alert separately, the SOC builds a graph.

Example:

```text
user_1 → logged into → host_3
host_3 → connected to → domain_X
domain_X → resolves to → IP_Y
host_3 → executed → process_Z
process_Z → downloaded → file_A
file_A → appeared on → host_7
```

## Deep Learning Approach

A graph neural network may help identify suspicious clusters or relationships.

## Possible Use

- Alert correlation
- Lateral movement detection
- Malware spread analysis
- Threat intelligence enrichment
- Entity risk scoring

## Risks

- Incorrect graph construction may mislead the model
- Missing edges may hide attack paths
- Explanations may be difficult
- Attackers may manipulate relationships

---

# 17. Evaluation of Deep Learning Cybersecurity Models

Deep learning models must be evaluated carefully.

Useful metrics include:

| Metric | Why It Matters |
|---|---|
| Accuracy | Overall correctness, but can be misleading |
| Precision | Controls false alarms |
| Recall | Measures attack detection capability |
| F1-score | Balances precision and recall |
| False positive rate | Important for analyst workload |
| False negative rate | Important for missed attacks |
| Detection latency | Important for time-sensitive attacks |
| Robustness | Measures performance under manipulation |
| Generalisation | Measures performance on new environments |
| Explainability | Whether analysts can understand the output |
| Computational cost | Whether deployment is practical |

## Evaluation Questions

Before accepting a deep model, ask:

1. Was it compared with classical baselines?
2. Was it tested on unseen time periods or environments?
3. Was class imbalance handled properly?
4. Was overfitting checked?
5. Was adversarial robustness tested?
6. Can analysts understand the result?
7. Does it meet operational latency requirements?
8. What happens when the model is wrong?

---

# 18. Common Pitfalls

## 18.1 Deep Learning Without Enough Data

Deep learning often requires large amounts of data.

If the dataset is small, a deep model may overfit.

Example:

```text
Training accuracy: 99%
Test accuracy: 70%
```

This suggests the model memorised training data instead of learning general patterns.

---

## 18.2 Ignoring Classical Baselines

A deep learning model should be compared with simpler models.

Possible baselines:

- Logistic regression
- Random forest
- Gradient boosting
- SVM
- Rule-based system

If a random forest performs similarly with better explainability, deep learning may not be justified.

---

## 18.3 Learning Dataset Artefacts

A deep model may learn shortcuts.

Examples:

- Specific file paths in malware datasets
- Lab-generated attack timing
- Source folder names
- Repeated campaign indicators
- Domain names that appear only in one class
- Duplicate samples across train and test sets

This leads to unrealistic performance.

---

## 18.4 Weak Explainability

Deep models may output:

```text
malicious probability = 0.94
```

But analysts need to know why.

A better output includes:

```text
Risk increased because:
- encoded PowerShell command was observed
- process chain is unusual
- unknown executable was downloaded
- persistence mechanism was created
```

---

## 18.5 Adversarial Manipulation

Attackers may modify inputs to reduce detection.

Examples:

- Reword phishing emails
- Change URL structure
- Pad malware binaries
- Slow down scans
- Split traffic across time
- Mimic normal user behaviour

Deep models must be tested against adaptive attackers.

MITRE ATLAS is a useful reference for adversarial threats against AI-enabled systems:  
<https://atlas.mitre.org/>

---

# 19. Week 5 Summary

This week focused on deep learning for cybersecurity.

Key points:

```text
Deep learning can learn representations from complex security data.

MLPs are useful for structured feature tables.

CNNs can learn local patterns in images, byte sequences, or traffic representations.

RNNs, LSTMs, and GRUs can model ordered security events.

Autoencoders can support anomaly detection when labelled attacks are limited.

Transformers are useful for text, logs, sequences, and threat reports.

Embeddings represent URLs, commands, files, users, hosts, and other entities numerically.

Graph neural networks can model relationships among security entities.

Deep learning is not automatically better than classical machine learning.

Evaluation must include baselines, generalisation, robustness, explainability, and operational cost.
```

Final takeaway:

> Deep learning is valuable in cybersecurity when it learns meaningful security behaviour, generalises beyond the dataset, and supports explainable security decisions.

---

# 20. Lab Sheet 5: Designing Deep Learning Pipelines for Cybersecurity

## Lab Overview

In this lab, you will design deep learning approaches for cybersecurity problems. You will not train a full deep model in this lab. Instead, you will focus on matching data types to model architectures, designing input representations, identifying risks, and evaluating whether deep learning is justified.

---

## Lab Duration

Approximate duration: 90 minutes.

---

## Lab Mode

Individual work followed by small-group discussion.

---

## Lab Objectives

By completing this lab, you should be able to:

1. Match cybersecurity data types to suitable deep learning architectures.
2. Design input representations for URLs, logs, malware, network flows, and security graphs.
3. Explain when deep learning is justified.
4. Compare deep learning with classical machine learning baselines.
5. Identify overfitting, explainability, and adversarial risks.
6. Propose suitable evaluation methods for deep learning security models.

---

# 21. Lab Dataset A: Cybersecurity Deep Learning Scenarios

Use the following simplified scenarios.

| ID | Scenario |
|---|---|
| D1 | A dataset of URLs labelled as benign, phishing, or malware-distribution URLs |
| D2 | Network flow records from an enterprise gateway with benign, scan, DDoS, and botnet labels |
| D3 | Endpoint process sequences from workstations, including benign activity and malware-like chains |
| D4 | Windows executable files represented as byte sequences |
| D5 | DNS query sequences from IoT devices |
| D6 | Security alerts involving users, hosts, IPs, domains, files, and processes |
| D7 | Email messages labelled as phishing or legitimate |
| D8 | Cloud API call sequences from administrator accounts |
| D9 | Vulnerability descriptions and exploitability labels |
| D10 | Normal-only traffic from industrial sensors |

---

# 22. Lab Task 1 — Match Data Type to Architecture

For each scenario, choose one or more suitable deep learning architectures.

Possible architectures:

```text
MLP
CNN
RNN
LSTM
GRU
Autoencoder
Transformer
Graph Neural Network
Hybrid model
Classical ML baseline
```

Complete the table.

| ID | Data Type | Suitable Architecture | Reason |
|---|---|---|---|
| D1 |  |  |  |
| D2 |  |  |  |
| D3 |  |  |  |
| D4 |  |  |  |
| D5 |  |  |  |
| D6 |  |  |  |
| D7 |  |  |  |
| D8 |  |  |  |
| D9 |  |  |  |
| D10 |  |  |  |

---

# 23. Lab Task 2 — Design Input Representation

Choose four scenarios from Dataset A.

For each one, describe how the input should be represented.

Examples:

```text
URL characters
URL tokens
flow feature vector
process sequence
byte sequence
log event sequence
graph of entities
text embeddings
time-series sensor values
```

Complete the table.

| Scenario ID | Input Representation | Why This Representation Is Suitable |
|---|---|---|
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |

---

# 24. Lab Task 3 — Deep Learning or Classical ML?

For each scenario, decide whether deep learning is justified.

Complete the table.

| Scenario ID | Use Deep Learning? Yes / No / Maybe | Classical Baseline to Compare | Justification |
|---|---|---|---|
| D1 |  |  |  |
| D2 |  |  |  |
| D3 |  |  |  |
| D4 |  |  |  |
| D5 |  |  |  |
| D6 |  |  |  |
| D7 |  |  |  |
| D8 |  |  |  |
| D9 |  |  |  |
| D10 |  |  |  |

Important:

> A deep model should be justified. Do not choose deep learning only because it is advanced.

---

# 25. Lab Task 4 — Identify Risks

For each chosen deep learning design, identify possible risks.

Possible risks:

```text
overfitting
class imbalance
poor labels
dataset leakage
weak explainability
adversarial evasion
high computational cost
privacy risk
deployment latency
concept drift
poor generalisation
```

Complete the table for three scenarios.

| Scenario ID | Risk 1 | Risk 2 | Risk 3 | Mitigation Idea |
|---|---|---|---|---|
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |

---

# 26. Lab Task 5 — Evaluation Plan

Choose one scenario and design an evaluation plan.

Your plan should include:

| Evaluation Element | Your Answer |
|---|---|
| Task definition |  |
| Model output |  |
| Baseline model |  |
| Dataset split strategy |  |
| Metrics |  |
| False positive cost |  |
| False negative cost |  |
| Explainability requirement |  |
| Robustness test |  |
| Deployment concern |  |

---

# 27. Lab Task 6 — Explain the Model Output

Rewrite this poor model output into an analyst-friendly explanation.

Poor output:

```text
Prediction: malicious
Confidence: 96%
```

Your improved explanation should include:

- Main evidence used by the model
- Risk-increasing factors
- Risk-reducing factors
- Missing context
- Confidence level
- Suggested next step
- Whether human review is required

---

# 28. Lab Task 7 — Architecture Critique

Read the following claim:

```text
A transformer model should be used for all cybersecurity detection tasks because transformers are state-of-the-art.
```

Answer:

1. Why is this claim too simplistic?
2. Which tasks may benefit from transformers?
3. Which tasks may not need transformers?
4. What baselines should be compared?
5. What deployment risks should be considered?
6. What evidence would convince you that a transformer is justified?

---

# 29. Lab Deliverable

Submit a short worksheet containing:

1. Architecture matching table.
2. Input representation table.
3. Deep learning versus classical ML justification.
4. Risk analysis table.
5. Evaluation plan.
6. Analyst-friendly model explanation.
7. Architecture critique.

Recommended length:

```text
1200–1800 words
```

---

# 30. Exercises

## Exercise 1 — Concept Check

Answer briefly.

1. What is deep learning?
2. What is representation learning?
3. What is the difference between an MLP and a CNN?
4. Why are sequence models useful in cybersecurity?
5. What is an autoencoder?
6. Why can autoencoders be used for anomaly detection?
7. What is an embedding?
8. Why might graph neural networks be useful for security operations?
9. Why is deep learning not always better than classical machine learning?
10. Why is explainability especially important for deep cybersecurity models?

---

## Exercise 2 — Short Analytical Answer

Write 250–300 words.

**Question:**  
When is deep learning justified in cybersecurity, and when might it be unnecessary?

Your answer should discuss:

- Data type
- Dataset size
- Feature engineering
- Interpretability
- Computational cost
- Baseline comparison
- Deployment constraints
- Security risk

---

## Exercise 3 — Architecture Selection

Choose a suitable architecture for each task and justify your answer.

| Task | Suggested Architecture | Justification |
|---|---|---|
| Phishing email classification |  |  |
| Malware byte sequence classification |  |  |
| Flow-based DDoS detection |  |  |
| Endpoint process-chain detection |  |  |
| IoT normal-behaviour anomaly detection |  |  |
| Alert correlation using user-host-domain relationships |  |  |
| Vulnerability description classification |  |  |

---

## Exercise 4 — Overfitting Reflection

A deep malware classifier reports:

```text
Training accuracy: 99.8%
Validation accuracy: 71%
Test accuracy: 68%
```

Answer:

1. What does this suggest?
2. What may have caused it?
3. What would you check in the dataset?
4. What regularisation or evaluation changes might help?
5. Why is this dangerous in cybersecurity?

---

## Exercise 5 — Autoencoder Case

An autoencoder is trained on normal cloud API activity.

Later, it flags many events as anomalous after the organisation migrates to a new cloud service.

Answer:

1. Is this necessarily an attack?
2. What other explanations are possible?
3. What additional context is needed?
4. How should the model be updated?
5. What monitoring should be in place?

---

## Exercise 6 — Explainability Practice

Rewrite this output:

```text
URL classified as malicious.
Confidence: 91%.
```

Your explanation should include:

- URL features
- Host or domain features
- Model uncertainty
- Risk-reducing evidence
- Recommended action
- Whether automatic blocking is justified

---

## Exercise 7 — Critical Reflection

Write 200–300 words.

**Question:**  
What is the biggest risk of deploying deep learning models in cybersecurity without strong evaluation and human oversight?

Discuss:

- False positives
- False negatives
- Overconfidence
- Poor explainability
- Adversarial evasion
- Business disruption
- Analyst trust

---

# 31. Further Reading

## Core Reading

1. **PyTorch Tutorials: Learn the Basics**  
   Useful for understanding the basic workflow of working with data, creating models, optimising model parameters, and saving trained models.  
   <https://docs.pytorch.org/tutorials/beginner/basics/intro.html>

2. **PyTorch Neural Networks Tutorial**  
   Useful for understanding neural network modules, loss functions, and the building blocks of deep neural networks.  
   <https://docs.pytorch.org/tutorials/beginner/blitz/neural_networks_tutorial.html>

3. **TensorFlow: Basic Classification Tutorial**  
   Useful for seeing a complete neural network classification workflow using TensorFlow and Keras.  
   <https://www.tensorflow.org/tutorials/keras/classification>

4. **TensorFlow: Convolutional Neural Network Tutorial**  
   Useful for understanding CNNs through an image classification example.  
   <https://www.tensorflow.org/tutorials/images/cnn>

5. **scikit-learn MLPClassifier Documentation**  
   Useful for understanding a basic multi-layer perceptron classifier for structured feature data.  
   <https://scikit-learn.org/stable/modules/generated/sklearn.neural_network.MLPClassifier.html>

6. **MITRE ATLAS**  
   Useful for understanding adversarial threats against AI-enabled systems.  
   <https://atlas.mitre.org/>

---

## Suggested Search Topics

Search for recent academic or technical material on:

- Deep learning for intrusion detection
- Deep learning for malware detection
- CNN for malware classification
- LSTM for system call sequence analysis
- Autoencoders for anomaly detection
- Transformers for cybersecurity logs
- Graph neural networks for cybersecurity
- Embeddings for URLs and commands
- Deep learning for phishing detection
- Explainable deep learning for cybersecurity
- Adversarial examples in cybersecurity
- Deep learning model drift in security
- Dataset leakage in deep learning cybersecurity models
- Benchmarking deep learning against classical ML in cybersecurity

---

# 32. Week 5 Summary

This week introduced deep learning for cybersecurity.

The most important lessons are:

```text
Deep learning can learn complex representations from security data.

Different architectures are suitable for different data types.

MLPs work with structured feature tables.

CNNs can learn local patterns from images, byte sequences, and traffic representations.

Sequence models can learn ordered behaviours.

Autoencoders can support anomaly detection.

Transformers can model text, logs, and long event sequences.

Graph neural networks can represent relationships among security entities.

Deep learning must be compared against classical baselines.

A deep model is useful only if it generalises, supports security decisions, and can be evaluated responsibly.
```

Final takeaway:

> Deep learning should not be used in cybersecurity because it is fashionable.  
> It should be used when the data, task, and operational need justify the complexity.
