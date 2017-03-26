title: Build Up A New Personal Blog
author: SErAphLi
abbrlink: 73bba9d9
categories:
  - Website
tags:
  - Note
  - Hexo
date: 2017-03-23 23:40:00
---

## Why build a new site

When I decide to write code about reinforcement learning, I notice there is just few website about reinforcement learning. And I want to share my experiences in RL. So when I look back, I would consider this as some kind of legacies. I would be **happy** if some one really get helps from this site.

<!--more-->

## Building process

It takes about two days to build this site. First I was trying to build a static site with jekyll, which is written in Ruby. But I saw most people recommended hexo, so I deleted the repo and switched to hexo.

Although it seems easy on the official website, it still has so much parts to customize, like selecting a theme. I spent about half the day and found this theme called "Yelee". But it don't have the functionality to count visit, so I spent 6 hours writing my own site visit counter, using leancloud.

## What packages I install

1. hexo-abbrlink
2. hexo-admin
3. hexo-deployer-git
4. hexo-generator-seo-friendly-sitemap
5. hexo-browsersync
6. hexo-math

```bash
npm install --save hexo-abbrlink hexo-admin hexo-deployer-git hexo-generator-seo-friendly-sitemap hexo-browsersync hexo-math
```

## Some mistakes I made when building

1. YAML need to add a space after colon
2. Don't add permalink in tags page, which will disable tags cloud
3. On windows, if you can not open the page http://localhost:4000/, you should try to use another port, i.e. `hexo s -p 3600`, and it works for me.
4. Mathjax can not be render in hexo is just because underscore character `_` will be translate in markdown, so the equation will miss `_` when rendering with Mathjax. Solution: install hexo-math, and add
  ```
  {% math %}
  {% endmath %}
  ```
  around the equation, [more][4]. Or just use `\_` to escape the markdown render.

## Next thing I need to do

- [x] Write page count code.
- [x] Change avatar.
- [x] Process background images in photoshop.
- [x] Change background.
- [x] Build up my own categories page using [API][2], [ref][3].
- [x] Add bitbuket icon.
- [x] Fix the issue that the newer post on the left and the older post on the right, reverse this setting. Because people are more used to "left stands for previous and right stands for next". Fix: it is a issue of hexo. [Issue related][1].
- [x] Fix the issue when sometime background of list items are not right. Fix: In the article.styl file, there is a style setting about `.article-entry > ol:last-child`, just delete it, otherwise it will render every article's last list in a different way, which is quite annoying.
- [x] Related link below the post.(Cancel: it is a new functionality. Maybe in the future I will develop it.)

## Just a reminder

1. git clone blog repository
2. cnpm install
3. cnpm install -g hexo-cli
4. replace `node_modules/hexo/lib/plugins/generator/post.js` with `post.js`. [Issue related][1].

[1]: https://github.com/hexojs/hexo/issues/2474
[2]: https://hexo.io/zh-cn/docs/helpers.html#list-categories
[3]: http://moxfive.xyz/2015/10/25/hexo-tag-cloud/
[4]: https://github.com/akfish/hexo-math
