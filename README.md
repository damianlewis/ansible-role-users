# Ansible Role: Users
User creation and management role.

## Requirements
None.

## Role Variables
Available variables are listed below, along with their default values.

```yaml
users_to_create: []
```
A list of users to create.

The following attributes are required:
- `username:string` - Name of the user to create.

The following attributes are optional:
- `password:string` - A hashed password to use for the user account. If a password isn't provided then the user account is disabled.
- `groups:list` - A list of secondary groups the user will be added to.
- `description:string` - The description (aka GECOS) of the user account.
- `uid:integer` - The numeric user id for the user.
- `shell:string` - The user's shell. Defaults to `users_shell` if omitted (see below).
- `home_directory:string` - The path to the user's home directory. Defaults to /home/{`username`} if omitted.
- `append_to_groups:boolean` - Defaults to `users_append_to_groups` if omitted (see below).
  - `true` - The user will be added to the groups specified in `groups` but will not be removed from any non-specified groups.
  - `false` - The user is only added to the groups specified in `groups`, removing the user from all other non-specified groups. 
- `create_home_directory:boolean` - Defaults to `users_create_home_directory` if omitted (see below).
  - `true` - A user home directory is created.
  - `false` - A user home directory isn't created.
- `update_password:boolean` - Defaults to `users_update_password` if omitted (see below).
  - `true` - If the `password` differs from the current user's password then the password will be updated. 
  - `false` - The `password` isn't updated. It is only set for newly created users.
- `ssh_keys:list` - A list of file paths to SSH public keys that will be added the authorized_keys file for the user account.
- `profile:string` - A string block added to the user's profile file for setting custom shell profiles.

```yaml
users_to_remove: []
```
A list of users to remove.

The following attributes are required:
- `username:string` - Name of the user to remove.

The following attributes are optional:
- `remove:boolean` - Defaults to `users_remove_user_directories` if omitted (see below).
  - `true` - Directories associated with the user account are removed.
  - `false` - User directories are left in place.
- `force:boolean` - Defaults to `users_force_remove` if omitted (see below).
  - `true` - Forces removal of the user and associated directories. 
  - `false` - The user isn't forcibly removed. 

```yaml
users_shell: /bin/bash
users_append_to_groups: no
users_create_home_directory: yes
users_update_password: yes
users_remove_user_directories: no
users_force_remove: no
```
Default settings
- `users_shell:string` - The default shell for the user accounts.
- `users_append_to_groups:boolean` - The default behaviour for adding users to groups.
- `users_create_home_directory:boolean` - The default behaviour for creating user home directories.
- `users_update_password:boolean` - The default behaviour for updating the user's password.
- `users_remove_user_directories:boolean` - The default behaviour for removing directories associated with the user account.
- `users_force_remove:boolean` - The default behaviour for forcibly removing users and their associated directories.

## Dependencies
None.

## Example Playbook
```yaml
- hosts: server
  become: yes

  vars:
    users_to_create:
    - username: admin
    - username: deployer

  tasks:
  - import_role:
      name: damianlewis.users
```

## License
MIT

## Author
Damian Lewis