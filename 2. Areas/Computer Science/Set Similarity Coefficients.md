**Tags:** #concept #nlp #similarity #set-similarity  
**Related:** [[Geometric View of Meaning]] · [[Bag-of-Words (BoW)]] · [[Cosine Similarity]]

## Definition
Set similarity coefficients compare two texts using **overlap of unique terms** (or binary BoW features). They are appropriate when lexical overlap is the signal and frequency/weights are not required.

## Notation
Let $A$ and $B$ be the sets of unique terms in two texts.

## Core Coefficients

### Jaccard Similarity
$$
J(A,B)=\frac{|A \cap B|}{|A \cup B|}
$$
Interprets similarity as overlap divided by total unique terms.

### Dice Coefficient
$$
D(A,B)=\frac{2|A \cap B|}{|A|+|B|}
$$
Emphasizes overlap more strongly than Jaccard via the factor of 2.

### Overlap Coefficient
$$
O(A,B)=\frac{|A \cap B|}{\min(|A|,|B|)}
$$
Measures containment of the smaller set within the larger.

## When to use
- Binary representations (set membership).
- Fast lexical baselines (keyword-like matching).
- Cases where containment is meaningful (Overlap coefficient).

## Limitations
- Ignores term frequency and informativeness unless extended to weighted variants.
- Sensitive to synonymy and vocabulary mismatch; motivates weighted and latent approaches (e.g., [[TF–IDF]], [[Latent Semantic Analysis (LSA)]]).
