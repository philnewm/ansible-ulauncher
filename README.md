Role Name
=========
[![ci-testing](https://github.com/philnewm/ansible-ulauncher/actions/workflows/molecule-ci.yml/badge.svg)](https://github.com/philnewm/ansible-ulauncher/actions/workflows/molecule-ci.yml)

Role description



This role includes a full vagrant based molecule testing setup at `extensions/molecule/default`

Structure
---------
```
📦 gnome_setup
 ┣ 📂 defaults
 ┃ ┗ 📜 main.yml
  ┣ 📂 files
 ┃ ┗ 📜 file_placeholder.yml
 ┣ 📂 handlers
 ┃ ┗ 📜 main.yml
 ┣ 📂 meta
 ┃ ┗ 📜 main.yml
 ┣ 📂 molecule
 ┃ ┗ 📂 default
 ┃   ┗ 📜, 📜, 📜, scenario_files
 ┣ 📂 tasks
 ┃ ┣ 📜 main.yml
 ┃ ┣ 📜 present.yml
 ┃ ┣ 📜 dependencies.yml
 ┃ ┣ 📜 absent.yml
 ┃ ┗ 📜 init.yml
 ┣ 📂 templates
 ┃ ┗ ⛩️ template.j2
 ┣ 📂 vars
 ┃ ┗ 📜 main.yml
 ┗ 🗒️ README.md
 ┗ 📓 requirements.txt

```

Describe and explain role structure. 

Requirements
------------

Elloborate external dependencies and how to use them.

Role Variables
--------------

* defaults/main.yml
  * first_var
  * sec_var
  * third_var
* vars/main.yml
  * first_var
  * sec_var
  * third_var


Dependencies
------------

List role ansible-galaxy dependencies - if any.

Example Playbook
----------------

Add an example playbook
```yaml
---

tasks:
  - name: Include ansible-role-template present
    ansible.builtin.include_role:
      name: ansible-role-template
    vars:
      ansible_role_template_state: present

...
```
License
-------

Add license - if any.
