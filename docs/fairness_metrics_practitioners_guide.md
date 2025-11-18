# Fairness Metrics: A Practitioner's Guide

A comprehensive guide to understanding, interpreting, and selecting fairness metrics for AI systems, organized by stakeholder concerns and practical use cases.

---

## Understanding Metric Categories

Different stakeholders need different fairness guarantees. This guide organizes metrics into four practical categories that align with business objectives and regulatory requirements. While this guide uses binary examples (common in high-stakes decisions), most fairness metrics also generalize to multi-class and multi-label settings. Jurity supports both.

**Important:** All threshold recommendations in this guide are illustrative best practices for internal auditing. They are not regulatory standards and may need to be adapted depending on domain, data, and stakeholder requirements.

---

## 1. 🏛️ Legal Compliance Metrics

**Category Overview:** *Meeting regulatory requirements*

These metrics help organizations meet legal standards and avoid discrimination lawsuits. They focus on *selection-rate parity*, which regulators use to screen for potential discrimination, though legal analysis also considers job-relatedness and business necessity.

**When to use this category:**
- Regulatory compliance is mandatory (hiring, lending, housing)
- Legal risk is primary concern
- Initial fairness screening needed

---

### Disparate Impact (DI)

What it measures: Ratio of selection rates between protected and majority groups.

Why it matters: Regulators use the "80% rule" (EEOC Guidelines) as an initial screen for potential discrimination in employment, lending, and housing decisions—failing it triggers legal scrutiny even if differences might be justifiable.

Interpretation:
- Protected/Majority ratio ≥ 0.80 = passes regulatory threshold
- Ratio < 0.80 = regulatory red flag requiring business necessity defense
- Ratio < 0.70 = high risk, immediate intervention needed
**Note:** Thresholds below 0.80 are used in EEOC screening guidance, but finer gradations (e.g., 0.70) are not part of any legal standard—they are risk indicators for internal auditing.
---

### Statistical Parity (SP)

What it measures: Absolute difference in positive prediction rates between demographic groups.

Why it matters: Large differences in selection rates create legal exposure under civil rights law and may indicate systemic discrimination, even when algorithms don't explicitly use protected attributes.

Interpretation:
- Difference ≤ 0.05 (5 percentage points) = generally acceptable
- Difference 0.05-0.10 = notable disparity, monitor closely
- Difference > 0.10 = significant disparity, reputational risk

---

## 2. 🎯 Merit-Based Fairness Metrics

**Category Overview:** *Protecting qualified individuals*

These metrics ensure that qualified people get fair opportunities and innocent people aren't wrongly penalized. They focus on *fair outcomes* based on actual merit, which is critical for maintaining system credibility and optimizing talent selection.

**When to use this category:**
- Protecting qualified individuals is critical
- Performance optimization matters
- Clear qualification standards exist
- High-stakes decisions with dual concerns

---

### Equal Opportunity (EO)

What it measures: Difference in true-positive rates between groups (qualified individuals).

Why it matters: If one group's qualified candidates are selected less often, you miss talent and introduce risk of systemic bias that undermines meritocracy.

Interpretation:
- 0 = perfect parity
- Closer to 0 = fairer with respect to qualified candidates
- > 0.10 = significant talent loss from underrepresented group

---

### Average Odds (AO)

What it measures: Average of TPR and FPR differences across groups—quantifies distance from Equalized Odds fairness goal. AO = average(|ΔTPR|, |ΔFPR|)

Why it matters: Provides a single comprehensive metric to track progress toward balanced fairness for both qualified and unqualified individuals across all decision types.

Interpretation:
- 0 = perfect Equalized Odds achieved
- \< 0.05 = close to fairness goal
- 0.05-0.10 = moderate gap, improvement needed
- \> 0.10 = far from Equalized Odds, comprehensive review required

---

### Predictive Equality (PE)

What it measures: Difference in false-positive rates between groups (innocent individuals).

Why it matters: Protects unqualified individuals from false approvals or unfair advantages—critical for maintaining system credibility and avoiding harmful false positives.

Interpretation:
- 0 = equal protection from false positives
- Closer to 0 = fairer protection for innocent individuals
- > 0.05 = one group unfairly affected by false approvals

---

## 3. 🔧 Performance Gap Metrics

**Category Overview:** *Measuring specific types of errors*

These metrics identify exactly where your model makes unfair mistakes, enabling targeted fixes. They help diagnose and fix *specific bias problems* by revealing which error types disproportionately affect particular groups.

**When to use this category:**
- Need to diagnose specific bias problems
- Debugging model fairness issues
- Targeting specific error types for improvement
- False negatives, false omissions, or false positives are costly

---

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

Why it matters: Identifies if certain groups receive unfair advantages (if approvals are beneficial) or create disproportionate risk (if approvals carry cost) exposure, affecting both fairness and business performance.

Interpretation:
- 0 = equal false approval rates
- < 0.05 = acceptable consistency
- 0.05-0.10 = moderate inconsistency, review criteria
- > 0.10 = severe risk imbalance, tighten approval standards

**Note:** FPR Difference is a supplementary diagnostic metric that may need to be computed manually (not always part of core fairness library APIs).

---

## 4. 💰 Economic Fairness Metrics

**Category Overview:** *Ensuring fair distribution of benefits*

