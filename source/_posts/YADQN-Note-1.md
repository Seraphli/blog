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

I will going to build the algorithm known as DQN. I decide to use [openai gym][1] to reproduce the result described in [Human-level control through deep reinforcement learning][2]. The article can be download from [here][3] for free.
I notice that there are so many repositories about DQN, but a lot of them don't generate any benchmark for algorithms. So I think I need a benchmark and algorithm comparision, and I decide to write my own repository.
I think writing code is going to be painful, so I need to write down the pains I have. By the way, I'm using tensorflow and gym together.
<!--more-->

## DQN

The algorithm consists of several parts.

1. Preprocessing
  `Working directly with raw Atari 2600 frames`, we need to convert {% math %}210 * 160{% endmath %} pixel images into {% math %}84 * 84 * 4{% endmath %} input vectors.
2. 

### Preprocessing

> First, to encode a single frame we take the maximum value for each pixel colour value over the frame being encoded and the previous frame. This was necessary to remove flickering that is present in games where some objects appear only in even frames while other objects appear only in odd frames, an artefact caused by the limited number of sprites Atari 2600 can display at once.

So in order to encode a single frame, we need two frames, current frame and previous frame, which will be stored in a queue.

## Tricks

1. Replace network parameters
  Here I find some elegant code about replacing the parameters of target network. First, set a collection name, [example][4]. Second, while using `get_varible`, set the collection name, [example][5]. Third, get all varibles in the collection using `get_collection`, [example][6].


## Todo List

[1]: https://gym.openai.com/
[2]: http://www.nature.com/nature/journal/v518/n7540/full/nature14236.html
[3]: https://www.cs.swarthmore.edu/~meeden/cs63/s15/nature15b.pdf
[4]: https://github.com/MorvanZhou/tutorials/blob/master/Reinforcement_learning_TUT/5_Deep_Q_Network/DQN_modified.py#L96
[5]: https://github.com/MorvanZhou/tutorials/blob/master/Reinforcement_learning_TUT/5_Deep_Q_Network/DQN_modified.py#L69
[6]: https://github.com/MorvanZhou/tutorials/blob/master/Reinforcement_learning_TUT/5_Deep_Q_Network/DQN_modified.py#L132
