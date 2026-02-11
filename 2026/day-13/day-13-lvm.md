ask 1: Check Current Storage
Run: lsblk, pvs, vgs, lvs, df -h

ubuntu@ip-172-31-16-85:~$ sudo su
root@ip-172-31-16-85:/home/ubuntu# pvs
root@ip-172-31-16-85:/home/ubuntu# lvs
root@ip-172-31-16-85:/home/ubuntu# vgs
root@ip-172-31-16-85:/home/ubuntu# df -h
Filesystem       Size  Used Avail Use% Mounted on
/dev/root        6.8G  2.2G  4.6G  32% /
tmpfs            458M     0  458M   0% /dev/shm
tmpfs            183M  872K  182M   1% /run
tmpfs            5.0M     0  5.0M   0% /run/lock
efivarfs         128K  3.8K  120K   4% /sys/firmware/efi/efivars
/dev/nvme0n1p16  881M   89M  730M  11% /boot
/dev/nvme0n1p15  105M  6.2M   99M   6% /boot/efi
tmpfs             92M   12K   92M   1% /run/user/1000
root@ip-172-31-16-85:/home/ubuntu# lsblk
NAME         MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
loop0          7:0    0 27.6M  1 loop /snap/amazon-ssm-agent/11797
loop1          7:1    0 27.8M  1 loop /snap/amazon-ssm-agent/12322
loop2          7:2    0   74M  1 loop /snap/core22/2163
loop3          7:3    0 48.1M  1 loop /snap/snapd/25935
loop4          7:4    0 50.9M  1 loop /snap/snapd/25577
nvme0n1      259:0    0    8G  0 disk
├─nvme0n1p1  259:1    0    7G  0 part /
├─nvme0n1p14 259:2    0    4M  0 part
├─nvme0n1p15 259:3    0  106M  0 part /boot/efi
└─nvme0n1p16 259:4    0  913M  0 part /boot
root@ip-172-31-16-85:/home/ubuntu#

Task 2: Create Physical Volume
pvcreate /dev/sdb   # or your loop device
pvs

we have created two volume 
root@ip-172-31-16-85:/home/ubuntu# lsblk
NAME         MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
loop0          7:0    0 27.6M  1 loop /snap/amazon-ssm-agent/11797
loop1          7:1    0 27.8M  1 loop /snap/amazon-ssm-agent/12322
loop2          7:2    0   74M  1 loop /snap/core22/2163
loop3          7:3    0 48.1M  1 loop /snap/snapd/25935
loop4          7:4    0 50.9M  1 loop /snap/snapd/25577
nvme0n1      259:0    0    8G  0 disk
├─nvme0n1p1  259:1    0    7G  0 part /
├─nvme0n1p14 259:2    0    4M  0 part
├─nvme0n1p15 259:3    0  106M  0 part /boot/efi
└─nvme0n1p16 259:4    0  913M  0 part /boot
nvme1n1      259:5    0    3G  0 disk
nvme2n1      259:6    0    2G  0 disk
root@ip-172-31-16-85:/home/ubuntu#

root@ip-172-31-16-85:/home/ubuntu# lsblk
NAME         MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
loop0          7:0    0 27.6M  1 loop /snap/amazon-ssm-agent/11797
loop1          7:1    0 27.8M  1 loop /snap/amazon-ssm-agent/12322
loop2          7:2    0   74M  1 loop /snap/core22/2163
loop3          7:3    0 48.1M  1 loop /snap/snapd/25935
loop4          7:4    0 50.9M  1 loop /snap/snapd/25577
nvme0n1      259:0    0    8G  0 disk
├─nvme0n1p1  259:1    0    7G  0 part /
├─nvme0n1p14 259:2    0    4M  0 part
├─nvme0n1p15 259:3    0  106M  0 part /boot/efi
└─nvme0n1p16 259:4    0  913M  0 part /boot
nvme1n1      259:5    0    3G  0 disk
nvme2n1      259:6    0    2G  0 disk
root@ip-172-31-16-85:/home/ubuntu#lvm
lvm> pvcreate /dev/nvme1n1 /dev/nvme2n1
  Physical volume "/dev/nvme1n1" successfully created.
  Physical volume "/dev/nvme2n1" successfully created.
lvm> pvs
  PV           VG Fmt  Attr PSize PFree
  /dev/nvme1n1    lvm2 ---  3.00g 3.00g
  /dev/nvme2n1    lvm2 ---  2.00g 2.00g
lvm> vgcreate dev_vg /dev/nvme1n1 /dev/nvme2n1
  Volume group "dev_vg" successfully created
lvm> vgs
  VG     #PV #LV #SN Attr   VSize VFree
  dev_vg   2   0   0 wz--n- 4.99g 4.99g
lvm> lvcreate -L 3G -n dev_lv dev_vg
  Logical volume "dev_lv" created.
lvm>
root@ip-172-31-16-85:/home/ubuntu# vgs
  VG     #PV #LV #SN Attr   VSize VFree
  dev_vg   2   1   0 wz--n- 4.99g 1.99g
root@ip-172-31-16-85:/home/ubuntu# lvs
  LV     VG     Attr       LSize Pool Origin Data%  Meta%  Move Log Cpy%Sync Convert
  dev_lv dev_vg -wi-a----- 3.00g                                        
