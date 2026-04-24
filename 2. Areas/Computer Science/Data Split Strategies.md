**Tags:** #concept #reco #ml
**Related:** [[User Item Interaction Model]], [[Cold Start Problem]]

## Definition

**Data split strategies** determine how a recommendation dataset is divided into **training** and **testing** sets to evaluate model performance correctly.

> [!info] Key Intuition
> The choice of split strategy directly determines whether your evaluation reflects real-world performance. A bad split can make a model look better or worse than it actually is in production.

## Three Main Strategies

### Random Split
Randomly assign each (user, item, rating) row to train or test sets.
- **Use when**: interactions are independent and time-order does not matter.
- **Risk**: a user's most recent interactions may end up in training, which is unrealistic.

### Stratified Split
Randomly split while ensuring the **same set of users and items appear in both** train and test.
- **Benefits**: prevents artificial cold start in the test set; more statistically sound.
- **Use when**: you need to evaluate the model on known users (e.g., movie recommendation with registered users).
- **Can filter by**: minimum interaction count per user/item.

> [!example]- Example: Stratified Split
> Movie recommendation: use stratified split to ensure every user in the test set also has training data. Otherwise, test users with no training examples will always produce poor results — but that's a data issue, not a model issue.

### Chronological Split
Split the data by **timestamp** — earlier interactions go to training, later ones go to test.
- **Use when**: user preferences drift over time (fashion, news, music).
- **Most realistic** for sequential behaviour modelling.
- **Can filter by**: user/item minimum interaction count.

> [!example]- Example: Chronological Split
> Fashion recommendation: customer tastes change seasonally. A chronological split ensures the model is tested on predicting future purchases, not past ones — which is the actual production task.

> [!warning] Common Misconception
> Using a purely random split for time-dependent data is **data leakage**: the model trains on future information to predict the past, making evaluation optimistically biased.

## Significance

Choosing the correct split strategy is critical for honest evaluation. Stratified splits are the standard for general recommendation; chronological splits are mandatory when temporal drift exists.
