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
- `shell:string` - The user's shell. Defaults to /bin/bash if omitted (see `users_default_shell` below).
- `home:string` - The path to the user's home directory. This defaults to /home/{`username`}.
- `append:boolean` - By default (false), the user is only added to the groups specified in `groups`, removing them from all other groups. If set to true, the user will be added to the groups specified in `groups` but not removed from other non-specified groups.
- `create_home:boolean` - By default (true), a user home directory is created. If set to false, a user home directory isn't created. 
- `update_password:boolean` - By default (true), if `password` differs from the current user's password then the password will be updated. If set to false, the `password` will only be set for newly created users.
- `ssh_keys:list` - A list of file paths to SSH public keys that will be added the authorized_keys file for the user account.
- `profile:string` - A string block added to the user's ~/.profile file for setting custom shell profiles.

```yaml
users_to_remove: []
```
A list of users to remove.

The following attributes are required:
- `username:string` - Name of the user to remove.

The following attributes are optional:
- `remove:boolean` - If set to true the directories associated with the user account are removed. Defaults to false.
- `force:boolean` - If set to true, the user and associated directories are forcibly removed. Defaults to false.

```yaml
users_default_shell: /bin/bash
```
Default settings.
- `users_default_shell:string` - The default shell for the user accounts.

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