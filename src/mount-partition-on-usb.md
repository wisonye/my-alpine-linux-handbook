# Mount partitions on USB

Before installing `Arch Liunx` to the USB, you need to mount the `Arch Linux root partition` and `Arch Linux boot partition`, then you can use `pacmanc` to install the newer Linux filesystem to the mounted folder.

You can run `fdisk -l /dev/sdX` to print the partition table again if you forgot.

```bash
mount /dev/sdX3 /mnt
mkdir /mnt/boot
mount /dev/sdX2 /mnt/boot

# You can `ls` to confirm 
ls -lht /mnt/boot
ls -lht /mnt

# You can run `df -Th` to confirm both partitions are using the correct format before you do the real installation.
df -Th | grep \/mnt
/dev/sdX3   ext4    /mnt
/dev/sdX2   vfat    /mnt/boot
```

</br>

![15.png](./images/virtual-box-installation/15.png)
