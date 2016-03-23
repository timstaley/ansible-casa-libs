casalibs-src
=============

An [Ansible](http://docs.ansible.com/) [role](https://galaxy.ansible.com/intro)
supplying a built-from-source installation of 
[casacore](https://github.com/casacore/casacore), 
[casarest](https://svn.astron.nl/viewvc/casarest?view=revision&revision=7395),
and the [python-casacore](https://github.com/casacore/python-casacore)
Python bindings.

Only tested with Ubuntu, currently.

Note that if you're using a supported distribution (e.g. Ubuntu 14.04)
you might prefer to use the ready-made apt-packages available from 
https://launchpad.net/~radio-astro/+archive/ubuntu/main.

To Do
-------
* Finish up role-metadata, add travis-testing.

Requirements
--------------
Assumes presence of git and pip on the machine.
(For the Vagrant test-vm these basics are installed from
[tests/base.yml](tests/base.yml).)

Role Variables
--------------

Key variables are:
- "repo_dir": All repositories are checked out under `{{ repo_dir }}/casalibs`
- "default_install_prefix": Libraries are built under `{{ default_install_prefix }}/casalibs`
- "casacore_github_version": Which casacore version-tag to checkout from github.
- "python_casacore_version": Which python-casacore version-tag to checkout from github.

See [defaults/main.yml](defaults/main.yml) and [vars/main.yml](vars/main.yml) for full details.

Example Playbook
----------------
See [tests/test-casalibs-src-role.yml](tests/test-casalibs-src-role.yml).


License
-------
BSD

Author
------------------
[Tim Staley](https://github.com/timstaley)
