---
title: "Automating Tasks with Cron Jobs"
description: "Learning how to use Cron Jobs from scratch."
category: "Tutorial"
tags: [tutorial, how-to, cron, linux, crontab, fedora]
---

### Disclaimer

There are many good tutorials available out there. This is my own tutorial based on my own experience. If there are mistakes please do comment below and let me know.

### Note

The tutorial will be in 3 parts. First part [showing the application](#lets_get_started), followed by the [explanation](#what_happened) and finally the [things to be aware of](#important_notes) when using cron jobs.
Check out [Anacron][5] too if you will.

## Let's get started!

Say you have a script called `magic.sh` and you want to run it at **3.33AM, on the 15th of every month**.

How do we do that?

Open terminal and type `crontab -e`

Then type in...

`33 3 15 * * /path/to/magic.sh`

Save and exit. If you're doing it correctly you should see *crontab: installing new crontab*.
If you were doing it wrong it will prompt you to either quit or re-edit so you know if you're doing it right or wrong.

Type `crontab -l` to show your previous crontab.

Viola! Your script will run at the 33rd minute of the 3rd hour of the 15th day of every month on any day! Now to delete the crontab entirely just type `crontab -r`. Confused? Okay. Explanation below.

## What happened?

As you can already guess, `crontab -e` means *edit crontab*.

Here comes the most important bit. Basically crontab takes 5 numbers seperated by spaces followed by the command you want it to run.

| Minute | Hour  | Day-of-Month | Month | Day-of-Week | Command |
| :----- | :---- | :----------- | :---- | :---------- | :------ |
| 33     | 3     | 15           | \*    | \*          | /path/to/magic.sh |

This is the basic you will need to know to schedule anything on cron.

The first 4 column is self-explanatory. The Day of Week however, seem to be a little vague.
It's a range of number from 0 to 7.

- 0 means Sunday
- 1 means Monday
- 2 means Tuesday
- 3 means Wednesday
- 4 means Thursday
- 5 means Friday
- 6 means Saturday
- 7 means Sunday

Notice that 0 and 7 both means Sunday. Hence you don't need to worry which number is for Sunday and just know that 1 means Monday and count from that. *Easy peasy*

Good news! There's shortcuts for you -laz- efficient people! [Source][1]

| Special string |	Meaning  |
| :------------- | :-------- |
| @reboot        |	Run once, at startup.             |
| @yearly        |	Run once a year, "0 0 1 1 \*".    |
| @annually      |	(same as @yearly)                 |
| @monthly       |	Run once a month, "0 0 1 \* \*".  |
| @weekly        |	Run once a week, "0 0 \* \* 0".   |
| @daily         |	Run once a day, "0 0 \* \* \*".   |
| @midnight      |	(same as @daily)                  |
| @hourly        |	Run once an hour, "0 \* \* \* \*" |

So just type...

`@weekly /path/to/script`

which is equal to

`0 0 * * 0  /path/to/script`

Oh! I forgot to mention, what's that *asterisks* (\*) are for. You can do much more things with the numbers.
You can actually use more than just *asterisks*. Altogether there's **asterisk (\*)** **comma (,)**, **dash (-)**, and **seperator (/)**.

This is how I remember their usage:

- Asterisks is for **ALL the Values**
- Comma is for a **List of Values**
- Dash is for a **Range of Values**
- Seperator is for the **Step Value**

Using \* on a field is just like saying on every *column*.
Putting \* on the hour field means it's gonna be on *every hour*

The way to use **comma** is to list like certain days. For example you want to run a script on Monday, Wednesday and Friday only. It will look something like this..

`0 0 * * 1,3,5  /path/to/script`

Script is ran on every 0:00 AM on any date of any month on every Monday or Wednesday or Friday.

The way to use **dash** is simple. Just like **comma** but instead of a list of values it's a range of values.
For example, running a script every weekdays.

`0 0 * * 1-5  /path/to/script`

Script is run on every 0:00AM on any date of any month on every Monday to Friday.

The way to use seperator is more tricky (for me at least). Say you want to run your script every 2 hours, how are you going to write it?

{% highlight bash %}
0 0 * * * /path/to/script
0 2 * * * /path/to/script
0 4 * * * /path/to/script
...
{% endhighlight %}

really? No.

You can do it by just typing...

`0 */2 * * * /path/to/script`

Every 2 hours it is executed. Simple. You can already deduce how to do it for minute, hour or month.
There's more advanced things you can do and play around with your creativity. For example if you want to [run a script every forthnight][3], you can but I'm not covering that in this tutorial. Just the basics.

There're more things you can do with crontabs. These are just the basics. You can look at the [references](#references) that I used for more advanced technique.


## Important notes

Cron jobs will not run if machine is not on at the specified scheduled time. So for example if you set a cron job that runs every Friday night at 10PM and your machine is not running at that specific moment, the cron job will not be executed. Nor will it execute if you turn your machine on after the specified time.

Different users will not share their crontab unless the crontab is by *root* user. Running `crontab -e` is creating a cron job for your current user. To create a cron job for other user type `crontab -u USERNAME -e`

So for example, if you set cron job for root, it will run no matter who is logged on.

Also while editing crontabs, you can have user specific commands (correct me if I'm using the wrong term for it).

`0 0 * * * USERNAME /path/to/script`

Another alternative for Cron would be [Anacron][4]. Check it out at [this post][5] to understand how to use Anacron.

That's all. I hope I didn't miss out any crucial points. All of these should be enough for my own future reference and also detailed enough to create simple cron jobs.

## References
To get more on cron jobs, I advice you to see the manuals by typing.

{% highlight bash %}
man cron
man crond
man crontab
man crontabs
{% endhighlight %}

Visit these links for more examples:

* [HowTo: Add Jobs To cron Under Linux or UNIX?][1]
* [Scheduling Tasks with Cron Jobs][2]


[1]: http://www.cyberciti.biz/faq/how-do-i-add-jobs-to-cron-under-linux-or-unix-oses/ "nixCraft"
[2]: http://net.tutsplus.com/tutorials/other/scheduling-tasks-with-cron-jobs/ "net tuts+"
[3]: http://www.fclose.com/1199/how-to-run-a-cron-job-every-two-weeks-months-days/ "Fclose.com"
[4]: http://anacron.sourceforge.net/ "Anacron soureforge"
[5]: /tutorial/2013/12/30/scheduling-tasks-with-anacron/ "Scheduling Tasks With Anacron"
