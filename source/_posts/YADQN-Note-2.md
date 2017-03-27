title: 'YADQN Note #2'
author: SErAphLi
abbrlink: 56c32fc8
categories:
  - YADQN
tags:
  - Note
  - RL
date: 2017-03-27 22:20:24
---

## Reminder

1. The game "Breakout" is in [here][1]. The observation is an array of shape (210, 160, 3).
2. Because preprocess part needs to record several image, which need a queue, so it can not be just one function. As I browse the documemt of tensorflow, I think I find a queue construction in tensorflow. Maybe I can try that.
3. The queues in tensorflow can be found [here][2].
4. One more clear example about queues in tensorflow is [here][3].

[1]: https://gym.openai.com/envs/Breakout-v0
[2]: https://www.tensorflow.org/programmers_guide/threading_and_queues
[3]: http://www.voidcn.com/blog/lujiandong1/article/p-6325966.html
