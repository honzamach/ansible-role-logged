.. _section-role-logged:

Role **logged**
================================================================================

* `Ansible Galaxy page <https://galaxy.ansible.com/honzamach/logged>`__
* `GitHub repository <https://github.com/honzamach/ansible-role-logged>`__
* `Travis CI page <https://travis-ci.org/honzamach/ansible-role-logged>`__

Main purpose of this role is to configure remote logging to central log server.

This role is designed as a client side counterpart to the role :ref:`section-role-logserver`,
the remote logging is automagically set up to all servers in the inventory group
**server_central_logserver**.

**Table of Contents:**

* :ref:`section-role-logged-installation`
* :ref:`section-role-logged-dependencies`
* :ref:`section-role-logged-usage`
* :ref:`section-role-logged-variables`
* :ref:`section-role-logged-files`
* :ref:`section-role-logged-author`

This role is part of the `MSMS <https://github.com/honzamach/msms>`__ package.
Some common features are documented in its :ref:`manual <section-manual>`.


.. _section-role-logged-installation:

Installation
--------------------------------------------------------------------------------

To install the role `honzamach.logged <https://galaxy.ansible.com/honzamach/logged>`__
from `Ansible Galaxy <https://galaxy.ansible.com/>`__ please use variation of
following command::

    ansible-galaxy install honzamach.logged

To install the role directly from `GitHub <https://github.com>`__ by cloning the
`ansible-role-logged <https://github.com/honzamach/ansible-role-logged>`__
repository please use variation of following command::

    git clone https://github.com/honzamach/ansible-role-logged.git honzamach.logged

Currently the advantage of using direct Git cloning is the ability to easily update
the role when new version comes out.


.. _section-role-logged-dependencies:

Dependencies
--------------------------------------------------------------------------------

This role is dependent on following roles:

* :ref:`certified <section-role-certified>`

No other roles have direct dependency on this role.


.. _section-role-logged-usage:

Usage
--------------------------------------------------------------------------------

Example content of inventory file ``inventory``::

    [server_central_logserver]
    your-backup-server

    [servers_logged]
    your-server

Example content of role playbook file ``role_playbook.yml``::

    - hosts: servers_logged
      remote_user: root
      roles:
        - role: honzamach.logged
      tags:
        - role-logged

Example usage::

    # Run everything:
    ansible-playbook --ask-vault-pass --inventory inventory role_playbook.yml


.. _section-role-logged-variables:

Configuration variables
--------------------------------------------------------------------------------


Internal role variables
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. envvar:: hm_logged__install_packages

    List of packages defined separately for each linux distribution and package manager,
    that MUST be present on target system. Any package on this list will be installed on
    target host. This role currently recognizes only ``apt`` for ``debian``.

    * *Datatype:* ``dict``
    * *Default:* (please see YAML file ``defaults/main.yml``)
    * *Example:*

    .. code-block:: yaml

        hm_logged__install_packages:
          debian:
            apt:
              - syslog-ng
              - ...


Foreign variables
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

:envvar:`hm_certified__cert_host_dir`

    The syslog-ng daemon will be configured to use custom server certificates.

:envvar:`hm_certified__trustedcert_ca_dir`

    The syslog-ng daemon will be configured to use custom CA certificate directory.


Built-in Ansible variables
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

:envvar:`ansible_lsb['codename']`

    Linux distribution codename. It is used for :ref:`template customizations <section-overview-role-customize-templates>`.


.. _section-role-logged-files:

Managed files
--------------------------------------------------------------------------------

.. note::

    This role supports the :ref:`template customization <section-overview-role-customize-templates>` feature.

This role manages content of following files on target system:

* ``/etc/syslog-ng/syslog-ng.conf`` *[TEMPLATE]*
* ``/etc/logrotate.d/apt`` *[TEMPLATE]*
* ``/etc/logrotate.d/aptitude`` *[TEMPLATE]*
* ``/etc/logrotate.d/dpkg`` *[TEMPLATE]*
* ``/etc/logrotate.d/syslog-ng`` *[TEMPLATE]*


.. _section-role-logged-author:

Author and license
--------------------------------------------------------------------------------

| *Copyright:* (C) since 2019 Honza Mach <honza.mach.ml@gmail.com>
| *Author:* Honza Mach <honza.mach.ml@gmail.com>
| Use of this role is governed by the MIT license, see LICENSE file.
|
