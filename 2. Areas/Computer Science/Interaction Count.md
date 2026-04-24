**Tags:** #concept #reco
**Related:** [[User Item Interaction Model]], [[Weighted Interaction Count]], [[Time Decay]], [[Affinity Matrix]]

## Definition

**Interaction count** is a data transformation technique that produces an **affinity score** between a user and an item by counting the total number of interactions between them.

$$\text{affinity}(u, i) = \sum_{t} \mathbf{1}[\text{user } u \text{ interacted with item } i \text{ at time } t]$$

> [!info] Key Intuition
> Simple counting says: "the more times a user touched an item, the more they presumably like it." It is the baseline transformation — every other affinity computation builds on or modifies this.

## How It Works

For each (user, item) pair, count every interaction event (click, view, purchase, etc.) regardless of type or time. The result is a raw affinity matrix entry.

> [!example]- Example
> User 1 viewed Movie A 3 times, Movie B once. Interaction count: A→3, B→1.

## Limitations

- Treats all interaction types equally (a purchase = a hover).
- Does not account for when the interaction occurred (a purchase 3 years ago = a purchase yesterday).
- Both limitations are addressed by [[Weighted Interaction Count]] and [[Time Decay]] respectively.

## Significance

Interaction count is the simplest and most interpretable affinity score. It is used as the baseline in the [[SAR Algorithm]] and other memory-based methods.
