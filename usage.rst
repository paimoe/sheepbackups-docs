Usage
========
``$ sheep -h`` will list all available options.

Version 0.0.6:

::

    $ sheep -h
    usage: sheep [-h] [--project PROJECT] [--limit LIMIT] [--test] [--config CONFIG] [-V] [action] [match]

    Sheep Backups 0.0.6. 
    
    positional arguments:
      action             What action to perform (backup, restore, list, check, ping, schedule)
      match              ID to match
    
    optional arguments:
      -h, --help         show this help message and exit
      --project PROJECT  Which project to use when searching
      --limit LIMIT      Number of results returned (default 10)
      --test             Do a test backup/restore, but don't actually run
      --config CONFIG    Path to config file (default ~/.sheepbackups/config.yaml)
      -V, --version      Return this version
      
=======
Actions
=======

backup
------
Runs the backups specified in the config file. This will loop through any projects available, run the required actions, create an archive then upload it to the specified destination. It then calls the API to log an entry on the Sheep Backups website.

restore
-------
Attempt to restore an older backup. This will essentially do the reverse of the backup instructions, e.g. move the files back into their directories, or import an .sql file using the same connection options. There will be a confirmation with checks before performing the restore. Occasionally, if files have changed too much, it will list and skip over those restores while performing the other actions.

Restore requires a unique ID, or a unique-enough ID. If multiple ones are available (e.g. ``$ sheep restore a``), it will list matches and require a more precise ID.

list
----
Retrieve the latest 10 entries from the :doc:`api`. If you use the `limit`_ option, you can change the number of entries requested.

check
-----
``check`` will load your backup config and attempt to find any errors, as well as any errors that may result if a backup is run. It will also check for installed modules (eg ``mysqldump``) if it's specified in the backup file.

========
Options
========

test
----
Adding the test flag will run through all the available backup options, combine them into a temp directory, archive them, but not call the API or perform the upload. The information will be returned (size, file location, any errors) and you can review the log file or simply delete them after.

project
------
Specify which project to return when running ``$ sheep list``

limit
-----
The number of entries returned from the API when using **list**.

config
------
Set the path to the config file. By default it uses ``~/.sheepbackups/config.yaml``.