These metrics ensure economic benefits and opportunities are distributed fairly across demographic groups. They focus on *fair distribution* of economic outcomes at a societal level, which is increasingly important for stakeholder accountability and policy impact assessment.

**When to use this category:**
- Stakeholders ask about benefit distribution
- Policy impact assessment required
- Societal-level fairness is the concern
- Resource allocation decisions affect multiple groups

---

### Theil Index

What it measures: How unevenly benefits are distributed across demographic groups relative to their population share. Technically, the index is an individual-level inequality measure that can be decomposed to show how much inequality comes from between-group differences.

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

## 🎭 Stakeholder-Specific Guidance

### 👔 For Executives
- **Primary Focus:** Legal Compliance + Merit-Based
- **Key Question:** "Are we protected legally while being fair to talent?"
- **Metrics to Track:** Disparate Impact, Equal Opportunity
- **Why:** Minimize legal risk while optimizing talent acquisition and maintaining organizational reputation

### ⚖️ For Legal/HR Teams
- **Primary Focus:** Legal Compliance + Merit-Based
- **Key Question:** "Do we meet regulatory requirements while treating qualified people fairly?"
- **Metrics to Track:** Statistical Parity, Disparate Impact, Equal Opportunity
- **Why:** Ensure compliance with EEOC guidelines and civil rights law while maintaining defensible hiring practices

### 📈 For Business Leaders
- **Primary Focus:** Merit-Based + Performance Gap
- **Key Question:** "Are we losing talent or taking unnecessary risks?"
- **Metrics to Track:** Equal Opportunity, FNR Difference, FPR Difference
- **Why:** Optimize business outcomes by identifying talent loss and managing risk exposure

### 🛠️ For Product/Engineering Teams
- **Primary Focus:** Performance Gap + Economic Fairness
- **Key Question:** "What specific problems can we fix, and what's the impact?"
- **Metrics to Track:** FNR/FOR/FPR Differences, Theil Index
- **Why:** Diagnose and fix specific technical issues while understanding systemic impact

---

## 🚀 Quick Decision Framework

```
┌─ Are you making high-stakes decisions? ─┐
│  (hiring, lending, admissions)          │
│                                         │
│  YES ──► Merit-Based Metrics            │
│          (Equal Opportunity, Avg Odds)  │
└─────────────────────────────────────────┘

┌─ Do you need legal compliance? ─┐
│                                 │
│  YES ──► Legal Compliance       │
│          (Disparate Impact,     │
│           Statistical Parity)   │
└─────────────────────────────────┘

┌─ Want to fix specific problems? ─┐
│                                  │
│  YES ──► Performance Gap         │
│          (FNR/FOR/FPR Diffs)     │
└──────────────────────────────────┘

┌─ Concerned about resource distribution? ─┐
│                                          │
│  YES ──► Economic Fairness               │
│          (Theil Index, GEI)              │
└──────────────────────────────────────────┘
```

---

## 💡 Key Principles

### Selection-Rate Parity vs. Merit-Based Outcomes
- **Legal Compliance:** Focuses on selection-rate parity as an initial screen for discrimination (though legal frameworks allow differences justified by job-relatedness and business necessity)
- **Merit-Based:** Focuses on fair outcomes based on actual qualifications

### Prevention vs. Detection
- **Merit-Based:** Prevents unfair treatment
- **Performance Gap:** Detects where unfairness occurs

### Individual vs. Societal
- **Merit-Based + Performance Gap:** Individual fairness
- **Economic Fairness:** Societal-level fairness

---

## 🎯 Implementation Priority

1. **Start with Legal Compliance** - Avoid regulatory risk
   - Begin with Disparate Impact to ensure you pass the 80% rule
   - Add Statistical Parity for comprehensive selection-rate monitoring

2. **Add Merit-Based metrics** - Protect qualified individuals
   - Use Equal Opportunity for talent optimization
   - Add Average Odds for comprehensive fairness tracking

3. **Use Performance Gap metrics** - Fix specific problems
   - Diagnose with FNR, FOR, and FPR differences
   - Target improvements to specific error types

4. **Consider Economic Fairness** - For policy and societal impact
   - Use Theil Index for general inequality assessment
   - Use GEI when different stakeholders have different priorities

---

## Best Practices

1. **Monitor multiple metric types** - No single metric captures all fairness dimensions
2. **Start with legal compliance** - Ensure regulatory requirements are met first
3. **Use performance gaps for diagnosis** - Identify exactly what's wrong
4. **Track economic impact** - Understand long-term societal effects
5. **Balance fairness with accuracy** - Trade-offs are inevitable, make them explicit
6. **Document your choices** - Justify which metrics matter for your use case
7. **Context matters** - Interpret all metrics within your specific domain and stakeholder needs

---

## 📚 Additional Resources

- **Technical Implementation:** [Jurity Library Documentation](https://jurity.readthedocs.io/)
- **Legal Background:** EEOC Guidelines on Employment Testing
- **Academic Foundation:** "Equality of Opportunity in Supervised Learning" (Hardt et al., 2016)

---

**Note:** All metrics should be interpreted in context of your specific domain, stakeholder needs, and legal requirements. Consult with legal counsel and domain experts when making high-stakes fairness decisions.

---

*This practitioner's guide synthesizes metric categories and detailed descriptions to help organizations choose and interpret the right fairness metrics based on their specific business context, stakeholder needs, and regulatory requirements.*
