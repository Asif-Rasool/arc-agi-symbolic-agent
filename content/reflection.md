---
title: "Reflection"
description: "Development lessons and comparison with human reasoning."
---

## Development Lessons

I started the project with the idea that ARC tasks should be solved through explicit explanations. At first, that mostly meant writing direct symbolic rules for recognizable patterns: rigid transforms, crops, recoloring, and simple panel operations.

Rule matching was not enough. Many tasks looked compatible with more than one local pattern, and some visible examples allowed a rule to fit for the wrong reason. As the benchmark became harder, the agent needed to search over explanations rather than jump from a problem to one stored trick.

The project gradually became symbolic hypothesis search. Feature extraction gave the agent a structural view of the task. Concept retrieval narrowed the search. Hypothesis fitting produced concrete explanations. Validation tested them. Ranking decided which explanations deserved trust. Repairs explored nearby variants when the broad idea looked right but one symbolic choice was wrong.

Keeping multiple hypotheses alive improved robustness. Exact visible matches were still important, but I learned not to treat them as the whole story. Several explanations can fit the visible examples, especially when the training pairs leave some ambiguity. Ranking mattered because the agent needed to prefer the explanation that fit both the examples and the structure of the task.

Repairs helped with brittleness. If a center, path route, symmetry mode, frame choice, or legend mapping was slightly wrong, a repaired candidate could sometimes recover without discarding the original concept family.

## Human Comparison

Working on the agent also changed how I thought about knowledge-based AI. The most valuable part was not only encoding knowledge as rules. The harder part was organizing those rules so the agent could choose, compare, and revise explanations.

Interpretability made debugging possible. When the agent failed, I could inspect whether the wrong concept was retrieved, the wrong parameters were fitted, the validator was too strict, the ranker preferred the wrong explanation, or repair was searching around the wrong starting point.

## Remaining Gap

The remaining gap is flexible abstraction. A human can reframe a task when the first representation feels wrong. The agent can only search within the concepts and repair rules I implemented.

Better object selection is another clear next step. The failure cases showed that choosing the right broad transformation is not enough if the agent selects the wrong center, object, or cue. Future work would need stronger grouping and distractor rejection, not just more concept classes.
