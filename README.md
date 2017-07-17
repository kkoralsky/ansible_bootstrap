Ansible bootstrap role
======================

My ansible bootstrap role.

Used to bootstrap cloud instance or vps. It does this:

- creates user with given name
- adds user to *sudoers* without password checking (configurable)
- copies given SSH pub key from remote or local host for pub key authorization
  purposes
- disables root login via ssh and optionally password authorization at all
- exposes newly created rsa key (copies it to clipboard) to paste into
  web based git repository such as gitlab/github/bitbucket etc.

Requirements
------------

Remote: Ubuntu / Debian OS. Host: Linux w/ xclip installed.
Either root access to remote host or sudo for ansible's `remote_user`
is assumed.

Role Variables
--------------

- `user` - user's username to create
- `home` - home dir. path; generated with given username by default
- `shell` - shell user wil be spawned after login; `/bin/bash` by default
- `ssh_pub_key` - user public key to use for further authentication
- `ssh_pub_key_file` - user public key file
- `disable_password_auth` - disables password authentication (default: true)
- `disable_root_login` - disables root login (default: false)
- `sudo_setup` - default: true
- `sudo_nopasswd` - dont ask for sudo password (default: true)

Example Playbook
----------------

    - hosts: all
      gather_facts: no
      remote_user: root
      roles:
         - { role: bootstrap, run_raw: yes }

License
-------

BSD
