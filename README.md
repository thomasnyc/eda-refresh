# Google Cloud Platform EDA Refresh 

This is the document for deploying common EDA application with Google Cloud Platform Cluster Toolkit . 

1. Creating the HPC cluster 
    1. Slurm Cluster
    2. Storage - Managed Lustre and Filestore
        1. Managed Lustre
        2. Filestore
2. Synopsys application - VCS
    1. Installation of software
    2. VCS sample run
    3. HSPICE sample run

## Cluster setup

We are using the Goolge Cloud Platform Cluster Toolkit to create a new cluster. 

By using the Cluster Toolkit blueprint yaml:
h4d-slurm-lustre-crd.yaml

This Blueprint has Slurm setup with Managed Lustre for H4D instances. Chrome Remote Desktop node is also added to the blueprint. 

Once the setup of the Cluster Toolkit, one can run the following 

```
./gcluster deploy -w hpc-slurm-h4d.yaml
```
After the cluster setup (about 45mins), login to the slurm login node and we can see the sinfo and lustre file system: 

Slurm cluster:
```
[thomashk_thomashk_altostrat_com@slurmh4d-slurm-login-001 ~]$ sinfo
PARTITION AVAIL  TIMELIMIT  NODES  STATE NODELIST
h4d*         up   infinite      2  down# slurmh4d-h4dnodeset-[0-1]
```

Storage: 
```
[thomashk_thomashk_altostrat_com@slurmh4d-slurm-login-001 ~]$ ls
[thomashk_thomashk_altostrat_com@slurmh4d-slurm-login-001 ~]$ df -h
Filesystem                     Size  Used Avail Use% Mounted on
devtmpfs                       7.7G     0  7.7G   0% /dev
tmpfs                          7.7G     0  7.7G   0% /dev/shm
tmpfs                          7.7G  8.5M  7.7G   1% /run
tmpfs                          7.7G     0  7.7G   0% /sys/fs/cgroup
/dev/sda2                       50G   20G   31G  39% /
/dev/sda1                      200M  5.9M  194M   3% /boot/efi
tmpfs                          1.6G     0  1.6G   0% /run/user/0
10.x.x.x@tcp:/lustrefs         35T   22M   35T   1% /data
10.x.x.x:/homeshare        2.5T     0  2.4T   0% /home
slurmh4d-controller:/opt/apps   50G   20G   31G  39% /opt/apps
tmpfs                          1.6G     0  1.6G   0% /run/user/1911945234
```

## Synopsys 

Download all these files from Synopsys SolvNetPlus Website:

- Installer binary: 
    - SynopsysInstaller_v5.9.run
- hspice binary: 
    - hspice_vX-2025.06-SP1_linux64.spf
- VCS binary: 
    - vcs_vW-2024.09-SP2-5_common.spf
    - vcs_vW-2024.09-SP2-5_linux64.spf
    - vcs_vW-2024.09-SP2-5_linux64.spf.part00
    - vcs_vW-2024.09-SP2-5_linux64.spf.part01
    - vcs_vW-2024.09-SP2-5_linux64.spf.part02

### Installation of Synopsys software:

```cd /apps
mkdir synopsys
gcloud storage cp gs://thomashk-synopsys-software/* .
chmod 755 SynopsysInstaller_v5.9.run
./installer
```

Prompt will ask site ID, location of the spf files and installation location
It will find all spf files and install everything 


Sumbitting a sample hspice job:

```batch
sbatch hspice.job
```
    
