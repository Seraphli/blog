title: "YADQN Todo List"
author: SErAphLi
abbrlink: 4656ea70
categories:
  - YADQN
tags:
  - "Todo List"
  - RL
date: 2017-03-27 22:04:21
description: "Here I list things and plans need to do about YADQN."
---

## Stage #1

In this stage I will use a specific game, "Breakout", to test the whole structure. 

- [x] Figure out the observation given by openai gym.
- [x] Complete preprocessing part.
- [x] Model architecture build.
- [x] Network parameter replace mechanism.
- [x] Original experience replay.
- [x] Epsilon decay.
- [x] Link all part.
- [x] Add debug information output.
- [x] Save session parameter.
- [ ] Random start (no op).
- [x] Test algorithm on game "Breakout".
- [x] Configuration setup for algorithm.

## Stage #2

In this stage I will continue building some parts for DQN.

- [x] Add Tensorflow tensorboard support.
- [x] Test algorithm on several games. (Aborted: because the algorithm takes too much time to converge)
- [x] Test on all games mentioned in the paper. (Same reason)
- [x] Generate last three column of Extended Data Table 2. (Same reason)

## Stage #3

- [x] Implement another memory mechanism
- [ ] Double DQN Implementation
- [ ] Prioritized Experience Replay
- [ ] Dueling network
- [ ] DQfD
- [ ] Store reported score in papers in the repo, and display them


## Double DQN

- [ ] Algorithm Implementation

## DQfQ

- [x] Change gym to ale, because each action in gym is repeatedly performed for a duration of kk frames. Fix: Gym provide another environment which don't have frame skip. [Link][1]
- [x] Store for experience replay and demostration replay.
- [x] Display replay file in pygame.
- [ ] Test algorithm.

[1]: https://github.com/openai/gym/blob/master/gym/envs/__init__.py#L344-L350
