---
title: "Failure Analysis"
---

The most useful failures happened when my agent found the right broad concept family but failed on a local symbolic choice.

## 28e73c20: Brittle Spiral Generation

![Problem 28e73c20](../images/failure-28e73c20.png)

Problem `28e73c20` was useful because the agent got the broad idea right. The input is almost empty, and the output is a spiral-like enclosure. Feature extraction and retrieval correctly pushed the task toward `SpiralGenerator`.

The reasoning broke inside the family. Several spiral variants can fit the visible examples. They can differ in turn direction, start location, corridor width, or wall interpretation while still looking reasonable on the training cases.

One selected variant fit the visible examples but did not generalize to the hidden case. The miss taught me that underconstrained generative tasks need stronger ways to rank parameterizations.

## 60a26a3e: Center Selection Under Distractors

![Problem 60a26a3e](../images/failure-60a26a3e.png)

Problem `60a26a3e` also reached the right broad family. The task is about choosing diamond centers and connecting them with blue lines. The top concept families, `ConnectDiamondCenters` and `CenterConnectionLibrary`, matched that high-level structure.

Anchor selection caused the failure. Once the agent chose the wrong center, the connection rule did exactly what it was designed to do, but from the wrong starting point. Repair generation could vary row-only or column-only linking and gap settings, while every repair still inherited the bad center choice.

The miss taught me that object selection is a separate problem from transformation selection. The agent can choose the right family and still fail if its perception of the relevant objects is too narrow. Better grouping, distractor rejection, and center selection would matter as much as adding more transformation rules.
