# Ansible LAMP Setup

A base LAMP environment for PHP deployment using Ansible.

The base setup is borrowed from the [Digital Ocean community ansible scripts](https://github.com/do-community/ansible-playbooks) and inspired by [My First 5 Minutes On A Server](https://plusbryan.com/my-first-5-minutes-on-a-server-or-essential-security-for-linux-servers) by Bryan Kennedy.

## Requirements

You will need a local install of Ansible and shell access to the deployment server.

Depending on the script you are running you will need to install these ansible roles.

```
ansible-galaxy install geerlingguy.apache
ansible-galaxy install geerlingguy.apache-php-fpm
ansible-galaxy install geerlingguy.certbot
ansible-galaxy install geerlingguy.composer
ansible-galaxy install geerlingguy.mysql
ansible-galaxy install geerlingguy.php
ansible-galaxy install geerlingguy.php-versions
```

`hosts` is an [Ansible inventory file](https://docs.ansible.com/ansible/latest/user_guide/intro_inventory.html).

You will need a minimal `/var/tmp/config.yml` file like this to get going.

```yaml
deploy_user: deploy

mysql_root_password: "super secret"

php_version: "7.4"
```

This file can live anywhere and you can change the path in the playbooks.

```
ansible-playbook -i hosts base.yml
ansible-playbook -i hosts mysql.yml
ansible-playbook -i hosts apache.yml
ansible-playbook -i hosts php.yml
```

## Ansible Lint

If you make any changes make sure you lint your Ansible playbooks.

```
ansible-lint base.yml
ansible-lint mysql.yml
ansible-lint apache.yml
ansible-lint php.yml
```

## Testing

Tested on Ubuntu 20.04 LTS with the help of [multipass](https://multipass.run/).

## Troubleshooting 

If you are using multipass check their network troubleshooting section here https://multipass.run/docs

Personally I had to stop dnsmasq and add a `nameserver 1.1.1.1` to the end of `/etc/resolv.conf` to get DNS working from inside the virtual machine.

```
sudo brew services stop dnsmasq
```
