# Shells
General shell related things + common applications, mostly bash / sh

## Tasks
* copy a file: `cp <old location> <new location>`
* SCP copy from remote server `scp -r user@server:/some/directory /local/dir` (scp <orig> <dest>)
* rename a file: `mv <oldname> <newname>`
* shutdown: **poweroff**
* restart: **reboot**
* view all running proceses `ps aux | less`

## Command glossary
### Filesystem
* source <file> - read and load the file in the current shell
* chown: change <file>|<folder> owner
* chmod: modify <file>|<folder> permissions
* chgrp: modify group
* cp: copy file
* mv: move / rename files and directories
* mkdir: make a directory
  - **-p** make parent directories as needed
  `mkdir -p parent/{child1, child2, child3}`

### Accounts
* useradd: create a new user
* usermod: modify a user, such as their groups. **-g** modifies primary group. **-a -G** modifies secondary
* useradd -g gr u : add user 'u' to group 'gr'
* groupadd: create a new group
* groups <user> : list all the groups for <user>

### Networks
* **netstat**: network statistics
  - `-a` - shows all sockets in use
  - `-l` - shows only the sockets currently listening for incoming connections
  - `-t` - shows the tcp sockets
  - `-u` - shows udp sockets
  - `-n` - numeric, shows the hosts and ports as numbers instead of resolving in dns and looking in /etc/services

## Bash
* reload terminal `source ~/.bashrc` or just type **bash**
* list all files in a dir recursively
  `for f in $(find ./folder -name '*.filetype');
   do echo "Processing $(basename $f) file.."; done`
* drop file extension
  `file = 'some-file.filetype'
   filename=${file%.*}
  `
* Optional parameters: `somecommand ${1-foo}`, use arg 1 otherwise use foo if arg 1 is unset or an empty string  

### Scripting
**Variables**: declared by just type and expression `name = value`, accessed with the `$` operator
**Arrays**: `arr[0] = value` or `arr=( value1 value2 value 3 )`
**Control structures**:
- `while [ <condition> ]; do <expressions> done`
- `if [ <condition> ]; then <expressions> fi`

## zsh
* `![command]` - shows the last command you typed using the command specified
* **history** - shows a history of your commands

## Zipped files
- tarball: `tar -zcvf archive-name.tar.gz directory-name`
- debian: install 7z or unzip
- redhat:

## Curl
- L option - follow redirects

## Notes
- by default, ubuntu executes commands using the `sh` shell
- `sh` does not support variables
