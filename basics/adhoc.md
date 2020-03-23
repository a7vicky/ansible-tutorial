# Ansible ad-hoc command

[Documentation](https://docs.ansible.com/ansible/latest/user_guide/intro_adhoc.html)

An Ansible ad-hoc command uses the /usr/bin/ansible command-line tool to automate a 
single task on one or more managed nodes. Ad-hoc commands are quick and easy.

Ad-hoc tasks can be used to reboot servers, copy files, manage packages and users, and much more. 
You can use any Ansible module in an ad-hoc task. Ad-hoc tasks, like playbooks, use a declarative 
model, calculating and executing the actions required to reach a specified final state. They 
achieve a form of idempotence by checking the current state before they begin and doing 
nothing unless the current state is different from the specified final state

```bash
$ ansible [pattern] -m [module] -a "[module options]"
```

```bash
$ ansible web -i hosts -m shell -a "uname"
10.0.89.4 | SUCCESS | rc=0 >>
Linux
```

```bash
$ ansible --become web -i hosts -m service -a "name=docker state=started" 
10.0.89.4 | SUCCESS => {
    "changed": false, 
    "name": "docker", 
    "state": "started", 
    "status": {
        "ActiveEnterTimestamp": "Mon 2020-03-23 10:13:03 EDT", 
        "ActiveEnterTimestampMonotonic": "4479143085", 
        "ActiveExitTimestampMonotonic": "0", 
        "ActiveState": "active", 
....
```

Facts represent discovered variables about a system. You can use facts to implement conditional 
execution of tasks but also just to get ad-hoc information about your systems. To see all facts:

```bash
$ ansible all -m setup
```


