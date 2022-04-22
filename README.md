# User-Creation-with-Encrypted-Password-using-Ansible

## Installing Ansible
```bash
sudo amazon-linux-extras install ansible2 -y

ansible --version
ansible 2.9.23
  config file = /etc/ansible/ansible.cfg
  configured module search path = [u'/home/ec2-user/.ansible/plugins/modules', u'/usr/share/ansible/plugins/modules']
  ansible python module location = /usr/lib/python2.7/site-packages/ansible
  executable location = /usr/bin/ansible
  python version = 2.7.18 (default, Jun 10 2021, 00:11:02) [GCC 7.3.1 20180712 (Red Hat 7.3.1-13)]
```
## Hosts file
```bash
[amazon]
172.31.14.3 ansible_ssh_user="ec2-user" ansible_ssh_port=22 ansible_ssh_private_key_file="key.pem"
```
## Useradd.yml
```bash
---

- name: "user creation"
  become: true
  hosts: amazon
  tasks:
    - name: "creating user and setting passwd"
      user:
        name: "admin"
        create_home: yes
        home: "/home/admin"
        append: yes
        password: "{{'admin@123' | password_hash('sha512')}}"
```
