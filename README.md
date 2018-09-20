Role Name
=========

Sets up linux client servers with an ansible user with one and only one public ssh key which matches the ansible master server's private key from the matching ansible-master role. We use the exclusive: yes parameter on the key deploy task to ensure that if the master's key is changed, the old key is removed from the dependant nodes.

Requirements
------------


Role Variables
--------------

The "{{ hostvars[item]['orchestrationkey'] }}" is used from the jefg60.ansible-master role in the tasks file, thus:

with_items: "{{ groups['ansible-master'] }}"

That means this role should always call the ansible-master role as a dependency, to get the ansible-master server's ansible user ssh public key.

set ansible_orchestration_user: to the name of the local user you would like to create on each managed server.

If this is being run for the first time obviously you'll have to set ansible up to use whatever username is appropriate for the initial run, and then change the inventory / vars to use the new ansible orchestration user once this has sucessfully run.


Dependencies
------------

role: jefg60.ansible-master

Example Playbook
----------------


    - hosts: ansible-master
      roles:
         - { role: jefg60.ansible-master, ansible_orchestration_user: ansibleuser }

    - hosts: linux-servers
      roles:
         - { role: jefg60.ansible-orchestration-linux, ansible_orchestration_user: ansibleuser }

License
-------

GPLv3

Author Information
------------------

Jeff Hibberd
