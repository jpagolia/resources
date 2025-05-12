# Modify the permissions of an entire directory with `chmod`
https://gps.uml.edu/tutorials/unix-linux/unix/chmod.htm#:~:text=This%20command%20will%20give%20read,else%20has%20read%2Donly%20permission.

## USE THIS: This applies to all files and subfolders in a directory and gives user rwx access and everyone else read only access
https://stackoverflow.com/questions/3740152/how-do-i-change-permissions-for-a-folder-and-its-subfolders-files \
`find /path/to/my_directory -type d -exec chmod 755 {} \;`\
`find /path/to/my_directory -type f -exec chmod 644 {} \;`

## Verify the changes
`ls -l my_directory`\
`namei -m /path/to/my_directory/`

## Other `chmod` things

### This modifies the permissions of every file in the directory recursively and gives the user sole read/write/execute access, while getting rid of all permissions for the group and others
`chmod -R u=rwx,g=,o= /path/to/my_directory/`

### This gives everyone read-only acccess
`chmod a=r my_directory`

### This gives yourself read, write, and execute access to the directory
`chmod u+rwx my_directory`

### This gives everyone read access but only the user read, write, and execute access
Modifies permissions for all files in that directory with `-R`\
`chmod -R +r,u=rwx /path/to/my_directory/`
