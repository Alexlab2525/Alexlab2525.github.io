---
title: "Cleaner Hospitals vs. Better Rehab: What Actually Gets Patients Home?"
date: 2025-01-01
layout: post
---

# Cleaner Hospitals vs. Better Rehab: What Actually Gets Patients Home?

### A data-driven look at what separates top-performing long-term care hospitals from the rest

---

![A physiotherapist helping a patient take their first steps after serious illness](https://media.post.rvohealth.io/wp-content/uploads/2023/08/senior-male-physical-therapy-walking-1296-728-header.jpg)
*Photo: Healthline*

---

When a seriously ill patient enters a long-term care hospital (LTCH),
the goal is simple: get them well enough to go home. But across hundreds
of U.S. hospitals treating the same types of patients, outcomes vary
dramatically. Some hospitals consistently send patients home. Others do not.

**What makes the difference?**

Is it cleaner wards with fewer infections? Lower costs? Better
physiotherapy?

Using data from **290 U.S. long-term care hospitals**, this analysis set
out to find the answer — and the results are surprising.

---

## The Four Questions

> **Q1** — What clinical factors separate high-performing hospitals from
> low-performing ones?
>
> **Q2** — Can a hospital's discharge performance be predicted from its
> quality metrics alone?
>
> **Q3** — Which factors matter most for that prediction?
>
> **Q4** — If a struggling hospital invests in improvement, what actually
> changes its outcome?

---

## Q1: The Surprising Gap Between Infections and Outcomes

The 290 hospitals in this dataset are rated by the Centers for Medicare &
Medicaid Services (CMS) into three performance groups based on how many of
their patients are successfully discharged home:

| Performance Group | Hospitals | Share |
|---|---|---|
| 🟢 Better than National Rate | 28 | 9.7% |
| 🔵 Average | 222 | 76.6% |
| 🔴 Worse than National Rate | 40 | 13.8% |

When comparing the clinical profiles of these three groups, a clear and
**surprising** pattern emerges:

| Metric | 🟢 Better | 🔵 Average | 🔴 Worse |
|---|---|---|---|
| Cost Efficiency (MSPB Score) | 0.93 | 0.99 | 1.04 |
| **Mobility Improvement Score** | **8.78** | **6.93** | **5.70** |
| Readmission Rate | 21.3% | 22.5% | 23.3% |
| Infection Rate (CAUTI SIR) | 0.54 | 0.70 | 0.82 |

> 💡 **Key finding:** The hospitals that send the most patients home are
> not necessarily the ones with the lowest infection rates — they are the
> ones that **get patients moving again.**

![Box plots comparing mobility improvement scores across the three hospital
performance groups](assets/images/fig_boxplots_features.png)
*Top-performing hospitals show nearly 54% higher mobility improvement
scores than low-performing ones.*

---

## Q2: Can Performance Be Predicted?

**Yes — with meaningful accuracy.**

A predictive model trained exclusively on quality metrics (infection rates,
readmission rates, cost efficiency, and mobility scores) was able to
classify hospital performance significantly better than chance.

Before drawing conclusions, it was important to remove **volume metrics**
from the model — features such as the number of catheter days or treatment
episodes that simply reflect how large a hospital is, not how well it
performs clinically. When only the seven genuine quality and rate metrics
were retained, the Logistic Regression model remained robust, while the
Random Forest model collapsed to near-random guessing. This tells us the
Random Forest had been relying on hospital size as a shortcut — not on
genuine clinical signals.

![Model accuracy comparison showing both models outperform the random
baseline of 33.3%](assets/images/fig_model_comparison.png)
*Both models outperform the random baseline. The Logistic Regression model
remains stable even after removing size-related features.*

> This tells us something important: the metrics we most commonly see
> reported in hospital rankings — infections and readmissions — are
> **not the strongest predictors** of whether patients actually go home.

---

## Q3: Which Factors Matter Most?

After ensuring the model uses only genuine quality metrics (not hospital
size proxies), the features were ranked by their predictive power:

| Rank | Factor | Predictive Importance |
|---|---|---|
| 🥇 1st | Cost Efficiency (MSPB Score) | Highest |
| 🥈 2nd | Mobility Improvement Score | High |
| 🥉 3rd | Readmission Rate | Moderate |
| 4th | Infection Rates (CAUTI, MRSA, CLABSI) | **Low** |

Infection control ranks at the bottom — despite being one of the **most
visible and widely reported** hospital quality metrics.

![Feature importances from the quality-only model showing MSPB score and
mobility at the top, infection rates at the
bottom](assets/images/fig_quality_model_comparison.png)
*Left panel: After removing size-related features, cost efficiency and
mobility improvement emerge as the decisive quality signals. Infection
rates rank last.*

> 💡 Reducing infections matters for patient safety. But infection metrics
> alone are a poor proxy for the outcome that matters most: **getting
> patients home.**

---

## Q4: What Actually Changes a Hospital's Outcome?

To answer this directly, a struggling hospital — currently rated *Worse
than the National Rate* — was simulated, and two improvement strategies
were tested step by step.

---

### Strategy 1: Invest in Rehabilitation 🏃

| Mobility Score | Outcome Prediction |
|---|---|
| 4.0 (starting point) | 🔴 Worse |
| **4.5** | **🔵 Average ← First flip** |
| **7.5** | **🟢 Better ← Second flip** |
| 10.0 | 🟢 Better (57% confidence) |

A **minimal improvement of just 0.5 points** in the mobility score was
enough to shift the prediction from *Worse* to *Average*. Reaching the
*Better* tier required a score of 7.5 — still below the Better-class
average of 8.78.

---

### Strategy 2: Invest in Infection Control 🧹

| Infection Rate (CAUTI SIR) | Outcome Prediction |
|---|---|
| 2.0 (starting point) | 🔴 Worse |
| 1.5 | 🔴 Worse |
| 1.0 (national average) | 🔴 Worse |
| 0.4 (best in class) | 🔴 Worse |

**No improvement was observed — at any level.** Reducing infection rates
from worst to best in class produced zero prediction flips. The hospital
remained *Worse* throughout.

![Side-by-side simulation showing outcome flips for rehabilitation vs.
infection control strategies](assets/images/fig_improvement_simulation.png)
*Left: Rehabilitation investment flips performance twice. Right: Infection
control investment changes nothing.*

> 💡 **A tiny improvement in rehabilitation flipped the outcome twice. A
> full reduction in infection rates to best-in-class changed nothing.**

---

## What This Analysis Cannot Tell Us

Every analysis has limits — and being transparent about them matters.

**Hospitals differ in size.** Larger hospitals treat more patients, which
can affect rates and scores in ways that are difficult to fully separate.
This is why volume metrics were deliberately excluded from the final model.

**These factors are connected.** A patient who develops an infection is
more likely to be readmitted, which increases costs. The model treats each
factor somewhat independently, so the indirect role of infection control
may be somewhat larger than it appears here.

**The simulation changes one variable at a time.** In reality, a hospital
that invests in rehabilitation also tends to see lower readmissions and
reduced costs as patients recover faster. The true benefit of
rehabilitation investment is likely **even greater** than shown here.

**The dataset is relatively small.** With only 28 hospitals in the top
group and 40 in the bottom group, results could shift with a larger or
more recent dataset.

---

## The Bottom Line

Three separate analyses — comparing group profiles, ranking predictors,
and simulating real-world improvement — all point to the same conclusion:

> **Getting patients home from a long-term care hospital is driven by
> rehabilitation and cost efficiency. Infection control, despite its
> prominence in quality reporting, plays a surprisingly small role.**

For hospital leaders and policymakers, the implications are direct:

- ✅ **Prioritise early mobilisation and physiotherapy programmes**
- ✅ **Monitor cost efficiency as a system-level quality signal**
- ✅ **Recognise that infection metrics alone are not a reliable proxy for
>   discharge performance**

This does not mean infection control is unimportant — reducing infections
matters for patient safety and wellbeing. But **if the goal is to get more
patients home, the data points clearly elsewhere.**

---

*Data source: Centers for Medicare & Medicaid Services (CMS), LTCH Quality
Reporting Program. 290 hospitals included in analysis. Full methodology,
code, and data available in the
[project notebook](link-to-your-notebook).*
