===================
Backup Options
===================
These are the available options for backups.
   
.. role:: red

##   
to
##

::

    backups:
        mysite:
            to:
                location: s3

+----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
|option                |description                                                                                                                                         |
+======================+====================================================================================================================================================+
|location :red:`(str)` | This should be a string that points to a setting in the ``locations`` block, to tell Sheep what to upload to. Currently this should only be ``s3`` |
+----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+

#######
collect
#######
``collect`` is a general purpose file fetching.

::

    backups:
        mysite:
            collect:
                dirs:
                    ex1: /example1
                    ex2: /example2/more
                files:
                    - /tmp/1
                exclude:
                    - "*.example"
                    

+----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
|option                | description                                                                                                                                                            |
+======================+========================================================================================================================================================================+
|dirs :red:`(dict)`    | Key/value dict. The keys will be the folders created inside the backup, and should just be a simple name. The values are absolute paths to the directories to include. |
+----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
|files :red:`(list)`   |A list of single files that will be collected.                                                                                                                          |
+----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
|exclude :red:`(list)` |A list of glob patterns to match against, which will be ignored when copying directories. Has no effect on the ``files`` option.                                        |
+----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#####
mysql
#####
Uses ``mysqldump`` to backup the db.

::

   backups:
      mysite:
         mysql:
            dbname: my_db
            config: /var/www/conf/my.cnf

+--------------------+------------------------------------------------------------------------------------------+
|option              |description                                                                               |
+====================+==========================================================================================+
|dbname :red:`(str)` | The name of the database to back up.                                                     |
+--------------------+------------------------------------------------------------------------------------------+
|config :red:`(str)` |A path to a file containing ``[mysqldump]`` arguments, including connection information.  |
+--------------------+------------------------------------------------------------------------------------------+
            
######
sqlite
######

This simple copies the sqlite files into the backup. The ``sqlite`` type is an array, listing all .sqlite dbs.

::

   backups:
      mysite:
         sqlite:
            - /var/www/db/my_db.db
            - /var/www/backups/other.sqlite
            