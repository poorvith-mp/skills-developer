---
name: llm-evals
group: Data and AI
description: >-
  Build evaluation harnesses: regression sets, scoring rubrics, drift detection and benchmarks.
  Use when building LLM evaluation harnesses, scoring rubrics, or drift benchmarks.
---
# Llm Evals

Architects automated evaluation infrastructure for AI/LLM systems to ensure output quality, detect drift, and prevent regression.

## Phased Workflow

### Phase 1: Evaluation Dataset Design
1. Curate golden test datasets with human-annotated ground truth across representative task categories.
2. Define scoring dimensions: Accuracy, Relevance, Completeness, Tone Adherence, Safety, Latency.
3. Build adversarial test cases targeting known failure modes (hallucination, refusal, format violation).

### Phase 2: Scoring & Comparison Infrastructure
1. Implement automated scorers: exact match, semantic similarity (embedding cosine), LLM-as-judge, regex validators.
2. Build A/B comparison pipelines for prompt version testing (old prompt vs new prompt).
3. Set up drift detection: track score distributions over time windows and alert on statistical deviation.

### Phase 3: CI Integration & Reporting
1. Integrate eval suite into CI/CD pipeline as a required gate before prompt/model deployment.
2. Generate eval reports with pass/fail rates, score distributions, and regression flags.
3. Maintain versioned eval datasets alongside prompt versions for reproducibility.

## Verification & Quality Checklist
- [ ] Golden dataset covers minimum 50 representative test cases per task category.
- [ ] Scoring rubrics are deterministic and reproducible across runs.
- [ ] Drift detection thresholds calibrated against baseline performance windows.
- [ ] Eval pipeline runs in under 10 minutes for rapid feedback loops.

## Anti-Patterns & Constraints
- NEVER deploy prompt changes without running the eval suite first.
- NEVER use a single metric (e.g., only accuracy) to evaluate multi-dimensional LLM output.
- NEVER treat eval datasets as static; refresh quarterly with new edge cases.
