# Fairness Metrics for Stakeholders: A Practical Guide

*Understanding when and why to use different fairness metrics in machine learning systems*

## Overview

When deploying AI systems in business contexts, different stakeholders need different fairness guarantees. This guide demonstrates **9 core fairness metrics from Jurity** plus **1 supplementary diagnostic metric** (FPR Difference, computed manually), organized into practical groups that align with business objectives and regulatory requirements.

---

## 📊 Metric Categories

### 1. 🏛️ Legal Compliance Metrics
*"Meeting regulatory requirements"*

These metrics help organizations meet legal standards and avoid discrimination lawsuits.

| Metric | What It Measures | When To Use |
|--------|------------------|-------------|
| **Disparate Impact** | 80% Rule compliance for employment law | Hiring, lending, any EEOC-regulated decisions |
| **Statistical Parity** | Selection-rate parity across groups | Initial screening for potential discrimination |

**Key Insight:** These focus on *selection-rate parity*, which regulators use to screen for potential discrimination, though legal analysis also considers job-relatedness and business necessity

---

### 2. 🎯 Merit-Based Fairness Metrics
*"Protecting qualified individuals"*

These ensure that qualified people get fair opportunities and innocent people aren't wrongly penalized.

| Metric | What It Measures | When To Use |
|--------|------------------|-------------|
| **Equal Opportunity** | Qualified candidates get equal chances | Hiring, admissions, promotions |
| **Average Odds** | Metric summarizing TPR/FPR differences across groups (assesses proximity to Equalized Odds) | High-stakes decisions with dual concerns |
| **Predictive Equality** | Innocent individuals protected from false accusations | Criminal justice, fraud detection |

**Key Insight:** These focus on *fair outcomes* based on actual merit

---

### 3. 🔧 Performance Gap Metrics
*"Measuring specific types of errors"*

These identify exactly where your model makes unfair mistakes, enabling targeted fixes.

| Metric | What It Measures | When To Use |
|--------|------------------|-------------|
| **FNR Difference** | Missing qualified candidates (talent loss) | When false negatives are costly |
| **FOR Difference** | Wrongly rejecting people (false accusations) | When rejection has serious consequences |
| **FPR Difference*** | Wrongly approving people (risk exposure) | When false positives create risk |

*\*FPR Difference is a supplementary diagnostic metric computed manually in the notebooks (not part of Jurity's core API).*

**Key Insight:** These help diagnose and fix *specific bias problems*

---

### 4. 💰 Economic Fairness Metrics
*"Ensuring fair distribution of benefits"*

These ensure economic benefits and opportunities are distributed fairly across demographic groups.

| Metric | What It Measures | When To Use |
|--------|------------------|-------------|
| **Theil Index** | How unevenly outcomes are distributed across groups | Resource allocation, economic impact assessment |
| **Generalized Entropy Index** | Inequality measure with adjustable sensitivity | Policy analysis, societal impact studies |

**Key Insight:** These focus on *fair distribution* of economic outcomes

---

## 🎭 Stakeholder-Specific Guidance

### 👔 **For Executives**
- **Primary Focus:** Legal Compliance + Merit-Based
- **Key Question:** "Are we protected legally while being fair to talent?"
- **Metrics to Track:** Disparate Impact, Equal Opportunity

### ⚖️ **For Legal/HR Teams**
- **Primary Focus:** Legal Compliance + Merit-Based
- **Key Question:** "Do we meet regulatory requirements while treating qualified people fairly?"
- **Metrics to Track:** Statistical Parity, Disparate Impact, Equal Opportunity

### 📈 **For Business Leaders**
- **Primary Focus:** Merit-Based + Performance Gap
- **Key Question:** "Are we losing talent or taking unnecessary risks?"
- **Metrics to Track:** Equal Opportunity, FNR Difference, FPR Difference

### 🛠️ **For Product/Engineering Teams**
- **Primary Focus:** Performance Gap + Economic Fairness
- **Key Question:** "What specific problems can we fix, and what's the impact?"
- **Metrics to Track:** FNR/FOR/FPR Differences, Theil Index

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

### **Selection-Rate Parity vs. Merit-Based Outcomes**
- **Legal Compliance:** Focuses on selection-rate parity as an initial screen for discrimination (though legal frameworks allow differences justified by job-relatedness and business necessity)
- **Merit-Based:** Focuses on fair outcomes based on actual qualifications

### **Prevention vs. Detection**
- **Merit-Based:** Prevents unfair treatment
- **Performance Gap:** Detects where unfairness occurs

### **Individual vs. Societal**
- **Merit-Based + Performance Gap:** Individual fairness
- **Economic Fairness:** Societal-level fairness

---

## 🎯 Implementation Priority

1. **Start with Legal Compliance** - Avoid regulatory risk
2. **Add Merit-Based metrics** - Protect qualified individuals
3. **Use Performance Gap metrics** - Fix specific problems
4. **Consider Economic Fairness** - For policy and societal impact

---

## 📚 Additional Resources

- **Technical Implementation:** [Jurity Library Documentation](https://jurity.readthedocs.io/)
- **Legal Background:** EEOC Guidelines on Employment Testing
- **Academic Foundation:** "Equality of Opportunity in Supervised Learning" (Hardt et al., 2016)

---

*This framework helps organizations choose the right fairness metrics based on their specific business context, stakeholder needs, and regulatory requirements.*