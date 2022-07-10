# 3-tier Web Application Architecture with a single database and an NFS server as a shared files storage

![ Architecture ](https://github.com/klemzi/3-tierWithNFS/blob/main/Images/architecture.png)

## Prepare NFS server
1. Spinned up an EC2 instance RHEL Linux 8 Operating System.
2. Attached 3 EBS volumes (10GB) and created 3 logical volumes off them.
<img width="678" alt="Logical volumes" src="https://user-images.githubusercontent.com/16520677/178125648-ee601e62-68ba-4c1f-ad9f-b1c448240e5c.png">

3. flashed a filesystem and mounted the logical volumes.

![ Mounted ](https://github.com/klemzi/3-tierWithNFS/blob/main/Images/Mounted.png)

4. Installed NFS server using `sudo yum install nfs-utils -y`, and ensured the nfs-server.service runs at boot.

 ![ nfs server running ](https://github.com/klemzi/3-tierWithNFS/blob/main/Images/nfs-server-running.png)
 
5. An NFS server maintains a table of local physical file systems that are accessible to NFS clients. The master export table is kept in a file named /var/lib/nfs/etab and is initialized with the contents of `/etc/exports` and files under `/etc/exports.d/`. Below is the contents added to the `/etc/exports` file and by invoking `exportfs -ar`, the master export table is initialized.

 ![ exports file ](https://github.com/klemzi/3-tierWithNFS/blob/main/Images/exportsfile.png)
 ![ master table ](https://github.com/klemzi/3-tierWithNFS/blob/main/Images/mastertable.png)
 
6. Get the NFS server port with `rpcinfo -p | grep nfs`, have the port as well as TCP 111, UDP 111, UDP 2049 accessible on the security group attached to the server.

 ![ ports ](https://github.com/klemzi/3-tierWithNFS/blob/main/Images/getports.png)
 ![ updated SG ](https://github.com/klemzi/3-tierWithNFS/blob/main/Images/securityGroups.png)

# Prepare Database server
1. Spinned up another server, installed MySQL server.
2. Created a database with command `create database tooling;` and switched to this database `use tooling;`.
3. Creates a database user webaccess
  
