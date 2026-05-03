**Tags:** #concept #nlp #sentiment
**Related:** [[Sentiment Analysis]], [[Sentiment Triple]], [[Aspect-Based Sentiment Analysis]]

## Definition

An opinion is formally described as a quintuple

$$(e, a, s, h, t)$$

where

- $e$ — the **target entity** the opinion is about
- $a$ — the **aspect** of that entity
- $s$ — the **sentiment** expressed toward the aspect
- $h$ — the **opinion holder**
- $t$ — the **time** of expression

> [!info] Key Intuition
> Sentiment is **relational**: it is not a property of words but of someone expressing an evaluation about something at a particular moment. The quintuple makes this dependency explicit.

## How the Quintuple Is Used

The general goal of sentiment analysis is to recover quintuples from text. Operationally, this involves:

- identifying entities and grouping synonymous references;
- extracting aspects of those entities;
- detecting opinion holders;
- identifying temporal information;
- assigning a sentiment label or score;
- reconstructing complete opinion structures;
- extracting reasons and qualifiers.

## The Standard Simplification

In most introductory and applied work, the quintuple is collapsed into **document-level polarity classification**. This implicitly assumes:

- each document expresses one dominant opinion,
- about one entity,
- by one holder.

This is reasonable for product reviews and individual social-media posts but breaks down for political speeches, multi-aspect reviews, or any discourse where multiple opinions interact.

> [!warning] Common Misconception
> A document-level positive label does not mean every aspect is praised. *"Camera is great but battery is awful"* gets a single label that erases the structural information the quintuple is designed to preserve. This is the gap [[Aspect-Based Sentiment Analysis]] fills.

## Significance

The quintuple is the formal target. Every modelling choice — from lexicon scoring to Naïve Bayes to neural classifiers — corresponds to predicting some subset of $(e, a, s, h, t)$, usually just $s$. Knowing the full structure clarifies what is being abstracted away.
