---
layout: post
title:  "Instalar VMware Tools em distros Debian like"
date:   2023-07-08 12:26:00 -0300
categories: [SO, Linux]
tags: [vm, linux, terminal]

---

![vmware_logo](/assets/img/1-vmware-logo.jpg)
_VMware logo_


Montar a imagem na VM e executar os comandos abaixo no terminal:

```shell
$ sudo mkdir /mnt/cdrom
$ sudo mount /dev/cdrom /mnt/cdrom
$ ls /mnt/cdrom
$ tar xzvf /mnt/cdrom/VMwareTools-x.x.x-xxxx.tar.gz -C /tmp/
$ cd /tmp/vmware-tools-distrib/
$ sudo ./vmware-install.pl
$ sudo reboot
```
Após rebootar a VM o ESXi/vCenter reconhecerá o VMware Tools.