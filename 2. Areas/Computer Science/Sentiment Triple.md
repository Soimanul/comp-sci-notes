**Tags:** #concept #nlp #sentiment
**Related:** [[Sentiment Analysis]], [[Opinion Quintuple]]

## Definition

A sentiment can be conceptualised as a triple

$$(y, o, i)$$

capturing three dimensions:

- $y$ — **emotion type** (anger, joy, fear, …)
- $o$ — **polarity** (positive, negative, or neutral)
- $i$ — **intensity** (how strongly it is expressed)

> [!info] Key Intuition
> "Sentiment" is not a single number. It is at minimum a category, a sign, and a magnitude. Most production systems predict only $o$, treating $y$ and $i$ as optional extensions.

## Emotion Taxonomies

A widely accepted basic-emotion classification (Ekman-style) includes **anger, disgust, fear, joy, sadness, surprise**. More recent work suggests consolidation into four fundamental emotions by grouping related pairs.

The "rational vs emotional" sentiment distinction is sometimes used in computational settings, though modern neuroscience treats reason and emotion as deeply intertwined.

## Significance

The triple makes explicit what most classifiers silently collapse: distinguishing $o$, $y$, and $i$ is what separates **polarity classification** from **emotion detection** from **intensity prediction**. It also explains why the [[Sentiment Lexicons]] catalogue differs along these axes — Bing encodes only $o$, AFINN adds $i$, NRC adds $y$.
