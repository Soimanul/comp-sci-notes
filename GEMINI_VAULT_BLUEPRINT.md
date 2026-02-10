# Vault Blueprint: PARA + Atomic Knowledge

This document defines the structural policies and formatting standards for this Obsidian vault. It is modeled after the **Natural Language Processing** course structure, which serves as the gold standard for organization and clarity.

## 1. PARA Map & Naming Rules

- **1. Projects**: Active courses.
  - **Naming**: `Y[Year]S[Semester] - [Course Name]` (e.g., `Y3S2 - Natural Language Processing`).
  - **Contents**: A single Course Landing Page.
- **2. Areas**: Reusable, source-independent atomic notes and hubs.
  - **Naming**: Title Case (e.g., `Binary Search`, `TF–IDF`).
  - **Contents**: The core knowledge engine of the vault.
- **3. Resources**: Source-bound materials (PDFs, raw lecture notes, external summaries).
  - **Contents**: Notes that track specific sessions or documents before they are distilled into Areas.
- **4. Archives**: Completed courses or projects no longer in active use.

## 2. Note Type Catalog

### Course Landing Page (Projects)
- **Role**: Purely organizational. Does not explain concepts.
- **Format**:
```markdown
**Status:** #active
**Semester:** Y3S2

---
# Knowledge Map
## Module [N]: [Module Name]
### Session [N]: [Session Anchor Link]
- [[Concept 1]]
- [[Concept 2]]
```

### Session Anchor / Hub Note (Areas)
- **Role**: Bridges high-level topics to atomic concepts. Provides narrative context and clear navigation.
- **Format**:
```markdown
**Tags:** #topic #hub #[subject]
**Related:** [[Course Landing Page]], [[Parent Hub]]

## Overview
[One paragraph explaining the scope of this hub. No explaining of concepts.]

## Knowledge Map
### 1. [[Sub-topic or Hub]]
- [[Atomic Concept 1]]
- [[Atomic Concept 2]]

### 2. [[Another Sub-topic]]
- [[Atomic Concept 3]]
```

### Atomic Concept Note (Areas)
- **Role**: Answers one clear question. Written for future-me.
- **Format**:
```markdown
**Tags:** #concept #[domain]
**Related:** [[Sibling Concept]], [[Parent Hub]]

## Definition
[Concise, stable definition.]

## [Core Mechanics/Explanation]
[The "How" or "Why". Use LaTeX for math.]

## [Examples/Visuals]
![[Image.png]]

## Significance
[Why this matters in the broader context.]
```

## 3. Linking & Canonical Concept Policy

- **Single Source of Truth**: There is exactly ONE canonical note per concept in `2. Areas`. 
- **Merge, Don't Duplicate**: If a new course introduces a concept already present (e.g., "Perceptron"), the new insights are merged into the existing note under a `## Perspectives from Courses` or similar section if specific context is needed.
- **Semantic Linking**: Links should represent relationships (e.g., `Related:`, `Advantage:`, `Issue:`).
- **Navigation**: 
  - Landing Page $
ightarrow$ Session Anchor $
ightarrow$ Atomic Concept.
  - Atomic Concepts link to each other and back to their Hubs.

## 4. Quality Standards

- **Atomic**: One note = one cognitive load.
- **Context-Free**: Written so it can be understood without knowing which course it came from.
- **Organizational Landing Pages**: No explanation text on landing pages; keep them as clean maps.
- **Formatting**: No top-level H1 (Title is file name). Use H2 for primary sections. Use Title Case for all file names.

---
*Blueprint generated on 2026-02-04. Enforced by Gemini.*