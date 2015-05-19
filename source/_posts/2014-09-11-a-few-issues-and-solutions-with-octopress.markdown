---
layout: post
title: "A few issues and solutions with octopress"
date: 2014-09-11 16:55:09 +0000
comments: true
categories: Tech 
---

### Errors when I run "rake generate"
```
Error reading file /home/wanglij/octopress/source/_posts/2014-09-11-first-try-with-github-and-octopress.markdown: (<unknown>): did not find expected key while parsing a block mapping at line 2 column 1
Error reading file /home/wanglij/octopress/source/_posts/2014-08-04-first-try-with-github-and-octopress.markdown: (<unknown>): did not find expected key while parsing a block mapping at line 2 column 1
```
This is because there are too double quote marks with the title like ""title"".
This is stupid, since it was generated automatically by rake new_post I believe.

### Errors when I run "rake new_post"
```
$rake new_post["title"]
zsh: no matches found: new_post[title]
```

This was resolved by adding 
```
alias rake='noglob rake' 
```
in the .zshrc file

Found the solution [here](https://github.com/robbyrussell/oh-my-zsh/issues/433)

### Error when I run "rake deploy"
```
...
To https://github.com/wanglij/wanglij.github.io
 ! [rejected]        master -> master (non-fast-forward)
error: failed to push some refs to 'https://github.com/wanglij/wanglij.github.io'
hint: Updates were rejected because the tip of your current branch is behind
hint: its remote counterpart. Integrate the remote changes (e.g.
hint: 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.

## Github Pages deploy complete
```
Sloved by running the following command in the /source/\_post direcotry
```
$ git pull origin master
```

### A good reference to make Octopress and Disques Comments work finally.
[Troubleshooting Octopress - Disqus Comments Not Visible](http://hal.case.edu/~rrc/blog/2013/09/29/disqus-comments-not-visible/)
