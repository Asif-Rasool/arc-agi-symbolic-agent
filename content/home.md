---
title: "Home"
---

## Project Overview

I built this ARC-AGI agent as a symbolic reasoning system for abstract visual tasks. The project was developed for Georgia Tech's CS7637 Knowledge-Based AI course.

My goal was to make the agent reason through each task before making a prediction. I designed it to read the structure of the examples, retrieve plausible symbolic concepts, fit concrete hypotheses, validate them against the visible training pairs, rank the candidates, and repair brittle local choices when possible.

I chose that design because I wanted the reasoning path to be inspectable. When the agent succeeds, I can see which explanation produced the answer. When it fails, I can usually trace the failure to a concept choice, a fitted parameter, a ranking decision, or an object-selection mistake.

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

I read the result as strong performance within the course project benchmark. The most useful lesson was how much the agent improved once I treated each task as a search for an explanation.

## Where to Start

Start with [Approach]({{< relref "approach" >}}) for the reasoning pipeline. Read [Examples]({{< relref "examples" >}}) for three solved tasks. Read [Failure Analysis]({{< relref "failure-analysis" >}}) for the hidden-test misses. Read [Reflection]({{< relref "reflection" >}}) for what the project taught me about symbolic reasoning and debugging.
