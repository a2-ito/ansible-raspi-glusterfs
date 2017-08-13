# ansible-raspi-glusterfs

## apt-get

````
sudo apt-get install glusterfs-server
sudo apt-get install xfsprogs
````

### mount hdd

````
sudo mkdir /mnt/shareglvol
sudo mkdir /mnt/brickdisk1
sudo mkdir /mnt/brickdisk2
sudo mkdir /mnt/brickdisk3
sudo mkdir /mnt/brickdisk4

$ sudo mkfs.xfs
$ mount -t xfs /dev/sdx /mnt/brickdisk1
$ umount /mnt/brickdisk1
$ vi /etc/fstab
$ sudo reboot
````

check UUID

````
$ blkid
````

fstab
````
UUID="" /mnt/brickdisk1 xfs rw,noauto 0 0 
UUID="" /mnt/brickdisk2 xfs rw,noauto 0 0 
UUID="" /mnt/brickdisk3 xfs rw,noauto 0 0 
UUID="" /mnt/brickdisk4 xfs rw,noauto 0 0 
````

### add peer
````
sudo gluster peer probe sv02
sudo gluster peer info
````

### make volume

````
$ sudo gluster volume create shareglvol stripe 2 replica 2 \
  localhost:/mnt/brick1 \
  localhost:/mnt/brick2 \
  localhost:/mnt/brick3 \
  localhost:/mnt/brick4
$ sudo gluster volume info
$ sudo gluster volume start shareglvol
````

### client

````
sudo apt-get install gluster
sudo mount -t glusterfs localhost:/shareglvol /mnt/shareglvol
sudo umount 
````

