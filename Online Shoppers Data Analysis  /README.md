# Online Shoppers Purchasing Intention

**Identifying the predictors of purchase from browsing behaviour**

Author: Mohammad Shahir Wakili

---

## Scope

This project analyses session level browsing data from an online retail store to
determine which behaviours distinguish sessions that end in a purchase from those
that do not.

The raw dataset contains 12,330 browsing sessions, reduced to 12,205 after removing
125 exact duplicates. Each row represents one visit and records 17 predictor
variables covering page visit counts, time spent by page type, engagement metrics,
and session context such as month, visitor type and traffic source. The response
variable `Revenue` is binary and indicates whether the session concluded in a
transaction. There is no missing data.

The outcome is imbalanced. 1,908 sessions, or 15.6%, resulted in a purchase.

Analysis is restricted to the variables supplied. No pricing, product category,
inventory or customer identity information is available.

---

## Objective

1. Which session behaviours are associated with a completed purchase, and how large
   is each effect?
2. Do behavioural variables carry more information than contextual variables such as
   month, visitor type and traffic source?
3. How accurately can purchase intent be predicted from session data alone, and how
   should performance be assessed given the class imbalance?

A secondary objective is methodological: to select a model appropriate to a binary
response, verify the assumptions that apply to it, and identify any predictor whose
construction may compromise the validity of the result.

---

## Method

**Data preparation.** Duplicates removed. Zero values retained, as a zero represents a
genuine observation rather than a missing value. Identifier coded columns (`Browser`,
`OperatingSystems`, `Region`, `TrafficType`) converted to factors, since their numeric
values are labels rather than quantities. `Month` levels set explicitly to preserve
calendar order.

**Exploratory analysis.** Group means compared between purchasing and non purchasing
sessions. Conversion rates calculated by visitor type, weekend status and month.
Distributions examined for skew.

**Collinearity.** Two strongly collinear pairs identified: `BounceRates` with
`ExitRates` at r = 0.90, and `ProductRelated` with `ProductRelated_Duration` at
r = 0.86. One variable from each pair removed, retaining `ExitRates` for its clearer
separation between outcome groups and `ProductRelated` as the simpler measure.

**Modelling.** Logistic regression, `glm(family = binomial)`, chosen because the
response is binary. Data split 70/30 into training and test sets. Factor levels with
fewer than 100 training observations collapsed into an "Others" category, with the
grouping learned from the training set only and then applied to the test set so that
no test set information influences model fitting. Two specifications fitted: a full
model, and a reduced model excluding `PageValues`.

**Diagnostics.** Variance inflation factors and Cook's distance.

**Evaluation.** Confusion matrix, sensitivity, specificity, precision and AUC computed
on the held out test set, at both the default threshold and a Youden optimal threshold.

---

## Outcome

### Behavioural predictors

`ExitRates` is the dominant predictor. Each one percentage point increase is
associated with approximately a **25% reduction** in the odds of purchase.

`ProductRelated` contributes positively but modestly, at roughly **2.2% higher odds
per ten additional product pages** viewed (OR 1.002 per page, p = 0.002).

`SpecialDay` is significant and negative (OR 0.556, p = 0.024), indicating that
proximity to a holiday is associated with lower rather than higher conversion.

`Administrative` and `Informational` page counts are not significant once other
variables are accounted for.

Descriptively, purchasing sessions view 48.2 product pages on average against 29.1
for non purchasing sessions, and spend 1,876 seconds against 1,083.

### Contextual predictors

Conversion varies by month, peaking at 25.5% in November against 1.7% in February.
A chi squared test confirms the association, χ²(9) = 282.7, p < 0.001, with November
contributing the largest standardised residual at +15.56. Cramér's V is 0.18,
indicating a small to moderate association, so month matters but less than the size
of individual residuals might suggest.

New visitors convert at 24.9% against 14.1% for returning visitors. Weekend sessions
convert at 17.5% against 15.1% on weekdays.

Contextual effects carry wider confidence intervals than the behavioural predictors,
reflecting smaller subgroup sizes, and are treated as less reliable.

### PageValues and the leakage question

`PageValues` is by far the strongest predictor in the full model. Sessions with a
non zero value convert at **56.3%** against **3.9%** otherwise, and including the
variable lowers AIC from 6,380.3 to 5,022.5, a difference of approximately 1,358 on
a single degree of freedom.

The variable is also essentially uncorrelated with every other predictor, which is
inconsistent with a measure of browsing behaviour, since the remaining variables are
all interrelated through visitor engagement. As `PageValues` is derived from
historical transaction data, it may partly encode the outcome being predicted.

The reduced model excluding `PageValues` is used for interpretation and evaluation.
The full model is reported for comparison.

### Model performance

AUC on the held out test set is **0.73**, indicating moderate ability to distinguish
purchasing from non purchasing sessions.

| Threshold | Sensitivity | Specificity | Precision |
|---|---|---|---|
| 0.50 (default) | 0.033 | 0.992 | 0.465 |
| 0.13 (Youden optimal) | 0.785 | 0.587 | 0.271 |

At the default threshold the model achieves 83.5% accuracy but identifies only 3.3%
of actual purchasers. This reflects the class imbalance rather than a failure of the
model, since predicted probabilities rarely exceed 0.5 when the base rate is 15.6%,
and it demonstrates why accuracy is an inadequate measure here.

The report adopts the lower threshold on the assumption that missing a genuine
purchaser is more costly than flagging a non purchaser, which suits a remarketing use
case. A different cost structure would justify a different threshold.

### Diagnostics

All adjusted GVIF values fall below 1.4, confirming that removing the collinear
variables resolved the issue identified in the exploratory analysis. Cook's distance
values are all below 0.012, well under any conventional threshold for influence, so
no observations were excluded.

---

## Files

| File | Description |
|---|---|
| `Analysis_2.Rmd` | Full analysis, knits to PDF |
| `Analysis_2.pdf` | Rendered report |
| `Analysis_2.csv` | Session level dataset, 12,330 rows |
| `README.md` | This document |

---

## Requirements

R with the following packages:

```
tidyverse   corrplot   patchwork   GGally
car         caret      pROC        broom      knitr
```

To reproduce, place `Analysis_2.csv` in the same directory as the Rmd file, restart R,
and knit. The analysis runs top to bottom without manual intervention.

---

## Limitations

The data is observational. The relationships reported describe how purchasing and non
purchasing sessions differ, and do not establish that any behaviour causes a purchase.
It is equally consistent with the evidence that visitors who already intend to buy
browse more extensively.

The construction of `PageValues` cannot be verified from the file supplied, so its
exclusion rests on inference from its statistical behaviour rather than on documented
provenance.

592 sessions, or 4.9%, record product pages viewed with zero total duration. These
were retained on the judgement that this reflects a tracking artefact rather than
invalid data.

No visitor identifier is available, so the assumption of independent observations
cannot be verified. A single visitor may contribute multiple sessions.

Variables likely to influence purchasing are absent, including price, product
category, stock availability and login status.

The dataset covers ten months. January and April are not represented, which limits
conclusions about the full annual cycle.
