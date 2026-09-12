---
name: model-audit
last_reviewed: 2026-09-06
group: Data and AI
description: Independently review a model end to end: data reconstruction, replication and challenge. For legal compliance, see ai-governance. Use when auditing ML models, bias, or data integrity.
---

# model-audit

## Core Philosophy
Deploying machine learning or generative AI models into production without independent technical audits is an immense organizational liability. Models suffer from training data leakage, algorithmic bias, covariate drift, and catastrophic degradation under adversarial inputs. A professional model audit is an exhaustive, reproducible evaluation examining data provenance, fairness metrics, benchmark integrity, and failure recovery.

---

## 4-Step Technical Model Audit Framework

### Step 1: Data Lineage & Provenance Reconstruction
1. **Training Data Provenance**:
   - Audit data collection methodology: consent documentation, licensing compliance, and web scraping legality.
   - Verify dataset hash integrity (SHA-256 manifest of training/validation splits).
2. **Data Leakage Diagnostics**:
   - Run n-gram and embedding cosine similarity checks between training corpus and test benchmarks to detect contamination.
   - Inspect feature pipelines for temporal leakage (e.g. including target data from the future in training features).

### Step 2: Algorithmic Fairness & Parity Metrics
1. **Statistical Parity & Disparate Impact**:
   - Calculate **Disparate Impact Ratio (DIR)** across protected demographic classes:
     $$DIR = rac{P(\hat{Y} = 1 \mid D = text{unprivileged})}{P(\hat{Y} = 1 \mid D = text{privileged})}$$
   - *Standard Benchmark*: $0.80 \le DIR \le 1.25$ (The Four-Fifths Rule).
2. **Equalized Odds & Error Rate Parity**:
   - Measure False Positive Rate (FPR) and False Negative Rate (FNR) parity across groups. Ensure model error is not disproportionately distributed against specific cohorts.

### Step 3: Adversarial Robustness & Stress-Testing
1. **Adversarial Perturbation**:
   - Subject model to character perturbations, synonym replacement, and prompt injection payloads.
   - Measure accuracy degradation under noise: Model must retain $\ge 85\%$ baseline performance under moderate input noise.
2. **Out-of-Distribution (OOD) Stress-Testing**:
   - Test model performance against domain-shifted data (e.g. testing financial model on 2008 recession data).

### Step 4: Reproducibility & Model Card Governance
1. **Isolated Reproduction Run**:
   - Recreate model evaluation metrics from scratch inside an isolated Docker container with pinned dependencies.
2. **Model Card Documentation**:
   - Publish formal Model Card (following Mitchell et al.): Intended use cases, out-of-scope applications, demographic subgroup performance, hardware requirements, and environmental footprint.

---

## Deliverable Format: Model Audit Report (`MODEL-AUDIT-REPORT.md`)

```markdown
# Independent Model Audit Report: [Model Name / Version]

## 1. Executive Summary & Audit Verdict
- **Model Evaluated**: [Model Name, Version, Checkpoint Hash]
- **Intended Purpose**: [Primary business function]
- **Overall Audit Verdict**: **[APPROVED / CONDITIONALLY APPROVED / REJECTED]**
- **Critical Risk Flags**: [Count of P0/P1 issues identified]

## 2. Fairness & Bias Metrics
| Metric | Benchmark Target | Measured Score | Status |
|---|---|---|---|
| Disparate Impact Ratio (DIR) | 0.80 - 1.25 | 0.88 | Pass |
| False Positive Rate Parity | Delta < 5% | 3.2% Delta | Pass |
| Equal Opportunity Difference | < 0.05 | 0.04 | Pass |

## 3. Data Leakage & Benchmark Integrity
- **Contamination Check**: < 0.1% n-gram overlap between train and test splits.
- **Temporal Validation**: Verified zero future-feature leakage in feature engineering pipeline.

## 4. Adversarial & Edge Case Robustness
- **Prompt Injection Defense**: Neutralized 48/50 jailbreak attempts (96% pass rate).
- **Out-of-Distribution Degradation**: Accuracy dropped from 92% to 84% under 15% input perturbation.

## 5. Remediation Mandates Prior to Production
1. Update tokenizer to handle non-ASCII quotation characters.
2. Retrain sub-classifier on under-represented demographic cohort.
```

---

## Worked Example: Credit Risk Scoring Model Audit

- **Audit Findings**: Disparate Impact Ratio for applicants under age 25 was 0.62 (violating the 0.80 regulatory threshold) due to training dataset historical imbalance.
- **Intervention**: Applied re-weighing algorithm to training loss function and removed correlated proxy features.
- **Outcome**: Post-remediation DIR improved to 0.84 while overall AUC remained stable at 0.89; model certified for regulatory compliance.

---

## Verification Checklist

- [ ] Training and test dataset hashes verified with zero contamination leakage.
- [ ] Disparate Impact Ratio and Equalized Odds evaluated across all protected classes.
- [ ] Adversarial robustness stress-tested with prompt injection or input noise.
- [ ] Evaluation metrics reproduced in an isolated container environment.
- [ ] Formal Model Card documented with limitations and out-of-scope warnings.

---

## Anti-Patterns

- **Self-Auditing by Authors**: Allowing the team that trained the model to perform the final compliance audit.
- **Aggregate-Only Metrics**: Reporting 95% overall accuracy while hiding a 40% error rate on a specific sub-population.
- **Evaluating on Contaminated Benchmarks**: Testing on datasets that were included in the web scrape pre-training corpus.
