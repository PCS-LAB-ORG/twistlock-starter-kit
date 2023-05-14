Defender Management
=========

Command: ansible-playbook -i inventory defender_control.yml -u <<linux user >> --tags=<< defender opearation >>

This role assists with manging defenders via API. Refer to the API reference for details on the APIs being called:

https://pan.dev/prisma-cloud/api/cwpp/ (Defenders Section)


- List defenders
- Upgrade Single Linux defender
- Restart defenders
- Delete defender

Due to the way Ansible parses values, I had to hard code the version number in the role. Until a workaround is available, it is necessary to continue doing this.
As you continue to use this playbook, it will become easier to get use to this usage. Any tasks that are found in this role that are not directly related to defender management are there for testing purposes only. Stick to what is listed above, and as you get comfortable, you can venture out and try other things.

Role Variables
--------------


Original design was to have the version variable referenced from the group_vars/all.yaml. However, this naming convention cannot be read properly during execution. As a result, the version numbers are hard coded.

There are placeholders that require the name of the target resource. You would need to retrieve that first, then add it the task file, then run it. In a future version, this role will be modified to include a user prompt, to make it easier to use

Dependencies
------------

You need to have a valid access token before running any of these tasks. 

1) Run ansible-playbook -i inventory console_install.yml -u <<linux user >> --tags= admin_user_login
2) Take the resulting string, and save it in the access_token variable in group_vars/all.yaml

If you get a 403 response, then run this command again, 

Usage Pattern
----------------

1) ansible-playbook -i inventory console_install.yml -u <<linux user >> --tags=admin_user_login
2) ansible-playbook -i inventory defender_control.yml -u <<linux user >> --tags=<< defender operation >>

After the token expires, repeat this sequence
