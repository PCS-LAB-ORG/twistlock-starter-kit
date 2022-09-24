Role Name
=========

This Ansible role deploys a Twistlock, Self-Hosted console. A product of Palo Alto Networks, this software enables the protection of application workloads. Whether it is for servers, containers, or serverless fuctions, Twistlock can protect the application. This role allows you to do the following:

- Deploy a console and defender combination on one VM for quick evaluation (onebox)
- Deploy a console on server for more involved testing. Suitable for more realistic use cases
- Upgrade a onebox install
- Upgrade a console
- Uninstall

Requirements
------------

#Any pre-requisites that may not be covered by Ansible itself or the role should be mentioned here. For instance, if the role uses the EC2 module, it may be a good idea to mention in this section that the boto package is required.

Server

- This is designed for CentOS 7/RHEL 7, but the process is the same for most distros
- For onebox installs, 50GB is the bare minimum required for storage. 100GB is recommended
- 8GB RAM

Software

This software runs on docker, so you will need a machine that has this installed. Either the community edition or standard will work. 

Role Variables
--------------

#A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.

All variables for this role are located in group_vars/all.yaml
- version: build number for release
- build: codename for the build
- upgrade_version: URL download link

As of this writing, there's an issue with the version variable, where it does not retain the underscores. As a result, this is hardcoded until a fix is found

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: console
      roles:
         - { role: onebox-install, x: 42 }

License
-------

This is proprietary software. An license is required for use. 

Author Information
------------------

Joel Jean-Claude
