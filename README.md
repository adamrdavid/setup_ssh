localcloud-common
=========
This role is designed to init fresh boxes wit ha minimal set of software. It will sync box clock, install default set
of software on a fresh box, create remote user of your choice and add it to `www-data` group enabling passwordless sudo,
inject your ssh key in with configurable set of additional keys to inject, then disable password logins for security.

Requirements
------------

A fresh Ubuntu 14 LTS box. 

Role Variables
--------------

`box_user`: required
This will be default user of your box. It will have you ssh keys added to authorised_keys file so you can use
passwordless login. This user will also be added to sudoers for paswordless sudo execution. And a home directory will
be created.

It is recommended that you intend to use the box as an app server you store all your vhosts in this user's
home directory. This user will also be added to same named group as well as `www-data` group.

`home_directory`: autogenerated
This will be autogenerated based on box_user and is just a shorthand you can reuse in your playbooks and configs.
You don't need to set that.

`inject_user_ssh_key`: optional, default is `True`
Whether to find your public ssh key and inject it into the box under box_user's authorized_keys.
It is suggested this option be left as true unless other mechanism is in place not to lock yourself out.

`inject_additional_ssh_keys`: optional, default is `[]` (none)
Provide an array of additional authorized_key on your local system to be injected. This way you can provide box
access to all users of your team, not just yourself.


Dependencies
------------

This role has no dependencies.

Example Playbook
----------------

```yml
- hosts: servers
  roles:
     - localcloud-common
  vars:
    box_user: username

```

License
-------

MIT License


