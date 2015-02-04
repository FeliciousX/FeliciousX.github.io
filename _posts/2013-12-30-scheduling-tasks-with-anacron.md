---
title: "Scheduling Tasks with Anacron on Fedora"
description: "Running tasks anachronistically"
category: "Tutorial"
tags: [anacron, tutorial, how-to, linux, fedora]
---

### Disclaimer
There are many good tutorials available out there. This is my own tutorial based on my own experience. If there are mistakes please do comment below and let me know.

## [Cron][1] vs [Anacron][2]

Just a few days ago, I [posted about Cron][3] and how you can schedule tasks to run on specific time. Cron has a weakness. A task with specified time will not run if the machine is not running as I have mentioned previously on my post. Anacron fixes this by enabling user to set when a task should run on boot time.

| Cron | Anacron |
| :--- | :------ |
| Sensitive to the minute | Sensitive to the number of days |
| Can be run by any user | Can only be run by root (there are workarounds) |
| Only executed if machine is running | Will execute during start up with delay in minutes |

Use Anacron if you want a task to be repeated every _x_ days and you don't care what time it is executed.

Use Cron if you want to execute a task automatically at a specific time (provided your machine is running).

## Implementation

The anacron configuration file can normally be found at `/etc/anacrontab` . If you were to run `cat /etc/anacrontab` you would see something like this...

{% highlight bash linenos %}
# /etc/anacrontab: configuration file for anacron

# See anacron(8) and anacrontab(5) for details.

SHELL=/bin/sh
PATH=/sbin:/bin:/usr/sbin:/usr/bin
MAILTO=root
# the maximal random delay added to the base delay of the jobs
RANDOM_DELAY=45
# the jobs will be started during the following hours only
START_HOURS_RANGE=0-23

#period in days   delay in minutes   job-identifier   command
1	5	cron.daily		nice run-parts /etc/cron.daily
7	25	cron.weekly		nice run-parts /etc/cron.weekly
@monthly 45	cron.monthly		nice run-parts /etc/cron.monthly
{% endhighlight %}

Lines that begins with _#_ are comments. ( _duh_ )

Line 5 to 11 (excluding comments) are environment variables.

__SHELL__ is for the path where your shell lies.

__PATH__ is the environment paths. ([do I really need to explain?][4])

__MAILTO__ specifies the user which anacron will mail to. (I'm not sure about this because I never needed it as I'm using my own workstation instead of a remote server)

__RANDOM_DELAY__ specifies a random delay in minutes when the job wil run after startup.

__START_HOURS_RANGE__ specifies the range of hours that the tasks will only run in. 0 means 12AM. 23 means 11PM. Go figure. (Default is 3-22 or 3AM to 10PM)

Line 14, 15 and 16 is where the magic really happens. There's 4 columns that I will tabulate below for an easier explanation.

| Period in days | Delay in minutes | Job Identifier | Command |
| :------------: | :--------------: | :------------- | :------ |
| 1 | 15 | cron.daily | your/command/here |

Basically, you can only specify how often the execution be in days. For the table above it's daily. Every 1 day that is. Each time the machine is started up, it will wait for a 15 minute delay and then it will run `your/command/here` and update the timestamp at `/var/spool/anacron/cron.daily` which is specified by the _Job Identifier_ column.



## References

For more in-depth knowledge, here's a few links:

- [Cron Vs Anacron: How to Setup Anacron on Linux][5]
- [Automate Linux with Cron and Anacron][6]
- [How to use anacrontab to schedule tasks][7]

[1]: http://en.wikipedia.org/wiki/Cron "Cron wiki"
[2]: http://anacron.sourceforge.net/ "Anacron Sourceforge"
[3]: /tutorial/2013/12/27/automating-tasks-with-cron-jobs/ "Automating Tasks with Cron Jobs"
[4]: http://www.linfo.org/path_env_var.html "PATH definition"
[5]: http://www.thegeekstuff.com/2011/05/anacron-examples/ "The Geek Stuff"
[6]: http://www.tuxradar.com/content/automate-linux-cron-and-anacron "Tux Radar"
[7]: http://www.linuxandlife.com/2013/03/how-to-use-anacrontab-to-schedule-tasks.html "Linux and Life"
