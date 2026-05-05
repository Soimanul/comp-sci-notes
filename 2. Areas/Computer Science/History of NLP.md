**Tags:** #topic #nlp #history 
**Related:** [[ELIZA]], [[The ELIZA Effect]], [[Symbolic view of language]]

## The Dawn of Computational Linguistics
Early Natural Language Processing (NLP) focused on **Symbolic Systems**. Researchers attempted to explicitly program the rules of language and the world into computers.

## Key Eras
1. **Symbolic Era (1950s - 1980s):**
    - Approached language as a logical, rule-based system.
    - Relied on manually crafted grammars and knowledge bases.
    - **Assumptions:** Language is a formal structure; meaning can be decomposed into symbols and logical relationships.
    - **Limitations:** Brittle; could not handle ambiguity or the vast complexity of real-world context.
        
2. **Statistical Era (1990s - 2010s):**
    - Shifted to probabilistic models (e.g., Hidden Markov Models).
    - Focus on "likely" sequences rather than "correct" rules.
        
3. **Neural/Deep Learning Era (2010s - Present):**
    - Use of dense vector representations (Embeddings) and Transformers.
        

## Seminal Systems

- **[[ELIZA]] (1966):** The first chatbot, simulating a Rogerian psychotherapist.
- **SHRDLU (1970):** A system that understood language within a "blocks world" micro-universe.

---

## Self-Test

> [!question] Hard Multiple Choice — 22 Questions
> Cover yourself, pick an answer, then expand the spoiler. Aim for ≥18/22 before moving on.

**1.** A 1968 system rejects the sentence *"Colorless green ideas sleep furiously"* as ungrammatical. Which era's assumptions does this most clearly violate?
- A. Statistical era — the n-gram probability is high
- B. Symbolic era — Chomsky himself used it to show syntax can be well-formed yet semantically empty
- C. Neural era — embeddings would map it near nonsense
- D. Connectionist era — backprop would assign it low loss

> [!success]- Answer
> **B.** The sentence is the textbook example that syntax-only systems accept; rejecting it means the system is conflating syntax with semantics, which the symbolic tradition explicitly tried to keep separate.

**2.** ELIZA's DOCTOR script worked best as a Rogerian therapist specifically because Rogerian therapy:
- A. Uses a fixed clinical vocabulary that's easy to pattern-match
- B. Reflects the patient's statements back as questions, masking the lack of world knowledge
- C. Was the only therapeutic style Weizenbaum was trained in
- D. Requires the therapist to interpret dreams symbolically

> [!success]- Answer
> **B.** The non-directive style means a competent therapist *should* mostly mirror — so ELIZA's deflection looked clinically appropriate rather than evasive.

**3.** Which scenario is the *purest* modern instance of the ELIZA Effect?
- A. A user double-checks GPT-4's citations and finds half are fabricated
- B. A developer benchmarks two LLMs on MMLU
- C. A user thanks ChatGPT and feels guilty about being rude to it
- D. A linguist criticizes BERT for lacking compositionality

> [!success]- Answer
> **C.** Anthropomorphizing a stateless text-predictor to the point of moral concern is the effect Weizenbaum warned about; the others are critical evaluations, not anthropomorphism.

**4.** Turing's 1950 paper deliberately avoided defining "thinking." The *methodological* point of this move was to:
- A. Sidestep dualism and replace an unanswerable question with a measurable one
- B. Hide the fact that he had no theory of mind
- C. Privilege behaviorist psychology over cognitive science
- D. Ensure machines could never pass

> [!success]- Answer
> **A.** Turing's whole rhetorical strategy was operationalization — swap "Can machines think?" for "Can they imitate?" because the latter is decidable.

**5.** SHRDLU appeared genuinely intelligent in 1970 mainly because:
- A. It used a primitive transformer
- B. Its world was small enough that hand-coded semantics covered every possible reference
- C. It learned from a corpus of physics textbooks
- D. It could pass the Turing Test reliably

> [!success]- Answer
> **B.** The blocks world had a closed ontology (a few shapes, colors, spatial relations); within those bounds full symbolic grounding was tractable. Outside it, the approach didn't scale.

**6.** A statistical-era POS tagger and a symbolic-era POS tagger both fail on *"Time flies like an arrow."* The failures differ because:
- A. The statistical tagger picks the *most frequent* parse; the symbolic tagger refuses to commit to one
- B. Both produce identical errors — the era doesn't matter
- C. The symbolic tagger is faster but wrong; the statistical one is slower but right
- D. The statistical tagger over-fits training data; the symbolic one over-fits hand-written rules

> [!success]- Answer
> **A.** The hallmark statistical-era move is "pick the likeliest" — even when wrong, it commits. Symbolic systems often produced multiple valid parses with no way to choose.

**7.** Which property is **least** characteristic of the symbolic era?
- A. Brittleness on unseen input
- B. Hand-crafted grammars
- C. Distributed representations
- D. Explicit ontologies

> [!success]- Answer
> **C.** Distributed representations (embeddings) are the signature of the neural era; the symbolic era used discrete, localist symbols.

**8.** Searle's Chinese Room is a direct counter-argument to which claim?
- A. Neural networks can scale
- B. Passing the Turing Test demonstrates genuine understanding
- C. Statistical models outperform symbolic ones
- D. The ELIZA Effect is harmless

> [!success]- Answer
> **B.** Searle grants the imitation but argues syntax-shuffling never produces semantics — so the test conflates simulation with cognition.

**9.** Why did HMM-based taggers (statistical era) outperform rule-based taggers despite being "dumber" about language?
- A. They had access to GPUs
- B. Probabilistic smoothing handled ambiguity gracefully where rules collided
- C. They used pre-trained word embeddings
- D. They incorporated WordNet by default

