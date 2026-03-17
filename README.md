# Creator Policy Impact Simulator
> A Trust & Safety analytics project simulating how YouTube Partner Program policy threshold changes affect creator monetization eligibility


## What this project is about

The YouTube Partner Program (YPP) decides which creators can earn money from ads on their videos. When YouTube changes the eligibility threshold — making it stricter or more relaxed — thousands of creators gain or lose monetization status overnight.

This project simulates the exact workflow a T&S Analytics team would run before any policy change goes live:

- How many creators are affected?
- Which creator tiers get hit hardest?
- Is the impact statistically significant or just noise?
- Does the change actually achieve its quality goal?
- What is the false positive cost — legitimate creators wrongly excluded?

---

## Dataset

**Source:** YouTube Trending Videos Dataset — [Kaggle](https://www.kaggle.com/datasets/datasnaek/youtube-new)

**Size:** ~40K videos aggregated into 2,153 unique creator profiles

**Key fields:** views, likes, dislikes, comment count, channel name, category, trending date, comments/ratings disabled flags

> Raw data not included. Download instructions in `data/README.md`

---

## The three policy scenarios simulated

| Scenario | Threshold | What it represents |
|---|---|---|
| Current policy (baseline) | Score ≥ 0.35 | Existing eligibility standard |
| Tighter policy | Score ≥ 0.50 | YouTube raises the quality bar |
| Looser policy | Score ≥ 0.25 | Expanded access for smaller creators |

---

## What we built

### Notebook 1 — Data Cleaning & Feature Engineering
- Transformed raw video-level data into a creator-level dataset (one row per channel)
- Engineered 4 signal categories: engagement quality, content health, scale, consistency
- Built a weighted composite eligibility score (0–1) for each creator
- Applied a content health penalty for creators who disable comments/ratings
- Segmented creators into 5 tiers: Micro, Small, Mid, Large, Mega

### Notebook 2 — Policy Simulation Engine
- Simulated all 3 policy scenarios and measured eligibility rate under each
- Chi-square significance testing to confirm policy impacts are statistically real
- Full precision/recall curve across 35 threshold values
- Segment analysis: which creator tier is most affected by each policy
- Logistic regression to identify the strongest predictors of eligibility

### Notebook 3 — A/B Test Analysis
- Simulated a real-world pre-launch test: 50/50 random split of creators
- Validated group balance before testing (p=0.192 — groups are comparable)
- Measured primary metric (eligibility rate) with chi-square significance
- Secondary metrics: engagement quality, false positive rate, equity by tier
- Final policy recommendation brief in analyst language

---

## Key Findings

**Finding 1 — Tighter policy removes 85% of eligible creators**
Moving from threshold 0.35 to 0.50 drops eligible creators from 260 to just 39 (12.1% → 1.8%). Statistically significant at p<0.001.

**Finding 2 — Small creators are locked out under all policies**
Micro, Small, and Mid creators have zero eligible creators even under the current policy. The program is already only accessible to Large and Mega channels.

**Finding 3 — Tighter policy is counterproductively worse on quality**
Precision drops from 62.7% to 38.5%. Eligible creators under the tighter policy actually have lower average engagement (0.0382 vs 0.0549). The policy fails its own quality goal.

**Finding 4 — False positive rate increases under the tighter policy**
FPR goes from 12.5% to 35.7% — a 23.2% increase. The tighter policy eliminates just 24 false positives while generating 846 false negatives (quality creators wrongly excluded).

**Finding 5 — The sweet spot is around threshold 0.25–0.30**
The precision/recall curve shows false positives and false negatives cross at this range — where both error types are roughly balanced and the policy is most defensible.

---

## Policy Recommendation

**REVIEW BEFORE PROCEEDING.** The tighter policy fails on every dimension that matters — it reduces eligibility by 89%, lowers the quality of who gets in, and increases false positives. If raising quality standards is the goal, the data suggests the 0.25–0.30 threshold range with a staged rollout and clear appeals process for affected creators.

---


## Tools & Stack

`Python 3.10` · `pandas` · `NumPy` · `scikit-learn` · `SciPy` · `Matplotlib` · `Seaborn` · `Jupyter`

---

## About

**Ajay Singh Rawat** — Data Analytics professional, 4+ years experience in marketing analytics, business intelligence, and applied data science.

[LinkedIn](http://www.linkedin.com/in/rawatajayrawat/) · [GitHub](https://github.com/ajayrawat266)
