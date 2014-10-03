# Readonly rootfs using aufs

These instructions were tested to work under Beaglebone Black running on Debian Wheezy

## Steps:

1. Add repository to ```/etc/apt/sources.list.d/machinekit.list```:

  ```
  sudo sh -c \
    "apt-key adv --keyserver hkp://keys.gnupg.net --recv-key 49550439; \
    echo 'deb http://0ptr.link/debian wheezy main' >> \
    /etc/apt/sources.list.d/machinekit.list"
  sudo apt-get update
  ```
2. Add needed packages:

  ```
  sudo apt-get install uboot-mkimage initramfs-tools e2fsck-static
  ```
3. 
