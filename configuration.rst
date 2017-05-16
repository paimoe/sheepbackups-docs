Configuration
===============

.. role:: red

After installation, the config file will be located at ``~/.sheepbackups/config.yaml``. This will be prefilled with some example data::

    # https://docs.sheepbackups.com/configuration
    api_key: 
    api_url: https://api.sheepbackups.com/0/
    email: contact@example.com
    
    locations:
      s3: 
        bucket: example
        prefix: backups
    
    backups:
      example:
        to: 
          location: s3
        collect:
          dirs:
            images: /www/website/media/images
            
* ``api_key`` is available on the dashboard of your account.
* ``email`` is for any emergency contact in case the api is unreachable.
* ``locations`` is a block that determines where the archives will be uploaded to. Currently it supports S3.
* ``backups`` is the block where your individual backup is configured.

Locations
---------
``locations`` currently supports ``s3``. The following options are available:

+--------+--------------------------------------------------------------------------------------------------------------------------------------+
| bucket | This is the s3 bucket to upload to.                                                                                                  |
+--------+--------------------------------------------------------------------------------------------------------------------------------------+
| prefix |This will be prepended to the key, for example a folder. Setting this to ``foo`` would create the S3 keys ``foo/<prefix>_<date>.zip`` |
+--------+--------------------------------------------------------------------------------------------------------------------------------------+

The connection details are sourced from the AWS CLI config file, which is usually located at ``~/.aws/config``. More information on the boto3 config can be found `here <http://boto3.readthedocs.io/en/latest/guide/quickstart.html#configuration>`_.

Backups
--------
The backups key contains the information for what will be saved, moved, run etc. Each section uses the name of the project. You can set this to anything you want, and it will be created if it doesn't exist, provided you have projects available. Under the project name, only one key is required: ``to``. This will point to an option in the ``locations`` block. The other options are different backup methods. These will all be run and executed and combined into a backup.

All available methods are on the :doc:`options` page.