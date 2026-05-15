---
title: "Home"
description: "Project overview, benchmark result, and portfolio summary."
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

## What the Project Shows

- How I framed visual reasoning as symbolic hypothesis search.
- Why concept families worked better than isolated rules.
- How validation, ranking, and repair helped when several explanations looked plausible.
- Where the agent still struggled with underconstrained generation and distractor objects.
