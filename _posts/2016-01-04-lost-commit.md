---
layout: post
title: Lost commit
tags: git, commit, remote
category: blog
permalink: /blog/lost-commit/
author: sachin
comments: true
---

Where's my commit after I did `git commit --amend`?

`git commit --amend` comes handy if one wants changes in a previous
commit or simply want to change a commit message but this results into
push errors and an extra over-head of a merge-commit. In this post,
lets go through the process.

Say I have three commit in my master branch but I'm not satisfied with
the last commit message.

![img]({{ site.baseurl }}/images/lost_commit/git_log_before_amend.png
"Commit logs before amend")
**Commit logs before amend**

I changed the commit message using the command.

    git commit --amend -m 'Attack plan-2'

![img]({{ site.baseurl }}/images/lost_commit/commit_amend.png
"Commit amend")
**Making an amendment to last commit message**

and tried to push the changes. Soon I'll encountered an error(see
image below). Something is not right. The remote server is not
accepting my changes. It says my local commits are not in-sync with
the remote commits. But what did I do? I just changed a commit
message.

![img]({{ site.baseurl }}/images/lost_commit/git_push_error.png
"Push error")
**git push throws error**

If I check the commit logs(see image below), I see my updated
message. This was expected. But what exactly went wrong?

![img]({{ site.baseurl }}/images/lost_commit/git_log_after_amend.png
"Git logs after amend")
**Commit logs after amend**

If I closely examine the commit hash of HEAD before and after the
amendment, I can see it has changed.

- Before amend: `36e2d601c446`
- After amend : `14c15632fa9d`

Which clearly means that *amend* changed the hash and now my local and
remote differs. My remote still has that old hash(with old commit
message) but HEAD's commit hash has changed.

This also means that I lost my old hash and that is now over-written
by a **brand-new** commit.

Below commands can be really handy:

- Check local commit

        git log

- Check remote commit

        git log origin

- View both local and remote(origin) logs all-together

        git log origin master

With the last command, I can see local commits plus the lost
commit(which still exits on the remote). Below figure can explain the
scenario in a better way.

![img]({{ site.baseurl }}/images/lost_commit/lost_commit.png "Lost commit")
**Lost(not visible) commit(in green) after amend**

In order to push, I first need to pull that lost commit from remote. A
simple

    git pull

or

    git pull origin master

should do the trick(image below).

![img]({{ site.baseurl }}/images/lost_commit/git_pull_origin_master.png "Git pull
from origin")
**Pull(and merge) commits from origin**

If I check the commit logs, I see my lost commit is in place just
below the *changed message* commit.

![img]({{ site.baseurl }}/images/lost_commit/git_log_after_pull.png
"Git log after pull") **Commit logs after pull**

But there's one extra commit, a **merge-commit** as HEAD(see figure
below)

![img]({{ site.baseurl }}/images/lost_commit/commits_after_pull.png
"Commits after pull")
**An extra merge-commit(in blue) on top of amended commit**

Now I can safely push to the remote as the *lost commit* exist in my
local commit log.

![img]({{ site.baseurl }}/images/lost_commit/git_push_origin_master.png
"Git push")
**Push merged commits**

Which should sync local & remote repos(figure below)

![img]({{ site.baseurl }}/images/lost_commit/commits_after_push.png "Commits after push")
**Local & remote commit are in-sync now**

*PS*: If you want to avoid a merge-commit, Git provides an excellent
 way to achieve it via
 [git-rebase](https://git-scm.com/docs/git-rebase). What it typically
 does is it rolls-up all the latest commits on the top of all the
 previous commits. Behind the curtains `git-rebase` completely
 re-writes the history. As the matter of fact one should never rebase
 commits that have been pushed to a public.
