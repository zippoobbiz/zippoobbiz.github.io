---
title: 'Git vs Mercurial: Why Git? Why Mercurial?'
date: 2016-12-04 17:01:24
tags: [Version Control, Git, hg]
categories: [Dev, Version Control]
---

I used to use SVN and Git, never used CVS and never heard about Mercurial. Okay, recently I joined a new company, and they use Mercurial hg, so I read some articles about it. Since Git is very popular nowadays, I would like to compare Mercurial to Git, to find what are different between them, what are the same? And which to choose.

[Git vs Mercurial: Why Git?](http://blogs.atlassian.com/2012/03/git-vs-mercurial-why-git/)
[Mercurial vs Git: Why Mercurial?](http://blogs.atlassian.com/2012/02/mercurial-vs-git-why-mercurial/)

First, I find these two articles, one prefers Git and the other likes Mercurial, but the tricky thing is both of them believe they pick the right one with a safer history control. If we have a closer look, we’d know that both of them are well in a given situation.

According to Charles O’Farrel, Git never deletes or modify something, the only thing you can do is commit, making a new object without eliminating the old one, keep the old one for 30 days then delete them if they do not have a reference. Mercurial do not have such features unless installing extensions, which have a few more steps to do than Git.

On the contrary, Steve Losh claims that it is risky to give users easy access to destructive commands, since they may not fully understand the commands, and sometimes, the git commands which have more arguments are a bit more complicated than Hg’s. Besides, you might lose the history completely in 30 days, but you will never lose them in Mercurial since most of the extensions will permanently back up any changesets that they destroy into a bundle, and these bundles will not be garbage collected, so “you don’t have to worry about your version control system eating your data”.


![Alt text](http://og2api1gp.bkt.clouddn.com/static/images/mercurial-vs-git.jpg "Optional title")

As mention above, Mercurial has more specific commands for each purpose, Git use less command with different arguments, the author in the second article prefers Mercurial, due to “ each command should do one thing and do it well”, which follows the UNIX philosophy.

![Alt text](http://og2api1gp.bkt.clouddn.com/static/images/git-vs-hg.jpg "Optional title")
