# tw-tod-crontab
A crontab setup to export a Time Of Day system variable, as a filter for http://taskwarrior.org

It is a re-imagining of an older project of mine (https://github.com/linuxcaffe/tw-tod-sh) that used a more convoluted approach.

One of the most important things to make your big task list manageable, is to filter out tasks that are not immediately actionable. Many tasks are ideally done at a certain time of day, for example, some like to make calls in the morning, run errands in the afternoon, work on hobbies in the evening, work on the garage on the weekend. Not every task is Time Of Day specific, but for those that are, it could be helpful to conceal those task outside of those times. 

This project (tw-tod-crontab) aims to make that work using taskwarrior's (new) ability to use system variables, and by allowing the use to add the appropriate tag(s) (+morn, +aft, +day, +eve, +night, +wkday, +wkend). Just filtering for the TOD tag won't be effective unless _every_ task has a correct TOD tag, much better is to filter out those tasks with TOD tags _other_ than the one you are in now. How does task know that? Crontab! The following crontab entries are an attempt to do that. 

(caveat, I havent got it working yet, I'm still learning how cron works, and could use some help) 

```
6-12 * * 1-5 export TOD=( -aft -eve -night -wknd )
12-17 * * 1-5 export TOD=( -morn -eve -night -wknd )
17-21 * * 1-5 export TOD=( -morn -aft -day -night -wknd )
21-23 * * 1-5 export TOD=( -morn -aft -day -eve -wknd )
6-12 * * 0,6 export TOD=( -aft -eve -night -wkday )
12-17 * * 0,6 export TOD=( -morn -eve -night -wkday )
17-21 * * 0,6 export TOD=( -morn -aft -day -night -wkday )
21-23 * * 0,6 export TOD=( -morn -aft -day -eve -wkday )
```

Once the TOD crontab is working (some help here?) the system varable $TOD could be use in a report or at the CLI to hide those tasks better accomplished at another time.  
