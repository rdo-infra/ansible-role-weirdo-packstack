ansible-role-weirdo-packstack
-----------------------------
This role provides an implementation of the
Packstack_ gate jobs for the WeIRDO_ project.

.. _Packstack: https://github.com/openstack/packstack
.. _WeIRDO: https://github.com/redhat-openstack/weirdo

Supported gate jobs
~~~~~~~~~~~~~~~~~~~

* gate-packstack-integration-scenario001-tempest-dsvm-centos7
* gate-packstack-integration-scenario002-tempest-dsvm-centos7
* gate-packstack-integration-scenario003-tempest-dsvm-centos7

Role variables
~~~~~~~~~~~~~~

For default values, see `defaults/main.yml`_

* ``project``: Name of the project, analogous to the role name
* ``openstack_release``: Name of the OpenStack release to select which trunk repository to use by default
* ``version``: Version/tag/branch of Packstack to clone
* ``repository``: URL to the Packstack repository
* ``clone_path``: Path where Packstack will be cloned
* ``install_from_source``: Whether Packstack should be installed from source or from packages
* ``delorean_url``: URL to the delorean repository .repo file.
* ``delorean_deps_url``: URL to the delorean-deps repository .repo file.
* ``packstack_workspace``: Path where Packstack should believe the jenkins workspace is at
* ``selinux_enforcing``: When set to true, it will enable selinux enforcing in the system deploying packstack
* ``nested_virtualization``: When set to true, it will enable nested virtualization in the system based on availability

.. _defaults/main.yml: https://github.com/redhat-openstack/ansible-role-weirdo-packstack/blob/master/defaults/main.yml

Included tasks
~~~~~~~~~~~~~~

* ``setup``: Clones the Packstack repository and prepares log retrieval
* ``run``: Runs the integration tests

Dependencies
~~~~~~~~~~~~

`ansible-role-weirdo-common`_ to be installed as ``common``

.. _ansible-role-weirdo-common: https://github.com/redhat-openstack/ansible-role-weirdo-common

Example playbook
~~~~~~~~~~~~~~~~

.. code-block:: yaml

    - name: Run packstack scenario001 tests
      hosts: openstack_nodes
      force_handlers: True
      roles:
        - { role: "packstack", test: "scenario001" }
