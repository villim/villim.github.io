---
title: Cron & Launchd
layout: post
---

It's quite usefull when want to run scripts under given date and time. At this moment, you will need Cron (for Unix/Linux) and Lauchd (OSX).

## Cron and Crontab

### Create Cron Job

```bash
$ crontab -e
```

You can add one line like folliwng:

```bash
1 2 3 4 5 /path/to/command.sh arg1 arg2
```
or

```bash
1 2 3 4 5 /root/command.sh
```

This means to run command.sh with parameter or not.

### The Cron job definition

The most sophiscated stuff is the cron expression, like previous "1 2 3 4 5 " what does it means?

```
* * * * * command to be executed
- - - - -
| | | | |
| | | | ----- Day of week (0 - 7) (Sunday=0 or 7)
| | | ------- Month (1 - 12)
| | --------- Day of month (1 - 31)
| ----------- Hour (0 - 23)
------------- Minute (0 - 59)
```

### Special String
And there's special string for simplify configuration:

| Special String 	| Meaning |
| ------------  	| ------------ | 
| @reboot	      	| Run once, at startup. |
| @yearly			| Run once a year, "0 0 1 1 *". |
| @annually		| (same as @yearly) |
| @monthly		| Run once a month, "0 0 1 * *". |
| @weekly			| Run once a week, "0 0 * * 0". |
| @daily	    	| Run once a day, "0 0 * * *". |
| @midnight		| (same as @daily) |
| @hourly			| Run once an hour, "0 * * * *". |

This means, you can wirte like this:

```bash
@daily /root/command.sh
```

### List Cron Jobs

```bash
$ crontab -l
$ crontab -u username -l
```


## Lauchd and Launchctl

Instead of simple commands, OSX's alternative tool is really urgly. 

You need to create XML .... -_-||

Whatever, if later have to use it. Here's a pretty good documentation. [Schedule jobs using launchd](http://nathangrigg.net/2012/07/schedule-jobs-using-launchd/)


