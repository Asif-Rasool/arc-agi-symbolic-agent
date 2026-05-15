---
title: "Home"
---

## Project Overview

I built the ARC-AGI Symbolic Reasoning Agent as a way to explore how far an explicit, knowledge-based solver could go on abstract visual reasoning tasks. The project was developed for Georgia Tech's CS7637 Knowledge-Based AI course.

My starting point was simple: ARC tasks should be solved by looking for explanations, not by guessing outputs directly. I wanted the agent to ask what kind of structure the examples contain, what transformation might explain that structure, and whether the same explanation works across every visible training pair.

I chose symbolic reasoning because I wanted the system's answers to be inspectable. When the agent makes a prediction, I can trace it back to a concept family, a fitted hypothesis, a validation result, and a ranking decision. When it fails, I can usually see where the reasoning broke.

Early versions were closer to direct rule matching. Over time, that became too brittle. The final version is organized around feature extraction, concept retrieval, hypothesis fitting, validation, ranking, and targeted repair. It became less like a list of tricks and more like a symbolic hypothesis-search system.

## Benchmark Result

On the CS7637 project benchmark, the final agent passed **93 of 96** evaluated problems in **about 20 seconds**.

| Metric | Result |
| --- | ---: |
| Visible training problems passed | 48 / 48 |
| Hidden test problems passed | 45 / 48 |
| Total problems passed | 93 / 96 |
| Visible training accuracy | 100% |
| Hidden test accuracy | 93.75% |
| Overall accuracy | 96.88% |
| Runtime | about 20 seconds |

I read the result as strong performance within the course project benchmark, not as a general solution to ARC-AGI. The interesting part for me was not only the score, but the path to getting there: making the solver more explicit, more testable, and better at handling ambiguity.

## Takeaway

The project changed how I thought about ARC-style reasoning.

At first, I treated many tasks as rule-matching problems. If I could recognize the pattern, I could write a solver for it. The approach worked for some tasks, but it quickly became brittle.

The better approach was to treat each task as a search over possible explanations. The agent needed to ask what kind of structure was present, which concept families were plausible, and which fitted explanation was most likely to generalize beyond the visible examples.

The final version depends so much on feature extraction, validation, ranking, and repair for that reason. The components made the agent less like a collection of tricks and more like a small symbolic reasoning system.

The remaining failures were not wasted effort. They showed me where the system was still too narrow: ambiguous generation, distractor objects, and cases where the right concept was found but the wrong symbolic choice was made.
