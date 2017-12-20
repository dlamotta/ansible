Role Name
=========

Expands an OpenShift Container Platform cluster.

Requirements
------------

This role will create partitions and filesystems, and subsequently mount them on the necessary instances. Said partitions must have been successfully created and mounted. 

Role Variables
--------------

| Variable Name | Description                                                           | Example           |
|---------------|-----------------------------------------------------------------------|-------------------|
| ocp_user   	  | OpenShift administrator username                   										| admin          	  | 
| ocp_pass    	| OpenShift administrator password           									          | password 	        |

Dependencies
------------

Prior to running this role, the following roles must have been previously executed:

  - provider (one or more; i.e., openstack)
  - ipa
  - keys
  - rhn
  - prepare

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: new_nodes
      roles:
         - { role: expand }

License
-------

BSD

