To modify config file for master container: 

``` 
    sudo docker run -it --rm --volume nextcloud_aio_mastercontainer:/mnt/docker-aio-config:rw alpine sh -c "apk add --no-cache nano && nano /mnt/docker-aio-config/data/configuration.json" 

check mount status
```lsblk

External Drive mount
```sudo mount /dev/sda1 /mnt/external_drive

To view disks, go to administrator settings > System (bottom)


Check Disk space: 
df -h

clean up manually:
sudo ncdu -x /

(GUI) auto cleanup:
sudo bleachbit



Youtube tutorial: 
https://www.youtube.com/watch?v=ewarxugZH3Q&t=101s