.. cyrusman:: cyr_withlock_run(8)

.. author: Bron Gondwana

.. _imap-reference-manpages-systemcommands-cyr_withlock_run:

====================
**cyr_withlock_run**
====================

is used to run system command with a lock held

..  warning::

    This command runs as the Cyrus user, so if you need to call something
    as root, the cyrus user may need sudo privileges.

Synopsis
========

.. parsed-literal::

    **cyr_withlock_run** [ **-C** *config-file* ] [ **-u** *userid* ] cmd args...

Description
===========

**cyr_withlock_run** will run the command and arguments provided on the
command line, either locking the entire server, or a particular user, so
no changes can be made to it while this command is running.

WARNING: since this takes an exclusive lock, it MUST NOT be used to run a cyrus
internal program, which will also try to take the same locks, and cause a deadlock.

It is most useful for running an external filesystem snapshot command, which can
be run safely, knowing that files aren't in a partial state.


**cyr_withlock_run** |default-conf-text|

Options
=======

.. program:: cyr_withlock_run

.. option:: -C config-file

    |cli-dash-c-text|

.. option:: -u, --user <userid>

   Lock just the specified userid rather than the global lock.

   NOTE: if you run for the global lock, then your server must have the
   `global_lock` config option set, or this command will fail with an
   error as it can't get a guaranteed lock.

Examples
========

.. parsed-literal::

    **cyr_withlock_run** sleep 300

..

        Pause all writes on the server for 300 seconds (stops any writes from getting locks)

Files
=====

/etc/imapd.conf

See Also
========

:cyrusman:`imapd.conf(5)`
