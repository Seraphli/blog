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

## Changes

1. `squared gradient momentum` and `min squared momentum` can not be found in tensorflow. So this two values are not presented in code.

[1]: https://gym.openai.com/envs/Breakout-v0
[2]: https://www.tensorflow.org/programmers_guide/threading_and_queues
[3]: http://www.voidcn.com/blog/lujiandong1/article/p-6325966.html
[4]: https://www.tensorflow.org/api_docs/python/tf/stack
[5]: http://stackoverflow.com/questions/16279441/image-show-wont-display-the-picture
[6]: http://www.cnblogs.com/xuchenCN/p/5888646.html
[7]: http://web.stanford.edu/class/cs20si/lectures/slides_14.pdf
