---
title: Build Up A New Personal Blog
date: 2017/03/23 23:40:00
categories:
  - Notes
tags:
  - Website
  - Hexo
abbrlink: '0'
---

# Why build a new site

When I decide to write code about reinforcement learning, I notice there is just few website about reinforcement learning. And I want to share my experiences in RL. So when I look back, I would consider this as some kind of legacies. I would be **happy** if some one really get helps from this site.

<!--more-->

# Building process

It takes about two days to build this site. First I was trying to build a static site with jekyll, which is written in Ruby. But I saw most people recommended hexo, so I deleted the repo and switched to hexo.

Although it seems easy on the official website, it still has so much parts to customize, like selecting a theme. I spent about half the day and found this theme called "Yelee". But it don't have the functionality to count visit, so I spent 6 hours writing my own site visit counter, using leancloud.

# Some mistakes I made when building

1. YAML need to add a space after colon
2. Don't add permalink in tags page, which will disable tags cloud

# Next thing I need to do

- [ ] Change avatar
- [ ] Change background
- [ ] Build up my own categories page using [API](https://hexo.io/zh-cn/docs/helpers.html#list-categories), [ref](http://moxfive.xyz/2015/10/25/hexo-tag-cloud/)
