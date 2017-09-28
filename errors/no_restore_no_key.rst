Specified key not found in backups when restoring.
==================================================

Errcode: 101
Errstr: no_restore_no_key

When restoring, the specified key needs to be found in the ``config`` file, under the backups heading. Otherwise the restorer won't know what to do with the backup.

Run ``$ sheep projects`` to view available projects found in the config file.