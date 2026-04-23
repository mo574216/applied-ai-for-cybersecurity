---
title: "Week 2 — Data, Features, and Classical Machine Learning for Security Analytics"
layout: default
permalink: "/docs/lectures/week2.html"
---

# Week 2 — Data, Features, and Classical Machine Learning for Security Analytics

## Overview

This week focuses on the practical core of many applied AI systems in cybersecurity:

- preparing cyber data;
- selecting and engineering features;
- applying classical machine-learning methods;
- evaluating results in ways that make operational sense.

Students often rush to deep learning or GenAI because these appear modern and powerful. In practice, many real security tasks are still solved effectively with careful preprocessing, feature engineering, and well-understood classical models.

The central message of this week is:

**A simple model on well-prepared data is often more valuable than a sophisticated model on badly understood data.**

---

## Learning Outcomes

By the end of this week, students should be able to:

1. explain the role of preprocessing and feature engineering in cyber datasets;
2. distinguish between supervised learning, unsupervised learning, and anomaly detection in security contexts;
3. apply basic classical machine-learning models to a cybersecurity dataset;
4. evaluate model results using metrics suitable for security problems;
5. identify common pitfalls such as class imbalance, leakage, overfitting, and unrealistic datasets.

---

## 1. Why data preparation matters

Cybersecurity data is rarely ready for modelling in raw form. Real datasets are often:

- incomplete;
- imbalanced;
- noisy;
- duplicated;
- inconsistently labelled;
- temporally messy;
- context-dependent.

A model trained on poorly prepared data may learn irrelevant patterns, produce unstable results, or appear strong in testing but fail in deployment.

### Example

Suppose a malicious URL dataset contains a feature such as “source list name” where one feed mainly contains malicious entries and another contains benign entries. A model may learn the feed source instead of learning meaningful URL behaviour. This is not intelligence. It is accidental shortcut learning.

---

## 2. Typical steps in cyber data preprocessing

### 2.1 Cleaning

This may include:

- removing duplicates;
- fixing malformed entries;
- handling missing values;
- normalising inconsistent categorical values;
- converting timestamps into usable formats.

### 2.2 Selection

Some columns may be irrelevant, redundant, or dangerous because they leak label information.

For example, if a field is created only after analyst confirmation, it may not be available at prediction time. Keeping it in training would produce unrealistic performance.

### 2.3 Transformation

Examples include:

- one-hot encoding of categorical variables;
- scaling or normalisation of numerical features;
- tokenisation of text;
- aggregation of event sequences;
- temporal summarisation over fixed windows.

### 2.4 Splitting the data

Students should separate data into training, validation, and test sets carefully.

In cyber contexts, random splits are not always sufficient. A time-based split may be more realistic because it better reflects deployment conditions.

---

## 3. Feature engineering in cybersecurity

A feature is a measurable property used by the model. Feature engineering is the process of designing or selecting features that help distinguish meaningful patterns.

### 3.1 Why features matter

The model only sees the world through the features it is given. If the features are weak, noisy, or misleading, the model will also be weak, noisy, or misleading.

### 3.2 Examples of cybersecurity features

#### Network-based features
- packet count;
- byte count;
- flow duration;
- source/destination port;
- protocol;
- number of failed connections;
- ratio of incoming to outgoing traffic.

#### Authentication features
- login time;
- geolocation;
- device novelty;
- failed login count;
- impossible travel indicators;
- privilege level.

#### Email and URL features
- domain age;
- character distribution;
- number of subdomains;
- URL length;
- attachment type;
- mismatch between displayed and actual link.

#### Host-based features
- process tree depth;
- unusual parent-child process pairs;
- registry modifications;
- frequency of script execution;
- file entropy indicators.

### 3.3 Good feature engineering principles

Good features are usually:

- available at the time of decision;
- interpretable enough to reason about;
- relevant to the threat model;
- not direct leaks of the answer;
- stable enough to be useful beyond one narrow dataset.

---

## 4. Supervised learning in security analytics

Supervised learning uses labelled examples.

### Typical security tasks
- phishing vs benign email;
- malicious vs benign URL;
- attack vs normal flow;
- malware family classification;
- suspicious vs routine alert.

### Common classical models
- logistic regression;
- decision trees;
- random forests;
- support vector machines;
- k-nearest neighbours;
- gradient boosting methods.

### When supervised learning works well
It works best when:

- labels are reasonably reliable;
- the threat pattern is learnable from the data;
- the training set is representative enough;
- the organisation understands the cost of different errors.

### Weaknesses
Supervised learning may struggle when:

- labels are scarce or inconsistent;
- attacker behaviour shifts;
- rare classes are underrepresented;
- models learn artefacts rather than security-relevant structure.

---

## 5. Unsupervised learning and anomaly detection

Many cyber problems do not have good labels. In these cases, unsupervised or semi-supervised approaches may be attractive.

### 5.1 Unsupervised learning

Unsupervised methods look for structure without labelled targets.

Examples:
- clustering similar alerts;
- grouping related behaviours;
- identifying outlier activity patterns.

