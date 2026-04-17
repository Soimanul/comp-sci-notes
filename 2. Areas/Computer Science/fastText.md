**Tags:** #concept #nlp #embeddings
**Related:** [[Word Embeddings]], [[Word2Vec]], [[The OOV Problem]]

## Definition

fastText (Facebook AI) extends Word2Vec by representing each word as the sum of its character $n$-gram embeddings rather than a single whole-word vector. This gives every word — including out-of-vocabulary words — a representation derived from its subword components.

> [!info] Key Intuition
> Instead of learning one vector per word, fastText learns vectors for character shingles. *"eating"* = sum of vectors for *"eat"*, *"ati"*, *"tin"*, *"ing"*, etc. — so *"eats"* gets a sensible vector even if it was never seen during training.

## Core Mechanics

Word representation:
$$\mathbf{v}(w) = \sum_{g \in \mathcal{G}(w)} \mathbf{z}_g$$

where $\mathcal{G}(w)$ is the set of character $n$-grams (typically $n = 3$–$6$) plus the full word form.

Training uses Skip-gram with negative sampling, replacing the centre word embedding with $\mathbf{v}(w)$.

**Advantages over Word2Vec**:
- Handles OOV words via shared subword embeddings
- Better morphologically rich languages (Turkish, Finnish, Arabic)
- Captures spelling-based similarity (*"colour"* ≈ *"color"*)

> [!example]- Worked Example
> Unseen word: *"unhappiness"*
> fastText decomposes → trigrams: *<un*, *unh*, *nha*, *hap*, *app*, *ppi*, *pin*, *ine*, *nes*, *ess*, *ss>*
> Its vector is the sum of learned trigram embeddings — capturing the morphological prefix *"un-"* and suffix *"-ness"*.

## Significance

fastText is the standard choice when the text domain involves noisy, user-generated, or morphologically complex language where OOV rates are high.
