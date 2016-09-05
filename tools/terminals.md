# Terminals
General terminal related things + common applications

## Tasks
* copy a file: `cp <old location> <new location>`
* SCP copy from remote server `scp -r user@server:/some/directory /local/dir` (scp <orig> <dest>)
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
* mkdir: make a directory
  - `-p`: make parent directories as needed
  `mkdir -p parent/{child1, child2, child3}`

### Accounts
* useradd: create a new user
* usermod: modify a user, such as their groups. `-g` modifies primary group. `-a -G` modifies secondary
* useradd -g gr u : add user 'u' to group 'gr'
* groupadd: create a new group
* groups <user> : list all the groups for <user>

## Bash
* reload terminal `source ~/.bashrc` or just type `bash`

## Zipped files
- tarball: `tar -zcvf archive-name.tar.gz directory-name`
- debian: install 7z or unzip
- redhat:

## Curl
- L option - follow redirects
