---
title: "Approach"
---

## Core Idea

I designed the agent around one central idea: solve each task by searching for an explicit symbolic explanation. Each fitted hypothesis has parameters and a deterministic `predict()` routine.

I start each task by asking what structure is visible in the examples. The agent measures grid shapes, colors, backgrounds, component counts, density, separators, and how the output size relates to the input. The measurements narrow the explanations worth trying.

## Pipeline

I ended up with this pipeline:

**Feature extraction → concept retrieval → hypothesis fitting → training validation → ranking → targeted repair generation → final prediction selection.**

Feature extraction gives the agent a first read on the problem. A smaller output points toward extraction. A separator points toward panel composition. A larger regular output points toward generative symmetry or pattern construction.

Concept retrieval uses that first read to choose a smaller set of symbolic concept families. I found concept families useful because many ARC tasks share a broad idea while changing local details. A center-connection problem, for example, may require the same high-level reasoning even when the exact anchors or path choices vary.

Hypothesis fitting turns broad families into concrete explanations. For a symmetry task, the agent tries specific symmetry hypotheses with specific parameters. The same idea applies to crops, recoloring, Boolean panel operations, legend-guided extraction, paths, frames, and object relations.

Training validation checks fitted hypotheses against the visible examples. Exact matches matter. Near misses also matter when they contain the right idea with one wrong symbolic choice, so I kept some of them available for ranking and repair.

Ranking became the bridge between fitting and prediction. I used the ranker to weigh training error, confidence, complexity, structural fit, and local analogy within the current problem. Its job is to prefer explanations that both match the visible examples and make sense for the kind of task the agent appears to be solving.

Targeted repair generation came later. Some hypotheses had the right broad idea but failed because of one local decision, such as a center choice, symmetry mode, path route, frame interpretation, or legend mapping. Repairs let the agent search nearby variants within the same concept family.

Final prediction selection uses the strongest exact, repaired, and near-miss candidates to return up to three distinct predictions. I wanted the outputs to represent meaningful alternatives.

## Why Symbolic Search

I chose symbolic search because ARC problems reward explanation. I wanted to know why a particular answer was chosen and how the same reasoning applied across examples.

The tradeoff is clear. The agent searches over the concepts I gave it, and the search is readable. I can inspect which concept was retrieved, which parameters were fitted, which examples passed validation, why one candidate outranked another, and where a failure began.