### 5.2 Anomaly detection

Anomaly detection asks whether a data point is unusual relative to a baseline.

Examples:
- unusual login time for a user;
- abnormal traffic volume from a device;
- rare process behaviour on an endpoint.

### Important caution

Anomalous does not necessarily mean malicious.

A system upgrade, a holiday period, or a new service rollout may look anomalous. This is why anomaly detection can produce many false positives in security environments.

---

## 6. Class imbalance and why accuracy is not enough

Many cyber datasets are heavily imbalanced. Malicious cases may be far rarer than benign ones.

### Example

Suppose 99% of events are benign and 1% are malicious.

A model that labels everything as benign gets 99% accuracy, but it is useless.

### Better metrics

#### Precision
Of the alerts flagged as malicious, how many are actually malicious?

High precision reduces analyst fatigue.

#### Recall
Of the actual malicious cases, how many did the model catch?

High recall reduces missed attacks.

#### F1-score
A balance between precision and recall.

#### ROC-AUC
Useful for ranking-based comparisons, but it can be misleading in highly imbalanced settings.

#### PR-AUC
Often more informative than ROC-AUC when the positive class is rare.

#### Confusion matrix
Shows true positives, true negatives, false positives, and false negatives directly.

### Security interpretation

A model is not good because it has a high number. It is good if its pattern of errors is acceptable for the operational setting.

---

## 7. Data leakage

Data leakage occurs when information from outside the true decision context enters training or testing.

### Common forms of leakage

- using future information in training features;
- including analyst-confirmed fields unavailable at prediction time;
- random splits that let near-duplicate events appear in both train and test;
- deriving features from the label itself.

Leakage is one of the main reasons published or classroom results may appear unrealistically strong.

### Rule of thumb

Always ask:

> Would this information actually exist at the moment the system must make the decision?

If the answer is no, it should not be part of the predictive feature set.

---

## 8. Overfitting and underfitting

### Underfitting
The model is too simple or the features are too weak to capture useful structure.

### Overfitting
The model learns peculiarities of the training data instead of generalisable patterns.

In cybersecurity, overfitting is especially dangerous because attackers and environments change. A model that memorises one dataset may collapse in a live setting.

### Practical warning signs
- strong training performance but weak test performance;
- unstable behaviour across splits;
- dependence on a few suspicious features;
- performance collapse on newer data.

---

## 9. Case study: intrusion detection with classical ML

Consider a simplified network intrusion dataset.

### Objective
Classify network flows as benign or attack-related.

### Candidate features
- protocol type;
- connection duration;
- source bytes;
- destination bytes;
- failed connection count;
- flag indicators.

### Possible models
- logistic regression;
- decision tree;
- random forest.

### Questions for evaluation
- Which model gives the highest recall?
- Which model gives the lowest false-positive rate?
- Which model is easiest to explain?
- Would the results hold on future traffic?
- Are any features likely to reflect artefacts of the dataset rather than the attack itself?

This case illustrates the difference between classroom experimentation and operational reasoning.

---

## 10. Practical workflow for students

A sensible machine-learning workflow for a cyber task is:

1. define the decision problem clearly;
2. inspect the dataset;
3. clean and transform the data;
4. split data carefully;
5. establish a baseline;
6. train one or two classical models;
7. evaluate with suitable metrics;
8. interpret errors;
9. reflect on realism and limitations.

This is a better workflow than immediately searching for the most advanced model.

---

## 11. Lab guidance

### Suggested lab theme
**Comparing classical models on a cybersecurity dataset**

### Suggested tasks
1. load a dataset for phishing, malicious URLs, or intrusion detection;
2. examine class balance and feature types;
3. preprocess the data;
4. train at least two classical models;
5. compare precision, recall, F1-score, and confusion matrices;
6. identify at least one limitation of the dataset and at least one likely deployment risk.

### Suggested extension
Ask students to compare:
- raw accuracy;
- operational usefulness;
- interpretability.

This helps shift thinking from benchmark culture to realistic evaluation.

---

## 12. Discussion questions

1. When is a simpler model preferable to a more complex one in cybersecurity?
2. Why can anomaly detection become noisy in real environments?
3. Which is worse in a phishing filter: false positives or false negatives?
4. Why is data leakage so easy to introduce in cyber datasets?
5. How should model evaluation change if the environment evolves rapidly?

---

## 13. Key terms

- Preprocessing
- Feature Engineering
- Supervised Learning
- Unsupervised Learning
- Anomaly Detection
- Class Imbalance
- Precision
- Recall
- F1-score
- PR-AUC
- Data Leakage
- Overfitting
- Underfitting

---

## 14. Week summary

This week showed that much of applied AI for cybersecurity depends on disciplined data work and careful evaluation.

Students should now understand:

- why cyber data needs thoughtful preprocessing;
- how features shape what the model can learn;
- how classical machine learning can support real security tasks;
- why imbalance, leakage, and weak metrics can distort results;
- why operational interpretation matters as much as model performance.

The next week moves to deep learning and generative AI, where modern capabilities increase, but so do complexity, risk, and the need for critical judgement.
