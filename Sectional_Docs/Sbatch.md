## Process Outline

6. Sbatch Script  
    * parts of your sbatch script  
        * slurm resource/job request
        * env setup
        *Nextflow call command
    * example

# **Sbatch Script**

The final step in this whole process is to create and run an sbatch script.  
The sbatch script will send a job request to slurm with the given resource requirements and then run any commands provided in the script.  
  
Just like the nf-param.json and sample_sheet.csv, you will want to save your sbatch file in your scripts directory. 
The process for writing the sbatch script is identical as nf-param.json, you can either use the nano text editor in your terminal or you can use a different texxt editor and then copy to the vacc using a file management software. 

## Parts of your sbatch script

### Slurm resource/job request
```
#!/bin/bash
#SBATCH --partition=bigmem
#SBATCH --nodes=1
#SBATCH --cpus-per-task=20
#SBATCH --mem=100G
#SBATCH --time=30:00:00
#SBATCH --job-name=nfcore_rnaseq
# %x=job-name %j=jobid
#SBATCH --output=./logs/%x_%j.out.txt
```

**Breakdown**

### Slurm job request / resource checkout
All lines should start with a "#" pound character in this part of your script only.

Sets language to bash
```
#!/bin/bash
```

Set the partition. In this case we use the VACC bigmem partition for the use of nodes with large memory
```
#SBATCH --partition=bigmem
```
Set the number of nodes you wish to use, as well as the number of cpus that will activly be working on each task in the pipeline
```
#SBATCH --nodes=1
#SBATCH --cpus-per-task=20
```
Request a certain amount of memory you estimate you will need, as well as time you think your script may take to run. (remember as long as you select "resume" in your nextflow set up the you can continue if you timeout)
```
#SBATCH --mem=100G
#SBATCH --time=30:00:00
```
Finally create a job name, as well as make an output location for the logs that will be generated. These lines do not need to be edited default names are good.
```
#SBATCH --job-name=nfcore_rnaseq
# %x=job-name %j=jobid
#SBATCH --output=./logs/%x_%j.out.txt
```



### Enviroment set-up

After your job request you need to set up your code that will actually run within the submited job. 

This starts with eviroment set-up.  
First activate an nf-core enviroment.
```
source activate nf-core
```
Next load Singularity
```
module load singularity
```
Finally add my_job_header, this will print information about the submited job once it is run
```
my_job_header
```

### Tell Nextflow to start your pipeline

This line tells nextflow to run its nf-core/rnaseq pipeline using your nf-params.json file for parameters.
It is important to also include the -resume at the end of this line so that your run may be continued if it times out.
```
nextflow run nf-core/rnaseq -r 3.14.0 -profile singularity -params-file nf-params.json -resume
```

### Your final sbatch script

In the end you shold have something that looks similar to this.
```
#!/bin/bash
#SBATCH --partition=bigmem
#SBATCH --nodes=1
#SBATCH --cpus-per-task=20
#SBATCH --mem=100G
#SBATCH --time=30:00:00
#SBATCH --job-name=nfcore_rnaseq
# %x=job-name %j=jobid
#SBATCH --output=./logs/%x_%j.out.txt

source activate nf-core

module load singularity

nextflow run nf-core/rnaseq -r 3.14.0 -profile singularity -params-file nf-params.json -resume
```

If you followed these steps in the nano text editor save this file with the name like "run_nfcore_rnaSeq.sh". If you followed these steps in a personal text editor use a filemanegment software or copy and paste your file into your VACC project scripts directory. 

---
---

