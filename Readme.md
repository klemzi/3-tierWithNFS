# 3-tier Web Application Architecture with a single database and an NFS server as a shared files storage

![ Architecture ](https://github.com/klemzi/3-tierWithNFS/blob/main/Images/architecture.png)

## Prepare NFS server
1. Spinned up an EC2 instance RHEL Linux 8 Operating System.
2. Attached 3 EBS volumes (10GB) and created 3 logical volumes off them.
<img width="678" alt="Logical volumes" src="https://user-images.githubusercontent.com/16520677/178125648-ee601e62-68ba-4c1f-ad9f-b1c448240e5c.png">
3. flashed a filesystem and mounted the logical volumes.
![Screenshot 2022-07-07 at 12 24 52](https://user-images.githubusercontent.com/16520677/178125903-168dafa0-7dcd-41bb-a5c7-96553f0c6cbc.png)
4. Installed NFS server using `sudo yum install nfs-utils -y`, and ensured the nfs-server.service runs at boot.
![Screenshot 2022-07-07 at 12 43 36](https://user-images.githubusercontent.com/16520677/178125923-e6bd425c-bbcc-4231-96a1-ce7fdab59212.png)
5. An NFS server maintains a table of local physical file systems that are accessible to NFS clients. The master export table is kept in a file named /var/lib/nfs/etab and is initialized with the contents of `/etc/exports` and files under `/etc/exports.d/`. Below is the contents added to the `/etc/exports` file and by invoking `exportfs -ar`, the master export table is initialized.
![Screenshot 2022-07-07 at 13 08 34](https://user-images.githubusercontent.com/16520677/178126093-e0ad5e9c-376d-49fc-82b8-f1a7169fa7ce.png)
![Screenshot 2022-07-08 at 01 45 54](https://user-images.githubusercontent.com/16520677/178126107-e1b6be89-f41d-49b3-a5ab-7dbfd6f6a383.png)
6. Get the NFS server port with `rpcinfo -p | grep nfs`, have the port as well as TCP 111, UDP 111, UDP 2049 accessible on the security group attached to the server.
![Screenshot 2022-07-08 at 01 52 41](https://user-images.githubusercontent.com/16520677/178126195-4f578826-4551-451e-89c7-565874884149.png)
![Screenshot 2022-07-08 at 01 55 43](https://user-images.githubusercontent.com/16520677/178126205-6b15fb1b-9ea6-424b-ab27-1988c3c6ab1f.png)

  
