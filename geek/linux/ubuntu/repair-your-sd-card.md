## Repair the RaspberryPi SD Card
Occasionally the RaspberryPi SD card file system will get corrupted and you
will see messages like 'FAT-fs (mmcblk0p1): Volume was not properly unmounted.
Some data may be corrupt. Please run fsck.' Below are the steps required to
build the latest fsck.fat to repair the partition.

1. Download and build the latest fsck.fat
```shell
cd /usr/local/src
git clone http://daniel-baumann.ch/git/software/dosfstools.git
cd dosfstools/
make
sudo make install
```

2. Unmount the boot partition
```shell
sudo umount /boot
```

3. Verify and repair the partition
```shell
sudo fsck.fat -Va /dev/mmcblk0p1
```

4. Mount the boot partition
```shell
sudo mount /boot
```
