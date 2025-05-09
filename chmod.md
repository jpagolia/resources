# Modify the permissions of an entire directory with `chmod`

## This modifies the permissions of every file in the directory recursively and gives the user sole read/write/execute access, while getting rid of all permissions for the group and others
`chmod -R u=rwx,g=,o= my_directory`

## This gives everyone read-only acccess
`chmod a=r my_directory`

## Verify the changes
`ls -l my_directory`
