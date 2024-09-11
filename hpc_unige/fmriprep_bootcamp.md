# This is for commands we used in the fmriprep_bootcamp sept 2024

## This is to get slurm to allocate you 12 cpus for 30 mins on shared-cpu partition
salloc --partition=shared-cpu --time=00:30:00 --cpus-per-task 12  

## MRIQC: 

### To pull a apptainer (ex-name: Singularity) image : 
`apptainer pull docker://nipreps/mriqc:latest`

### To run the image you pulled: 
`apptainer run mriqc_latest.sif --version` 

### To run mriqc with sbatch as a slurm job: 
use an sbatch by putting this is a file called "mriqc.sbatch"

```
#!/bin/bash
#SBATCH --time=1:00:00 #NOTE: likely longer than generally needed 
#SBATCH --ntasks 1
#SBATCH --cpus-per-task=16
#SBATCH --mem-per-cpu=1G
#SBATCH --partition=shared-cpu
#SBATCH --reservation=share_courvoisier_workshop_570
# Outputs ----------------------------------
#SBATCH --output log/%x-%A-%a.out
#SBATCH --error log/%x-%A-%a.err
#SBATCH --mail-user=asli.erdemli@unige.ch
#SBATCH --mail-type=ALL
# ------------------------------------------
srun apptainer run mriqc_latest.sif \
     $HOME/ds005454/ $HOME/derivatives/mriqc-24.0.2 participant \
     -m T1w -vv --dsname bootcamp --nprocs 12 --omp-nthreads 8
```
then run it via 
`sbatch mriqc.sbatch`
## fMRIprep image: 
### to pull the image: 
`apptainer pull docker://markiewicz/fmriprep:24.1.0rc2` # This was the "most recent" available at the time 
### to run the image: 
make an sbatch file called `fmriprep.sbatch` which has:
```
#!/bin/bash
#SBATCH --time=4:00:00 #NOTE: likely longer than generally needed
#SBATCH --ntasks 1
#SBATCH --cpus-per-task=16
#SBATCH --mem-per-cpu=1G
#SBATCH --partition=shared-cpu
#SBATCH --reservation=share_courvoisier_workshop_570
# Outputs ----------------------------------
#SBATCH --output log/%x-%A-%a.out
#SBATCH --error log/%x-%A-%a.err
#SBATCH --mail-user=asli.erdemli@unige.ch
#SBATCH --mail-type=ALL
# ------------------------------------------
srun apptainer run fmriprep_24.1.0rc2.sif \
     $HOME/horikawa/Horikawa_python_test/data/raw $HOME/horikawa/Horikawa_python_test/data/derivatives/fmriprep24.1.0 participant \
      --nprocs 12 --omp-nthreads 8 --fs-license=$HOME/horikawa/license.txt
```

