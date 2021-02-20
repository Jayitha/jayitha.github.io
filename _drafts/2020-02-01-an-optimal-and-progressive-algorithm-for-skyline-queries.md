---
title: An Optimal and Progressive Algorithm for Skyline Queries
author: Jayitha C
date: 2020-02-01 11:33:00 +0000
categories: [Paper Summaries]
tags: [skyline, dimitris papadias, yufei tao, greg fu, bernhard seeger]
math: true
---

> Papadias, Dimitris, et al. "An optimal and progressive algorithm for skyline queries." Proceedings of the 2003 ACM SIGMOD international conference on Management of data. 2003.

This paper is pretty ideal for someone who wants to figure out which skyline computation method works best for their application. I take this opportunity to describe all the skyline computation algorithms in this paper in sufficient detail using a simple 2D example.

## Problem Statement

To develop a progressive algorithm to efficiently compute the skyline point set

## Hotels Dataset

To describe previous algorithms and the one in this paper, I use the following dataset (as also provided in the paper)

The hotels dataset consists of 12 hotels. For each hotel, the price per night and the distance from the beach are recorded. 

| Hotel Name | Distance | Price |
|:---|:---|:---|
|a|1|9|
|b|2|10|
|c|4|8|
|d|6|7|
|e|9|10|
|f|7|5|
|g|5|6|
|h|4|3|
|i|3|2|
|k|9|1|
|l|10|4|
|m|6|2|
|n|8|3|

## Definitions

### Dominance

Given a $$ d- $$ dataset $$ \mathcal{D} $$, where the domains of all the attributes are at least partially ordered, a point $$ p (\in \mathcal{D}) $$ is said to weakly dominate another point $$ q (\in \mathcal{D}) $$ is $$ p $$ is not worse than $$ q $$ in all attributes and $$ p $$ is better than $$ q $$ in at least one attribute. Formally if $$ > $$ represents dominance or "better value" then

$$ p > q \leftrightarrow \left ( \forall_{a \in \mathcal{A}} p[a] \geq_a q[a] \right ) \wedge \left ( \exists_{a \in \mathcal{A}} p[a] >_a q[a] \right ) $$

where $$ \mathcal{A} $$ indicates the set of attributes, $$ p[a] $$ indicates the $$ a $$th attribute of point $$ p $$ and $$ >_a $$ represents the dominance relation for attribute $$ a $$.

For the dataset described above, we would naturally like to pick hotels which minimize both the price and the distance from the beach. In the dataset, there are some points which are clearly "better" than others. For instance, hotel i $$ (3, 2) $$ is both cheaper and closer to the beach than hotel h $$ (4, 3) $$

### Skyline Set

The skyline set (denoted by $$ skyline_{\mathcal{D}} $$) of a dataset $$ \mathcal{D} $$ consists of all those points which are not dominated by any other point in the dataset. Formally,

$$ p \in skyline_{\mathcal{D}} \leftrightarrow \neg \exists_{q \in \mathcal{D}} q > p $$

For the hotels dataset, the skyline set while minimizing both attributes is 

$$ skyline_{\mathcal{D}} = \{ a, i, k \} $$








