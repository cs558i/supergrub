Updated instructions can be found at:

http://www.supergrubdisk.org/wiki/Super_Grub2_Disk_test_in_virtual_machine

Introduction
=============

Super Grub2 Disk needs to be tested to see if EFI mode was builtin in it or not. So you need a virtual machine with an EFI capable boot firmware (not sure of the right technical name).

Virtualbox
==========
  Select Virtual machine
  Settings
  System
  Enable EFI (only special OS)
  OK

KVM and Ovmf
============
This is to force an EFI-only system so that you know that it actually works.
Requisites

apt-get install kvm ovmf

Test KVM and Ovmf

qemu-system-x86_64 \
-bios /usr/share/ovmf/OVMF.fd \
-cdrom ~/gnu/sgd\
/supergrub2_upstream/supergrub2\
/super_grub2_disk_hybrid_2.00s1-beta6.iso
