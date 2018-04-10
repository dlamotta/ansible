Role Name
=========

Registers with subscription manager and enables the OpenShift repositories required for installation.

Requirements
------------

Subscription manager credentials and pool ID are required as variables. See below.

Role Variables
--------------

| Variable Name | Description                                                           | Example           |
|---------------|-----------------------------------------------------------------------|-------------------|
| rhn_user   	  | Subscription manager username              										        | bruce@gotham.com  | 
| rhn_pass    	| Subscription manager password             									          | batmanrulez!      |
| rhn_pool    	| OpenShift subscription pool ID             									          | abcd123etcetc     |
| version    	  | OpenShift version                         									          | 3.7               |

Dependencies
------------

None.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: all
      roles:
         - { role: prepare, version: 3.7 }

License
-------

BSD