Playbooks
=========

The project will consist of two playbooks to be run in succession. The project starts with a fresh Debian install 

1. First playbook to disable root login, create an admin user with sudo (no password) and upload a public key from the local (to be selected by the local user). Once this is done, the second playbook will be run as the admin user
2. The second playbook takes care of most of the work and is described in details below.

"root user" playbook
==============

The "root user" playbook accesses the remote server as root with password (prompted). It needs to

1. disable root login
1. disable password SSH login for all users
1. create an admin user
1. prompt for the name of a local ssh key, read the .pub file from $HOME/.ssh
1. append the value of the key to the remote's authorized_key for admin user
1.
