First Steps
===========

Mounting the root FS on an SD card
----------------------------------

1. Enable ext4 support
.. code:: bash
    # opkg update
    # opkg install block-mount kmod-fs-ext4 kmod-usb-storage-extras e2fsprogs fdisk

2. Format SD card
.. code:: bash
    # mkfs.ext4 /dev/mmcblk0p1

3. Copy root fs to SD
.. code:: bash
    # mount /dev/mmcblk0p1 /mnt
    # tar -C /overlay -cvf - . | tar -C /mnt -xf -
    # umount /mnt

4. Generate *fstab* (file system partitions table) from the current fs configuration
.. code:: bash
    # block detect > /etc/config/fstab

5. Edit *fstab*
.. code:: bash
    config 'mount'
      option  target  '/overlay'
      ...
      option  enabled '1'

6. Reboot