---
tags: artificial-intelligence
---

### what is reinforcement learning?
- about learning through trial and error
- over time... an agent should learn the best strategy (policy) in order to yield long-term rewards

### components of reinforcement learning
- **AGENT:** the decision-maker (your model)

- **ENVIRONMENT**: the world the agent interacts with

- **STATE**: a snapshot of the current situation

- **ACTION**: a choice the agent makes

- **REWARD**: feedback from the environment telling how good the action was.

- **POLICY**: the strategy the agent uses to decide actions

- **VALUE**: how good a state or action is in the long run (not just the immediate reward)

### key concepts
- ***exploration*** vs. ***exploitation***: try new actions (explore) vs stick to known good actions (exploit)

- **discount factor**: future rewards are worth less than immediate ones (just like money today is better than money tomorrow)
	- relates to the **time value of money**

- **q-learning**: a popular algorithm where the agent learns the value (Q-value) of actions in different states