A set of roles for installing an OpenShift Container Platform cluster on Red Hat Enterprise Linux machines.
The installation has been broken down into several roles to make consumption easier. Each role has a set of variables that may be overwritten at execution time.

It is assumed that the RHEL machines do not exist so the very first role will create the instances. You have full control where instances are created; currently,
the only provider that exists is OpenStack but there is nothing that prevents others such as AWS, Azure, VMware, CloudForms, etc, from co-existing with each other.

The IPA machine is NOT created as part of this installation. You may ommit or modify that role if your DNS is served elsewhere.

Please contribute! We are happy for any pull request to make this installer better. Know that this was created exclusively for standing up OpenShift lab environments in an automated and repeatable fashion.

Start Here
------------

The first thing you'll want to check is the [inventory](inventory) file. This is where your soon-to-be-created instances are declared, along with some variables. Next up, see [group_vars/masters](group_vars/masters) and [group_vars/nodes](group_vars/nodes) in order to specify variables for all hosts specified in the inventory. Last but not least, take a look at the [cluster-create.yml](cluster-create.yml) and then look at each role to see what it's doing.

If you'd like to blow away your OpenShift cluster--in other words, delete all instances and clean up IPA--, then you can use the [cluster-delete.yml](cluster-delete.yml) playbook.

When you are ready to expand your cluster, take a look at [cluster-expand.yml](cluster-expand.yml). Roles invocation remains almost identical as with cluster installation, except that instead of calling the OpenShift Ansible install playbook we call the OpenShift Ansible scaleup playbook.

Again, everything is driven from the [inventory](inventory) file; if you want to get creative and perform installation or expansion interactively, all you need is a process where the file is updated after the user provides input, and then the appropriate playbook (install or expand) is invoked.

Requirements
------------

All variables mentioned below are required--see below for each role's required variables. Additionally, you will need:

  - Current and valid Red Hat OpenShift subscription
  - An IPA server - used for DNS. 
  - A control_machine - this can very well be an Ansible Tower machine. Or, you can also elect to run this from the CLI in which case control_machine can simply be 'localhost'. See the vars: section in [cluster-create.yml](cluster-create.yml)
  - OpenStack, or AWS, or Azure, or RHV - basically an environment for your OpenShift machines to reside in.

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

The following example is exactly how the roles in this repository are being used in [cluster-create.yml](cluster-create.yml).

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
This is currently a work in progress and by no means perfect (yet).

License
-------

BSD
