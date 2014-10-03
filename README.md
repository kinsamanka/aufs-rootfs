# Readonly rootfs using aufs

These instructions were tested to work under Beaglebone Black running on Debian Wheezy

## Steps:

1. Add repository to ```/etc/apt/sources.list.d/machinekit.list```:


  ```
  $ sudo sh -c \
      "apt-key adv --keyserver hkp://keys.gnupg.net --recv-key 49550439; \
      echo 'deb http://0ptr.link/debian wheezy main' >> \
      /etc/apt/sources.list.d/machinekit.list"
  $ sudo apt-get update
  ```
2. Install aufs kernel

  ```
  $ sudo apt-get install linux-image-xenomai-aufs
  ```
3. Update kernel and reboot

  ```
  $ sudo cp /boot/vmlinuz-3.8-1-xenomai.beaglebone-omap /boot/uboot/zImage
  $ sudo reboot
  ```
4. Add needed package:


  ```
  $ sudo apt-get install e2fsck-static
  ```
5. Download and copy intramfs scripts


  ```
  $ git clone https://github.com/kinsamanka/aufs-rootfs.git
  $ sudo cp -av aufs-rootfs/files/etc/initramfs-tools/* /etc/initramfs-tools/
  ```
6. Add ```aufs``` module to ```/etc/initramfs-tools/modules```


  ```
  $ sudo sh -c 'echo aufs >> /etc/initramfs-tools/modules'
  ```
7. Edit ```/boot/uboot/uEnv.txt```, add ```rwfs=tmpfs``` to the ```bootargs``` variable and make sure that the initrd is loaded. See the sample uEnv.txt.
8. Update initrd


  ```
  $ sudo aufs-rootfs/update_initrd.sh
  ```
9. Edit ```/etc/fstab``` and remove the line containing the rootfs and make sure that all filesystems are mounted read-only
10. Reboot