


Download all these files from Synopsys SolvNetPlus Website:

- Installer binary: 
SynopsysInstaller_v5.9.run

- hspice binary: 
hspice_vX-2025.06-SP1_linux64.spf

- VCS binary: 
vcs_vW-2024.09-SP2-5_common.spf
vcs_vW-2024.09-SP2-5_linux64.spf
vcs_vW-2024.09-SP2-5_linux64.spf.part00
vcs_vW-2024.09-SP2-5_linux64.spf.part01
vcs_vW-2024.09-SP2-5_linux64.spf.part02



Installation of Synopsys software:

cd /apps
mkdir synopsys
gcloud storage cp gs://thomashk-synopsys-software/* .
chmod 755 SynopsysInstaller_v5.9.run
./installer


Prompt will ask site ID, location of the spf files and installation location
It will find all spf files and install everything 


Sumbitting a sample hspice job:

```batch
sbatch hspice.job
```
