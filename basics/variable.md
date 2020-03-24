# Ansible tutorial: Managing Variables

[Documentation](http://docs.ansible.com/ansible/playbooks_variables.html)
[]

## Introduction

Ansible supports variables that can be used to store values that can be reused throughout files in
an entire Ansible project.
Variables provide a convenient way to manage dynamic values for a given environment in your
Ansible project. 

Note: Variables have names which consist of a string that must start with a letter and can only contain
letters, numbers, and underscores.

Examples:
```bash
Invalid variable names    Valid variable names

   web server                  web_server
  remote.file                 remote_file
```

Variables can be defined in a bewildering variety of places in an Ansible project. However, this can
be simplified to three basic scope levels:
• Global scope: Variables set from the command line or Ansible configuration
• Play scope: Variables set in the play and related structures
• Host scope: Variables set on host groups and individual hosts by the inventory, fact gathering, or
registered tasks

## VARIABLES IN PLAYBOOKS

```yaml
- hosts: all
vars:
user: joe
home: /home/joe
```

```yaml
vars:
user: joe
tasks:
# This line will read: Creates the user joe
- name: Creates the user {{ user }}
user:
# This line will create the user named Joe
name: "{{ user }}"
```

Overriding a vaiable from the command line
```bash
$ ansible-playbook main.yml --limit=demo2.example.com -e "key=value"
```
