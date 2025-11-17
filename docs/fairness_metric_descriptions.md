# Fairness Metrics Descriptions

A practitioner's guide to understanding and interpreting fairness metrics for AI systems.

---

## Legal Compliance Metrics

### Disparate Impact (DI)

What it measures: Ratio of selection rates between protected and majority groups.

Why it matters: Regulators use the "80% rule" (EEOC Guidelines) as an initial screen for potential discrimination in employment, lending, and housing decisions—failing it triggers legal scrutiny even if differences might be justifiable.

Interpretation:
- Protected/Majority ratio ≥ 0.80 = passes regulatory threshold
- Ratio < 0.80 = regulatory red flag requiring business necessity defense
- Ratio < 0.70 = high legal risk, immediate intervention needed

---

### Statistical Parity (SP)

What it measures: Absolute difference in positive prediction rates between demographic groups.

Why it matters: Large differences in selection rates create legal exposure under civil rights law and may indicate systemic discrimination, even when algorithms don't explicitly use protected attributes.

Interpretation:
- Difference ≤ 0.05 (5 percentage points) = generally acceptable
- Difference 0.05-0.10 = notable disparity, monitor closely
- Difference > 0.10 = significant disparity, legal and reputational risk

---

## Merit-Based Fairness Metrics

### Equal Opportunity (EO)

What it measures: Difference in true-positive rates between groups (qualified individuals).

Why it matters: If one group's qualified candidates are selected less often, you miss talent and introduce risk of systemic bias that undermines meritocracy.

Interpretation:
- 0 = perfect parity
- Closer to 0 = fairer with respect to qualified candidates
- > 0.10 = significant talent loss from underrepresented group

---

### Average Odds (AO)

What it measures: Average of TPR and FPR differences across groups—quantifies distance from Equalized Odds fairness goal.

Why it matters: Provides a single comprehensive metric to track progress toward balanced fairness for both qualified and unqualified individuals across all decision types.

Interpretation:
- 0 = perfect Equalized Odds achieved
- < 0.05 = close to fairness goal
- 0.05-0.10 = moderate gap, improvement needed
- > 0.10 = far from Equalized Odds, comprehensive review required

---

### Predictive Equality (PE)

What it measures: Difference in false-positive rates between groups (innocent individuals).

Why it matters: Protects unqualified individuals from false accusations or unfair advantages—critical for maintaining system credibility and avoiding harmful false positives.

Interpretation:
- 0 = equal protection from false positives
- Closer to 0 = fairer protection for innocent individuals
- > 0.05 = one group unfairly affected by false approvals

---

## Performance Gap Metrics

### FNR Difference (False Negative Rate)

What it measures: Difference in rates of missing qualified candidates between demographic groups.

Why it matters: Reveals if your model systematically overlooks qualified talent from specific groups, leading to diversity loss and potential discrimination claims.

Interpretation:
- 0 = equal miss rates across groups
- < 0.05 = acceptable variation
- 0.05-0.10 = moderate talent loss, adjust thresholds
- > 0.10 = severe talent loss, immediate model fix required

---

### FOR Difference (False Omission Rate)

What it measures: Difference in reliability of negative predictions across groups.

Why it matters: High FOR differences mean your model's rejections are less trustworthy for one group, causing unfair denial of opportunities and undermining decision credibility.

Interpretation:
- 0 = equally reliable rejections
- < 0.05 = acceptable calibration
- 0.05-0.10 = moderate reliability gap
- > 0.10 = severe miscalibration, recalibrate model

---

### FPR Difference (False Positive Rate)

What it measures: Difference in rates of wrongly approving unqualified individuals between groups.

Why it matters: Identifies if certain groups receive unfair advantages or create disproportionate risk exposure, affecting both fairness and business performance.

Interpretation:
- 0 = equal false approval rates
- < 0.05 = acceptable consistency
- 0.05-0.10 = moderate inconsistency, review criteria
- > 0.10 = severe risk imbalance, tighten approval standards

---

## Economic Fairness Metrics

### Theil Index

What it measures: How unevenly benefits are distributed across demographic groups relative to their population share.

Why it matters: Quantifies systemic inequality in opportunity allocation—regulators and stakeholders increasingly care about whether AI systems concentrate advantages or distribute them fairly across society.

Interpretation:
- 0 = perfect equality (benefits proportional to population)
- 0.00-0.10 = low inequality, relatively fair distribution
- 0.10-0.25 = moderate inequality, some groups advantaged
- 0.25-0.50 = high inequality, significant distributional issues
- > 0.50 = severe inequality, major systemic bias

---

### Generalized Entropy Index (GEI)

What it measures: Comprehensive inequality measurement with adjustable sensitivity (α parameter) to different parts of the benefit distribution.

Why it matters: Different stakeholders care about different inequality types—social programs focus on helping worst-off (α=0), while wealth policies limit extreme advantages (α=2); GEI provides tailored perspectives for each concern.

Interpretation:
- α = 0: Most sensitive to disadvantaged groups
  - Use when: Protecting worst-off is priority
- α = 1: Balanced sensitivity (equals Theil Index)
  - Use when: General-purpose inequality measure needed
- α = 2: Most sensitive to advantaged groups
  - Use when: Limiting extreme advantages is priority

Score interpretation (all α values):
- 0 = perfect equality
- < 0.15 = acceptable distributional fairness
- 0.15-0.30 = moderate distributional concerns
- > 0.30 = significant distributional inequality

---

## Metric Selection Guide

**Use Legal Compliance Metrics when:**
- Regulatory compliance is mandatory (hiring, lending, housing)
- Legal risk is primary concern
- Initial fairness screening needed

**Use Merit-Based Metrics when:**
- Protecting qualified individuals is critical
- Performance optimization matters
- Clear qualification standards exist

**Use Performance Gap Metrics when:**
- Need to diagnose specific bias problems
- Debugging model fairness issues
- Targeting specific error types for improvement

**Use Economic Fairness Metrics when:**
- Stakeholders ask about benefit distribution
- Policy impact assessment required
- Societal-level fairness is the concern

---

## Best Practices

1. **Monitor multiple metric types** - No single metric captures all fairness dimensions
2. **Start with legal compliance** - Ensure regulatory requirements are met first
3. **Use performance gaps for diagnosis** - Identify exactly what's wrong
4. **Track economic impact** - Understand long-term societal effects
5. **Balance fairness with accuracy** - Trade-offs are inevitable, make them explicit
6. **Document your choices** - Justify which metrics matter for your use case

---

**Note:** All metrics should be interpreted in context of your specific domain, stakeholder needs, and legal requirements. Consult with legal counsel and domain experts when making high-stakes fairness decisions.
