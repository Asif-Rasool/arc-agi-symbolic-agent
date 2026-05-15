---
title: "Architecture"
---

## System Structure

![High-level ARC-AGI agent architecture](../images/architecture.png)

The implementation in `ArcAgent.py` follows the same reasoning loop described in the approach page. I tried to keep the major pieces separate so I could debug the agent by asking where a candidate explanation entered, passed, ranked, or failed.

`FeatureExtractor` reads the training pairs and builds a `ProblemFeatures` object. The object is the agent's compact description of the task: shapes, colors, background behavior, separators, component counts, density, and other structural cues. The goal is to give the rest of the system a useful frame before any concept tries to solve the task.

`ProblemClassifier` uses those features to form a coarse judgment about the problem. It does not decide the answer. It helps the agent decide whether the task looks more like extraction, composition, shape preservation, generation, or object-relational reasoning.

`ConceptRegistry` then selects concept families whose applicability scores are positive for the current problem. Each symbolic concept class inherits from `Concept` and knows how to fit one kind of explanation. Some concepts are narrow, such as a direct crop or color mapping. Others generate several variants because the broad idea can appear in more than one form.

When a concept fits, it produces a `FittedConcept`. The fitted object is the actual explanation the agent can test and apply. It contains the chosen parameters and a deterministic prediction routine.

`Validator` checks fitted hypotheses against the visible training pairs. Exact fits become the strongest candidates. Near misses are still useful because they may preserve the right abstraction with one local choice wrong.

`Ranker` orders the candidates after validation. It uses visible fit, residual error, confidence, complexity, and structural agreement with the problem frame. `CaseMemory` adds a small within-problem analogy signal so structurally similar explanations can support each other during ranking.

## Concept Families

The symbolic concept classes are the agent's knowledge base. They cover rigid transforms, crops, recoloring, Boolean panel logic, symmetry, object movement, paths, legends, frames, motif completion, center connections, enclosure repair, and other visual patterns from the benchmark.

The most important change was moving from single rules to concept families. A family lets the agent keep the broad explanation while testing several parameterizations. The shift mattered for tasks where the right idea was clear but the exact local choice was fragile.

## Ranking and Repair

The architecture works because fitting is not the final decision. Several explanations can fit the visible examples, and some can fit for the wrong reason. Ranking gives the agent a way to compare them using more than exact training accuracy.

Repair generation adds one more layer of search. If a candidate has the right family but one brittle choice, the agent can vary that choice in a controlled way. Center repairs may vary anchors or row-versus-column linking. Legend repairs may vary the selected object or mapping. Spiral repairs may vary path parameters. The repairs are still symbolic, so they remain inspectable.
