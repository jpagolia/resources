# Modify the permissions of an entire directory with `chmod`

## This modifies the permissions of every file in the directory recursively and gives the user sole read/write/execute access, while getting rid of all permissions for the group and others
`chmod -R u=rwx,g=,o= /path/to/my_directory/`

## This gives everyone read-only acccess
`chmod a=r my_directory`

## This gives yourself read, write, and execute access to the directory
`chmod u+rwx my_directory`

## Use this - This gives everyone read access but only the user read, write, and execute access
Modifies permissions for all files in that directory with `-R`\
`chmod -R +r,u=rwx /path/to/my_directory/`

## Verify the changes
`ls -l my_directory`\
`namei -m /path/to/my_directory/`
