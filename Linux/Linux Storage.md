___
- **MBR:** 
	- It is mostly used with BIOS systems. 
	- In MBR a partition table is present at start of drive that defines how partition are made up.
	- MBR is only limited to up to 4 drives.
- **GPT:**
	- GPT is used UEFI systems mostly.
	- GPT also has partition table at start of drive but it also replicates on other locations of drive.
	- GPT comes with default CRC checksum that is applied to files.
	- GPT can handle more partition and more data than MBR.
- Partition representation of drive:
	```
	sda
		sda1
		sda2
	```
- Root `/` is mounted at `/dev/sda1`. 
- Everything in Linux is a file and is present inside of root file system `/`.
- `/proc/` and `/sys/` are virtual file systems and they are a way to interact with kernel.
- Virtual file system is like an interface that is represented as a file system.
- USB drives are represented in `/media/USB1`.
- If another drive is mounted it will be at `/dev/sda2`.
- Linux file system is monolithic.
- Partitions are organizational units for drives.
- To check block devices and partition on a system:
	- `lsblk`.
	- `df -h`.
	- `cat /proc/partitions`.
- To check disk usage of file `du -h file`.
- Tools for editing partitions on system:
	- G parted,
	- `parted`.
	- `fdisk`. 
- To check if drive is GPT or MBR `sudo parted -l`.
- Linux file systems:
	- Ext is most widely used and mature. It comes in ext2, ext3 and ext4 which is most reliable.
	- xfs is an older file system but it still used by CentOS.
	- btrfs is new and has many features but it is abandoned.
	- To create ext4 file system on `/dev/sdb1`.
		```
		mkfs.ext4 /dev/sdb1
		lsblk -f
		```
- After creating partition and making file system partition can be mounted on an empty folder.
- To mount ext4 `/dev/sdb1`partition on `/mnt/emptydir`.
- `mount -t ext4 /dev/sdb1 /mnt/emptydir`.
- To unmount and check all mounts.
	```
	umount /mnt/emptydir
	mount
	```
- To get UUID of partitions  `sudo blkid` is used.
- `/etc/fstab` is used to define which partitions should be mounted at boot time.
- To scan a partition manually `fsck /dev/sdb1`.
- To automatically scan partition on boot time:
	- `/etc/fstab` can be edited where for root partition dump value should be 1 and for other partitions it should be 2.
	- Second condition is when maximum mount count has been reached by mount count for partition than scan should occur. By default maximum mount count is set to -1 mean it will not scan.
	- To check maximum mount count `tune2fs -l /dev/sda1`.
	- To update maximum mount count `tune2fs -c 10 /dev/sda1`.
	- After scan mount count will automatically set to 0.
- Logical volume is a way to combine group of hard drives and partitions into a bucket of storage.
- Four 10 GB hard drives can be combined into one volume group of 40 GB and Logical Volume of 32 GB can be created form it.
- To check physical volumes and logical volumes `pvdisplay`, `vgdisplay` and `lvdisplay`. 
- Creating logical volume groups using drives:
	```
	pvcreate /dev/sdb /dev/sdc /dev/sdb /dev/sde
	vgcreate bucket /dev/sdb /dev/sdc /dev/sdb /dev/sde
	lvcreate -L 32G -n BIG_SIZE bucket
	mkfs.ext4 /dev/bucket/BIG_SIZE
	lvextend -L+5G /dev/bucket/BIG_SIZE
	```
- Creating Raid drives:
	```
	mdadm --create --verbose /dev/md0 --level=5 --raid-devices=4 /dev/sdb1 /dev/sdb2 /dev/sdb3 /dev/sdb4
	cat /proc/mdstat
	mdadm --detail --scan > /etc/mdadm/mdadm.conf
	mkfs.ext4 /dev/md0
	```
___