**Tags:** #concept #reco #ml
**Related:** [[Offline vs Online Metrics]], [[Recommendation System Architectures]]

## Definition

**A/B testing** (controlled experiment) is the standard method for evaluating whether a recommendation model improves real-world business metrics by randomly assigning users to a **control group** (A) and a **treatment group** (B).

> [!info] Key Intuition
> A/B testing is the "gold standard" for measuring a model's true impact. It answers: "Does replacing the old system with the new one *actually* improve user behaviour?" You can't answer this from offline metrics alone.

## How It Works in Recommendation Systems

1. **Split traffic**: Randomly assign ~50% of users to the old model (A = control), 50% to the new model (B = treatment).
2. **Run for a statistical power duration**: Typically 1–4 weeks to gather enough data.
3. **Measure business metrics**: Compare CTR, Conversion Rate, AOV, MAU, LTV between groups.
4. **Statistical significance test**: Use t-test or chi-squared test to determine if the difference is real.
5. **Deploy or rollback**: If B significantly outperforms A, roll out to 100% of traffic.

> [!example]- Example
> You train a new NCF model. A/B test: 50% see old ALS-based recommendations, 50% see NCF. After 2 weeks: NCF group has +3.5% higher CTR and +2.1% higher conversion rate with p < 0.05. → Ship NCF.

## Multi-Variate Testing

When testing **more than two groups** simultaneously, the test is called a **Multi-Variate Test** (MVT). Example: test 3 models against each other in one experiment with 3 traffic splits.

> [!warning] Common Misconception
> A/B testing requires randomisation at the **user level**, not at the session or page level. Otherwise, the same user might see both variants and contaminate the experiment.

## Significance

A/B testing is mandatory before shipping any recommendation change to production. It bridges the offline/online metric gap and is the only way to measure true business impact, controlling for confounding factors.
