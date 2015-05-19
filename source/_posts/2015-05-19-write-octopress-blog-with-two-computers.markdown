---
layout: post
title: "Write Octopress Blog With Two Computers"
date: 2015-05-19 16:43:32 +0000
comments: true
categories: 
---

### Issue

Sometime, when I want to continue my writing in my blog, the computer where I had the work half way done may not be available to me. So it will be great if I can check out my latest work in any computer and continue my previous work. Now that we used github to host our blog, we surely can have this advantage.

### Repository

I've already deployed my octopress blog in github by following [this article 1](http://purplepalmdash.github.io/blog/2014/07/30/zai-githubshang-bu-shu-ni-de-octopressbo-ke/).

Octopress repositories have two branches, master and source. [2] 

master	|	source
--------|----------
contains the blog itself | contains the files that are used to generate the blog
is stored in \_depoly subfolder	| is stored in octopress directory
gets updated when we run rake depoly | was not in the remote repository yet

Push source to remote repository:

```
cd octopress
git remote add origin <github HTTPS/SSH clone URL>
git commit -m 'any message'
git push origin source
```

If it gives the following error message when you are trying to run 'git remote add origin', then it means there is already a source branch in the repository. You'd better double check if the existing source branch is what you want. To remove it, run 'git remote rm origin'

```
 ! [rejected]        source -> source (fetch first)
error: failed to push some refs to '<github HTTPS/SSH clone URL>'
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
hint: to the same ref. You may want to first integrate the remote changes
hint: (e.g., 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```

### References
1. [在github上部署你的octopress博客](http://purplepalmdash.github.io/blog/2014/07/30/zai-githubshang-bu-shu-ni-de-octopressbo-ke/)
2. [Clone Your Octopress to Blog From Two Places](http://blog.zerosharp.com/clone-your-octopress-to-blog-from-two-places/)
