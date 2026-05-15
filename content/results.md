---
title: "Results"
description: "Verified course benchmark metrics and interpretation."
---

## Overall Performance

The final agent reached the following result on the CS7637 project benchmark:

| Metric | Result |
| --- | ---: |
| Visible training problems passed | 48 / 48 |
| Hidden test problems passed | 45 / 48 |
| Total problems passed | 93 / 96 |
| Visible training accuracy | 100% |
| Hidden test accuracy | 93.75% |
| Overall accuracy | 96.88% |
| Runtime | about 20 seconds |

The visible training score shows that the concept library covered the visible problem families in the benchmark. The hidden test score matters more to me because it shows whether the explanations generalized beyond the examples I could inspect directly.

## Interpretation

Passing 45 of 48 hidden test problems suggests that the architecture generalized well within the course benchmark. Feature extraction, concept retrieval, validation, ranking, and repair worked together better than direct rule matching alone.

The score does not mean the agent solves ARC-AGI generally. It means the symbolic knowledge base and search procedure fit this benchmark well. The agent still depends on the concepts I implemented, and it cannot invent a fundamentally new representation during a task.

The hidden-test failures were useful because they showed where the architecture was still narrow. One failure came from an underconstrained spiral-generation task. Another came from selecting the wrong center when distractors looked too similar to valid anchors. The misses helped me see the difference between choosing the right broad family and making the right local symbolic decision.

## Scope

I see the result as evidence that symbolic hypothesis search can be effective when the benchmark rewards explicit visual transformations. I do not see it as evidence that a hand-built symbolic library is enough for open-ended ARC-AGI.
