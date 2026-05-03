**Tags:** #concept #nlp #sentiment #discourse
**Related:** [[Sentiment Analysis]], [[Three Perspectives on Sentiment Classification]]

## Definition

Sentiment can be tracked as a **time series** indexed by sentence position rather than as a single document-level label. For a discourse $d = (s_1, \dots, s_T)$, compute per-sentence sentiment

$$p_i = P(y = 1 \mid s_i)$$

and treat the sequence $(p_1, \dots, p_T)$ as a trajectory.

> [!info] Key Intuition
> A document-level label flattens emotional structure into a number. A sentiment trajectory preserves the *shape* — escalation, decline, turning points — that gives discourse its rhetorical force.

## What the Trajectory Reveals

Plotting $p_i$ against $i$ exposes:

- **Emotional peaks and valleys** — climaxes and pivots
- **Gradual intensification** toward a conclusion
- **Strategic negativity** in middle sections (problem-then-solution structure)
- **Sustained tone** vs **oscillation**

The classifier itself does not interpret rhetoric; it produces statistical signals. But examining those signals **dynamically** turns sentiment analysis from a static classification task into a tool for **discourse and narrative analysis**.

## Rhetorical Patterns Worth Watching For

- **Emotional amplification** — increasing intensity over time
- **Polarisation** — sharpening contrast between segments
- **Us-vs-them framing** — alternating polarity between in-group and out-group references
- **Blame attribution** — negative spikes tied to specific entities
- **Fear escalation** vs **hope crescendo**
- **Moral elevation** — shift toward positive abstract vocabulary near conclusion

> [!example]- Worked Example
> A political speech segmented into 50 sentences, each scored with VADER's compound score. Plot reveals: opening 10 sentences strongly positive (greeting), middle 25 mixed-to-negative (problem statement), final 15 sharply rising positive (call to action) — a textbook hope-crescendo arc.

## Significance

This reframes sentiment analysis as a quantitative method for **discourse analysis**. The same per-sentence classifier that powers a product-review system becomes a diagnostic instrument for political speeches, sermons, marketing copy, or any rhetorically structured text — once outputs are interpreted as a sequence rather than a sum.

> [!warning] Common Misconception
> Aggregating the trajectory back to a single mean throws away exactly the information that motivated computing it. The shape *is* the signal; do not collapse it.
