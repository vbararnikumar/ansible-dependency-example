# Ansible Dependency Example

You can tweak and run yourself with `ansible-playbook -i localhost site.yml`

## Using vars: in deps.

e.g.

```
# Role1
dependencies:
- name: lc.test-dep
  vars:
    var1: Set in Role1
    var2: Set in Role1

# Role2
dependencies:
- name: lc.test-dep
  vars:
    var1: Set in Role2  
```

Results in:

```
PLAY [localhost] ***************************************************************************************************************************************************************************************************************************************************************

TASK [Gathering Facts] *********************************************************************************************************************************************************************************************************************************************************
ok: [localhost]

TASK [lc.test-dep : This is the test-dep role! I'm a dependency of both Role1 and Role2. Here is the value of var1 --] *********************************************************************************************************************************************************
ok: [localhost] => {
    "var1": "Set in Role1"
}

TASK [lc.test-dep : This is the test-dep role! I'm a dependency of both Role1 and Role2. Here is the value of var2 --] *********************************************************************************************************************************************************
ok: [localhost] => {
    "var2": "Set in Role1"
}

TASK [lc.test-dep : This is the test-dep role! I'm a dependency of both Role1 and Role2. Here is the value of var1 --] *********************************************************************************************************************************************************
ok: [localhost] => {
    "var1": "Set in Role2"
}

TASK [lc.test-dep : This is the test-dep role! I'm a dependency of both Role1 and Role2. Here is the value of var2 --] *********************************************************************************************************************************************************
ok: [localhost] => {
    "var2": "Set in Role1"
}

PLAY RECAP *********************************************************************************************************************************************************************************************************************************************************************
localhost                  : ok=5    changed=0    unreachable=0    failed=0

```


## Using params in deps.

e.g.

```
# Role1
dependencies:
- name: lc.test-dep
  var1: Set in Role1
  var2: Set in Role1

# Role2
dependencies:
- name: lc.test-dep
  var1: Set in Role2
```

Results in:

```
PLAY [localhost] ***************************************************************************************************************************************************************************************************************************************************************

TASK [Gathering Facts] *********************************************************************************************************************************************************************************************************************************************************
ok: [localhost]

TASK [lc.test-dep : This is the test-dep role! I'm a dependency of both Role1 and Role2. Here is the value of var1 --] *********************************************************************************************************************************************************
ok: [localhost] => {
    "var1": "Set in Role1"
}

TASK [lc.test-dep : This is the test-dep role! I'm a dependency of both Role1 and Role2. Here is the value of var2 --] *********************************************************************************************************************************************************
ok: [localhost] => {
    "var2": "Set in Role1"
}

TASK [lc.test-dep : This is the test-dep role! I'm a dependency of both Role1 and Role2. Here is the value of var1 --] *********************************************************************************************************************************************************
ok: [localhost] => {
    "var1": "Set in Role2"
}

TASK [lc.test-dep : This is the test-dep role! I'm a dependency of both Role1 and Role2. Here is the value of var2 --] *********************************************************************************************************************************************************
ok: [localhost] => {
    "var2": ""
}

PLAY RECAP *********************************************************************************************************************************************************************************************************************************************************************
localhost                  : ok=5    changed=0    unreachable=0    failed=0

```
