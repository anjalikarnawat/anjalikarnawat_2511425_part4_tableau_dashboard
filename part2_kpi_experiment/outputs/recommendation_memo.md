# Recommendation Memo
## New Onboarding & Activation Campaign — Launch Decision

**To:** Product Leadership  
**From:** Business Analyst  
**Date:** June 2026  
**Subject:** A/B Experiment Results & Launch Recommendation

---

## 1. Executive Summary

The new onboarding and activation campaign was tested in a randomized A/B experiment with 1,408 users (693 Control, 715 Treatment). The treatment group experienced a **+120.5% improvement in paid conversion rate** — from 3.17% to 6.99% — a result that is statistically significant at the 95% confidence level (p = 0.0011).

**Recommendation: LAUNCH the new campaign with active monitoring of support ticket rate.**

---

## 2. Business Problem Statement

**Decision to be made:** Should the new onboarding and activation campaign be launched to all users?

**Who it impacts:** Product team, growth team, customer support, and all new users signing up.

**Metric to improve:** Paid Conversion Rate (North Star Metric)

**Risks to monitor:** Support ticket rate (significantly elevated in treatment), refund rate (small but nonzero in treatment vs zero in control)

**Evidence required:** Statistically significant improvement in paid conversion rate without material degradation of guardrail metrics.

---

## 3. North Star Metric

**Selected North Star: Paid Conversion Rate = Users Who Converted to Paid / Total Users**

This metric was chosen because:
- It directly measures whether the onboarding experience turns free users into paying customers
- It is the clearest signal of campaign effectiveness and revenue impact
- It connects directly to business sustainability and growth
- Other metrics (engagement, onboarding completion) are leading indicators that feed into this outcome

**What could go wrong if optimized blindly:** Over-aggressive prompts to convert could inflate short-term conversion while increasing refunds, churns, and support burden — eroding long-term revenue quality.

---

## 4. KPI Tree Explanation

The North Star metric (Paid Conversion Rate) is driven by three primary levers:

**Driver 1 — Acquisition Funnel Depth**
- Landing Page Visit Rate, Trial Start Rate, Onboarding Completion Rate
- Users must progress through each step before converting

**Driver 2 — Product Experience Quality**
- Engagement Score, Days to Convert, Average Revenue per User
- Higher engagement signals users finding value; lower days to convert = less friction

**Driver 3 — Revenue Quality**
- Revenue per Converted User, Plan Type Mix, Retention Rate
- Conversion must translate to durable revenue, not one-time or refunded transactions

**Guardrail Metrics (do not optimize blindly against these):**
- Refund Rate, Support Ticket Rate, Engagement Score decline, Segment-level drop-off

---

## 5. Experiment Result Summary

| Metric | Control | Treatment | Lift | Significant? |
|--------|---------|-----------|------|-------------|
| Paid Conversion Rate | 3.17% | 6.99% | +120.5% | ✅ YES (p=0.0011) |
| Onboarding Completion | 15.58% | 21.26% | +36.5% | ✅ YES (p=0.0061) |
| Avg Engagement Score | 57.03 | 62.93 | +10.4% | ✅ YES (p<0.0001) |
| Days to Convert | 8.86d | 6.40d | -27.8% | ✅ YES (p=0.0036) |
| Avg Revenue/User | ₹51.75 | ₹53.88 | +4.1% | ❌ Not significant |
| Support Ticket Rate | 0.219 | 0.372 | +69.6% | ⚠️ YES — Risk |
| Refund Rate | 0.00% | 0.42% | +0.42% | ⚠️ Monitor |

---

## 6. Hypothesis Test Interpretation

A two-proportion Z-test on the primary metric (paid conversion rate) was conducted:
- **Z-statistic: 3.252**, **P-value: 0.0011**
- At α = 0.05, we reject the null hypothesis
- Conclusion: The new campaign produces a statistically significant improvement in conversion rate

Additional tests confirmed onboarding completion (p=0.0061) and engagement score (p<0.0001) improvements are also statistically significant and not due to chance.

---

## 7. Guardrail Analysis

Three guardrail metrics were evaluated:

**Guardrail 1 — Support Ticket Rate** 🔴 ELEVATED  
Treatment: 0.372 tickets/user vs Control: 0.219 (p=0.000027). A 69.6% increase. This is statistically significant and must be investigated. Possible causes: onboarding confusion, unclear feature expectations, billing questions. Risk: medium-to-high if unresolved.

**Guardrail 2 — Refund Rate** 🟡 MINOR CONCERN  
Control: 0 refunds. Treatment: 3 refunds (0.42%). While small, this is a signal to watch. The sample of converters is small (n=50 treatment converters) so this may not be representative, but refunds are worth monitoring.

**Guardrail 3 — Engagement Score** 🟢 POSITIVE  
Engagement is significantly HIGHER in treatment (+10.4%). This guardrail is not violated. Higher engagement suggests users in the new campaign are finding the product more valuable.

---

## 8. Segment-Level Insights

| Segment | Dimension | Ctrl Conv% | Treat Conv% | Note |
|---------|-----------|-----------|-------------|------|
| Premium Plan | plan_type | 7.7% | 15.4% | Strongest uplift |
| Email Traffic | traffic_source | 5.3% | 11.6% | Best channel |
| Desktop Users | device_type | 4.0% | 8.2% | Consistent uplift |
| North Region | region | 3.9% | 8.9% | Highest regional lift |
| Paid Search | traffic_source | 2.2% | 5.7% | Moderate; check ROI |

No segment showed a decline in conversion under treatment. The campaign performs consistently across all tested dimensions.

---

## 9. Final Recommendation: LAUNCH

**Decision: Launch the new onboarding campaign to all users.**

This is supported by:
- The North Star metric (paid conversion rate) improved by +120.5% with statistical significance
- All three supporting metrics (onboarding completion, engagement, days-to-convert) moved in the right direction
- No segment showed regression
- Revenue per user trended slightly higher (not significant, but no harm detected)

**Conditions on launch:**
- Set up a support ticket rate dashboard with weekly review for 30 days post-launch
- Investigate root causes of higher support ticket rate before launch (recommended: 1-week sprint)
- Monitor refund rate at the 30-day and 60-day marks
- Alert threshold: if support ticket rate exceeds 0.5 tickets/user or refund rate exceeds 2%, pause and investigate

---

## 10. Risks and Limitations

- **Support ticket burden:** A 69.6% increase is operationally significant. Customer support capacity may need to scale.
- **Small converter sample:** Only 72 users (22 control, 50 treatment) converted. While the proportional test is valid, the absolute numbers are small.
- **Outlier in control revenue:** One control user had ₹8,610 in revenue (vs. max ₹2,660 in treatment). This may skew average revenue comparisons.
- **30-day window:** Long-term retention, churn, and LTV are not captured in this experiment period.
- **Refund data limitation:** Control had 0 refunds; it's unclear if this is real or a data collection gap.

---

## 11. Next Steps

1. **Week 1:** Investigate support ticket root cause — survey treatment users, analyze ticket topics
2. **Week 1:** Launch to all new users with monitoring dashboards in place
3. **Week 4:** Review post-launch support ticket rate, refund rate, and 30-day conversion
4. **Week 8:** Full LTV and retention analysis for treatment vs control cohorts
5. **Month 3:** Consider A/B test variant focused on reducing support ticket rate (e.g., improved FAQ, in-app guidance)
