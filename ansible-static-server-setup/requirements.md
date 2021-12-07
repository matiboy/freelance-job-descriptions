Playbooks
=========

The project will consist of two playbooks to be run in succession. The project starts with a fresh Debian install 

1. First playbook to disable root login, create an admin user with sudo (no password) and upload a public key from the local (to be selected by the local user). Once this is done, the second playbook will be run as the admin user
2. The second playbook takes care of most of the work and is described in details below.

The project should be run using a virtual environment and Ansible should use that environment's Python. This should be set using the cfg file. Python packages should be in a requirements file. `poetry` is an acceptable alternative.

"root user" playbook
====================

The "root user" playbook accesses the remote server as root with password (prompted). It needs to

1. disable root login
1. disable password SSH login for all users
1. create an admin user
1. prompt for the name of a local ssh key, read the .pub file from $HOME/.ssh
1. append the value of the key to the remote's `authorized_keys` for admin user
1. add the `admin` user to sudoers
2. remove prompting password for the all sudoers

"Server setup"
==============

This playbook is now run by the `admin` user using the ssh key that was selected in the "root user" playbook.

Its tasks are:

1. Packages
  - Update apt-get
  - install vim (without prompts). Other packages may be added later on. They should go into a "variables" file for easier modifications
  - Install docker engine  (something like this: https://docs.docker.com/engine/install/ubuntu/)
2. Python
  - Make sure Python3 is installed
  - Make sure pip3 is installed
  - Other requirements as needed by the rest of the playbook's remote tasks
3. Security
  - enable ufw with all outbound allowed and only ports 22, 80 and 443 inbound allowed
  - any additional security features you may suggest are welcome 
4. Run docker in swarm mode
5. 
