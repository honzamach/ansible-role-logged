.. _section-cookbook-roles-logged:

Central logging - client
================================================================================


.. _section-cookbook-roles-logged-newserver:

Enable logging to central log server
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

You central log server should already be installed and running using the role
:ref:`logged <section-role-logserver>`.

From the point of view of the log server you must enable access for the client.
Please refer to section :ref:`section-cookbook-roles-logserver-newclient` for more
details.

From the point of view of the client you only need to meet following conditions:

1. You must use appropriate ``trusted_ca`` certificates to be able to verify log
   server identity. These certificates are managed by the :ref:`certified <section-role-certified>`
   role and you will ussually use the same set of certificates on both client and
   server. The most easiest approach is then to place all CA certificate files to
   ``inventory/group_files/servers/honzamach.certified/ca_certs`` directory. They
   will be uploaded to ``/etc/ssl/trusted_ca`` directory on remote servers and
   the syslog-ng daemon will be automatically configured to use them.

2. You must add ``your-server`` to inventory group ``servers_logged``.

Then execute the role::

    apbf role_logged.yml

Please refer to role :ref:`logged <section-role-logged>` for more details.
