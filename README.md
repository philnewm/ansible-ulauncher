# Ulauncher Ansible Role

[![Alma9-CI](https://github.com/philnewm/ansible-ulauncher/actions/workflows/alma9-ci-caller.yml/badge.svg)](https://github.com/philnewm/ansible-ulauncher/actions/workflows/alma9-ci-caller.yml) [![Rocky9-CI](https://github.com/philnewm/ansible-ulauncher/actions/workflows/rocky9-ci-caller.yml/badge.svg)](https://github.com/philnewm/ansible-ulauncher/actions/workflows/rocky9-ci-caller.yml) [![CentOSStream9-CI](https://github.com/philnewm/ansible-ulauncher/actions/workflows/centosstream9-ci-caller.yml/badge.svg)](https://github.com/philnewm/ansible-ulauncher/actions/workflows/centosstream9-ci-caller.yml) [![Fedora43-CI](https://github.com/philnewm/ansible-ulauncher/actions/workflows/fedora43-ci-caller.yml/badge.svg)](https://github.com/philnewm/ansible-ulauncher/actions/workflows/fedora43-ci-caller.yml)<br>
[![Ubuntu2404-CI](https://github.com/philnewm/ansible-ulauncher/actions/workflows/ubuntu2404-ci-caller.yml/badge.svg)](https://github.com/philnewm/ansible-ulauncher/actions/workflows/ubuntu2404-ci-caller.yml) [![Debian13-CI](https://github.com/philnewm/ansible-ulauncher/actions/workflows/debian13-ci-caller.yml/badge.svg)](https://github.com/philnewm/ansible-ulauncher/actions/workflows/debian13-ci-caller.yml)

This role builds and installs [Ulauncher v5](https://github.com/Ulauncher/Ulauncher/tree/v5).

Additionally, the role provides a `present` and `absent` version. This is to install or uninstall.<br>
This can be utilized by providing the state variable to the role, check the end of this README for an example.

This role includes a molecule testing setup at `molecule`

## Structure

```code
📦 ansible-ulauncher
 ┣ 📂 defaults
 ┃ ┗ 📜 main.yml
 ┣ 📂 meta
 ┃ ┗ 📜 main.yml
 ┣ 📂 molecule
 ┃ ┗ 📂 default
 ┃   ┗ 📜, 📜, 📜, scenario_files
 ┣ 📂 tasks
 ┃ ┣ 📜 absent.yml
 ┃ ┣ 📜 dependencies.yml
 ┃ ┣ 📜 install_debian.yml
 ┃ ┣ 📜 install_redhat.yml
 ┃ ┣ 📜 install_ubuntu.yml
 ┃ ┣ 📜 main.yml
 ┃ ┣ 📜 present.yml
 ┃ ┗ 📜 tests.yml
 ┣ 📂 vars
 ┃ ┗ 📜 main.yml
 ┗ 🗒️ README.md
 ┗ 📓 requirements.txt

```

Any variables containing dependencies are stored in `vars/main.yml` while configuration related variables are stored in `default/main.yml`.<br>
The `present_-tasks` are split into the main `tasks/present.yml` file and according to their content further into `tasks/present_install.yml` and `tasks/present_configure`.<br>
This split-up keeps the task-files shorter and more easy to read due to logical grouping.

## Requirements

Check the [Ulauncher website](https://ulauncher.io/#Download) for distros supported out-of-the-box.<br>
Additonally, these are the dependencies for Almalinux9

Global dependencies

* wmctrl
* keybinder3
* xdg-utils
* python3-gobject
* python3-dbus
* python3-pyxdg
* python3-inotify
* python3-websocket-client
* webkit2gtk3

Build dependencies - will be removed after build if they are unused

* pip
* python3-distutils-extra
* rpm-build
* rsync
* yarnpkg

Python packages

* wheel
* Levenshtein

## Role Variables

* defaults/main.yml
  * state - Desired state for ulauncher
  * ulauncher_download_path - custome download path for git repository
  * package_search - contains package search command per os family

* vars/main.yml
  * ulauncher_global_dependencies - any dependencies needed at runtime
  * ulauncher_build_dependencies - additional dependencies needed for building
  * ulauncher_pip_dependencies - python packages needed for build and runtime

## Dependencies

This role doesn't depend on any additional ansible-galaxy roles

## Example Playbook

```yaml
---

- name: Create and configure ansible-role-template
  hosts: client

  roles:
    - role: ansible-ulauncher
      tasks_from: main
      state: present

...
```
