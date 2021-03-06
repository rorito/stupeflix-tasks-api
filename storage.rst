.. highlight:: js

Storage systems
===============

Storage systems, introduced in the :doc:`/v2 API <api>`, allow you to choose
where your task output files are stored.

Here is an example request storing two thumbnails in the
:ref:`storage_persistent` and :ref:`storage_volatile` storages::

    {
        "tasks": [
            {
                "task_name": "image.thumb",
                "task_store": {
                    "type": "volatile"
                },
                "url": "http://files.com/image.jpg"
            },
            {
                "task_name": "image.thumb",
                "task_store": {
                    "type": "persistent"
                },
                "url": "http://files.com/image.jpg"
            }
        ]
    }

.. _storage_persistent:

persistent
----------

This is the default storage system, it stores files permanently on Cloudfront.

You can change the lifetime of your files with
:http:post:`/v2/storage/expiration`.

You can manage the files in your persistent storage with the
:ref:`v2_storage_api`.

Additional costs are applied to the persistent storage, `please read our
pricing <https://developer.stupeflix.com/pricing/#hosting>`_.

.. _storage_volatile:

volatile
--------

Files are stored for a week on S3, and permanently deleted.

youtube
-------

Upload videos on Youtube. It requires the following parameters:

    * **access_token** (string) - Target user's access token with upload
      authorization.
    * **developer_key** (string) -Youtube developer key of a registered app.
    * **title** (string) - Video title.

The following optional parameters are also accepted:

    * **description** (string) - Video description.
    * **tags** (list of strings) - List of video tags.
    * **category_id** (integer) - Video category ID number.
    * **privacy_status** (string) - Privacy status of the video. Accepted
      values are "public", "private" and "unlisted" *(default: "public")*.

s3_signed
---------

Upload to S3 signed URLs. It requires the following parameters:

    * **url** (string) - the S3 signed URL to upload to.
