# ansible-hetzner

Notes
-----

**Caution when using. Systems are installed without further inquiry.**

Platforms
---------

Tested on Ubuntu. Should work on all platforms.

Example playbook
----------------

```yml
- name: provision hetzner root server
  hosts: hetzner
  gather_facts: no
  remote_user: root

  vars:
    ansible_ssh_private_key_file: ~/.ssh/id_rsa # your private key file
    hetzner_authorized_keys:
    - ssh-rsa AAAA ... # your hetzner authorized key
    hetzner_webservice_username: "your_hetzner_webservice_user"
    hetzner_webservice_password: "your_hetzner_webservice_password"

  tasks:
  - import_role:
      name: provision-hetzner

```

Example autosetup file
----------------------

The following ``autosetup`` file  will be used by default. Further details regarding
the file can be found at [Hetzner in the wiki](https://wiki.hetzner.de/index.php/Installimage/en#autosetup).

```
DRIVE1 /dev/sda
DRIVE2 /dev/sdb
SWRAID 1
SWRAIDLEVEL 0
BOOTLOADER grub
HOSTNAME hetzner.andyneeb.com
PART /boot ext3 512M
PART lvm vg0 500G
PART lvm cinder-volumes all

LV vg0 root / ext4 100G
LV vg0 swap swap swap 5G

IMAGE http://boernig.de/CentOS-75-el-x86_64-minimal.tar.xz

```
