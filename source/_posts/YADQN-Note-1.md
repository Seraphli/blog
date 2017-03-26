title: "YADQN Note #1"
author: SErAphLi
abbrlink: 8c38ea69
categories:
  - YADQN
tags:
  - Note
date: 2017-03-25 20:17:00
---
## Things

I will going to build the algorithm known as DQN. I decide to use [openai gym][1] to reproduce the result described in [Human-level control through deep reinforcement learning][2].
I notice that there are so many repositories about DQN, but a lot of them don't generate any benchmark for algorithms. So I think I need a benchmark and algorithm comparision, and I decide to write my own repository.
I think writing code is going to be painful, so I need to write down the pains I have.
<!--more-->

## DQN

The algorithm consists of several parts.

1. Preprocessing
  `Working directly with raw Atari 2600 frames`, we need to convert {% math %}210 * 160{% endmath %} pixel images into {% math %}84 * 84 * 4{% endmath %} input vectors.
2. 


## Todo List

[1]: https://gym.openai.com/
[2]: http://www.nature.com/nature/journal/v518/n7540/full/nature14236.html
