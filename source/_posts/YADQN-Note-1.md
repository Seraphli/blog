title: "YADQN Note #1"
author: SErAphLi
abbrlink: 8c38ea69
categories:
  - YADQN
tags:
  - Note
  - RL
date: 2017-03-25 20:17:00
---
## Things

I will going to build the algorithm known as DQN. I decide to use [openai gym][1] to reproduce the result described in [Human-level control through deep reinforcement learning][2]. The article can be download from [here][3] for free.
I notice that there are so many repositories about DQN, but a lot of them don't generate any benchmark for algorithms. So I think I need a benchmark and algorithm comparision, and I decide to write my own repository.
I think writing code is going to be painful, so I need to write down the pains I have. By the way, I'm using tensorflow and gym together.
<!--more-->

## DQN

The main goal of DQN is to estimate accumulate reward, known as Q-value, using deep neural network. The algorithm consists of several parts.

1. Preprocessing
  `Working directly with raw Atari 2600 frames`, we need to convert {% math %}210 \times 160{% endmath %} pixel images into {% math %}84 \times 84 \times 4{% endmath %} input vectors.
2. Neural Network
  Input demension of network is {% math %}84 \times 84 \times 4{% endmath %}. `The output layer is a fully-connected linear layer with a single output for each valid action. The number of valid actions varied between 4 and 18 on the games we considered.`
3. Experience Replay
  Store the transition in a memory.

The whole algorithm in the paper.

> **Deep Q-learning with experience replay**
> Initialize replay memory {% math %}D{% endmath %} to capacity {% math %}N{% endmath %}
> Initialize action-value function {% math %}Q{% endmath %} with random weights {% math %}\theta{% endmath %}
> Initialize target action-value function {% math %}\hat{Q}{% endmath %} with weights {% math %}\theta^- = \theta{% endmath %}
> **For** episode = {% math %}1, M{% endmath %} **do**
> &nbsp;&nbsp;&nbsp;&nbsp;Initialize sequence {% math %}s_1=\{x_1\}{% endmath %} and preprocessed sequence {% math %}\phi_1 = \phi(s_1){% endmath %}
> &nbsp;&nbsp;&nbsp;&nbsp;**For** {% math %}t{% endmath %} = {% math %}1, T{% endmath %} **do**
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;With probability {% math %}\varepsilon{% endmath %} select a random action {% math %}a_t{% endmath %}, otherwise select {% math %}a_t = \arg\max_a Q(\phi(S_t), a; \theta){% endmath %}
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Execute action {% math %}a_t{% endmath %} in emulator and observe reward {% math %}r_t{% endmath %} and image {% math %}x_{t+1}{% endmath %}
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Set {% math %}s_{t+1} = s_t, a_t, x_{t+1}{% endmath %} and preprocess {% math %}\phi_{t+1} = \phi(s_{t+1}){% endmath %}
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Store transition {% math %}(\phi_t, a_t, r_t, \phi_{t+1}){% endmath %} in {% math %}D{% endmath %}
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Sample random minibatch of transitions {% math %}(\phi_j, a_j, r_j, \phi_{j+1}){% endmath %} from {% math %}D{% endmath %}
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Set {% math %}y_j = \left\{ \begin{matrix} r_j & \mbox{if episode terminates at step j+1} \\ r_j+\gamma \max_{a'} \hat{Q}(\phi_j, a'; \theta^-) & \mbox{otherwise} \end{matrix} \right.{% endmath %}
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Perform a gradient descent step on {% math %}(y_j-Q(\phi_j,a_j;\theta))^2{% endmath %} with respect to the network parameters {% math %}\theta{% endmath %}
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Every {% math %}C{% endmath %} steps reset {% math %}\hat{Q}=Q{% endmath %}
> &nbsp;&nbsp;&nbsp;&nbsp;**End For**
> **End For**

### Preprocessing

> First, to encode a single frame we take the maximum value for each pixel colour value over the frame being encoded and the previous frame. This was necessary to remove flickering that is present in games where some objects appear only in even frames while other objects appear only in odd frames, an artefact caused by the limited number of sprites Atari 2600 can display at once.

So in order to encode a single frame, we need two frames, current frame and previous frame, which will be stored in a queue.

### Neural Network

#### Model Architecture

1. input layer {% math %}84 \times 84 \times 4{% endmath %}.
2. conv2d, {% math %}8 \times 8{% endmath %} kernel size with stride 4, 32 kernels, relu.
3. conv2d, {% math %}4 \times 4{% endmath %} kernel size with stride 2, 64 kernels, relu.
4. conv2d, {% math %}3 \times 3{% endmath %} kernel size with stride 1, 64 kernels, relu.
5. full-connected, 512 rectifier units.
6. output layer,  a single output for each valid action, varied between 4 and 18 on the games.

#### Parameters Update

> More precisely, every C updates we clone the network Q to obtain a target network {% math %}\hat{Q}{% endmath %}and use {% math %}\hat{Q}{% endmath %} % for generating the Q-learning targets {% math %}y_j{% endmath %} for the following C updates to Q.

### Experience Replay

> First, we use a technique known as experience replay in which we store the agent’s experiences at each time-step, {% math %} e_t = (s_t, a_t, r_t, s_{t+1}) {% endmath %}, in a dataset {% math %} D_t = \{e_1, \dots ,e_t\} {% endmath %}, pooled over many episodes (where the end of an episode occurs when a terminal state is reached) into a replay memory.
> In practice, our algorithm only stores the last {% math %} N {% endmath %} experience tuples in the replay memory,and samples uniformly at random from {% math %} D {% endmath %} when performing updates.This approach is in some respects limited because the memory buffer does not differentiate important transitions and always overwrites with recent transitions owing to the finite memory size {% math %} N {% endmath %}.

And there is a improvement of experience replay.

> A more sophisticated sampling strategy might emphasize transitions from which we can learn the most, similar to prioritized sweeping.

## Tricks

1. Replace network parameters
  Here I find some elegant code about replacing the parameters of target network. First, set a collection name, [example][4]. Second, while using `get_varible`, set the collection name, [example][5]. Third, get all varibles in the collection using `get_collection`, [example][6].

2. Replay memory
  Here is a lecture about reinforcemnt learning and its tensorflow implement. The whole lesson can be found [here][7]. This class is called `CS 20SI: Tensorflow for Deep Learning Research`, and you can find more information [here][8].


[1]: https://gym.openai.com/
[2]: http://www.nature.com/nature/journal/v518/n7540/full/nature14236.html
[3]: https://www.cs.swarthmore.edu/~meeden/cs63/s15/nature15b.pdf
[4]: https://github.com/MorvanZhou/tutorials/blob/master/Reinforcement_learning_TUT/5_Deep_Q_Network/DQN_modified.py#L96
[5]: https://github.com/MorvanZhou/tutorials/blob/master/Reinforcement_learning_TUT/5_Deep_Q_Network/DQN_modified.py#L69
[6]: https://github.com/MorvanZhou/tutorials/blob/master/Reinforcement_learning_TUT/5_Deep_Q_Network/DQN_modified.py#L132
[7]: http://web.stanford.edu/class/cs20si/lectures/slides_14.pdf
[8]: http://web.stanford.edu/class/cs20si/
