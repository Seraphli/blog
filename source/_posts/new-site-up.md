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

# What packages I install

1. hexo-abbrlink
2. hexo-admin
3. hexo-deployer-git
4. hexo-generator-seo-friendly-sitemap
5. hexo-browsersync

```bash
npm install --save hexo-abbrlink hexo-admin hexo-deployer-git hexo-generator-seo-friendly-sitemap hexo-browsersync
```

# Some mistakes I made when building

1. YAML need to add a space after colon
2. Don't add permalink in tags page, which will disable tags cloud
3. On windows, if you can not open the page http://localhost:4000/, you should try to use another port, i.e. `hexo s -p 3600`, and it works for me.


# Next thing I need to do

- [x] Write page count code
- [x] Change avatar
- [ ] Process background images in photoshop
- [ ] Change background
- [x] Build up my own categories page using [API](https://hexo.io/zh-cn/docs/helpers.html#list-categories), [ref](http://moxfive.xyz/2015/10/25/hexo-tag-cloud/)
- [x] Add bitbuket icon

# Just a reminder

1. git clone blog repository
2. cnpm install
3. cnpm install -g hexo-cli

