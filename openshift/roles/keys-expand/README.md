Role Name
=========

This role fetches the SSH key on the master specified in the ocp-master variable, and then copies the public key to all hosts in the newnodes group.

Requirements
------------

An SSH key must have previously been created in one of the OCP masters.

Role Variables
--------------

Check the [inventory](invnetory) and also [group_vars/newnodes](group_vars/newnodes) for places to initialize variables.

| Variable Name | Description                                                           | Example           |
|---------------|-----------------------------------------------------------------------|-------------------|
| ocp_master 	  | OpenShift master where the OpenShift Ansible installer was run    		| ocp-m1        	  | 

Dependencies
------------

Albeit obvious but we'll need an OpenShift cluster previously installed and running. A valid Op

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: newnodes
      roles:
         - { role: keys-expand }

License
-------

BSD