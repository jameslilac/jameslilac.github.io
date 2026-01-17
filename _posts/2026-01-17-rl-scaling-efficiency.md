---
layout: post
title: "RL's Scaling Edge: On-Policy Learning and Negative Gradients"
date: 2026-01-17
---

In a recent interview, Kimi's founder Zhang Zhilin suggested that Reinforcement Learning (RL) offers more efficient scaling for Large Language Models (LLMs) compared to traditional pre-training [3]. This efficiency is attributed to two core concepts: **on-policy learning** and the use of **negative gradients**.

## 1. The Power of On-Policy Learning

*   **Pre-training as an Off-Policy Task**
    - Standard pre-training is an "off-policy" process where the model learns from a massive, static dataset collected beforehand.
    - This data's distribution is fixed and doesn't change, regardless of the model's performance or evolving capabilities.
    - The model has no mechanism to adapt to the distribution of text it will actually generate during inference.

*   **Solving Distribution Shift with RL**
    - RL, in contrast, is an "on-policy" method where the model generates its own training data by interacting with an environment and receiving feedback [2].
    - This dynamically addresses the critical issue of **distribution shift** (also known as covariate shift), where the data distribution seen during training differs from the distribution encountered during real-world testing and inference [4].
    - By training on its own outputs, RL ensures the model learns to handle the exact distribution it will face during deployment.

*   **Learning from Mistakes and Recovery**
    - Because RL is on-policy, the model continuously learns from its own outputs, including its errors.
    - If the model generates a nonsensical or factually incorrect response, the RL feedback loop can penalize that trajectory.
    - This teaches the model not only what a good answer looks like but also **how to recover and get back on track** after making a mistake.
    - The model develops robustness to its own errors, learning correction strategies that weren't present in the static training data.

*   **The Brittleness of Pre-training**
    - A model trained exclusively on a static dataset learns to mimic that data exceptionally well.
    - However, when it generates a response that deviates from what it has seen (a common occurrence during inference), it enters an unfamiliar state.
    - Lacking a mechanism to understand it has made an error, the model can continue down a path of **compounding mistakes**, leading to hallucinations or nonsensical outputs [2].
    - This is the covariate shift problem: the model was never trained on the distribution of "text generated after making an error," so it doesn't know how to recover.

## 2. The Role of Negative Gradients

*   **Explicitly Penalizing Wrong Answers**
    - A key advantage of some RL methods is the ability to apply **negative gradients**, meaning the model can be explicitly taught what *not* to do by penalizing incorrect or undesirable responses.
    - This is a more direct and powerful learning signal than simply rewarding correct answers, as it provides explicit feedback about failure modes.
    - Traditional pre-training only implicitly discourages wrong answers by maximizing the probability of correct sequences, but never explicitly penalizes errors.

*   **Surprising Effectiveness of Negative Reinforcement**
    - Research has shown that using negative reinforcement alone—without even rewarding correct responses—can substantially improve an LLM's reasoning abilities [1].
    - The paper "The Surprising Effectiveness of Negative Reinforcement in LLM Reasoning" demonstrates that training with only negative samples (Negative Sample Reinforcement, or NSR) consistently improves performance over the base model.
    - In many cases, NSR alone matches or surpasses more complex RL algorithms like PPO and GRPO, while also preserving output diversity [1].
    - This highlights the power of directly penalizing errors rather than only rewarding successes.

## The Unbeaten Strength of Pre-training

*   **Knowledge Acquisition Remains Superior**
    - Despite RL's efficiency in refining behavior and improving reasoning, pre-training remains superior for acquiring a broad base of factual knowledge.
    - The sheer volume and diversity of data in pre-training corpora (often trillions of tokens) are what give LLMs their extensive understanding of the world.
    - RL cannot replace this knowledge acquisition phase—it can only refine how that knowledge is used.

*   **RL Needs a Foundation to Build Upon**
    - RL fine-tuning is not about learning new facts from scratch; it's about learning how to *use* the knowledge gained during pre-training to perform specific tasks, follow instructions, and reason more effectively.
    - An RL process would eventually exhaust the knowledge contained within its own policy if it didn't have a vast pre-trained foundation to draw upon.
    - The model can only learn from the distribution of responses it generates, which is inherently limited by what it already knows.
    - This is why the most successful approaches combine massive pre-training for knowledge with RL for behavior refinement and reasoning improvement [3].

---

### References

1.  Zhu, X., et al. (2025). [The Surprising Effectiveness of Negative Reinforcement in LLM Reasoning](https://arxiv.org/abs/2506.01347). arXiv:2506.01347.
2.  Zhang, W., et al. (2025). [On-policy RL meets Off-policy Experts: Harmonizing Supervised Fine-tuning and Reinforcement Learning via Dynamic Weighting](https://arxiv.org/abs/2508.11408). arXiv:2508.11408.
3.  Zhang Zhilin interview (2025). [Kimi Founder Zhang Zhilin: Agentic LLMs](https://www.youtube.com/watch?v=91fmhAnECVc).
4.  Seldon. (2021). [What is Covariate Shift?](https://www.seldon.io/what-is-covariate-shift/)
