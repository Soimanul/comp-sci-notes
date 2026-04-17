**Tags:** #concept #nlp #sentiment
**Related:** [[Sentiment Lexicons]], [[Sentiment Analysis]]

## Definition

VADER (Valence Aware Dictionary and sEntiment Reasoner) is a rule-augmented sentiment lexicon specifically tuned for social media text. It produces four scores: positive, negative, neutral proportions, and a normalised compound score in $[-1, +1]$.

> [!info] Key Intuition
> VADER handles the peculiarities of informal text — ALL CAPS, exclamation marks, emoji, slang, and negation — through explicit heuristic rules layered on top of a hand-validated lexicon, without any ML training.

## Core Mechanics

**Lexicon construction**: 7,500+ features crowd-rated on a –4 to +4 scale; mean and standard deviation retained per word.

**Five heuristic rules**:
1. **Punctuation** — "!!!" amplifies intensity
2. **Capitalisation** — ALL CAPS intensifies polarity of known sentiment words
3. **Degree modifiers** — *extremely*, *kind of*, *slightly* shift magnitude
4. **"But" conjunctions** — sentiment after "but" dominates (shift emphasis right)
5. **Tri-gram negation** — "wasn't very good" inverts *good* within a 3-token window

**Compound score** aggregation:
$$\text{compound} = \frac{\sum s_i}{\sqrt{\sum s_i^2 + \alpha}}$$
where $\alpha = 15$ is a normalisation constant; thresholds: $\geq 0.05$ positive, $\leq -0.05$ negative.

> [!example]- Worked Example
> Input: *"The food was NOT good :("*
> - "good" raw = +1.9 → negated to –1.9
> - ":(" = –1.3
> - No caps, no "!!"
> - Compound ≈ –0.54 → classified **negative**

## Significance

VADER is the go-to baseline for short informal text because it requires no training data and handles emoji/slang that trip up general lexicons. It underperforms on domain-specific or long-form text.
