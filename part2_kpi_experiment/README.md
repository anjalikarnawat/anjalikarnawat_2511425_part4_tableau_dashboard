# Part 2: KPI Framework, Business Experiment Analysis & Decision Recommendation

## 1. Business Context

A subscription-based digital product company launched a new onboarding and activation campaign. Users were randomly assigned to two groups:
- **Control group:** Existing onboarding experience (693 users)
- **Treatment group:** New campaign experience (715 users)

Leadership wants to know whether the treatment should be launched to all users.

---

## 2. Business Problem Statement

**Decision:** Should the new onboarding campaign be launched to all users?  
**Who it impacts:** Product team, growth team, customer support, all new users  
**Metric to improve:** Paid Conversion Rate (North Star Metric)  
**Risks to monitor:** Support ticket rate spike, refund rate  
**Evidence required:** Statistically significant improvement in conversion rate without guardrail violations

---

## 3. North Star Metric Selected

**Paid Conversion Rate** = Users who converted to paid / Total users in group

This metric was selected because it directly measures whether the campaign drives business value (revenue). All other metrics either feed into it (funnel metrics) or guard against gaming it (guardrail metrics).

---

## 4. KPI Tree Summary

The North Star metric breaks into three primary KPI drivers:

- **Acquisition Funnel Depth:** Landing page visit rate → Trial start rate → Onboarding completion rate
- **Product Experience Quality:** Engagement score, Days to convert, Revenue per user
- **Revenue Quality:** Revenue per converted user, Plan type mix, Retention rate

Guardrail metrics monitored: Refund Rate, Support Ticket Rate, Engagement Score decline, Segment-level drop-offs

See `outputs/kpi_tree.png` for the visual KPI tree.

---

## 5. Experiment Analysis Approach

### Data Cleaning (Task 4)
- 1,408 total records; 693 Control, 715 Treatment
- Missing values: device_type (18), traffic_source (24), engagement_score (14)
- 8 duplicate user_ids identified and flagged
- All binary columns (0/1) validated — no invalid values found
- `days_to_convert` has 1,336 nulls — valid (only converters have values)
- One revenue outlier in control (₹8,610) retained with a note

### Analysis files:
- `analysis/experiment_analysis.xlsx` — Cleaned data + metrics + segment breakdowns
- `analysis/hypothesis_test_notes.md` — Full statistical test documentation

---

## 6. Hypothesis Test Summary

| Test | Metric | Test Type | p-value | Result |
|------|--------|-----------|---------|--------|
| H1 (Primary) | Paid Conversion Rate | 2-prop Z-test | 0.0011 | ✅ Significant |
| H2 | Onboarding Completion | 2-prop Z-test | 0.0061 | ✅ Significant |
| H3 | Engagement Score | t-test | <0.0001 | ✅ Significant |
| H4 (Guardrail) | Support Ticket Rate | t-test | 0.000027 | ⚠️ Risk |
| H5 | Days to Convert | t-test | 0.0036 | ✅ Significant |

Significance level: α = 0.05

---

## 7. Guardrail Metrics Considered

| Guardrail | Control | Treatment | Status |
|-----------|---------|-----------|--------|
| Refund Rate | 0.00% | 0.42% | ⚠️ Monitor |
| Support Ticket Rate | 0.219/user | 0.372/user | ⚠️ High Risk |
| Engagement Score | 57.03 | 62.93 | ✅ Positive |

---

## 8. Final Recommendation

**LAUNCH** the new onboarding campaign to all users, with the following conditions:
- Investigate support ticket increase before or immediately after launch
- Set alert: if support ticket rate > 0.5/user or refund rate > 2%, pause and review
- Monitor for 30 days post-launch

---

## 9. Assumptions and Limitations

- Experiment was run for 30 days; long-term retention/LTV not captured
- Small absolute number of converters (72 total) — proportional test valid but wide confidence intervals
- Refund data completeness for control group is uncertain (0 refunds may reflect data gap)
- Ambiguous dates stored as Excel serial numbers; not used in analysis

---

## 10. Screenshots Included

| File | Shows |
|------|-------|
| `screenshots/summary_metrics.png` | Control vs Treatment metric comparison table |
| `screenshots/hypothesis_test_output.png` | Statistical test results |
| `screenshots/kpi_tree_preview.png` | Full KPI tree diagram |

---

## Repository Structure

```
part2_kpi_experiment/
├── data/
│   └── campaign_experiment_data.xlsx
├── analysis/
│   ├── experiment_analysis.xlsx
│   └── hypothesis_test_notes.md
├── outputs/
│   ├── kpi_tree.png
│   ├── experiment_summary.xlsx
│   └── recommendation_memo.md
├── screenshots/
│   ├── summary_metrics.png
│   ├── hypothesis_test_output.png
│   └── kpi_tree_preview.png
└── README.md
```
