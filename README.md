This is just a test of a particular structure of ansible role. See the sources.

```
$ cat group_vars/all
---
use_source: true
$ ansible-playbook playbook.yml
statically included: /home/martin/projects/ansible-role-example/roles/foobar/tasks/source.yml
statically included: /home/martin/projects/ansible-role-example/roles/foobar/tasks/packages.yml

PLAY [Istallation and setup of foobar] *****************************************

TASK [setup] *******************************************************************
ok: [localhost]

TASK [foobar : Installing foobar from the sources] *****************************
ok: [localhost]

TASK [foobar : Installing foobar from the binary package] **********************
skipping: [localhost]

TASK [foobar : Common setup] ***************************************************
ok: [localhost]

PLAY RECAP *********************************************************************
localhost                  : ok=3    changed=0    unreachable=0    failed=0   

$ sed -i 's/use_source: true/use_source: false/' group_vars/all 
$ ansible-playbook playbook.yml
statically included: /home/martin/projects/ansible-role-example/roles/foobar/tasks/source.yml
statically included: /home/martin/projects/ansible-role-example/roles/foobar/tasks/packages.yml

PLAY [Istallation and setup of foobar] *****************************************

TASK [setup] *******************************************************************
ok: [localhost]

TASK [foobar : Installing foobar from the sources] *****************************
skipping: [localhost]

TASK [foobar : Installing foobar from the binary package] **********************
ok: [localhost]

TASK [foobar : Common setup] ***************************************************
ok: [localhost]

PLAY RECAP *********************************************************************
localhost                  : ok=3    changed=0    unreachable=0    failed=0   

$
```
