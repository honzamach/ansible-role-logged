.. _section-role-feature-logged:

Role feature-logged
================================================================================

Ansible role for convenient configuration of remote logging to central log server.

* `Ansible Galaxy page <https://galaxy.ansible.com/honzamach/logged>`__
* `GitHub repository <https://github.com/honzamach/ansible-role-logged>`__
* `Travis CI page <https://travis-ci.org/honzamach/ansible-role-logged>`__


Description
--------------------------------------------------------------------------------

Main purpose of this role is to configure remote logging to central log server.

The remote logging is automagically set up to all servers in the inventory group
**server-central-logserver**.

.. note::

    This role supports the :ref:`template customization <section-overview-customize-templates>` feature.


Requirements
--------------------------------------------------------------------------------

This role does not have any special requirements.


Dependencies
--------------------------------------------------------------------------------

This role is dependent on following roles:

* :ref:`certified <section-role-certified>`

No other roles have direct dependency on this role.


Managed files
--------------------------------------------------------------------------------

This role directly manages content of following files on target system:

* ``/etc/syslog-ng/syslog-ng.conf``
* ``/etc/logrotate.d/apt``
* ``/etc/logrotate.d/aptitude``
* ``/etc/logrotate.d/dpkg``
* ``/etc/logrotate.d/syslog-ng``


Role Variables
--------------------------------------------------------------------------------

There are following internal role variables defined in ``defaults/main.yml`` file,
that can be overriden and adjusted as needed:

.. envvar:: hm_logged__package_list:

    List of role-related packages, that will be installed on target system.

    * *Datatype:* ``string``
    * *Default:* (please see YAML file ``defaults/main.yml``)


Foreign variables
--------------------------------------------------------------------------------


:envvar:`hm_certified__cert_host_dir`

    The syslog-ng daemon will be configured to use custom server certificates.

    * *Occurence:* **mandatory**

:envvar:`hm_certified__trustedcert_ca_dir`

    The syslog-ng daemon will be configured to use custom CA certificate directory.

    * *Occurence:* **mandatory**


Usage and customization
--------------------------------------------------------------------------------

This role is (attempted to be) written according to the `Ansible best practices <https://docs.ansible.com/ansible/latest/user_guide/playbooks_best_practices.html>`__. The default implementation should fit most users,
however you may customize it by tweaking default variables and providing custom
templates.


Variable customizations
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Most of the usefull variables are defined in ``defaults/main.yml`` file, so they
can be easily overridden almost from `anywhere <https://docs.ansible.com/ansible/latest/user_guide/playbooks_variables.html#variable-precedence-where-should-i-put-a-variable>`__.


Template customizations
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This roles uses *with_first_found* mechanism for all of its templates. If you do
not like anything about built-in template files you may provide your own custom
templates. For now please see the role tasks for list of all checked paths for
each of the template files.


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


Example Playbook
--------------------------------------------------------------------------------

Example content of inventory file ``inventory``::

    [server-central-logserver]
    remote

    [servers-logged]
    localhost

Example content of role playbook file ``playbook.yml``::

    - hosts: servers-logged
      remote_user: root
      roles:
        - role: honzamach.logged
      tags:
        - role-logged

Example usage::

    ansible-playbook -i inventory playbook.yml


License
--------------------------------------------------------------------------------

MIT


Author Information
--------------------------------------------------------------------------------

Jan Mach <honza.mach.ml@gmail.com>
