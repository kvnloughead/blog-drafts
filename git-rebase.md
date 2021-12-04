---
title: 'Keeping it Clean with Git Rebase'
excerpt: | 
  A nice little story about how I used rebase to keep my commit history tidy.
coverImage: ''
date: '2021-11-28'
author:
  name: Kevin Loughead
  picture: ''
ogImage:
  url: ''
---

Rebasing in git is a tricky thing to get the hang of, and I am by no means a pro at it. But is a great way to keep your commit history clean. I'll give you a rather inconsequential seeming use case that comes up all the time for me. Say you've been writing some blog posts, but you finished that and moved on to doing some styling. You have a commit history that looks like this:

```plain-text
657e31 (HEAD -> dev) fix code styles
39fe561 update blog post  
```

But then you notice that you'd left a typo in the text of one of your posts[^1]. You'd really rather fix that typo and amend the the `update blog post` commit. But how can you do that? Well, I wish it were as easy as `git commit --amend <commit-hash>`, but it's not. But it's ok, we can use `git rebase`. You can start an interactive rebasing session with the `-i` flag, specifying the *parent* of the last commit that you want to edit. So, I want to edit the commit before `HEAD`, which is `HEAD~1`. So you supply `HEAD~2` to `rebase` as an argument.

```plain-text
git rebase -i HEAD~2
```

This will open a file that should look something like this in your default editor:

TODO 
- insert image 1
- show image 2
- change `pick` to `edit` for all commits to be edited
- save
- show image 3
- git docs say "this tells you exactly what to do", but...
- now is the time to make changes, add them, then amend
- run `git log` to show we are still in the middle of rebase
- now run `git rebase --continue`
- now rebase is done


[^1] This is just one example. Don't write blogs? Well, suppose you were working on a certain part of your code and had left some superfluous `console.log` statements there. The principal is the same. 