---
layout: post
title: Change default org-mode HTML tags
tags: org-mode, emacs, HTML, tags
category: blog
permalink: /blog/org-html-tags/
author: sachin
comments: true
---

This brief post is result of a
[question](https://plus.google.com/110929313922902668537/posts/8FLNDvKc3sp)
posted by Icaro Perseo. He used org-mode for blogging using
[org2blog](https://github.com/punchagan/org2blog), but was not
satisfied with default HTML tags used by org-mode.

He wanted to change the default emphasis on text when it is converted
to HTML in org-mode. By default during conversion from org to HTML,

`/text/` converts to `<i>text</i>`

and

`*text*` converts to `<b>text</b>`

He wished to use `<em>` and `<strong>` instead of `<i>` and `<b>`.

Well, everything can be customized from Emacs and Icaro's solution to
his problem lies in the customization of group `org-appearance`. To
customize this group, type

    M-x customize-group org-appearance

and search for the variable `Org Emphasis Alist`


![img]({{ site.baseurl }}/images/org-html-tags/OrglEmphasisAlist.png "Variable: Org Emphasis Alist")

**Variable: Org Emphasis Alist**

Now change the value of **HTML start tag** and **HTML end tag**
to whatever you want.

#### Update - March 1, 2016: This solution is NOT valid for Emacs-pretest version(25.0.91.1)
