# Ansible Ad-Hoc Public Domain Playbooks
**[public draft] Ansible Ad-Hoc project contain several single-file playbooks
dividide into categories that are ready to use alone or be used as initial
inspiration on your more complex playbooks. Everything this repository contains
is distributed under the Public Domain license**: it means that maintain the
attribution in the source YAML codes when using full scripts without any change
are not a legal or moral requirement, but are just welcome.

---
<!-- TOC -->

- [Ansible Ad-Hoc Public Domain Playbooks](#ansible-ad-hoc-public-domain-playbooks)
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
        - [Ansible](#ansible)
            - [How to install Ansible](#how-to-install-ansible)
        - [SSH access to remote machines](#ssh-access-to-remote-machines)
            - [`--ask-pass` and `--ask-become-pass`](#--ask-pass-and---ask-become-pass)
            - [SSH Passwordless Login](#ssh-passwordless-login)
            - [Create a new SSH Key and add to a remote server](#create-a-new-ssh-key-and-add-to-a-remote-server)
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

### Ansible

This repository assumes you already have installed Ansible on your machine.

#### How to install Ansible

See <https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html>.

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