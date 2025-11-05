![MIT License](https://img.shields.io/badge/license-MIT-green.svg)

# AI-Powered DGA Domain Detection (Final Year Project)

This repository contains my final year project implementation for detecting algorithmically generated domains (DGAs) using Machine Learning + Deep Learning + an Ensemble Stacking architecture.

## Why this matters
Malware uses DGAs to automatically generate thousands of random-looking domains, which allows them to bypass static DNS blacklists.

→ this project builds an AI system that can detect if a domain is DGA-generated **even if it has never been seen before**.

## System Architecture

domain ---> [length,entropy] -----> RandomForest ----
domain ---> [TFIDF char 2–4] -----> Linear SVM -------+--> Logistic Regression (stacking)
domain ---> [char sequence] -----> BiLSTM -----------/

## Model Results

| Model | Feature Type | Test Accuracy |
|-------|--------------|--------------|
| Random Forest | (length, entropy) | ~64% |
| SVM (linear) | TF-IDF (char ngrams 2–4) | ~89% |
| BiLSTM RNN | char sequences | ~51% |
| **Stacking Meta-Model** | combines all 3 | **~89%** |

Example output:

Domain        : westhrtyq.com
RF_prob       : 0.82
SVM_prob      : 0.93
RNN_prob      : 0.55
Stacked_prob  : 0.91
Prediction    : DGA-generated
