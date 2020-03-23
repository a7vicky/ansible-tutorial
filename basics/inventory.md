# Ansible tutorial: Inventory

The default location for inventory is a file called /etc/ansible/hosts. You can specify 
a different inventory file at the command line using the -i <path> option. You can also 
use multiple inventory files at the same time, and/or pull inventory from dynamic or 
cloud sources or different formats (YAML, ini, etc)

[Documentation](https://docs.ansible.com/ansible/latest/user_guide/intro_inventory.html)

### INI inventory example

```bash
[webservers]
foo.example.com
bar.example.com

[dbservers]
one.example.com
two.example.com
three.example.com
```
### yaml format

```bash
all:
  hosts:
    mail.example.com:
  children:
    webservers:
      hosts:
        foo.example.com:
        bar.example.com:
    dbservers:
      hosts:
        one.example.com:
        two.example.com:
        three.example.com:
```

Another exapmle:

```bash
host0 ansible_host=192.168.33.10 ansible_user=root
host1 ansible_host=192.168.33.11 ansible_user=root
host2 ansible_host=192.168.33.12 ansible_user=root
```

`ansible_host` is a special _variable_ that sets the IP ansible will use when
trying to connect to this host. It's not necessary here if you use the
vagrant-hostmaster gem. Also, you'll have to change the IPs if you have set up
your own virtual machines with different addresses.

`ansible_user` is another special _variable_ that tells ansible to
connect as this user when using ssh. By default ansible would use your
current username, or use another default provided in ~/.ansible.cfg
(`remote_user`).

## Testing

Now that ansible is installed, let's check everything works properly.

```bash
ansible -m ping all -i hosts
```

What ansible will try to do here is just executing the `ping` module (more on
modules later) on each host.

The output should look like this:

```json
host0 | success >> {
    "changed": false,
    "ping": "pong"
}

host1 | success >> {
    "changed": false,
    "ping": "pong"
}

host2 | success >> {
    "changed": false,
    "ping": "pong"
}
```

