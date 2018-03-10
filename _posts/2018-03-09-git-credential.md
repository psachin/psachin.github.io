---
layout: post
title: 2 factor authentication and git
tags: git, GitHub, Gmail, 2FA, 2 Step Verification, git-credential, git-send-email
category: blog
permalink: /blog/using-git-credential/
author: sachin
comments: true
---


Google's [2 Step Verification](https://www.google.com/landing/2step/)
and GitHub's [2 Factor
Authentication](https://help.github.com/articles/about-two-factor-authentication/)
are preferred & secured but they are quite confusing when using `git`.
In this post lets see how to setup those and configure ``git`` using
generated password/token to send patch using `git-send-email` & push
commit to remote server using ``git-push``.


## Google's 2 Step Verification

Using this link
[https://security.google.com/settings/security/apppasswords](https://security.google.com/settings/security/apppasswords)
and setup App password. You need to login using your usual password
first. After successful login, a section **Password & sign-in method**
will show that your **2 Step Verification** is _Off_. Click the arrow
to turn on 2 Step Verification as shown below.

<p align="center">
<img src="{{ site.baseurl }}/images/git-credential/2StepVerification.png"
	alt="2StepVerification"
	width=""
	height="">
</p>

Next, you need to provide your phone number to receive a verification
code. You can get the code using _Text message_ or a _Phone call_ as
show below. Enter phone number and click _Next_.

<p align="center">
<img src="{{ site.baseurl }}/images/git-credential/1-3.png"
	alt="Enter Phone number"
	width=""
	height="">
</p>


Enter verification code and click _Next_.

<p align="center">
<img src="{{ site.baseurl }}/images/git-credential/2-3.png"
	alt="Enter verification code"
	width=""
	height="">
</p>


and click **TURN ON**

<p align="center">
<img src="{{ site.baseurl }}/images/git-credential/3-3.png"
	alt="Enter Phone number"
	width=""
	height="">
</p>

This is also a good time to have alternate backup option. I use [Free
OTP](https://play.google.com/store/apps/details?id=org.fedorahosted.freeotp)
but [Google
Authenticator](https://play.google.com/store/apps/details?id=com.google.android.apps.authenticator2)
is also good choice.

<p align="center">
<img src="{{ site.baseurl }}/images/git-credential/G-AuthenticatorApp.png"
	alt="Enter Phone number"
	width=""
	height="">
</p>


Next page will make you select the app and the device. 

<p align="center">
<img src="{{ site.baseurl }}/images/git-credential/select_app_select_device.png"
	alt="Select app & device"
	width=""
	height="">
</p>


For sake of this post I want to use the token to send Email using
``git-send-email``, I will select the app as **Mail**.

<p align="center">
<img src="{{ site.baseurl }}/images/git-credential/select_app.png"
	alt="Select app"
	width=""
	height="">
</p>


The device is nothing but my GNU/Linux system, I prefer to select
**Other (Custom name)**.

<p align="center">
<img src="{{ site.baseurl }}/images/git-credential/select_device.png"
	alt="Select device"
	width=""
	height="">
</p>

Name the app anything you want. As I plan to use the generated
password for ``git-send-email``, I prefer the same name. This also
will help me to manage multiple apps in future. Click **GENERATE** to
generate password.

<p align="center">
<img src="{{ site.baseurl }}/images/git-credential/app_name.png"
	alt="Enter app name"
	width=""
	height="">
</p>

A password is 16 characters. We need this password to send patches via
``git``

<p align="center">
<img src="{{ site.baseurl }}/images/git-credential/app_password.png"
	alt="Generate app password"
	width=""
	height="">
</p>


Once the password is handy, create a file ``~/git-credentials`` with
following line. Replace ``<username>`` with Gmail login name and
``<16CharPassword>`` with generated password. (_Note: This file is in
plan text._)

{% highlight bash linenos %}
smtp://<username>%40gmail.com:<16CharPassword>@smtp.gmail.com%3a587
{% endhighlight %}

Or store details in ``~/.gitconfig``

{% highlight bash linenos %}
[user]
    name = <FirstName LastName>
	email = <username>@gmail.com
[sendemail]
	smtpEncryption = tls
	smtpServer = smtp.gmail.com
	smtpUser = <username>@gmail.com
	smtpPass = <16CharPassword>
	smtpServerPort = 587
	suppresscc = all
{% endhighlight %}

Or you can use [``git credential helper
store``](https://git-scm.com/docs/git-credential-store) to store above
details

Test the settings by sending a patch,

{% highlight bash linenos %}
git send-email --to=user@somedomain.com -1
{% endhighlight %}


## GitHub's 2 Factor Authentication

Generate new token using this link
[https://github.com/settings/tokens](https://github.com/settings/tokens)
and click **Generate new token** as shown below,

<p align="center">
<img src="{{ site.baseurl }}/images/git-credential/generate-github-token.png"
	alt="Generate GitHub token"
	width=""
	height="">
</p>

and store the token in ``~/.git-credentials`` as below,

{% highlight bash linenos %}
https://<GitHub username>:<GitHub Token>@github.com
{% endhighlight %}

Test the setting by pushing a commit.

Each credential is stored on its own line in file
``~/.git-credentials`` file, something like,

{% highlight bash linenos %}
smtp://<username>%40gmail.com:<16CharPassword>@smtp.gmail.com%3a587
https://<GitHub username>:<GitHub Token>@github.com
{% endhighlight %}


## Reference

1. [git-send-email](https://git-scm.com/docs/git-send-email)
2. [git-credential-store](https://git-scm.com/docs/git-credential-store)
3. [GitHub Gist](https://gist.github.com/psachin/2c441d199bd2e7c015441238c8fe1c8b)


