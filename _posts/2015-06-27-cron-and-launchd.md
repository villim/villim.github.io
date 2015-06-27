---
title: Cron & Launchd
layout: post

---
It's quite usefull when want to run scripts under given date and time. At this moment, you will need Cron (for Unix/Linux) and Lauchd (OSX).

## Cron and Crontab

### Create Cron Job
{% highlight bash %}
$ crontab -e
{% endhighlight %}

You can add one line like:
{% highlight bash %}
1 2 3 4 5 /path/to/command arg1 arg2
or
1 2 3 4 5 /root/backup.sh
{% endhighlight %}

### The Cron job definition
{% highlight bash %}
* * * * * command to be executed
- - - - -
| | | | |
| | | | ----- Day of week (0 - 7) (Sunday=0 or 7)
| | | ------- Month (1 - 12)
| | --------- Day of month (1 - 31)
| ----------- Hour (0 - 23)
------------- Minute (0 - 59)
{% endhighlight %}

And there's special string for simplify configuration:

|Special string	|Meaning|
| ------------ | ------------- | 
|@reboot	|Run once, at startup.|	
|@yearly	|Run once a year, "0 0 1 1 *".|
|@annually	|(same as @yearly)|
|@monthly	|Run once a month, "0 0 1 * *".|
|@weekly	|Run once a week, "0 0 * * 0".|
|@daily	    |Run once a day, "0 0 * * *".|
|@midnight	|(same as @daily)|
|@hourly	|Run once an hour, "0 * * * *".|

### List Cron Jobs
{% highlight bash %}
$ crontab -l
$ crontab -u username -l
{% endhighlight %}

## Lauchd and Launchctl

Instead of simple command, OSX's alternative tool is really urgly. You need to create XML .... -_-||

Whatever, if later have to use it. Here's a pretty good documentation. [Schedule jobs using launchd](http://nathangrigg.net/2012/07/schedule-jobs-using-launchd/)


