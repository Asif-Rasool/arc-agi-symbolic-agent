---
title: "Approach"
description: "How the symbolic solver frames ARC tasks as interpretable hypothesis search."
---

## Core Idea

I designed the agent around one central idea: solve each task by searching for an explicit explanation. A candidate answer is not an opaque score or a learned embedding. It is a symbolic hypothesis with parameters and a deterministic `predict()` routine.

The agent starts by trying to understand the structure of the task. It measures grid shapes, colors, backgrounds, component counts, density, separators, and how the output size relates to the input. The measurements do not solve the problem by themselves, but they help the agent decide what kind of explanation is worth trying.

## Pipeline

The final pipeline is:

**Feature extraction -> concept retrieval -> hypothesis fitting -> training validation -> ranking -> targeted repair generation -> final prediction selection.**

Feature extraction gives the agent a first read on the problem. If an output is smaller than the input, extraction becomes more plausible. If a separator divides the grid into panels, composition becomes more plausible. If the output grows into a larger regular pattern, the agent should consider generative symmetry or pattern construction.

Concept retrieval uses that first read to choose a smaller set of symbolic concept families. I found that families were more useful than one-off rules because many ARC tasks share a broad idea but differ in local details. A center-connection problem, for example, may require the same high-level reasoning even when the exact anchors or path choices vary.

Hypothesis fitting turns those broad families into concrete explanations. Instead of asking whether a task is "about symmetry" in general, the agent tries specific symmetry hypotheses with specific parameters. The same pattern holds for crops, recoloring, Boolean panel operations, legend-guided extraction, paths, frames, and object relations.

Training validation checks those fitted hypotheses against the visible examples. Exact matches matter, but I learned that exact matching alone was not enough. A near miss can still contain the right idea with one wrong symbolic choice. Throwing it away too early made the agent brittle.

Ranking became the bridge between fitting and prediction. The ranker weighs training error, confidence, complexity, structural fit, and local analogy within the current problem. Its job is to prefer explanations that both match the visible examples and make sense for the kind of task the agent thinks it is solving.

Targeted repair generation came later. Some hypotheses clearly had the right broad idea but failed because of one local decision, such as a center choice, symmetry mode, path route, frame interpretation, or legend mapping. Repairs let the agent search nearby variants without abandoning the concept family.

Final prediction selection takes the strongest exact, repaired, and near-miss candidates and returns up to three distinct predictions. I wanted the outputs to represent meaningful alternatives rather than tiny variations of the same guess.

## Why Symbolic Search

I chose symbolic search because ARC problems reward explanation. A black-box model might produce an answer, but I wanted to know why a particular answer was chosen and how the same reasoning applied across examples.

The tradeoff is clear. The agent can only search over the concepts I gave it. At the same time, the search is readable. I can inspect which concept was retrieved, which parameters were fitted, which examples passed validation, why one candidate outranked another, and where a failure began.
