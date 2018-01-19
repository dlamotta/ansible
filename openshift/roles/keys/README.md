Role Name
=========

This role creates an SSH key on the first master, and then copies the public key to all hosts in the inventory.

Requirements
------------

None.

Role Variables
--------------

None.

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