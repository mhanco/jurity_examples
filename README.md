# Fairness Metrics for Machine Learning: A Practical Guide

> **Educational notebooks demonstrating when and how to use different fairness metrics in AI systems**

This repository contains interactive Jupyter notebooks that teach practitioners how to measure, understand, and improve fairness in machine learning systems. Each notebook focuses on a specific category of fairness metrics, providing both theoretical context and practical implementation using the [Jurity](https://github.com/fidelity/jurity) fairness library.

## Overview

When deploying AI systems in business contexts, different stakeholders need different fairness guarantees. This collection of notebooks demonstrates **9 core fairness metrics from Jurity** plus **1 supplementary diagnostic metric** (FPR Difference, computed manually), organized into practical categories aligned with business objectives and regulatory requirements.

### What You'll Learn

- **When** to use each type of fairness metric
- **Why** different metrics matter for different stakeholders
- **How** to implement fairness measurements using Jurity
- **What** to do when fairness metrics indicate problems

## Quick Start

### Prerequisites

```bash
# Python 3.8 or higher
python --version

# Install required packages
pip install jurity pandas numpy matplotlib seaborn scikit-learn jupyter
```

### Running the Notebooks

```bash
# Navigate to the notebook directory
cd notebooks

# Start Jupyter
jupyter notebook

# Open any notebook (recommended order: 1 → 2 → 3 → 4)
```

## Notebook Structure

### 1. Legal Compliance Metrics 🏛️
**File:** `1_legal_compliance_metrics.ipynb`

**Focus:** Meeting regulatory requirements and avoiding discrimination lawsuits

**Metrics Covered:**
- **Disparate Impact** - 80% Rule compliance for employment law
- **Statistical Parity** - Selection-rate parity across demographic groups

**When to Use:**
- Hiring, lending, or any EEOC-regulated decisions
- When legal compliance is mandatory
- Public sector or government contracting

**Key Insight:** These metrics focus on *selection-rate parity*, which is often how regulators screen for potential discrimination, even though legal analysis also considers job-relatedness and business necessity

---

### 2. Merit-Based Fairness Metrics 🎯
**File:** `2_merit_based_fairness_metrics.ipynb`

**Focus:** Protecting qualified individuals and ensuring fair outcomes

**Metrics Covered:**
- **Equal Opportunity** - Qualified candidates get equal chances
- **Average Odds** - Metric summarizing TPR/FPR differences across groups (used to assess how close you are to Equalized Odds)
- **Predictive Equality** - Innocent individuals protected from false accusations

**When to Use:**
- High-stakes decisions (hiring, admissions, promotions)
- When qualifications matter and merit should be rewarded
- Balancing accuracy with fairness

**Key Insight:** These metrics focus on *fair outcomes* based on actual merit

---

### 3. Performance Gap Metrics 🔧
**File:** `3_performance_gap_metrics.ipynb`

**Focus:** Diagnosing specific types of bias in your model

**Metrics Covered:**
- **FNR Difference** - Missing qualified candidates (talent loss)
- **FOR Difference** - Wrongly rejecting people (false rejections / missed opportunities)
- **FPR Difference** - Wrongly approving people (risk exposure) *[Supplementary diagnostic metric computed manually in notebooks]*

**When to Use:**
- Debugging bias issues in existing models
- Understanding exactly where your model is unfair
- Targeted bias mitigation

**Key Insight:** These metrics help *diagnose and fix specific bias problems*

---

### 4. Economic Fairness Metrics 💰
**File:** `4_economic_fairness_metrics.ipynb`

**Focus:** Ensuring fair distribution of economic benefits

**Metrics Covered:**
- **Theil Index** - Measures how unevenly outcomes are distributed (high = concentrated in one group, low = even distribution)
- **Generalized Entropy Index** - Similar inequality measure with adjustable sensitivity to different parts of the distribution

**When to Use:**
- Resource allocation decisions
- Policy impact assessment
- Societal-level fairness audits

**Key Insight:** These metrics focus on *fair distribution* of economic outcomes at the societal level

---

## Decision Framework

Not sure which metrics to use? Start here:

```
┌─ Are you making regulated decisions? ────┐
│  (hiring, lending, housing)               │
│  YES ──► Legal Compliance Metrics (1)     │
└───────────────────────────────────────────┘

┌─ Are qualifications important? ──────────┐
│  (merit-based selection)                  │
│  YES ──► Merit-Based Metrics (2)          │
└───────────────────────────────────────────┘

┌─ Need to fix existing bias? ─────────────┐
│  (debugging model problems)               │
│  YES ──► Performance Gap Metrics (3)      │
└───────────────────────────────────────────┘

┌─ Concerned about societal impact? ───────┐
│  (policy evaluation, distribution)        │
│  YES ──► Economic Fairness Metrics (4)    │
└───────────────────────────────────────────┘
```

See `docs/fairness_metric_categories.md` for detailed stakeholder-specific guidance.

## Recommended Learning Path

### Beginners
1. Read `fairness_metric_categories.md` for context
2. Start with **Legal Compliance Metrics** (Notebook 1)
3. Move to **Merit-Based Metrics** (Notebook 2)
4. Explore other categories as needed

### Practitioners
1. Identify your use case using the decision framework
2. Jump to the relevant notebook
3. Reference `fairness_metric_categories.md` for cross-category comparisons

### Researchers
1. Review all notebooks to understand the full landscape
2. Compare metrics across categories
3. Examine the implementation details in each notebook

## Dataset

All notebooks use the **Adult Income dataset** from the UCI Machine Learning Repository:
- **Source:** [UCI Adult Dataset](https://archive.ics.uci.edu/ml/datasets/adult)
- **Context:** Employment income prediction (>$50K vs ≤$50K)
- **Protected Attribute:** Gender (Male vs Female)
- **Size:** ~48,000 samples

This dataset is ideal for demonstrating fairness metrics because:
- It represents a real-world regulated use case (employment)
- It contains clear protected attributes
- It exhibits realistic bias patterns
- It's widely recognized in fairness research

## Key Concepts

### Selection-Rate Parity vs Merit-Based Outcomes
- **Legal Compliance:** Focuses on selection-rate parity as an initial screen for discrimination (though legal analysis also considers job-relatedness and business necessity)
- **Merit-Based:** Focuses on fair outcomes based on actual qualifications

### Individual vs Societal Fairness
- **Merit-Based + Performance Gap:** Individual-level fairness
- **Economic Fairness:** Societal-level fairness

### Prevention vs Detection
- **Merit-Based:** Prevents unfair treatment
- **Performance Gap:** Detects where unfairness occurs

## Implementation Best Practices

### 1. Monitor Multiple Metrics
Don't rely on a single fairness metric. Use a combination:
- Legal compliance metrics for regulatory protection
- Merit-based metrics for business optimization
- Performance gap metrics for debugging
- Economic metrics for societal impact

### 2. Establish Baselines
Before deploying interventions:
- Measure current fairness levels
- Document baseline metrics
- Set improvement targets

### 3. Regular Auditing
- Monthly monitoring for high-stakes systems
- Quarterly comprehensive audits
- Annual strategic fairness reviews

### 4. Stakeholder Communication
Different stakeholders need different information:
- **Executives:** Risk levels, business impact
- **Legal Teams:** Compliance status, regulatory exposure
- **Technical Teams:** Specific metrics, implementation details
- **Policy Teams:** Societal impact, distributional effects

## Technical Details

### Library: Jurity
These notebooks use [Jurity](https://github.com/fidelity/jurity), an open-source fairness metrics library developed by Fidelity Investments.

**9 Core Jurity Metrics Demonstrated:**
1. **Disparate Impact** - Legal compliance (80% Rule)
2. **Statistical Parity** - Equal treatment across groups
3. **Equal Opportunity** - Fair chances for qualified individuals
4. **Average Odds** - Comprehensive merit-based fairness metric
5. **Predictive Equality** - Protection for innocent individuals
6. **FNR Difference** - False negative rate gaps
7. **FOR Difference** - False omission rate gaps
8. **Theil Index** - Measures how unevenly outcomes are distributed
9. **Generalized Entropy Index** - Inequality measure with adjustable sensitivity

**Supplementary Diagnostic Metric:**
- **FPR Difference** - False positive rate gaps (computed manually in notebooks as an additional diagnostic tool)

**What Jurity Provides (and Doesn't)**

Jurity does:
- Compute vetted fairness metrics
- Provide consistent APIs
- Support binary classification fairness audits
- Offer strong test coverage

Jurity does not:
- Debias the model
- Optimize thresholds

**Your Workflow:**
1. Train model
2. Evaluate fairness with Jurity
3. Explore remediations (thresholding, reweighting, feature adjustments, etc.)

**Key Features:**
- Comprehensive fairness metric collection
- Simple, consistent API
- Tested for applied work
- Active maintenance and support

### Model: Random Forest Classifier
The notebooks use scikit-learn's Random Forest for demonstrations:
- Easy to understand
- Good baseline performance
- Realistic bias patterns
- Industry-standard algorithm

## Additional Resources

### Documentation & References
- **Jurity Documentation:** [https://jurity.readthedocs.io/](https://jurity.readthedocs.io/)
- **EEOC Guidelines:** [Uniform Guidelines on Employee Selection](https://www.eeoc.gov/laws/guidance/uniform-guidelines-employee-selection-procedures)
- **Academic Foundation:** "Equality of Opportunity in Supervised Learning" (Hardt et al., 2016)

### Complementary Tools
- **Aequitas:** Bias audit toolkit
- **Fairlearn:** Microsoft's fairness library
- **AI Fairness 360:** IBM's fairness toolkit

### Legal & Policy Resources
- NIST AI Risk Management Framework
- Partnership on AI Guidelines
- IEEE Standards for Algorithmic Accountability

## Project Structure

```
README.md                              # This file
docs/
└── fairness_metric_categories.md          # Stakeholder decision guide
notebooks/
├── 1_legal_compliance_metrics.ipynb       # Legal/regulatory fairness
├── 2_merit_based_fairness_metrics.ipynb   # Merit and qualification fairness
├── 3_performance_gap_metrics.ipynb        # Diagnostic bias detection
└── 4_economic_fairness_metrics.ipynb      # Societal distribution fairness
```

## Contributing

Contributions are welcome! Areas for improvement:
- Additional fairness metrics
- More diverse datasets
- Industry-specific examples
- Bias mitigation techniques
- Additional visualizations

## License

This project is part of the `jurity_examples` repository and is intended for educational purposes.

## Citation

If you use these notebooks in your research or work, please cite:

```bibtex
@misc{jurity-fairness-notebooks,
  title={Fairness Metrics for Machine Learning: A Practical Guide},
  author={Jurity Examples Contributors},
  year={2024},
  howpublished={\url{https://github.com/fidelity/jurity}}
}
```

## Support & Feedback

- **Issues:** Report issues or request features via GitHub Issues
- **Questions:** Consult the Jurity documentation or open a discussion
- **Community:** Join the fairness in ML community discussions

---

## Quick Reference: All Metrics at a Glance

**Note:** Thresholds below are illustrative starting points, not hard regulatory standards.

| Category | Metric | Focus | Threshold |
|----------|--------|-------|-----------|
| **Legal Compliance** | Disparate Impact | 80% Rule | ≥0.80 ratio |
| | Statistical Parity | Equal rates | ±5% difference |
| **Merit-Based** | Equal Opportunity | Qualified people | <5% TPR difference |
| | Average Odds | Both qualified & innocent | <5% avg difference |
| | Predictive Equality | Innocent people | <5% FPR difference |
| **Performance Gap** | FNR Difference | Missing talent | <5% difference |
| | FOR Difference | False rejections | <5% difference |
| | FPR Difference | False approvals | <5% difference |
| **Economic** | Theil Index | Uneven distribution of benefits | <0.10 |
| | Gen. Entropy Index | Comprehensive inequality | <0.15 |

---

**Start your fairness journey:** Open `fairness_metric_categories.md` to understand the framework, then dive into the notebooks!