> [!success]- Answer
> **B.** Rules conflict on ambiguous input and offer no principled tiebreaker; HMMs fall back on data-driven priors.

**10.** Weizenbaum became a critic of AI partly because his own secretary asked him to *leave the room* while she "talked" to ELIZA. The deeper lesson he drew was:
- A. ELIZA needed better pattern coverage
- B. The danger isn't that machines fool us — it's how willingly we let them
- C. Therapists should be replaced by chatbots
- D. Pattern matching is a sufficient theory of mind

> [!success]- Answer
> **B.** Weizenbaum's *Computer Power and Human Reason* (1976) emphasized human projection, not machine capability, as the ethical problem.

**11.** The Turing Test's original 30%-after-5-minutes pass condition is best read as:
- A. A statistical confidence threshold
- B. A loose 50-year prediction, not a strict pass mark
- C. The Bayes-optimal decision boundary
- D. A Cohen's kappa value

> [!success]- Answer
> **B.** Turing offered it as a forecast for the year 2000, not a formal criterion — popular accounts often hardened it into a rule it was never meant to be.

**12.** Which transition best describes moving from the symbolic to the statistical era?
- A. From "what is correct?" to "what is likely?"
- B. From "what is likely?" to "what is correct?"
- C. From neural networks to logic programming
- D. From transformers to expert systems

> [!success]- Answer
> **A.** The era's defining shift was epistemic: replace prescriptive rules with probability distributions over data.

**13.** A modern LLM still inherits a structural weakness from ELIZA. Which one?
- A. Reliance on regex
- B. Inability to produce grammatical output
- C. Producing fluent text without grounded semantic commitment
- D. Limited to English

> [!success]- Answer
> **C.** ELIZA showed that fluency ≠ understanding. LLMs are vastly more sophisticated but the gap between surface coherence and grounded reference is the same family of problem.

**14.** "Language is decomposable into symbols and logical relationships." This assumption underwrites which era?
- A. Neural
- B. Statistical
- C. Symbolic
- D. Connectionist

> [!success]- Answer
> **C.** It's the founding compositional premise of the symbolic tradition — meaning is built from atoms by combinatorial rules.

**15.** Why is brittleness the *predictable* failure mode of rule-based systems, not just bad luck?
- A. Because rules are written in LISP
- B. Because rule sets cannot enumerate the long tail of natural-language phenomena
- C. Because hardware in the 1970s was slow
- D. Because Chomsky's grammars were incomplete

> [!success]- Answer
> **B.** Natural language has a heavy-tailed distribution of constructions; any finite rule set leaves vast uncovered territory.

**16.** SHRDLU and ELIZA both used symbolic methods, but only SHRDLU could *answer questions about its world.* The difference is:
- A. ELIZA had a knowledge base; SHRDLU did not
- B. SHRDLU had a model of its (tiny) world; ELIZA had none
- C. SHRDLU was probabilistic
- D. ELIZA used reinforcement learning

> [!success]- Answer
> **B.** SHRDLU maintained a state representation of the blocks world and could reason over it; ELIZA had no model whatsoever — only string transformations.

**17.** Which of these claims would Turing himself most likely endorse?
- A. A machine that cannot feel cannot be said to think
- B. The interesting question is behavioral, not metaphysical
- C. Symbol manipulation is sufficient for consciousness
- D. Imitation is identical to understanding

> [!success]- Answer
> **B.** Turing's whole framing was operational: shift from metaphysics to behavior. C and D are stronger claims he did *not* commit to.

**18.** Why did the neural era *not* simply replace the statistical era's mathematics?
- A. It abandoned probability entirely
- B. It kept probabilistic objectives (cross-entropy, MLE) but learned representations end-to-end
- C. It returned to hand-crafted features
- D. It used only deterministic symbolic logic

> [!success]- Answer
> **B.** Neural NLP is statistical NLP with learned features — the loss functions and likelihood framing carry over; what changed is where the features come from.

**19.** A user reports that a chatbot "really understood my grief." From an NLP perspective, the most defensible technical reading is:
- A. The bot solved the Chinese Room
- B. The bot's outputs activated the ELIZA Effect — fluency was read as empathy
- C. The bot has theory of mind
- D. The bot passed the Turing Test for the user

> [!success]- Answer
> **B.** D is tempting but the Turing Test is adversarial; this user wasn't trying to detect a machine. B names the specific phenomenon: anthropomorphic projection onto coherent text.

**20.** Which of the following is the *strongest* historical reason the symbolic era stalled?
- A. Lack of compute
- B. Combinatorial explosion of rules required to cover real-world ambiguity
- C. Absence of GPUs
- D. Loss of funding to robotics

> [!success]- Answer
> **B.** Compute mattered, but the deeper issue was that scaling rule sets to cover language's variability is super-exponential — a structural, not hardware, limit.

**21.** Which pair correctly matches a system to its underlying technique?
- A. ELIZA — Hidden Markov Models
- B. SHRDLU — Transformer attention
- C. ELIZA — Pattern matching with substitution
- D. SHRDLU — Pure pattern matching

> [!success]- Answer
> **C.** ELIZA's mechanism was keyword-driven decomposition + reassembly templates. SHRDLU additionally used a procedural semantic model.

**22.** A student says: *"GPT-4 has passed the Turing Test, so it understands language."* The cleanest single objection is:
- A. GPT-4 has not been tested
- B. The Chinese Room: behavioral indistinguishability is compatible with the absence of understanding
- C. GPT-4 fails on math
- D. The Turing Test requires speech, not text

> [!success]- Answer
> **B.** The student conflates a behavioral benchmark with a semantic claim — exactly Searle's target. The other options either dodge or are factually weak.