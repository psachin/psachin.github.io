---
layout: post
title: Commit part of a file
tags: git, partial commit, file
category: blog
permalink: /blog/partial-commit/
author: sachin
comments: true
---

We seldom have a situation where only a part of a file needs to be
committed. This may be due to the fact that within a file, we do not
want to commit those changes of which we are unsure about. Let me
introduce you to `--patch`, one of the options of `git-add`.

I have few parts in a file, lets call them "hunk". Some of the hunks,
I wish to commit, others I don't want to commit(I'm not sure if they
are worth it).

As usual, I start by adding a file, but this time, instead of using
`git add <FILENAME>`, I'll include an option `--patch` to `git-add`,

``` bash
git add --patch <FILENAME>
```

This will give me a chance to review my changes. Git carefully scans
my changes, and will prompt me for every hunk he detects modified
content. I'll have an option to stage(y), do not stage(n), quit(q),
stage all hunks(a), and so no. Full list of options with explanation
is displayed while using option `--interactive` with `git-add`.

I want to stage the first hunk, I will say 'y' here as show in below
snapshot.

![img]({{ site.baseurl }}/images/partial-commit/readme_warning_yes.png
 "Commit ReadMe.org warning"){: center-image}

Git will go head and present me with second hunk. I'm not sure of
these changes and I'll say 'n' at the prompt.

![img]({{ site.baseurl }}/images/partial-commit/test_use-package_no.png
 "Do not commit use-package test"){: center-image}

Git will not stage that piece of change, and will jump to next hunk. I
want to commit this hunk. I'll enter 'y' as show below.

![img]({{ site.baseurl }}/images/partial-commit/prog-mode-hook_yes.png
 "Commit prog-mode-hook"){: center-image}

If I check the status of the file after completed answering the
prompts, I still see that file in un-staged area. This is similar to
modifying the file after staging. This is expected as I have partially
staged the file(Note that `st` is an alias for `status`).

![img]({{ site.baseurl }}/images/partial-commit/git_status.png
 "Git status"){: center-image}

Further, `git diff` will display the changes, I ignored during the
interactive mode.

![img]({{ site.baseurl }}/images/partial-commit/git_diff.png "Git
diff"){: center-image}

But `git diff --cached` will have all staged hunks.

![img]({{ site.baseurl }}/images/partial-commit/git_diff_cached.png
 "Git diff cached"){: center-image}

Ensuring that I have what I needed in my staging area, I can go ahead
and commit my changes.

- Reference

	[https://git-scm.com/docs/git-add](https://git-scm.com/docs/git-add)

