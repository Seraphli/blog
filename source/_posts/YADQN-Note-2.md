title: "YADQN Note #2"
author: SErAphLi
abbrlink: 56c32fc8
categories:
  - YADQN
tags:
  - Note
  - RL
date: 2017-03-27 22:20:24
description: "Notes while building YADQN"
---

## Reminder

1. The game "Breakout" is in [here][1]. The observation is an array of shape (210, 160, 3).
2. Because preprocess part needs to record several image, which need a queue, so it can not be just one function. As I browse the documemt of tensorflow, I think I find a queue construction in tensorflow. Maybe I can try that.
3. The queues in tensorflow can be found [here][2].
4. One more clear example about queues in tensorflow is [here][3].
5. If you test tensorflow gpu code in PyCharm, you will get the error `ImportError: libcudart.so.8.0: cannot open shared object file: No such file or directory`. That's because PyCharm don't have the path variable set correctly. Path variable like this:
  ```
  PATH=/usr/local/cuda/bin:$PATH
  CUDA_HOME=/usr/local/cuda
  LD_LIBRARY_PATH=/usr/local/lib:/usr/local/cuda/lib64:/usr/local/cuda/extras/CUPTI/lib64:$LD_LIBRARY_PATH
  ```
  Location need to be set:
  `Setting->Build, Execution, Deployment->Console->Python Console`
  `Run->Edit Configurations`: `Defaults->Python` and `Defaults->Python tests->Unittests`. Delete no default settings, and it will generate setting again based on default settings.
6. Use [tf.stack][4] to stack image. It will convert numpy.narray into tensor.
7. Although observation from gym may seem empty when you print this variable, it actually is not empty. And you don't have to render the game UI.
8. You can use `tf.image.convert_image_dtype` to convert image.
9. Y channel in the paper just means converting RGB image into grayscale image.
10. `PIL.Image.Show()` don't show any window. Solution: `sudo apt-get install imagemagick`. [Reference][5]. `Image.fromarray` need uint8 image.
11. Maybe using queue is not a good idea, because we need to get 4 images in one time.
12. There is a timeline module which can be imported using `from tensorflow.python.client import timeline`. [Reference][6].
13. You can not use `tf.layers.conv2d` function because this function don't contain `collection_name` parameter. It will cause some troubles when trying to replace network parameters.
14. [Here][7] are some codes about epsilon decay. It also contain experience replay code.
15. A strange thing: when the action is `0`, the environment of openai gym don't change; when the action is `1`, the agent's action is waiting.
16. This [repo][8] contain [dqn][9] and [a3c][10].
17. Python `with` statement, `contextmanager` and `yield`, [link][11].
18. Avoid `sess.run` will significantly improve the performance.
19. `env.render()` raise an error. Because you can not call initialization of tensorflow before `env.render()`. [Reference][12].
20. In tensorflow, you have to define all ops in the beginning, otherwise memory usage will continuously increase. Use `sess.graph.finalize()` to see if you define ops below finalize.
21. Tensorflow will only update variable after `sess.run(ops)`, no matter how `op` in `ops` arrange.
22. You have to excute some operations before others.
  ```python
  self._sess.run(self._max_img_update, feed_dict={self._input: input_img})
  self._sess.run(self._update, feed_dict={self._input: input_img})
  ```
  If you excute maximizing two images and excute storing last image in the same time, it will result in `_max_img` and `_last` have same value.
23. After define all operation before `sess.graph.finalize()`, the code run much faster than before, and there is no memory leak problem.
24. While using deque as buffer of experience replay, there is a [problem][13] related to python version. There is no problem when you use python 2.7 or 3.5, but you will get a error while using python 3.4. Update my environment to python 3.5 fix this problem. But still there are some dependency needed to be installed.
  ```
  sudo apt-get install libssl-dev
  sudo apt-get install make build-essential libssl-dev zlib1g-dev libbz2-dev libsqlite3-dev
  ```
25. Running this code require about 6GB memory for the experience replay. So I upgrade my PC building.
26. While training, loss always stay low, but the performance of the network is not well.
27. [Example][14] about how to set the speed of environment in openai gym. But configure method has been removed, but you can set mode in render method. And disable rendering game will speed up the training process.
28. Deque size larger than 65535 may cause memory exploded.
29. Strange thing is that I have to wait for about 100000 runs of game, and there is no improvement of the performance.
30. One transition in experience replay will take {% math %}4 \times (84 \times 84 \times 4 \times 2 + 1 + 1) = 225800{% endmath %} Bytes, which is about 220KB.

## Changes

1. `squared gradient momentum` and `min squared momentum` can not be found in tensorflow. So this two values are not presented in code.
2. Because the code require too much memory, I change the experience replay size from 1000000 to 100000, replay start size from 50000 to 5000, and others remain the same.

[1]: https://gym.openai.com/envs/Breakout-v0
[2]: https://www.tensorflow.org/programmers_guide/threading_and_queues
[3]: http://www.voidcn.com/blog/lujiandong1/article/p-6325966.html
[4]: https://www.tensorflow.org/api_docs/python/tf/stack
[5]: http://stackoverflow.com/questions/16279441/image-show-wont-display-the-picture
[6]: http://www.cnblogs.com/xuchenCN/p/5888646.html
[7]: http://web.stanford.edu/class/cs20si/lectures/slides_14.pdf
[8]: https://github.com/ppwwyyxx/tensorpack
[9]: https://github.com/ppwwyyxx/tensorpack/tree/master/examples/DeepQNetwork
[10]: https://github.com/ppwwyyxx/tensorpack/tree/master/examples/A3C-Gym
[11]: http://preshing.com/20110920/the-python-with-statement-by-example/
[12]: https://github.com/openai/gym/issues/418
[13]: http://stackoverflow.com/questions/40181284/how-to-get-random-sample-from-deque-in-python-3
[14]: https://github.com/openai/gym/issues/185
