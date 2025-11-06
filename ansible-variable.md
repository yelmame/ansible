
# variables
  ## types of variables:





1- host variable
2- playbook variable 
   internal 
   external
3- global variable
 

 # 2- playbook variables
### 1 built-in variable playbook examples
 1> print the hostname of inventory files hosts
 vim built-in-var.yaml

```bash
---
- hosts: all
  tasks:
    - name: ansible- built-in-variable
      debug:
        msg: "{{ inventory_hostname }}"
```

  command:
  ansible-playbook --syntax-check built-in-var.yaml
  ansible-playbook built-in-var.yaml


2> another builtin variable is "{{ hostvars }}"

### 2 user-defined variable 

 1> string type variable
 vi user-defined.yaml

```bash
---
- hosts: all
  vars:
    salutation: hello eveyone
  tasks:
    - name: example of userdefined variable
      debug:
        msg: "{{ salutation }}"
```
commands:
ansible-playbook user-defined.yaml
print the string "hello everyone " on all hosts

2> list type variable
examples: vi mypckgs.yaml

``` bash
---
- name: example of listing type playbook variable
  hosts: all
  vars:
    mypkgs:
      - ftp
      - vsftpd
      - zsh
  tasks:
    - name: installing the packages
      yum:
        name: "{{ mypkgs }}"
        state: present
```
4> array type variable:
examples: vi array-var.yaml (please install 2 nd package from list )

```bash
---
- name: example of listing type playbook variable
  hosts: all
  vars:
    mypkgs:
      - ftp
      - vsftpd
      - zsh
  tasks:
    - name: installing the packages
      yum:
        name: "{{ mypkgs [1] }}"
        state: presentray-var.yaml
```

5> prompt ariable type
example: 
vi prompt-var.yaml

```bash
---
- name: prompt for user input
  hosts: all
  vars_prompt:
    - name: user_name
      prompt: please enter your username
      private: no
    - name: password
      prompt: please enter your password
      private: yes
  tasks:
    - debug:
        msg: " The username is {{ user_name }} and password is {{ password }}
          "
``` 

ansible-playbook --ansible-check prompt-var.yaml
ansible-playbook prompt-var.yaml