root@ip-172-31-16-85:/home/ubuntu# mkfs.ext4 /dev/dev_vg/dev_lv
mke2fs 1.47.0 (5-Feb-2023)
Creating filesystem with 786432 4k blocks and 196608 inodes
Filesystem UUID: 929d0ece-56a0-4303-ae72-bd429981fb76
Superblock backups stored on blocks:
        32768, 98304, 163840, 229376, 294912

Allocating group tables: done
Writing inode tables: done
Creating journal (16384 blocks): done
Writing superblocks and filesystem accounting information: done

root@ip-172-31-16-85:/home/ubuntu# mkdir /mnt/data
root@ip-172-31-16-85:/home/ubuntu# mount /dev/d
dev_vg/   disk/     dm-0      dma_heap/ dri/
root@ip-172-31-16-85:/home/ubuntu# mount /dev/dev_vg/dev_lv /mnt/data/
root@ip-172-31-16-85:/home/ubuntu# df -h
Filesystem                 Size  Used Avail Use% Mounted on
/dev/root                  6.8G  2.2G  4.6G  32% /
tmpfs                      458M     0  458M   0% /dev/shm
tmpfs                      183M  900K  182M   1% /run
tmpfs                      5.0M     0  5.0M   0% /run/lock
efivarfs                   128K  3.8K  120K   4% /sys/firmware/efi/efivars
/dev/nvme0n1p16            881M   89M  730M  11% /boot
/dev/nvme0n1p15            105M  6.2M   99M   6% /boot/efi
tmpfs                       92M   12K   92M   1% /run/user/1000
/dev/mapper/dev_vg-dev_lv  2.9G   24K  2.8G   1% /mnt/data
root@ip-172-31-16-85:/home/ubuntu# lvextend -L +100M /dev/dev_vg/dev_lv
  Size of logical volume dev_vg/dev_lv changed from 3.00 GiB (768 extents) to <3.10 GiB (793 extents).
  Logical volume dev_vg/dev_lv successfully resized.
root@ip-172-31-16-85:/home/ubuntu# df -h
Filesystem                 Size  Used Avail Use% Mounted on
/dev/root                  6.8G  2.2G  4.6G  32% /
tmpfs                      458M     0  458M   0% /dev/shm
tmpfs                      183M  900K  182M   1% /run
tmpfs                      5.0M     0  5.0M   0% /run/lock
efivarfs                   128K  3.8K  120K   4% /sys/firmware/efi/efivars
/dev/nvme0n1p16            881M   89M  730M  11% /boot
/dev/nvme0n1p15            105M  6.2M   99M   6% /boot/efi
tmpfs                       92M   12K   92M   1% /run/user/1000
/dev/mapper/dev_vg-dev_lv  2.9G   24K  2.8G   1% /mnt/data
root@ip-172-31-16-85:/home/ubuntu# resize /dev/dev_vg/dev_lv
Command 'resize' not found, but can be installed with:
apt install xterm
root@ip-172-31-16-85:/home/ubuntu# resize2fs /dev/dev_vg/dev_lv
resize2fs 1.47.0 (5-Feb-2023)
Filesystem at /dev/dev_vg/dev_lv is mounted on /mnt/data; on-line resizing required
old_desc_blocks = 1, new_desc_blocks = 1
The filesystem on /dev/dev_vg/dev_lv is now 812032 (4k) blocks long.

root@ip-172-31-16-85:/home/ubuntu# df -h
Filesystem                 Size  Used Avail Use% Mounted on
/dev/root                  6.8G  2.2G  4.6G  32% /
tmpfs                      458M     0  458M   0% /dev/shm
tmpfs                      183M  900K  182M   1% /run
tmpfs                      5.0M     0  5.0M   0% /run/lock
efivarfs                   128K  3.8K  120K   4% /sys/firmware/efi/efivars
/dev/nvme0n1p16            881M   89M  730M  11% /boot
/dev/nvme0n1p15            105M  6.2M   99M   6% /boot/efi
tmpfs                       92M   12K   92M   1% /run/user/1000
/dev/mapper/dev_vg-dev_lv  3.0G   24K  2.9G   1% /mnt/data
root@ip-172-31-16-85:/home/ubuntu# df -h /mnt/data/
Filesystem                 Size  Used Avail Use% Mounted on
/dev/mapper/dev_vg-dev_lv  3.0G   24K  2.9G   1% /mnt/data
root@ip-172-31-16-85:/home/ubuntu# resize2fs /dev/dev_vg/dev_lv
resize2fs 1.47.0 (5-Feb-2023)
The filesystem is already 812032 (4k) blocks long.  Nothing to do!

root@ip-172-31-16-85:/home/ubuntu# df -h
Filesystem                 Size  Used Avail Use% Mounted on
/dev/root                  6.8G  2.2G  4.6G  32% /
tmpfs                      458M     0  458M   0% /dev/shm
tmpfs                      183M  900K  182M   1% /run
tmpfs                      5.0M     0  5.0M   0% /run/lock
efivarfs                   128K  3.8K  120K   4% /sys/firmware/efi/efivars
/dev/nvme0n1p16            881M   89M  730M  11% /boot
/dev/nvme0n1p15            105M  6.2M   99M   6% /boot/efi
tmpfs                       92M   12K   92M   1% /run/user/1000
/dev/mapper/dev_vg-dev_lv  3.0G   24K  2.9G   1% /mnt/data
root@ip-172-31-16-85:/home/ubuntu