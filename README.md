# A/B Test Analysis — Free-Trial Screener

A full end-to-end A/B test analysis replicating a real experiment run by 
Udacity's growth team — covering experiment design, sanity checks, 
statistical testing, and a business launch recommendation.

---

## Experiment Overview

Udacity tested a screener shown after clicking "Start Free Trial" that asked
students how many hours per week they could commit to the course.

- **5+ hours/week** → proceeded to checkout as normal (control experience)
- **Fewer than 5 hours** → redirected to free course materials instead

**Business goal:** Reduce early cancellations from low-intent students 
without hurting revenue from genuinely committed students.

---

## Hypothesis

- **H0 (null):** The screener has no effect on enrollment or payment rates
- **H1 (alt):** The screener reduces enrollments while maintaining payment rate

---

## Dataset

- **Source:** Udacity A/B Testing Final Project (Kaggle)
- **Link:** https://kaggle.com/datasets/olusegunhenry/udacity-ab-testing-final-project
- **Files:** Baseline Values, Control Results, Experiment Results
- **Scale:** 690,203 pageviews | 56,703 clicks | 37 days

---

## Tools & Tech

| Tool | Purpose |
|------|---------|
| Python (Pandas, NumPy) | Data loading, cleaning, metric computation |
| SciPy (stats) | Two-proportion z-test, p-value, CI calculation |
| Matplotlib | Bar charts, trend lines, CI plot |
| Google Colab | Development environment |
| GitHub | Version control and portfolio hosting |

---

## Metrics

### Invariant Metrics (must not change between groups)
| Metric | Purpose |
|--------|---------|
| Pageviews | Randomization unit — must be ~50/50 split |
| Clicks | Occur before screener is shown |

### Evaluation Metrics (what we're testing)
| Metric | Formula | Goal |
|--------|---------|------|
| Gross Conversion | Enrollments / Clicks | DECREASE |
| Net Conversion | Payments / Clicks | No significant decrease |

---

## Sanity Checks

| Metric | Control | Experiment | Split | Result |
|--------|---------|-----------|-------|--------|
| Pageviews | 345,543 | 344,660 | 50.06% | ✅ PASSED |
| Clicks | 28,378 | 28,325 | 50.05% | ✅ PASSED |

Randomization is valid. Safe to proceed to results analysis.

---

## Results

### Gross Conversion (Enrollments / Clicks)

| | Control | Experiment | Difference |
|-|---------|-----------|-----------|
| Rate | 21.89% | 19.83% | ▼ 2.06pp |
| 95% CI | | | [-0.0291, -0.0120] |
| P-value | | | 0.0000 |
| Significant | | | ✅ YES |
| Goal met | | | ✅ YES |

### Net Conversion (Payments / Clicks)

| | Control | Experiment | Difference |
|-|---------|-----------|-----------|
| Rate | 11.76% | 11.27% | ▼ 0.49pp |
| 95% CI | | | [-0.0116, 0.0019] |
| P-value | | | 0.1558 |
| Significant | | | ⚠️ NO |
| Goal met | | | ⚠️ PARTIAL |

---

## Visualizations

<img width="1590" height="1180" alt="download (1)" src="https://github.com/user-attachments/assets/695bb0d3-4b38-4317-9401-2c8c24e20498" />


---

## Launch Decision

**⚠️ CONDITIONAL LAUNCH — Do not ship without a monitoring plan**

- Gross Conversion dropped 2.06pp (p < 0.0001) — screener successfully
  filters low-intent students ✅
- Net Conversion dropped 0.49pp but is NOT statistically significant —
  revenue is not provably hurt, but the CI barely touches zero ⚠️
- The experiment does not provide strong enough evidence that net revenue
  is fully protected to justify an immediate full launch

---

## Recommendations

| Priority | Recommendation | Rationale |
|----------|---------------|-----------|
| High | Launch to 10% of traffic with payment rate alert at 11.0% | Captures upside while limiting revenue risk |
| High | Extend experiment 4–6 weeks to increase statistical power | Net conversion was underpowered at 17K clicks/group |
| Medium | Segment results by new vs returning users | Controls for primacy effect in returning user base |

---

## Resume Bullet Points

> Designed and executed an end-to-end A/B test on Udacity's free-trial 
> screener across 690K pageviews and 37 days; validated experiment integrity 
> via sanity checks on invariant metrics before analyzing results.

> Applied two-proportion z-tests and 95% CI analysis on gross and net 
> conversion metrics; found statistically significant 2.06pp enrollment 
> drop (p<0.0001) with no significant revenue impact (p=0.156); delivered 
> a conditional launch recommendation with staged rollout and monitoring plan.

---

## Project Structure
```
ab-test-free-trial-screener/
│
├── ab_test_analysis.ipynb        # Full analysis notebook
├── ab_test_results.png           # 4-chart visualization output
├── README.md                     # Project documentation
└── data/                         # Download dataset from Kaggle link above
```

---

## How to Run

1. Download the 3 CSV files from the Kaggle link above
2. Open `ab_test_analysis.ipynb` in Google Colab
3. Upload all 3 files when prompted
4. Run all cells in order

---

## Key Concepts Demonstrated

- Experiment design (hypothesis, metrics, invariant vs evaluation)
- Sanity checks and randomization validation
- Two-proportion z-test and pooled standard error
- Confidence interval interpretation
- Statistical vs practical significance
- Business launch decision framework

---

## Author

**Aakash Malhan**  
