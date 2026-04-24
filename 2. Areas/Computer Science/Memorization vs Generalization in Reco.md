**Tags:** #concept #reco
**Related:** [[Wide and Deep Model]], [[Content-Based Filtering]], [[Collaborative Filtering]]

## Definition

In the context of recommendation systems, **memorisation** is the ability to learn and exploit specific historical co-occurrences of features (e.g. "users who installed Word also install Excel"). **Generalisation** is the ability to discover new feature combinations and apply learned patterns to unseen user-item pairs.

> [!info] Key Intuition
> Memorisation says: "I've seen this exact pattern before — use it." Generalisation says: "I've never seen this user-item pair, but their embeddings are similar to ones I have seen — extrapolate."

## Memorisation

- Achieved by **linear models** (wide component in Wide & Deep) on sparse, raw features and crossed feature transforms
- Requires manual feature engineering: explicit cross-product features (e.g. `AND(gender=female, installed=Pinterest)`)
- Works well when the exact combination has been seen frequently in training data
- Fails to generalise: if a new feature value appears, the linear model has no weight for it

> [!example]- Memorisation Example
> Rule: "Users who install *Game A* AND are in the 18–25 age group → recommend *Game B*."
> Learned from frequency counts. Requires `game_A × age_18_25` as an explicit feature.

## Generalisation

- Achieved by **deep models** (deep component) via low-dimensional embeddings
- Embeddings allow similar unseen feature combinations to share statistical strength
- Does not require explicit feature engineering — the MLP learns interactions automatically
- Risk: over-generalisation (recommending irrelevant items just because they share embedding space)

> [!warning] Trade-off
> Pure deep models can **over-generalise**, recommending items that are semantically related but not actually desired. Pure wide models can **under-generalise**, failing for new users/items. Wide & Deep addresses both by joint training.

## Significance

The memorisation vs. generalisation distinction is the core design principle of Wide & Deep and its successors (DCN, DeepFM). It explains why production recommendation systems rarely use a single model type and instead combine linear and neural components.
