**Tags:** #concept #nlp #sentiment
**Related:** [[Sentiment Analysis]], [[Aspect-Based Sentiment Analysis]]

## Definition

Opinion Mining is the automated extraction of opinions, sentiments, and subjective information from text. The canonical output is a tuple: *(entity, aspect, sentiment, opinion holder, time)*.

> [!info] Key Intuition
> An opinion is always about something (entity/aspect) expressed by someone — reducing text to just a polarity score discards most of the actionable information.

## Core Structure

The five-tuple representation:
- **Entity** — the target object (e.g., a product, person, organisation)
- **Aspect** — the specific feature of the entity (e.g., battery life, camera)
- **Sentiment** — polarity or emotion (positive / negative / neutral; or a valence score)
- **Opinion holder** — who expressed the opinion
- **Time** — when it was expressed

Opinion mining tasks are typically decomposed into:
1. **Subjectivity detection** — is the text even expressing an opinion?
2. **Polarity classification** — positive, negative, or neutral?
3. **Aspect extraction** — what feature is the opinion about?
4. **Holder identification** — who holds the opinion?

> [!example]- Worked Example
> Sentence: *"The battery life on this phone is terrible but the camera is stunning."*
> - Entity: *phone*
> - Aspects: *battery life* (negative), *camera* (positive)
> - Holder: implicit (the reviewer)
> A document-level classifier would output "mixed" and lose the per-aspect signal entirely.

## Significance

Opinion mining underpins review analysis, brand monitoring, political polling, and product feedback aggregation. Its value lies precisely in structured extraction — not just aggregate polarity.
