A set of roles for installing an OpenShift Container Platform cluster on Red Hat Enterprise Linux machines.
The installation has been broken down into several roles to make consumption easier. Each role has a set of variables that may be overwritten at execution time.

It is assumed that the RHEL machines do not exist; as such, they will be 

Requirements
------------

Subscription manager credentials and pool ID are required as variables. See below.

Role Variables
--------------

See group_vars/masters and group_vars/nodes in order to specify variables for all hosts in their corresponding group. Each role has their own set of variables, broken down as follows:

  - [OpenStack](roles/openstack/README.md)
  - [IPA](roles/ipa/README.md)
  - [Keys](roles/keys/README.md)
  - [RHN](roles/rhn/README.md)
  - [Prepare](roles/prepare/README.md)
  - [Install](roles/install/README.md)

Dependencies
------------

All the rolez!

Example Playbook
----------------

    ---
    - name: Install OpenShift
      hosts: all
      gather_facts: False
      vars:
        ansible_ssh_common_args: -o StrictHostKeyChecking=no
        domain: cloudsalab.com
      roles:
        # deploy in target platform. if other platforms are required, create a role for that
        # platform and add another line. Destination provider is defined as a group variable.
        - { role: openstack, when: "hostvars[inventory_hostname]['provider'] == 'openstack'" }

        # create and add DNS entries
        - { role: ipa }

        # create and copy SSH keys
        - { role: keys }    

        # register with subscription manager
        - { role: rhn, version: '3.7'}

        # prepare all hosts for installation
        - { role: prepare } 

        # prepare all hosts for installation
        - { role: install }

License
-------

BSD