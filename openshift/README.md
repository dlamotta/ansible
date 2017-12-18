A set of roles for installing an OpenShift Container Platform cluster on Red Hat Enterprise Linux machines.
The installation has been broken down into several roles to make consumption easier. Each role has a set of variables that may be overwritten at execution time.

It is assumed that the RHEL machines do not exist so the very first role will create the instances. You have full control where instances are created; currently,
the only provider that exists is OpenStack but there is nothing that prevents others such as AWS, Azure, VMware, CloudForms, etc, from co-existing with each other.

The IPA machine is NOT created as part of this installation. You may ommit or modify that role if your DNS is served elsewhere.

Please contribute! We are happy for any pull request to make this installer better. Know that this was created exclusively for standing up OpenShift lab environments in an automated and repeatable fashion.

Start Here
------------

The first thing you'll want to check is the [inventory](inventory) file. This is where your soon-to-be-created instances are declared, along with some variables. Next up, see [group_vars/masters](group_vars/masters) and [group_vars/nodes](group_vars/nodes) in order to specify variables for all hosts specified in the inventory. Last but not least, take a look at the [site.yml](site.yml) and then look at each role to see what it's doing.

Requirements
------------

Subscription manager credentials and pool ID are required as variables. See below.

Role Variables
--------------

Each role has their own set of variables, broken down as follows:

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

The following example is exactly how the roles in this repository are being used in [site.yml](site.yml).

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

TODO
-------
This is currently a work in progress and by no means perfect (yet). Still needed:

  - An instance dedicated for NFS. Will need to create group_vars/nfs and modify group_vars/masters since currently the master is being used for all NFS volumes
  - We should not be modifying /etc/resolv.conf [see IPA role](roles/ipa/tasks/main.yml) and instead modify /etc/sysconfig/network-scripts/ifcfg-eth0 for setting the domain
  - Expanding the cluster
  - Environment cleanup in order to make it easy to start from a clean slate
  - Set hostnames after instance creation

License
-------

BSD
