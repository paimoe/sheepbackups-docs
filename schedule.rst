========
Schedule
========

The scheduler uses the installed ``crontab`` program::

    $ sheep schedule
    
Will allow you to check whether it is currently running in crontab::

    $ sheep schedule <option>
    
Adding ``option`` (currently only ``midnight``) will allow you to set the cron, if it doesn't already exist. Alternatively, you can also manually edit it::

    $ crontab -e
    
    # sheepbackups
    0 0 * * * /usr/bin/sheep backup