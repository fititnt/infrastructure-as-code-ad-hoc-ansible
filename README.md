# ansible-ad-hoc-tasks
**[draft] Ansible Ad-Hoc useful ready to use single file scripts.
Initially based on https://github.com/fititnt/ap-application-load-balancer**

- The scripts assume are stored on a folder `ad-hoc/info/`
- The scripts assume your inventory file is `hosts` on current directory

## How to "install" this collection of Ansible Ad Hoc scripts

### Manually copy each content file from the public page

- Go to <https://github.com/fititnt/ansible-ad-hoc>
- Choose what files you want, ignore the others
- Copy and paste where you want
  - Then just use different paths than `ad-hoc/info/` on your documentation

### Add a copy to a folder called "ad-hoc" on your current project

```bash
git clone https://github.com/fititnt/ansible-ad-hoc.git ad-hoc/

## What do you want to do: ignore or commit the full folder on your repository?
# If want to ignore, add ad-hoc/ to .gitignore
echo "ad-hoc/" >> .gitignore

# If want to commit delete the ad-hoc/.git folder
rm -r ad-hoc/.git

```

### Clone to ~/.ansible-ad-hoc and symlink to your current project

```bash
git clone https://github.com/fititnt/ansible-ad-hoc.git ~/.ansible-ad-hoc/

ln -s ~/.ansible-ad-hoc/ ad-hoc/

echo "ad-hoc/" >> .gitignore
```