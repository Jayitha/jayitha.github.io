---
title: ! "Reinforcement Learning: An Introduction - Chapter 1 Introduction"
author: Jayitha C
date: 2021-01-19 11:33:00 +0800
categories: [Reinforcement Learning, "Reinforcement Learning: An Introduction"]
tags: [textbook, machine learning]
math: true
image: /assets/img/RL_system.jpg
---


This is the first in a series of posts which partly summarize chapters from the following book

> "Reinforcement Learning: An Introduction" Second Edition, by Richard S. Sutton and Andrew G. Barto. 

These posts might be updated later as I understand more. 

---

## What is Reinforcement Learning?

It is learning what to do such that a numerical reward is maximized. It learns the mapping from situation to action by performing a trial-and-error search. Many times actions taken might not _just_ affect the immediate reward but might also affect subsequent rewards (something akin to local and global optimum). 

> Both trial-and-error search and delayed reward characterize _reinforcement learning (RL)_

Reinforcement learning is different from  

- _supervised learning_ - In interactive problems (which are what learning agents are more often present in), it might not be possible to get labeled data allowing the agent to learn which the right actions should be. The agent should be able to learn from it's own experience. 

- _unsupervised learning_ - While reinforcement learning doesn't rely on labelled "correct" data, it tries to learn situation-action mapping that maximizes a reward rather than just trying to find structure in unlabelled data (which is what the unsupervised paradigm tries to do)

Reinforcement learning differs from the other two in another way, it suffers from the **exploration-exploitation** dilemma

| exploration-exploitation dilemma |
|:---|
|To maximize rewards, the learning agent must play actions that it's tried before and knows maximizes the expected reward. But to discover maximizing actions, it has to try actions it hasn't selected before. With stochastic tasks, it has to execute a given action multiple times to be able to estimate the expected reward. This dilemma still remains unsolved. |

$$ \text{MACHINE LEARNING} = \begin{cases} \text{SUPERVISED LEARNING}\\\\ \text{UNSUPERVISED LEARNING}\\\\ \text{REINFORCEMENT LEARNING} \end{cases} $$

### The Paradigm Shift

- Since the 1960's, AI researchers believed that there were no _general principles_ and that intelligence was possessed due to a large number of tricks and heuristics. 

> If you could get _enough_ facts in a machine, it would be intelligent. 

- But in fact too little work had been done to find these _general principles_ and reinforcement learning is trying to find simpler and fewer principles of AI

## Examples

- A chess game agent. The agent should make moves based on both the current position, possible plays (actions) and the possible counter plays.

- Roomba: An automatic vacuum cleaner which enters a room looking for dirt to clean. It has to make a choice - to move into the room or return to a charging port based on how much charge it has and how far it is from the charging port. 

- A normal person preparing their breakfast. 

And so on ...

All examples stated so far involve a decision-making learning agent _interacting_ with it's environment to achieve a goal despite any _uncertainty_ it might face (from the environment). Sometimes the agent might not be able to fully predict rewards for a particular action. But the agent will still be able to "see" how close it is to it's _goal_. While initial knowledge influences what is important to learn, interaction with the environment is essential for adjusting behavior to exploit features of the task at hand. 

## Elements of Reinforcement Learning

| Element | Description |
|:---|:---|
|**_POLICY_**|It is a mapping between perceived states of the environment and actions to be taken when in those states. The policy could be a simple function like a look-up table, or a computationally expensive search process or even stochastic.|
|**_REWARD SIGNAL_**|It defines the goal. Every time the agent performs an action, the environment returns a _reward_ which the agent uses to decide if the performed actions are "good" or "bad". It can be a stochastic function of environment state and actions taken. For example, in humans, rewards can be pleasure or pain. The agent tries to maximize the cumulative reward.|
|**_VALUE FUNCTION_**|The _value_ of a state is the total amount of reward an agent expects to accumulate starting from that state. While _rewards_ indicate immediate desirability of a state, _value_ indicate _long-term_ desirability of that state. While we make decisions based the _value_, _values_ cannot be computed without _rewards_. _value estimation_ is arguably the most difficult problem within RL|
|**_MODEL_**|(optional) mimics the environment allowing inferences to be made about how the environment will behave. Knowing the model allows _model-based learning_ by which a course of action can be decided by considering possible situations _before they are experiences_. It's also possible for systems to first use _model-free learning_ (trial-and-error) to learn a model and then _plan_ using this model. |

> Modern RL spans the spectrum - low-level trial-and-error \\( \rightarrow \\) high-level deliberative planning

## Limitations and Scope

- RL relies highly on the _state_ of the environment. As input to policy, value function and model and output from the model. 

- In the book, they focus mostly on the problem of value estimation. Although _value estimation_ is not necessary - for instance, in evolutionary algorithms like genetic algorithms, genetic programming, simulated annealing and so on policies are learnt through static processes. In cases where there's a small search space or a long amount of time, evolutionary algorithms might be useful. That being said evolutionary algorithms do not interact with the environment and hence cannot make good use of the structure and information and agent might have.

## Example: Tic Tac Toe

![](/assets/img/tic_tac_toe.png){: width="400"}
_Tic Tac Toe game_

Under the assumption that we are playing an imperfect player (can make "incorrect" moves). Our goal is to construct a player who learns imperfections of opponent's plays and maximize it's chances of winning. We might consider the following approaches 

| Approach | Description |
|:---|:---|
|Classical _minimax_ solution from game theory (GT)|A minimax player would never reach a state in which it could lose even if it can win if the opponent makes an "incorrect" play because this approach assumes the opponent plays a particular way.|
|Dynamic Programming|This method can compute optimal solutions for any opponent but would require the opponent's action probability distribution. While practically unavailable, this can be estimated.|
|Evolutionary Algorithm|A genetic algorithm for example, will consider a sample of policies from the policy space, evaluate those policies through experimentation and mutate those with high rewards. But these methods reward the "whole policy", even moves that may not have been played.|

RL Approach:

If our agent is playing $$ \mathbf{X}s $$

- Create a table for each state of the game. For the states where there exists a row of \\( 3 \mathbf{X}s \\) we set the _value_ to be \\( 1 \\), the states where there exists a row of \\( 3 \mathbf{O}s \\) we set the _value_ to be \\( 0 \\) and \\( 0.5 \\) for the remaining states where the _value_ indicates the probability of winning from that state.

- This agent plays games against the opponent. Out of the possible set of actions the agent _greedily_ picks actions which lead to higher value states. Occasionally random _exploratory_ actions are selected to gain experience. After each _greedy_ move we update the previous state's value to be _closer_ to the new state.

For example, if \\( S_t \\) denotes state at time \\( t \\), \\( V(S_t) \\) denotes _value_ of state \\( S_t \\) and \\( S_{t+1} \\) denotes state after choosing the _greedy_ action, then \\( V(S_t) \\) could be updated as follows

$$ V(S_t) \leftarrow V(S_t) + \alpha \left [ V(S_{t+1} - V(S) \right ] $$

where $$ \alpha $$ is the _step-size_ and this is an example of _temporal difference learning_


