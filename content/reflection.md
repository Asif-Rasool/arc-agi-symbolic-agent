---
title: "Reflection"
---

## Development Lessons

I started the project with the idea that ARC tasks should be solved through explicit symbolic explanations. Early versions mostly used direct rules for recognizable patterns: rigid transforms, crops, recoloring, and simple panel operations.

Rule matching became brittle as the benchmark grew harder. Many tasks supported more than one local interpretation, and some visible examples allowed a rule to fit for the wrong reason. The agent needed a way to search through explanations and compare them before committing to an answer.

Over time, the project became symbolic hypothesis search. Feature extraction gave the agent a structural view of the task. Concept retrieval narrowed the search. Hypothesis fitting produced concrete explanations. Validation tested them. Ranking decided which explanations deserved trust. Repairs explored nearby variants when the broad idea looked right and one symbolic choice looked fragile.

Keeping multiple hypotheses alive improved robustness. Exact visible matches still mattered, and I learned to treat them as one signal within a broader reasoning process. Several explanations can fit the visible examples, especially when the training pairs leave some ambiguity. Ranking mattered because the agent needed to prefer the explanation that fit the examples and made sense for the task structure.

Repairs also changed how I thought about failures. A center, path route, symmetry mode, frame choice, or legend mapping could be slightly wrong even when the broader concept family was right. Repair gave the agent a controlled way to revise a nearly correct explanation.

## Connection to Human Cognition

When I solve ARC tasks by hand, I usually start by looking for the important structure. I ask whether the task is about objects, separators, symmetry, color roles, repeated patterns, cropping, counting, or transformations. I do not inspect every cell as if every location matters equally.

The agent mirrors that broad strategy in a limited way. It extracts structural cues, retrieves plausible concept families, fits explanations, tests them against the visible examples, ranks the strongest candidates, and tries repairs when an explanation is nearly right.

The connection to human cognition is strongest in the process: abstraction, analogy, hypothesis generation, hypothesis testing, attention to salient objects and relations, and revision when a first explanation almost works. Those are the parts of human problem solving I wanted the agent to approximate at a symbolic level.

The connection has clear limits. A human can reframe a problem much more flexibly. I might first see a task as object manipulation, then realize it is driven by a color key, a global symmetry, or a relation between regions. My agent can only search within the concept families and repair rules I implemented.

Case-based reasoning fits here in a careful way. The agent uses within-problem analogy to compare explanations inside the current task. Its case memory is local to one problem, so it supports ranking among related candidates rather than long-term learning across ARC tasks.

## What Debugging Taught Me

Working on the agent changed how I thought about knowledge-based AI. Encoding knowledge as rules was only the starting point. The harder part was organizing those rules so the agent could choose, compare, and revise explanations.

Interpretability mattered because it let me debug the reasoning process. When the agent failed, I could ask whether it read the wrong structure, retrieved the wrong concept family, fitted the wrong parameter, ranked the wrong explanation, or repaired around the wrong starting point.

That kind of debugging felt closer to how I analyze my own mistakes on ARC tasks. I can usually tell whether I missed the relevant object, chose the wrong abstraction, overfit a visible example, or trusted the wrong cue. The agent gave me a narrower version of that same diagnostic loop.

## Remaining Gap

Flexible abstraction remains the biggest gap. Humans can change representations when the first interpretation fails. My agent searches through the concepts and repairs I gave it.

Better object selection is another clear next step. The failure cases showed that choosing the right broad transformation still fails when the agent selects the wrong center, object, or cue.

Future work would need stronger grouping, better distractor rejection, and more flexible representation switching. Adding more concept classes would help only if the agent also became better at deciding what should count as the important structure in the first place.
