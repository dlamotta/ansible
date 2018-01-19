Role Name
=========

Deletes DNS entries and records for all hosts provided. Additionally, this role will delete the apps subdomain.

Requirements
------------

This role requires an existing (and functioning) IPA server.

Role Variables
--------------

| Variable Name | Description                                                           | Example           |
|---------------|-----------------------------------------------------------------------|-------------------|
| ipa_server 	  | Used to join nodes to IPA/IdM                     										| ipa.example.com	  | 
| ipa_user	    | User account used to join nodes to IPA/IdM								           	| admin		          | 
| ipa_pass     	| Password used to join nodes to IPA/IdM  										          | password 	        |
| domain       	| Domain name for instance FQDN and for OpenShift apps subdomain        | example.com       |
| fqdn          | Value should be set to {{ inventory_hostname }}.{{ domain }}          |                   |

Dependencies
------------

None.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: all
      roles:
         - { role: ipa-cleanup }

License
-------

BSD
