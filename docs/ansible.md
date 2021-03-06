# Running this playbook

This playbook is meant to be run using [Ansible](https://www.ansible.com/).


## Supported Ansible versions

Generally, Ansible 2.4 or later is required.

If you're on Ansible 2.5.x, then at least Ansible 2.5.2 is required.


## Checking your Ansible version

In most cases, you won't need to worry about the Ansible version.
The playbook will try to detect it and tell you if you're on an unsupported version.

To manually check which verison of Ansible you're on, run: `ansible --version`.

If you're on an old version of Ansible, you should upgrade to a newer version.


## Upgrading Ansible

Depending on your distribution, you may be able to upgrade Ansible in a few different ways:

- by using an additional repository (PPA, etc.), which provides newer Ansible versions

- by removing the Ansible package (`yum remove ansible` or `apt-get remove ansible`) and installing via [pip](https://pip.pypa.io/en/stable/installing/) (`pip install ansible`).

If using the `pip` method, do note that the `ansible-playbook` binary may not be on the `$PATH` (https://linuxconfig.org/linux-path-environment-variable), but in some more special location like `/usr/local/bin/ansible-playbook`. You may need to invoke it using the full path.


**Note**: Both of the above methods are a bad way to run system software such as Ansible.
If you find yourself needing to resort to such hacks, please consider reporting a bug to your distribution and/or switching to a sane distribution, which provides up-to-date software.


## Using Ansible via Docker

Alternatively, you can run Ansible itself from a Docker container on your computer.

Here's a sample command to get you started (run this from the playbook's directory):

```bash
docker run -it --rm \
-w /work \
-v `pwd`:/work \
-v $HOME/.ssh/id_rsa:/root/.ssh/id_rsa:ro \
--entrypoint=/bin/sh \
qmxme/ansible
```

The above command tries to mount an SSH key (`$HOME/.ssh/id_rsa`) into the container (at `/root/.ssh/id_rsa`).
If your SSH key is at a different path (not in `$HOME/.ssh/id_rsa`), adjust that part.
If you don't use SSH keys for authentication, simply remove that whole line (`-v $HOME/.ssh/id_rsa:/root/.ssh/id_rsa:ro`).

Once you execute the above command, you'll be dropped into a `/work` directory inside a Docker container.
The `/work` directory contains the playbook's code.

You can execute `ansible-playbook` commands as per normal now.