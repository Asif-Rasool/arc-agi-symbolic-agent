---
title: "Examples"
---

## 0520fde7: Separator-Based Boolean Composition

![Problem 0520fde7](../images/example-0520fde7.png)

In problem `0520fde7`, the first thing I noticed was the vertical separator. It divides the input into two aligned panels, and the output is much smaller than the input. The task looked less like object movement and more like a comparison between the two sides.

The agent framed the task the same way. Feature extraction detected the separator and the compressed output, so retrieval favored panel-composition concepts. The successful concept family was `SplitBoolean`.

`SplitBoolean` treats the two sides as aligned masks and searches for a cell-by-cell Boolean relationship. The solution worked because one comparison rule explained every visible training output, even though the final pattern changed across examples.

The example shows the value of structural cues. A clean separator gave the agent a strong reason to compare regions instead of searching through unrelated transformations.

## 62c24649: Generative Symmetry from a Small Seed

![Problem 62c24649](../images/example-62c24649.png)

In problem `62c24649`, I noticed that the output grows from a small seed into a larger, regular design. Cropping and recoloring were not enough to explain that behavior. The important clue was the symmetry of the generated output.

The agent framed the task as generative because the output was larger than the input. Retrieval then favored concepts that could build a structured output from a compact starting pattern. The concept family that solved it was `QuadrantMirror`.

The fitted hypothesis treated the input as a seed, mirrored it across horizontal and vertical axes, and placed the copies into a larger arrangement. The solution worked because the same symmetric construction explained all visible examples.

The example matters because it shows that the agent was not limited to extracting or recoloring existing objects. It could also generate a larger structured output when the transformation had a clear symbolic form.

## e9b4f6fc: Legend-Guided Extraction and Recoloring

![Problem e9b4f6fc](../images/example-e9b4f6fc.png)

In problem `e9b4f6fc`, I noticed two things at once: a main multicolor object and small detached color pairs elsewhere in the grid. The detached pairs looked like a legend, not background noise.

The agent framed the task as extraction plus recoloring. Plain cropping was not enough, and plain recoloring was not enough. The successful concept family was `LegendPairRecolorExtract`.

The fitted explanation selected the main object, read the detached pairs as a source-to-target color map, cropped the relevant region, and applied the mapping. The solution worked because the same "read the legend, then recolor the object" procedure fit the visible examples.

The example shows why concept families and ranking became important. Several legend interpretations can look plausible. The final agent succeeded because the selected explanation aligned the object choice, extraction behavior, and recoloring logic at the same time.
