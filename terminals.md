# Terminals
## Tasks
* copy a file: `cp <old location> <new location>`
* rename a file: `mv <oldname> <newname>`
* shutdown: `poweroff`
* restart: `reboot`

## Command glossary
### Filesystem
* chown: change <file>|<folder> owner
* chmod: modify <file>|<folder> permissions
* chgrp: modify group
* cp: copy file
* mv: move / rename files and directories

### Accounts
* useradd: create a new user
* usermod: modify a user, such as their groups. `-g` modifies primary group. `-a -G` modifies secondary
* useradd -g gr u : add user 'u' to group 'gr'
* groupadd: create a new group
* groups <user> : list all the groups for <user>

## Bash
* reload terminal `source ~/.bashrc` or just type `bash`
