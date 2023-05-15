Overview
=========

This role assists with installing the Twistlock console. This inspiration for this Ansible role set was from the onebox installation:

https://docs.paloaltonetworks.com/prisma/prisma-cloud/22-06/prisma-cloud-compute-edition-admin/install/install_onebox

The steps from this document have been captured in the Ansible roles below:

- onebox install: ansible-playbook -i inventory onebox_install.yml -u <<linux user >> --tags=install
- onebox upgrade: ansible-playbook -i inventory onebox_upgrade.yml -u <<linux user >> --tags=install
- onebox uninstall
- console install: ansible-playbook -i inventory console_install.yml -u <<linux user >>
- console upgrade: ansible-playbook -i inventory console_upgrade.yml -u <<linux user >> 
- console uninstall

Purpose of this set of Ansible roles is to assist users with setting up a instance that is cloud agnostic. I provides a way to automate the process of the deploying the console and upgrading it. In addition, this includes, sample users and groups, ando controls for defender management, which make up some of the on-going tasks that would be performed over the lifecycle of an installation. 

Role Variables
--------------

Intent was to include variables for all roles in the group_vars/all.yaml file. However, as I expanded functionality of other roles, this file became too large. As a result, this file will have what's necessary to get the console installed, and any other settings will reside in the respective folder for the role (<role>/vars/all.yaml)

Relevant variables for this role are below:

version: Version number
install_version: URL link from release notes (From the support portal PDF file, not the gihub document)
upgrade_version: URL link from release notes (From the support portal PDF file, not the gihub document) (Used when upgrading)
build: Codename for release, 
admin_user: text
admin_password: text
access_token: string/text
twistlock_license: string/text
API_token: Comes from the 'Path to 
For the variables above, use the existing value as an example of how to use it. (For the best effect, use vim to see active values)

The access token and twistlock_license variables come from the 90 day Evaluation page in the LOOP. Ask around for the link

The API_token variable can be found in the console under Compute -> System -> Utilities. For the console_install and onebox_install roles, this will also come up during installation. 

NOTE: This is a known bug. When using the console_install playbook, the task 'License the console' may fail the first time you run it. you can re-run the task by using the command below:

ansible-playbook -i inventory console_install.yml -u <<linux user >> --start-at-task='License the Console'


Dependencies
------------

- Version (Joule, Kepler, Lagrange, Maxwell, etc)
- License key
- Console Download link. Set this in the group_vars/all.yaml file
- Inventory file 
- Server with docker installed (CE or standard should work. This role was tested on Docker CE 20.03)


Usage Pattern
----------------

Setup:
 - Retrieve access_token and license key from the page in the LOOP. Add values to group_vars/all.yaml file
 - Set admin credentials
 - Optional: set credentials for ci_user
 - Create a VM with docker installed
 - Add IP address of the VM in the previous step to the inventory file

Usage:
1) ansible-playbook -i inventory console_install.yml -u <<linux user >> --tags=install
2) Copy API_token
3) Paste API_token in API_token variable in group_vars/all.yaml file
4) If needed, run this command if the task 'License the Console' fails: ansible-playbook -i inventory console_install.yml -u <<linux user >> --start-at-task='console-install : License the Console'


