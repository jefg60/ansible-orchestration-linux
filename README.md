Role Name
=========

Sets up linux client servers with an ansible user with one and only one public ssh key which matches the ansible master server's private key. We use the exclusive: yes parameter on the key deploy task to ensure that if the master's key is changed, the old key is removed from the dependant nodes.

Requirements
------------


Role Variables
--------------

The "{{ hostvars[item]['orchestrationkey'] }}" is used from the jefg60.ansible-master role in the tasks file, thus:

with_items: "{{ groups['ansible-master'] }}"

That means this role should always call the ansible-master role as a dependency, to get the ansible-master server's ansible user ssh public key.

set ansible_user: to the name of the local user you would like to create on each managed server.

If this is being run for the first time obviously you'll have to set ansible up to use whatever username is appropriate for the initial run, and then change the inventory / vars to use the new ansible orchestration user once this has sucessfully run.

A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.

Dependencies
------------

role: jefg60.ansible-master

(TODO: add this to meta/main.yaml)
A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too (see ansible-master role README for details of that).

    - hosts: ansible-master
      roles:
         - { role: jefg60.ansible-master, ansible_user: ansibleuser }

    - hosts: linux-servers
      roles:
         - { role: jefg60.ansible-orchestration-linux, ansible_user: ansibleuser }

License
-------

GPLv3

Author Information
------------------

Jeff Hibberd
