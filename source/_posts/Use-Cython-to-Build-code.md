title: "Use Cython to Build Code"
author: SErAphLi
abbrlink: 433d1379
date: 2017-03-29 09:35:35
categories:
  - Notes
tags:
  - Python
  - Cython
description: "Use cython to build code"
---
## TL;DR

1. Build your code like a module, and change file name .py to .pyx
2. Add setup.py in your folder
3. Add code in setup.py
  ```python
  from distutils.core import setup
  from Cython.Build import cythonize

  setup(
    name = 'Your App Name',
    ext_modules = cythonize("your_code.pyx"),
  )
  ```
Remeber to change `name` and `ext_modules`
4. Run `python setup.py build_ext --inplace` to build code into .so file
5. Add a new file, which will import your lib and run the code
  ```
  import your_code
  ```

## Resource

[Official Guide][1]

[1]: http://cython.readthedocs.io/en/latest/src/quickstart/build.html