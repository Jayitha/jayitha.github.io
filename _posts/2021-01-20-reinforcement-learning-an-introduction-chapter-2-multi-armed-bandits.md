---
title: ! "Reinforcement Learning: An Introduction - Chapter 2 Multi-armed Bandits"
author: Jayitha C
date: 2021-01-20 11:33:00 +0800
categories: [Reinforcement Learning, "Reinforcement Learning An Introduction", "Tabular Solution Methods"]
tags: [textbook, machine learning]
math: true
---

This is the second in a [series](https://jayitha.github.io/categories/reinforcement-learning-an-introduction/) of posts which partly summarize chapters from the following book

> "Reinforcement Learning: An Introduction" Second Edition, by Richard S. Sutton and Andrew G. Barto. 

These posts might be updated later as I understand more. 

---

As described in the first post in the series, RL differs from other learning paradigms in the sense that it involves two kinds of feedback - _evaluative feedback_ and _instructive feedback_. Evaluative feedback depends on the action taken and indicates how "good" the action was whereas instructive feedback indicates the correct action to be taken independent of the action actually taken. 

In this chapter, they explore evaluative feedback in a simple $$ k $$-armed bandit problem

---

$$ \newcommand{\E}{\mathbb{E}} $$

## A $$ k $$-armed Bandit Problem

In this learning problem, you are given a set of $$ k $$ actions, at each _time step_ you pick an action from the set and are given a reward based on a probability distribution for the action you picked. Therefore, each of the $$ k $$ actions has an expected reward which is also termed to be the $$ value $$ of that action.

Given that at time step $$ t $$ we pick action $$ A_t $$ with corresponding reward $$ R_t $$, then the $$ value $$ of action $$ a $$ denoted by $$ q_{\ast}(a) $$ is the expected reward

$$ q_{\ast}(a) =  \E \left [ R_t | A_t = a\right ] $$

> If you know all the $$ values $$ then you'd always pick the action with the highest $$ value $$, but we assume you do not know


