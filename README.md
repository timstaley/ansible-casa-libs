casalibs-src
=============

An [Ansible](http://docs.ansible.com/) [role](https://galaxy.ansible.com/intro)
supplying a built-from-source installation of 
[casacore](https://github.com/casacore/casacore),
the [python-casacore](https://github.com/casacore/python-casacore) Python bindings,
and optionally the
[casarest](https://svn.astron.nl/viewvc/casarest?view=revision&revision=7395)
library.

This is useful if you want to:
- Install casacore / python-casacore from time-to-time without having to remember
  all the fine details of the install process.
- Integrate casacore installation into a larger Ansible-powered install process.
- Check that a particular version of casacore builds OK for your target system -
  tweak the Vagrantfile parameters accordingly and then simply `vagrant up`.
  (*In a hurry?* - fire up an EC2 instance with e.g. 36 cores,
   configure an Ansible
   [inventory](http://docs.ansible.com/ansible/intro_inventory.html)
   to point at the instance, then run
   [tests/test-casalibs-src-role.yml](tests/test-casalibs-src-role.yml)
   using the `ansible-playbook` command.)

The scripts go through all the required steps of:
- Installing system packages
- Downloading the source repositories and CASA measures data
- Configuring CMake builds with the required paths,
- Running the casacore build
- Running a python-casacore install-and-build from PyPI with the corresponding
  casacore library path specified.

The final product is a folder containing versioned builds and simple shell
scripts to add them to your $PATH / $PYTHONPATH, e.g.:

    ~$ ls /opt/casalibs/ -lh
    drwxrwxr-x 5 vagrant vagrant 4.0K Mar 23 13:08 casacore-2.0.1
    -rw-rw-r-- 1 vagrant vagrant   62 Mar 23 13:10 init-casabinaries-2.0.1.sh
    lrwxrwxrwx 1 vagrant vagrant   40 Mar 23 13:10 init-casabinaries.sh -> /opt/casalibs/init-casabinaries-2.0.1.sh
    -rw-rw-r-- 1 vagrant vagrant  337 Mar 23 13:10 init-casalibs-2.0.1.sh
    lrwxrwxrwx 1 vagrant vagrant   36 Mar 23 13:10 init-casalibs.sh -> /opt/casalibs/init-casalibs-2.0.1.sh
    drwxrwxr-x 5 vagrant vagrant 4.0K Mar 23 13:10 pycasacore-2.0.0_with-core-2.0.1_packagedir



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

See [defaults/main.yml](defaults/main.yml) and [vars/main.yml](vars/main.yml)
for default values and full details.

Example Playbook
----------------
See [tests/test-casalibs-src-role.yml](tests/test-casalibs-src-role.yml).


License
-------
BSD

Author
------------------
[Tim Staley](https://github.com/timstaley)
