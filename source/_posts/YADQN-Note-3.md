title: 'YADQN Note #3'
author: SErAphLi
abbrlink: 21c41f5e
categories:
  - YADQN
tags:
  - Note
  - RL
description: "Notes with new idea"
date: 2017-04-23 22:25:06
---

In the process of implementing DQN and related algorithm, my understanding of these algorithms was greatly improved. In the beginning my algorithm can not run the code with replay size of 1000000. And now the code is able to run such configuration just using about 1GB memory.

Now I'm coming up with a new idea, a memory with baseline. I'm first going to implement deuling network and double q learning, and with these improvement, I will test my memory implement.