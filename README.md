# moosefs_ubuntu

Install MooseFS file system on Ubuntu 16.04 via Ansible

This is just an example of the way we have implemented MooseFS here on premises. Use at your own risk, this has only been installed once on Ubuntu 16.04.

Setup 6 servers with large 10 TB RAID mounted on /data and tiny ssds mounted on /ssd.

## Known issues

#### No connection between chunkservers and master
When looking at the logs (`journalctl`) it gave the following error message:
```
mfschunkserver[6272]: MATOCS_MASTER_ACK - wrong meta data id (file chunkserverid.mfs:5B28ECE4FC168CA4 ; received from master:5B5F1B3FD4FCC69E). Can't conne ct to master
```
According to [this](https://github.com/moosefs/moosefs/issues/74#issuecomment-333080324) comment. Deleting ` /var/lib/mfs/chunkserverid.mfs` and `/mnt/[hdd mount point]/.metaid` helps. In our case this was the solution for the problem.
