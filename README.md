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