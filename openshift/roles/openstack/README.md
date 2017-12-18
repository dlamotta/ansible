Role Name
=========

Creates instances in an OpenStack environment.

Requirements
------------

Enough quota available to provision as many instances as specified in the inventory file. Also, enough storage quota to create all volumes specified for all entries in group_vars.
This role also requires a previously-created SSH key that can be embedded via cloud-init (see variables below); this is required for Ansible in order to manage the instances created.

Role Variables
--------------

| Variable Name      | Description                                                           | Example                              |
|--------------------|-----------------------------------------------------------------------|--------------------------------------|
| osp_server 	       | OpenStack API endpoint                            										 | http://osp.exmaple.com:5000/v2.0/    | 
| osp_user           | OpenStack tenant administrator username    									         | tenant_admin              	          |
| osp_pass     	     | OpenStack tenant administrator password    									         | password                   	        |
| osp_tenant 	       | OpenStack tenant with enough resources available   									 | redhatrulez                          | 
| osp_key   	       | SSH key-pair name to allow Ansible to manage instances								 | mykey                                | 
| osp_image          | Glance image ID that will be used to provision new instances  				 | 157e2f64-a397-498e-9a30-33a4ae11e4be | 
| osp_public_key     | Public SSH key to allow passwordless connection from masters to nodes | ssh-rsa ABCDetcetcetc                | 
| osp_security_group | OpenStack network security group (i.e., ingress/egress rules)         | wide-open                            | 
| osp_floating_ip    | Whether to create a floating IP or not (master only, by default)      | True                                 | 

Dependencies
------------

None.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too.
See the inventory file and define the provider there. Other providers can coexist but their corresponding roles will need to be created.

    - hosts: all
      roles:
         - { role: openstack, when: "hostvars[inventory_hostname]['provider'] == 'openstack'" }

License
-------

BSD

