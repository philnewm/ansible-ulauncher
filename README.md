# Ulauncher Ansible Role

[![ci-testing](https://github.com/philnewm/ansible-ulauncher/actions/workflows/molecule-ci.yml/badge.svg)](https://github.com/philnewm/ansible-ulauncher/actions/workflows/molecule-ci.yml)

This role builds and installs [Ulauncher v5](https://github.com/Ulauncher/Ulauncher/tree/v5) on Almalinux. It includes a bunch of custom settings and applies a [forked theme](https://github.com/philnewm/ulauncher_theme).<br>
It will also work for XOrg and Wayland since this requires a few [adjustments](https://github.com/Ulauncher/Ulauncher/wiki/Hotkey-In-Wayland) when it comes to the configured hotkey.

Additionally the role provides a `present` and and `absent` version. This is to install or uninstall it while also removing settings and unused dependencies.<br>
This can be utilized by providing the state variable to the role, check the end of this file for an example.

This role includes a full vagrant based molecule testing setup at `extensions/molecule/default`

## Structure

```
📦 gnome_setup
 ┣ 📂 defaults
 ┃ ┗ 📜 main.yml
 ┣ 📂 meta
 ┃ ┗ 📜 main.yml
 ┣ 📂 molecule
 ┃ ┗ 📂 default
 ┃   ┗ 📜, 📜, 📜, scenario_files
 ┣ 📂 tasks
 ┃ ┣ 📜 main.yml
 ┃ ┣ 📜 present.yml
 ┃ ┣ 📜 present_install.yml
 ┃ ┣ 📜 present_configure.yml
 ┃ ┣ 📜 dependencies.yml
 ┃ ┣ 📜 absent.yml
 ┃ ┗ 📜 init.yml
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
Additonally these are the dependencies for Almalinux9.4 

**Global dependencies**
  * wmctrl
  * keybinder3
  * xdg-utils
  * python3-gobject
  * python3-dbus
  * python3-pyxdg
  * python3-inotify
  * python3-websocket-client

**Build dependencies** - will be removed after build if they are unused
  * pip
  * python3-distutils-extra
  * rpm-build
  * rsync
  * yarnpkg

**Python packages**
  * wheel
  * Levenshtein


## Role Variables

* defaults/main.yml
  * ulauncher_download_path - custome download path for git repository
  * ulauncher_settings_dir - ulaunchers default settings directory path
  * ulauncher_themes_dir - ulaunchers default themes directory path
  * ulauncher_settings - custom settings for settings.json file
  * ulauncher_extensions - extensions to install right away
  * ulauncher_github_repo_theme - list of themes to get from github
  * ulauncher_gdm_config_file - distro specific config paths to check for displayserver
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
      ansible_role_template_state: present

...
```
