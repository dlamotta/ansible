Role Name
=========

This role fetches the SSH key on the master specified in the ocp-master variable, and then copies the public key to all hosts in the newnodes group.

Requirements
------------

An SSH key must have previously been created in one of the OCP masters.

Role Variables
--------------

ocp-master

Dependencies
------------

None.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: all
      roles:
         - { role: keys }

License
-------

BSD