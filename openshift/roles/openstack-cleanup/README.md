Role Name
=========

Deletes instances in an OpenStack environment.

Requirements
------------

None other than values for the variables below.

Role Variables
--------------

| Variable Name      | Description                                                           | Example                              |
|--------------------|-----------------------------------------------------------------------|--------------------------------------|
| osp_server 	       | OpenStack API endpoint                            										 | http://osp.exmaple.com:5000/v2.0/    | 
| osp_user           | OpenStack tenant administrator username    									         | tenant_admin              	          |
| osp_pass     	     | OpenStack tenant administrator password    									         | password                   	        |
| osp_tenant 	       | OpenStack tenant with enough resources available   									 | redhatrulez                          | 

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

