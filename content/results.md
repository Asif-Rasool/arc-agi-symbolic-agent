---
title: "Results"
---

## Overall Performance

My final agent reached the following result on the CS7637 project benchmark:

| Metric | Result |
| --- | ---: |
| Visible training problems passed | 48 / 48 |
| Hidden test problems passed | 45 / 48 |
| Total problems passed | 93 / 96 |
| Visible training accuracy | 100% |
| Hidden test accuracy | 93.75% |
| Overall accuracy | 96.88% |
| Runtime | about 20 seconds |

Passing every visible training problem showed that the concept library covered the visible problem families in the benchmark. I care more about the hidden test score because it shows whether the explanations generalized beyond the examples I could inspect directly.

## Set-by-Set Results

| Set | Training | Hidden Test | Total |
| --- | ---: | ---: | ---: |
| B | 16 / 16 | 15 / 16 | 31 / 32 |
| C | 16 / 16 | 16 / 16 | 32 / 32 |
| D | 16 / 16 | 14 / 16 | 30 / 32 |

## Interpretation

Passing 45 of 48 hidden test problems suggests that the architecture generalized well within the course benchmark. Feature extraction, concept retrieval, validation, ranking, and repair worked together better than direct rule matching alone.

I read the score as evidence that the symbolic knowledge base and search procedure fit the CS7637 project benchmark well. The agent still depends on the concepts I implemented, so the result should stay in that benchmark context.

I found the hidden-test failures useful because they showed where the architecture was still narrow. One failure came from an underconstrained spiral-generation task. Another came from selecting the wrong center when distractors looked too similar to valid anchors. The misses helped me see the difference between choosing the right broad family and making the right local symbolic decision.

## Scope

I see the result as evidence that symbolic hypothesis search can be effective when the benchmark rewards explicit visual transformations. Open-ended ARC-AGI would require broader abstraction than this hand-built concept library provides.
