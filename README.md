# ansible-hetzner

Notes
-----

**Caution when using. Systems are rebooted and installed without further inquiry.**

Platforms
---------

Tested on RHEL / CentOS. Should work on all platforms.

Activate webservice
-------------------

To use the webservice, go to ``Settings > Webservice settings`` in portal and define a password. You will receive your user via Mail from Hetzner.

Example playbook
----------------

```yml
- name: provision hetzner root server
  hosts: hetzner
  gather_facts: no
  remote_user: root

  vars:
    hetzner_webservice_username: "your_hetzner_webservice_user"
    hetzner_webservice_password: "your_hetzner_webservice_password"
    hetzner_image: "/root/.oldroot/nfs/install/../images/CentOS-75-64-minimal.tar.gz"
    hetzner_hostname: "hostname.example.com"

  tasks:
  - import_role:
      name: provision-hetzner

```

Example autosetup file
----------------------

The following ``autosetup`` file  will be used by default. Modify ``roles/provision-hetzner/templates/autosetup`` or create your own and set ``{{ hetzner_autosetup_file }}``.
 Further details regarding the file can be found at [Hetzner in the wiki](https://wiki.hetzner.de/index.php/Installimage/en#autosetup).

```
DRIVE1 /dev/sda
DRIVE2 /dev/sdb
SWRAID 1
SWRAIDLEVEL 0
BOOTLOADER grub
HOSTNAME {{ hetzner_hostname }}
PART /boot ext3 512M
PART lvm vg0 500G
PART lvm cinder-volumes all

LV vg0 root / ext4 100G
LV vg0 swap swap swap 5G

IMAGE {{ hetzner_image }}
```

Hetzner offers a collection of images which can be set via ``{{ hetzner_image }}``. Examples include:

* archlinux-latest-64-minimal.tar.gz
* CentOS-610-64-minimal.tar.gz
* CentOS-75-64-minimal.tar.gz
* CoreOS-1298-64-production.bin.bz2
* Debian-811-jessie-64-minimal.tar.gz
* Debian-95-stretch-64-minimal.tar.gz
* Ubuntu-1604-xenial-64-minimal.tar.gz
* Ubuntu-1710-artful-64-minimal.tar.gz
* Ubuntu-1804-bionic-64-minimal.tar.gz

License
-------

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at http://www.apache.org/licenses/LICENSE-2.0.

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.


