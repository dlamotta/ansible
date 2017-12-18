Role Name
=========

Creates DNS entries and records for all hosts provided. Additionally, this role will create an apps subdomain

Requirements
------------

This role requires an existing IPA server. Additionally, machines in the inventory must have a valid IP address associated with them.

Role Variables
--------------

| Variable Name | Description                                                           | Example           |
|---------------|-----------------------------------------------------------------------|-------------------|
| ipa_server 	  | Used to join nodes to IPA/IdM                     										| ipa.example.com	  | 
| ipa_user	    | User account used to join nodes to IPA/IdM								           	| admin		          | 
| ipa_pass     	| Password used to join nodes to IPA/IdM  										          | password 	        |
| domain       	| Domain name for instance FQDN and for OpenShift apps subdomain        | example.com       |

Dependencies
------------

Prior to running this role, the following roles must have been previously executed:

  - provider (one or more; i.e., openstack)

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: all
      roles:
         - { role: ipa }

License
-------

BSD