How do I kill a process / stop a program in Linux?
==================================================

Often times a process misbehaves and you may want to terminate or kill
it. In this post, lets see few ways to terminate a process or
application from Command line as well as via Graphical interface. We
will take [gedit](https://wiki.gnome.org/Apps/Gedit) as an example
application.


Kill/Stop process using Command line
------------------------------------

1. Using termination characters

   Ctrl + C
   --------

	One of the problem invoking `gedit` from command-line(if you are not
	using the command `gedit &`) that it will not free up the prompt. As a
	result that session is blocked. In such case Ctrl+C(Press Control key
	in combination with 'C' key) comes handy. That will terminate `gedit`
	and all work is lost(unless the file was saved).

	What Ctrl+C does at background is, it sends
    [SIGINT](http://man7.org/linux/man-pages/man7/signal.7.html)
    signal to gedit. This is a stop signal, The default action of this
    signal is to terminate the process. It instructs shell to stop
    gedit and return to main loop and you get the prompt back.


	```
	$ gedit
	^C
	```


   Ctrl + Z
   --------

   This is called a _suspend character_. It sends
   [SIGTSTP](http://man7.org/linux/man-pages/man7/signal.7.html)
   signal to process. This is also a stop signal but the default
   action is not to kill the process but to suspend the process.

   It will stop(not kill or terminate) gedit and return back the shell
   prompt.

   ```
   $ gedit
   ^Z
   [1]+  Stopped                 gedit
   ```

   One the process is suspended, in this case gedit, it is not
   possible to write or do anything with gedit. In the background it
   becomes a _job_. You can verify by typing `jobs`

   ```
   $ jobs
   [1]+  Stopped                 gedit
   ```

   The _jobs_ allows user to control multiple processes within a
   single shell session. One can stop, resume, move job to background
   or foreground at will.

   Lets resume gedit in background and free up a prompt to run other
   commands. This can be done using a command `bg` followed by job
   ID(Notice `[1]` from output of `jobs`, that is the job ID)

   ```
   $ bg 1
   [1]+ gedit &
   ```

   This is similar to running with `&` as in,

   ```
   $ gedit &
   ```


2. Using `kill`

   `kill` allows a fine controls over signal allowing a user to send
   signals to a process by specifying either a signal name or signal
   number followed by process ID or PID.

   What I like about `kill` is that it can also work with job IDs as
   well. Lets take gedit as an example again, but this time, lets
   start it using `gedit &`. Assuming I have a job ID of gedit by
   executing `jobs` command, lets send SIGINT to gedit

   ```
   $ kill -s SIGINT %1
   ```

   Notice that the job ID should be prefixed with '%', else `kill`
   will consider it as PID.

   `kill` works without specifying signal, a default action is to send
   SIGTERM which terminated the process. Execute `kill -l` to list all
   signal names and execute `man kill` to learn more about `kill`.

3. Using `killall`

   If you don't like specifying job ID or PID, `killall` lets you
   specify process name. A simplest usage of `killall` to terminate
   gedit is,

   ```
   $ killall gedit
   ```

   This will kill all the processes with name "gedit". Like `kill`,
   the default signal is SIGTERM. It has fancy option to ignore
   case using '-I'. For example,

   ```
   $ gedit &
   [1] 14852

   $ killall -I GEDIT
   [1]+  Terminated              gedit
   ```

   Learn various flag provided by `killall` like '-u' which allows to
   kill user owned process by exploring its man-page(`man killall`)


Kill/Stop graphical application
-------------------------------


1. Using `xkill`

	Ever encountered an issue where media player like
	[VLC](https://www.videolan.org/vlc/index.html) grayed out and you
	are not able to do anything? Well now you can certainly find PID
	and kill the application using above command or why not use
	`xkill`?


	[IMAGE: xkill_gedit.png]
	Caption: Using xkill

	`xkill` allows you to kill a windows using mouse, simply execute
	`xkill` in a terminal which should change the mouse cursor to
	**X** or a tiny skull icon and click **X** on a windows you want
	to close. Be careful using `xkill` though, it can be dangerous as
	its man-page says. You have been warned.


This brings to the end of this article. We learned few techniques to
kill & stop processes. Refer man-page of each command we discussed to
understand it's usage & working. I have left commands like `pkill` and `pgrep`,
for you to explore.
