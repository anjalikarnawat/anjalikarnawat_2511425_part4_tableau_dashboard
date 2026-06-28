# Hypothesis Test Notes — Campaign Experiment Analysis

## Experiment Overview

- **Experiment Type:** A/B Test (Randomized Controlled Experiment)
- **Control Group:** Existing onboarding experience — 693 users
- **Treatment Group:** New campaign onboarding experience — 715 users
- **Observation Period:** 30 days post sign-up
- **Significance Level (α):** 0.05

---

## Hypothesis 1: Paid Conversion Rate (PRIMARY — North Star Metric)

### Setup

| Field | Value |
|-------|-------|
| **Null Hypothesis (H₀)** | The new campaign does NOT improve paid conversion rate. Conversion rate (Treatment) ≤ Conversion rate (Control) |
| **Alternate Hypothesis (H₁)** | The new campaign INCREASES paid conversion rate. Conversion rate (Treatment) > Conversion rate (Control) |
| **Test Type** | Two-proportion Z-test (one-tailed) |
| **Significance Level** | α = 0.05 |
| **Metric Being Tested** | Paid Conversion Rate = Users converted to paid / Total users |
| **Reason for Choosing This Metric** | This is the North Star metric directly tied to revenue growth and business sustainability. Improving it means the campaign is working as intended. |

### Test Inputs

| Input | Value |
|-------|-------|
| Control conversions | 22 out of 693 users |
| Control conversion rate | 3.17% |
| Treatment conversions | 50 out of 715 users |
| Treatment conversion rate | 6.99% |
| Pooled proportion | 0.0512 |
| Standard Error | 0.01172 |

### Test Output

| Metric | Value |
|--------|-------|
| Z-statistic | 3.252 |
| P-value | 0.00115 |
| Critical Z (α=0.05, one-tailed) | 1.645 |
| Decision | **REJECT H₀** |

### Business Interpretation

The treatment group showed a **+120.5% lift** in paid conversion rate (3.17% → 6.99%). The result is statistically significant (p = 0.0011 < α = 0.05). This means the new onboarding campaign has a meaningful, non-random improvement in converting users to paid subscriptions. We have strong statistical evidence to recommend launching the new campaign.

---

## Hypothesis 2: Onboarding Completion Rate (Supporting Metric)

| Field | Value |
|-------|-------|
| **H₀** | Onboarding completion rate (Treatment) ≤ Onboarding completion rate (Control) |
| **H₁** | New campaign increases onboarding completion rate |
| **Test Type** | Two-proportion Z-test (two-tailed) |
| **Significance Level** | α = 0.05 |
| **Metric** | Completed onboarding / Total users |

### Results

| Metric | Control | Treatment |
|--------|---------|-----------|
| Completion rate | 15.58% | 21.26% |
| Z-statistic | 2.743 | |
| P-value | 0.0061 | |
| Decision | **REJECT H₀** — Significant improvement |

### Interpretation
The new campaign significantly improves onboarding completion (+36.5%). This is a key driver of conversion and supports the North Star metric result. Users in the treatment are more likely to complete the setup steps before converting.

---

## Hypothesis 3: Engagement Score (Supporting Metric)

| Field | Value |
|-------|-------|
| **H₀** | Mean engagement score (Treatment) = Mean engagement score (Control) |
| **H₁** | New campaign produces higher engagement scores |
| **Test Type** | Independent samples t-test (two-tailed) |
| **Significance Level** | α = 0.05 |
| **Metric** | Average engagement score (0–100 scale) |

### Results

| Metric | Control | Treatment |
|--------|---------|-----------|
| Mean engagement score | 57.03 | 62.93 |
| T-statistic | -7.944 | |
| P-value | < 0.0001 | |
| Decision | **REJECT H₀** — Highly significant |

### Interpretation
Treatment users are significantly more engaged (p < 0.0001). Engagement score is a leading indicator of long-term retention and upsell potential. A +10.4% lift in engagement strengthens confidence in a full launch.

---

## Hypothesis 4: Support Ticket Rate (GUARDRAIL — Risk Test)

| Field | Value |
|-------|-------|
| **H₀** | Support ticket rate (Treatment) = Support ticket rate (Control) |
| **H₁** | New campaign changes support ticket rate |
| **Test Type** | Independent samples t-test (two-tailed) |
| **Significance Level** | α = 0.05 |
| **Metric** | Average support tickets per user in 30 days |

### Results

| Metric | Control | Treatment |
|--------|---------|-----------|
| Avg tickets/user | 0.219 | 0.372 |
| T-statistic | -4.214 | |
| P-value | 0.000027 | |
| Decision | **REJECT H₀** — ⚠️ SIGNIFICANT INCREASE |

### Interpretation
This is a **guardrail violation**. The treatment group generates 69.6% more support tickets per user (p < 0.0001). This suggests the new onboarding may be creating confusion or unmet expectations. While the primary metric improved, this guardrail risk must be investigated before a full launch. We recommend monitoring this post-launch and investigating root cause (e.g., onboarding clarity, feature discoverability).

---

## Hypothesis 5: Days to Convert (Supporting / Speed Metric)

| Field | Value |
|-------|-------|
| **H₀** | Days to convert (Treatment) ≥ Days to convert (Control) |
| **H₁** | New campaign reduces days to convert |
| **Test Type** | Independent samples t-test (one-tailed, among converters only) |
| **Significance Level** | α = 0.05 |
| **Sample** | Only users who converted (Control n=22, Treatment n=50) |

### Results

| Metric | Control | Treatment |
|--------|---------|-----------|
| Avg days to convert | 8.86 days | 6.40 days |
| T-statistic | 3.014 | |
| P-value | 0.0036 | |
| Decision | **REJECT H₀** — Significantly faster conversion |

### Interpretation
Users in the treatment group convert 2.46 days faster on average (-27.8%). This indicates the new onboarding journey creates urgency and reduces friction in the conversion funnel. Combined with the higher conversion rate, this confirms the campaign is effective at accelerating the user journey.

---

## Summary of All Hypothesis Tests

| Test | Metric | p-value | Decision | Business Impact |
|------|--------|---------|----------|-----------------|
| H1 | Paid Conversion Rate | 0.0011 | REJECT H₀ ✅ | +120.5% lift — Launch |
| H2 | Onboarding Completion | 0.0061 | REJECT H₀ ✅ | +36.5% — Supports launch |
| H3 | Engagement Score | <0.0001 | REJECT H₀ ✅ | +10.4% — Supports launch |
| H4 | Support Ticket Rate | 0.000027 | REJECT H₀ ⚠️ | +69.6% — GUARDRAIL RISK |
| H5 | Days to Convert | 0.0036 | REJECT H₀ ✅ | -27.8% faster — Supports launch |

---

## Overall Decision Logic

Given that:
1. The North Star metric (paid conversion rate) shows a statistically significant +120.5% lift (p=0.0011)
2. Two supporting metrics (onboarding completion, engagement) confirm the direction
3. One guardrail metric (support ticket rate) shows a significant concern

**Recommendation: LAUNCH with conditional monitoring.** The primary evidence strongly supports launch. The support ticket concern should be tracked for 30 days post-launch, and a root cause investigation should run in parallel.
