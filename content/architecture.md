---
title: "Architecture"
---

## System Structure

![High-level ARC-AGI agent architecture](../images/architecture.png)

I organized the agent as a reasoning pipeline. Each stage has a specific role: understand the task, narrow the search, test possible explanations, rank the strongest candidates, repair fragile choices, and generate final predictions.

The main design goal was inspectability. I wanted to know why an answer was chosen and where the reasoning failed when the answer was wrong.

## Reading the Task

The first stage gives the agent a compact view of the training examples. It looks at structural cues such as grid size, output size, colors, background color, object components, density, separators, and whether the output looks like a crop, a transformation, a generated pattern, or a composition of multiple regions.

This stage gives the rest of the system a better starting point. A separator suggests panel comparison, a smaller output suggests extraction, and a larger symmetric output suggests generative structure.

## Searching Through Concepts

After reading the task, the agent retrieves symbolic concept families that appear relevant. A concept family is a broad explanation type with room for local variation. Examples include cropping, recoloring, rigid transforms, panel composition, symmetry, object connection, legend-guided extraction, motif completion, and enclosure repair.

Concept families became an important shift in the project. A flat list of isolated rules was too brittle. Concept families let the agent keep the broad idea while testing different local choices inside that idea.

## Fitting Explanations

Once a concept family is selected, the agent tries to fit concrete explanations to the visible training pairs. A fitted explanation includes the transformation idea and the parameters needed to apply it.

For example, a panel-composition explanation may need to identify the separator, the two panels, the background color, the output color, and the Boolean relationship between the panels. A legend-guided explanation may need to identify the main object, read detached color pairs, infer a mapping, crop the object, and recolor it.

## Validating and Ranking

The agent tests each fitted explanation against the visible examples. Exact matches become strong candidates. Near misses can also be useful when they contain the right broad idea with one local choice wrong.

Ranking became important because several explanations can fit the same visible examples. The agent compares candidates using visible fit, structural agreement, simplicity, confidence, and local consistency within the same problem. The goal is to prefer the explanation that is correct on the examples and most likely to generalize to the test case.

## Repairing Fragile Candidates

Some failures came from one fragile symbolic choice: selecting the wrong center, choosing the wrong symmetry mode, routing a path incorrectly, or reading the wrong object as the target.

Targeted repair handles those cases by staying within a promising concept family and varying one local decision at a time. Repair gives the agent a controlled way to search nearby alternatives when the broad explanation looks right.

## Final Prediction Selection

The final stage selects up to three distinct predictions. I wanted those predictions to represent meaningful alternatives, not tiny variations of the same guess. The agent first prefers strong validated explanations, then considers repaired or near-miss candidates when they provide a plausible alternative.

The architecture made the agent easier to improve. When a task failed, I could usually tell whether the problem was task reading, concept retrieval, hypothesis fitting, ranking, repair, or object selection. Debugging became much more useful than simply knowing the final answer was wrong.
