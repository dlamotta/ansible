Role Name
=========

Installs all necessary packages required for installation. See https://docs.openshift.com/container-platform/latest/install_config/install/host_preparation.html
Additionally, docker-storage-setup is executed and the docker service is started.

Requirements
------------

For Red Hat Enteprise Linux, a valid username and password for Subscription Manager.

Role Variables
--------------

None.

Dependencies
------------

Since this role will configure docker storage, one of the provider roles (i.e., openstack) must have been previously executed in order to create the storage device for docker.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: all
      roles:
         - { role: prepare }

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
