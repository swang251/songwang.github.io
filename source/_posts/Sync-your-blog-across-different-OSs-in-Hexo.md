---
title: Sync your blogs across different OSs in Hexo
date: 2019-01-07 01:13:04
tags: [Hexo]
categories: daily
toc: true
---

This is an article about how to synchronize blogs across your different operating systems.
<!--more-->

It has been one year since I first set up Hexo and half a year since my first meaningful blog. I think it better to note down the steps I used to set up my GitHub Pages.

## GitHub Pages + Hexo + Maupassant
### GitHub Pages
> [GitHub Pages](https://pages.github.com/) is a static site hosting service designed to host your personal, organization, or project pages directly from a GitHub repository.

- You would need to create a new repository named "username.github.io".

### Static Generator
The static generator would help transform your plain text into static webpages. There are several choices, the most widely used of which are [Jekyll](https://jekyllrb.com/), [Hugo](https://gohugo.io/) and [Hexo](https://hexo.io). I didn't try everything. Instead, I try to read comparison articles online and find the one suit for me. I remember that one of the reasons that Hexo attracts me is its "Blazing Fast".
> [Hexo](https://hexo.io/) is a fast, simple and powerful blog framework. You write posts in Markdown (or other languages) and Hexo generates static files with a beautiful theme in seconds.

### Theme
You might need a theme for your blog and again, there are [hundreds of options](https://hexo.io/themes/). Finally, I decide to go for [Maupassant](https://github.com/tufu9441/maupassant-hexo) because it looks concise.
> [Maupassant](https://github.com/tufu9441/maupassant-hexo) - A simple Hexo template with great performance on different devices, ported from a Typecho theme by [Cho](https://github.com/pagecho/maupassant), forked and modified from [icylogic](https://github.com/icylogic).

## Installation
- The setup of Hexo is really simple. I just follow the [Hexo Documentation](https://hexo.io/docs/) and its done. This would include:
  - Install [Git](https://hexo.io/docs/#Install-Git)
  - Install [Node.js](https://hexo.io/docs/#Install-Node-js)
  - Install [Hexo](https://hexo.io/docs/#Install-Hexo)
  
## Setup
### Hexo Setup
1. Go to the directory of the GitHub Page repository
2. `hexo init`, initialization. Several folders and files would be generated.
3. `npm install`, install packages based on *package.json* generated during `hexo init`, where `npm` is short for Node.js package manager. Actually, `npm install` should already be called during `hexo init`. (ref. [Hexo Setup](https://hexo.io/docs/setup), [npm-install](https://docs.npmjs.com/cli/install.html))
4. Follow the way of [deployment using Git](https://hexo.io/docs/deployment#Git).

### Directory Structures
Several folders and files would be generated after `hexo init`

- **[_config.yml]((https://hexo.io/docs/setup#config-yml))**: site [configuration](https://hexo.io/docs/configuration) file, where one can configure most settings here
- **[package.json](https://hexo.io/docs/setup#package-json)** and **package-lock.json**: Application data, including the modules you need. The **package-lock.json** is automatically generated for any operations where npm modifies either the node_modules tree, or package.json. It describes the exact tree that was generated, such that subsequent installs are able to generate identical trees, regardless of intermediate dependency updates. (ref. [npm-package-lock.json](https://docs.npmjs.com/files/package-lock.json) and [npm-package.json](https://docs.npmjs.com/files/package.json)).
- **[node_modules]**: the folder that local modules/packages of Node.js drop into. Its contents should correspond to **package.json** and is generated based on `npm install`
- **[scaffolds](https://hexo.io/docs/setup#scaffolds)**: Seems like a folder for templates.
- **[source](https://hexo.io/docs/setup#source)**: the source folder including the original contents of the site, e.g., your Markdown files.
- **[themes](https://hexo.io/docs/setup#themes)**: the theme folders.
- **db.json**: no ideas about it, seems to be generated by `hexo generate` and is kind of cache which stores all posts, tags, categories, etc. in a JSON format for faster parsing. It would correspond to the generated sites.
- **public**: All the static webpage files generated by `hexo generate` and also the ones deployed to the git repository using `hexo-deployer-git`.
- **.deploy_git**, the folder for deployment of the static pages.

### Theme Setup
- Follow the installation of the theme [Maupassant](https://github.com/tufu9441/maupassant-hexo).

### Git the whole blogs instead of the only the static websites
You might have already noticed that using `hexo-deployer-git`, only the static websites would be git to the GitHub repository and you'll lose everything if your laptop dies without backup. Also, it is hard to synchronize across your multiple computers. So here is how to git everything including the original markdowns using two branches. The is based on this [article](http://crazymilk.github.io/2015/12/28/GitHub-Pages-Hexo%E6%90%AD%E5%BB%BA%E5%8D%9A%E5%AE%A2/%23more) which is 404 now. But you could still refer to his answer in [知乎](https://www.zhihu.com/question/21193762/answer/79109280)

1. Create the repository username.github.io
2. Add the following to .gitignore
```node_modules/
public/
package-lock.json
.deploy_git/
db.json```
3. Create two branches: master and hexo.
4. Set hexo as the default branch.
5. clone the repository and set up based on the instruction above.
6. set the `deploy -> branch` in **_config.yml** to master.

This way, the static webpages generated and deployed by `hexo g -d` would be stored in the master branch which the original markdown files and the configuration would be in hexo branch using `git push origin hexo`.








