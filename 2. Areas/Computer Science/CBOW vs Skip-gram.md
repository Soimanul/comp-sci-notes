**Tags:** #concept #nlp #embeddings
**Related:** [[Word2Vec]], [[Word Embeddings]]

## Definition

CBOW (Continuous Bag-of-Words) and Skip-gram are the two Word2Vec architectures. CBOW predicts the centre word given surrounding context words; Skip-gram predicts surrounding context words given the centre word.

> [!info] Key Intuition
> CBOW averages context signals — fast and good for frequent words. Skip-gram treats each context word as a separate prediction task — slower but better for rare words and capturing fine-grained semantics.

## Core Mechanics

| Property | CBOW | Skip-gram |
|---|---|---|
| Input | context words | centre word |
| Target | centre word | each context word |
| Training speed | faster | slower |
| Rare word quality | weaker | stronger |
| Frequent word quality | comparable | comparable |

**CBOW**: average (or sum) input embeddings of context words → predict centre word via softmax.

**Skip-gram**: input embedding of centre word → for each context position, predict that word via softmax (or negative sampling).

Skip-gram with negative sampling (SGNS) is the most commonly used variant due to its strong performance on semantic similarity and analogy tasks.

> [!example]- Worked Example
> Sentence: *"the quick brown fox jumps"*, window = 1, centre = *"brown"*
> - CBOW: input = {*quick*, *fox*} → predict *brown*
> - Skip-gram: input = *brown* → predict *quick*, then predict *fox* (two separate updates)

> [!warning] Common Misconception
> CBOW is not simply "worse" than Skip-gram. For large datasets and frequent vocabulary, CBOW trains faster with comparable performance. The preference for Skip-gram applies specifically to rare words and smaller datasets.
