# Infrastructure As Code Ad-Hoc Tasks with Ansible
**[public draft] IaC Ad-Hoc Tasks with Ansible contain several single-file
_"task oriented"_ playbooks ready to be used directly or be used as initial
inspiration for your more complex implementations.**

**Everything this repository contains is distributed under the Public Domain
license**: it means that maintain the attribution in the source YAML codes when
using full scripts without any change are not a legal or moral requirement, but
are just welcome.

**The target audience is both who is new to IaC (or IaC with Ansible) and veterans
who just _want get things done_ without creating custom playbooks or importing
Ansible Roles for _ad-hocs_ group of tasks**.

As convention, we recommend you store the files used at a folder called `ad-hoc`
at root of your project (but is up to you commit with you projects or ignore the
folder). Or store at home folder named `~/.ad-hoc` so you can reuse.

---
<!-- TOC -->

- [Infrastructure As Code Ad-Hoc Tasks with Ansible](#infrastructure-as-code-ad-hoc-tasks-with-ansible)
    - [Categorized collections of the Ad-Hoc playbooks](#categorized-collections-of-the-ad-hoc-playbooks)
        - [info](#info)
            - [show-ansible-facts-local.yml](#show-ansible-facts-localyml)
            - [show-firewall-status.yml](#show-firewall-statusyml)
            - [show-ports-open.yml](#show-ports-openyml)
        - [install](#install)
            - [install-debug-tools.yml](#install-debug-toolsyml)
        - [test](#test)
            - [install-mariadb.yml](#install-mariadbyml)
            - [install-redis.yml](#install-redisyml)
    - [Requeriments](#requeriments)
        - [Ansible (only on local machine, does not required on remote hosts!)](#ansible-only-on-local-machine-does-not-required-on-remote-hosts)
            - [How to install Ansible](#how-to-install-ansible)
        - [SSH access to remote machines](#ssh-access-to-remote-machines)
            - [`--ask-pass` and `--ask-become-pass`](#--ask-pass-and---ask-become-pass)
            - [SSH Passwordless Login](#ssh-passwordless-login)
            - [Create a new SSH Key and add to a remote server](#create-a-new-ssh-key-and-add-to-a-remote-server)
        - [How to define the target hosts](#how-to-define-the-target-hosts)
            - [The "-i example.com," comma trick](#the--i-examplecom-comma-trick)
                - [How the comma trick works](#how-the-comma-trick-works)
            - [hosts file](#hosts-file)
    - [How to "install" or reuse](#how-to-install-or-reuse)
        - [1. Manually copy each content file from the public repository](#1-manually-copy-each-content-file-from-the-public-repository)
        - [2. Add a copy to a folder called "ad-hoc" on your current project](#2-add-a-copy-to-a-folder-called-ad-hoc-on-your-current-project)
        - [3. Clone to ~/.ansible-ad-hoc and symlink to your current project](#3-clone-to-ansible-ad-hoc-and-symlink-to-your-current-project)
    - [License](#license)

<!-- /TOC -->
---

<!--

- The scripts assume are stored on a folder `ad-hoc/info/`
- The scripts assume your inventory file is `hosts` on current directory

-->

## Categorized collections of the Ad-Hoc playbooks

<!--

 ### backup
> This collection is a draft. Not ready for use.
-->

### info

**The info collection is safe to use: is granted to not try to install or do
actions that could break the target nodes.** If some task requires some special
tool, you will be warned to install manually.

#### show-ansible-facts-local.yml
See [info/show-ansible-facts-local.yml](info/show-ansible-facts-local.yml).

#### show-firewall-status.yml
See [info/show-firewall-status.yml](info/show-firewall-status.yml).

#### show-ports-open.yml

See [info/show-ports-open.yml](info/show-ports-open.yml).

### install
#### install-debug-tools.yml

See [install/install-debug-tools.yml](install/install-debug-tools.yml).

### test
> **This category is intended only for testing or very fast boostraping. DO NOT
USE ON PRODUCTION.** They do not even have idempotency (e.g. are not designed
to be re-run again without trying to redoing some actions, and this upsed
_Ansible veterans_).

Even if they may require explicit manual input to run (so it can mitigate
missuse) consider this folder of playbooks to be tested only on servers that
you are using for testing and can reinstall the full operational system.

Anyway, these scripts can be used as initial reference for your own playbooks,
but consider using Ansible Roles already published by community. Or at least,
yes, you can use then in a emergency, but after installed, manage the nodes
without these scripts.

#### install-mariadb.yml
See [test/install-mariadb.yml](test/install-mariadb.yml).

#### install-redis.yml
See [test/install-redis.yml](test/install-redis.yml).

## Requeriments

### Ansible (only on local machine, does not required on remote hosts!)

This repository assumes you already have installed Ansible on your machine.

#### How to install Ansible

- Use `pip` in your selected Python environment to install the Ansible package of your choice for the current user:

`python3 -m pip install --user ansible`

- You can test that Ansible is installed correctly by checking the version:

`ansible --version`

### SSH access to remote machines
Most ad-hoc playbooks will also require you be able to SSH into some remote
machine. You can either manually enter the password each time with `--ask-pass`
and `--ask-become-pass` or setup SSH Passwordless Login.

#### `--ask-pass` and `--ask-become-pass`

```bash
# Reference command (requires SSH Passwordless Login)
ansible-playbook ad-hoc/info/show-ports-open.yml -i hosts

# Command asking root password
ansible-playbook ad-hoc/info/show-ports-open.yml -i hosts --ask-pass
ansible-playbook ad-hoc/info/show-ports-open.yml -i hosts --ask-become-pass
```

#### SSH Passwordless Login

#### Create a new SSH Key and add to a remote server
If you already does not have one SSH key, the same tutorial used for GitHub
give one way to create it:

- <https://help.github.com/en/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent>

This Digital Ocean tutorial explains how to create an SSH key, and also how to
add to a remote server for SSH Passwordless Login.

- <https://www.digitalocean.com/community/tutorials/how-to-set-up-ssh-keys-on-ubuntu-1804>

We know the first time to be able to do SSH Passwordless Login can be thought.
But take your time to learn it, even look for other places with references on
it. You can do it :).

### How to define the target hosts



This projects provide you the single YAML playbook need for _do your thing_. But
you still need explain what hosts the ad-hoc task will run when using `ansible`
or `ansible-playbook`.

`ansible` or `ansible-playbook`, since are much more powerfull than one averange
cli command, are mean to have not only _simple list of targets_ but a
[powerfull inventory with targets and options](https://docs.ansible.com/ansible/latest/user_guide/intro_inventory.html).

#### The "-i example.com," comma trick
This trick is using comma `,` even if is just for a single target.
```bash
# Reference command (requires a file called 'hosts' with your target hostnames/IPs in each new line)
ansible-playbook ad-hoc/info/show-ports-open.yml -i hosts

# Equivalent without need of hosts file for a host with domain or ip
ansible-playbook ad-hoc/info/show-ports-open.yml -i example.com,
ansible-playbook ad-hoc/info/show-ports-open.yml -i 203.0.113.0,
ansible-playbook ad-hoc/info/show-ports-open.yml -i example.com,203.0.113.0,example.org,
```
##### How the comma trick works
Why this works? Because if your `-i` (`--inventory`) have at least a comma,
will be considered as a direct list, not as a file that must be saved on some
place. From the documentation:

> ```bash
> $ ansible --help
> # (...)
>   -i INVENTORY, --inventory=INVENTORY, --inventory-file=INVENTORY
>      specify inventory host path or comma separated host
>       list. --inventory-file is deprecated
> ```


#### hosts file

There are several ways to [build your inventory](https://docs.ansible.com/ansible/latest/user_guide/intro_inventory.html)
(can be a plain text file, an INI file, and YAML) but the simplest way is have
an `hosts` file on the directory that runs `ansible` or `ansible-playbook` with
a content like this:

```
example.com
203.0.113.0
example.org
```

**Important note: by default the ad-hoc scripts on this diretory will run agains
`all` your hosts (by default just not localhost), so this may not be desirable.**


## How to "install" or reuse

Choose **one** of the options. This repository is not one Ansible Role, and
every script here is one-file-script.

### 1. Manually copy each content file from the public repository

- Go to <https://github.com/fititnt/ansible-ad-hoc>
- Choose what files you want, ignore the others
- Copy and paste where you want
  - Then just use different paths than `ad-hoc/info/` on your documentation

### 2. Add a copy to a folder called "ad-hoc" on your current project

```bash
git clone https://github.com/fititnt/ansible-ad-hoc.git ad-hoc/

## What do you want to do: ignore or commit the full folder on your repository?
# If want to ignore, add ad-hoc/ to .gitignore
echo "\n# Ignoring Ansible Ad-Hoc files from https://github.com/fititnt/ansible-ad-hoc \nad-hoc/" >> .gitignore

# If want to commit delete the ad-hoc/.git folder
rm -r ad-hoc/.git

```

### 3. Clone to ~/.ansible-ad-hoc and symlink to your current project

```bash
git clone https://github.com/fititnt/ansible-ad-hoc.git ~/.ansible-ad-hoc/

ln -s ~/.ansible-ad-hoc/ ad-hoc/

echo "ad-hoc/" >> .gitignore
```

## License

[![Public Domain](https://i.creativecommons.org/p/zero/1.0/88x31.png)](UNLICENSE)

To the extent possible under law, [Emerson Rocha](https://github.com/fititnt)
has waived all copyright and related or neighboring rights to this work to
[Public Domain](UNLICENSE).

Optionally, you can choose to use the [MIT License](https://opensource.org/licenses/MIT)
instead of Public Domain unlicense. But if your project already have some
license you could choose the same.
