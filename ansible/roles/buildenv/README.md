# buildenv role

Installs `build-essential` and other tools needed by many of the other roles

## Requirements

`apt` must be installed

## Role variables

- `project_group`: this is the group name of the account dspace will run as
- `project_user`: this is the user name of the account dspace will run as
- `project_user_home`: the home director of the account dspace will run as
