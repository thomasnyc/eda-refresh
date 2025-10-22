# Cluster Toolkit for Synopsys run and details**

The page has a sample blueprint synopsys-blueprint.yaml which is design for EDA. It includes the following components: 

- Slurm cluster with H4D instances 
- Managed Lustre service - for apps directory
- Filestore service - for Home directory 
- License server
- Chrome Remote Desktop 

Please update the blueprint with the correct Project ID . Then use the following command to deploy the cluster: 

```
./gcluster deploy -w eda-slurm-h4d.yaml
```

At finish, the cluster shall be up and running. It may take about an hour for the whole deployment: 

# Synopsys installation  

## List of files downloaded from Synopsys:

Download all these files from Synopsys SolvNetPlus Website:

- Installer binary: 
```
SynopsysInstaller_v5.9.run
```
- Synopsys Common Licensing (SCL) binary
```
scl_v2025.03-SP2_common.spf
scl_v2025.03-SP2_linux64.spf
scl_v2025.03-SP2_linuxaarch64.spf
```
- hspice binary: 
```
hspice_vX-2025.06-SP1_linux64.spf
```
- VCS binary: 
```
vcs_vW-2024.09-SP2-5_common.spf
vcs_vW-2024.09-SP2-5_linux64.spf
vcs_vW-2024.09-SP2-5_linux64.spf.part00
vcs_vW-2024.09-SP2-5_linux64.spf.part01
vcs_vW-2024.09-SP2-5_linux64.spf.part02
```

## Installation of Synopsys software:

```
cd /apps
mkdir synopsys
gcloud storage cp gs://thomashk-synopsys-software/* .
chmod 755 SynopsysInstaller_v5.9.run
./SynopsysInstaller_v5.9.run
./installer
```

Prompt will ask site ID, location of the spf files and installation location
It will find all spf files and install everything 

## License:

Please make the Installer and Synopsys Common Licensing (SCL) binary available in the license server. Run the installer application at finish: one will see this message: 

Synopsys tools require that a supported version of Synopsys Common
Licensing (SCL) be installed and serving the necessary licenses.

### Applying license file:

WIP

## Sample hspice job:

User can submit the job by leveaging the hspice.job file in this repo: 

Submit the job: 

```batch
sbatch hspice.job
```
