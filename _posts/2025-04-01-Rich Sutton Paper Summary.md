---
layout: post
title: "Rich Sutton Paper Summary"
date: 2025-04-01
---

Two papers by Rich Sutton: "Bitter Lesson" in 2019 and "Age of Experience" in 2025:

### 202504 "Age of Experience" paper by David Silver, Richard Sutton

- Experiential agent needs 1) information to casrry across entire system and its behavior to adatp from past experiences, 2) long term goals, where the immediate step may even be detrimental to contribute to LT success
- Recently, coding and tool-use are increasingly built upon execution feedback (i.e., use tool and observe what happens, and learn), as opposed to SFT with human tool uses
- Rewards based on human preferences are not grounded in reality. Relying on human feedbacks lead to ceiling in model perf. Necessary to use grounded rewards to improve beyond human. RLHF bypassed core RL concepts: need for machine-estimated value functions, "exploration" reduced by strong priors from human data
- There's arguement that a singal grounded reward can induce broadly capable intelligence, because achieving a simple goal in complex environment requires mastering a variety of skills
- To align with human preference, one can use "bi-level optimization" where the upper level optimize a function of grounded rewards to human preference, and lower level optimizes policy to grounded signals from the envrionment
- Human language is unlikely the optimal instance for reasoning. Need feedback loop from RL to learn optimal method of throught
<br>


### 201903 "Bitter Lesson"

- General methods that leverage computation are ultimately the most effective, and by a large margin
- Seeking ST improvement, researchers may leverage human domain knowledge, but the only thing that matters in the LT is the leveraging of computation. We have to learn the bitter lesson that building in how we think we think does not work in the LT; instead, we should build in only the meta-methods that can find and capture the brain's vast complexity
- Search and learning are the two most important classes of techniques that scales with massive amounts of computation
