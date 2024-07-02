# **Contents**

7. Runing Your Job  
    * review repo structure
    * preview post submission repo structure
    * submitting an sbatch script to slurm

8. Post Submission Review  
    * check running job progress
    * check completed job slurm statistics

9. Trouble Shooting  

# **Running your job**

If you have followed this tutorial correctly you should currently have a project repository that looks similar to this.
```
-scratch
    -RNAseqProjectTutorial
        -scripts
            -nf-params.json
            -run_nfcore_rnaSeq.sh  
            -sample_sheet.csv
        -nf-core_rnaSeq_out (either an empty directory or one that will be made by nextflow)
```
Once your run your project for the first time a logs, and work directory will be added to your scripts directory.
```
-scratch
    -RNAseqProjectTutorial
        -scripts
            -logs
            -nf-params.json
            -run_nfcore_rnaSeq.sh  
            -sample_sheet.csv
            -work
        -nf-core_rnaSeq_out (either an empty directory or one that will be made by nextflow)
```

### Submit your sbatch script

Navigate to your scripts directory  

Run the following code to submit you slurm request.
```
sbatch run_nfcore_rnaSeq.sh
```
If your chose a different name for your sbatch file replace run_nfcore_rnaSeq.sh with that name.  

  
If done correctly you should see your job submission and the job id printed onto your terminal. 
  
---
---

# **Post Submission**

Check your job is running with
```
squeue -u $USER
```
This will display things like time run, job id, and the node it is running on.

### Check job statistics while running

Navigate into the node your job is running on (replace the # with the node number you say in the prev. command)
```
ssh node#
```

Filter the running jobs to just your job with
```
top -u $USER
```

This page you now see should be giving you information about mem usage, cpu usage, run time etc... for each job in your pipeline.  
  
Use "f" to bring up a list of fields. 

Edit which fields are displayed by arrow key navigation and slecting them on or off with "d"

Use "q" to navigate back to your job statistics. 

### Post completion review of job statistics

After a job has been completed you can use 
```
my_job_statistics jobid
```
to review a report. (replace jobid with the id in your logs directory)

---
---

# **Trouble shooting**

After your first run, a logs directory will be made in your scripts directory. 

If you navigate to this directory there will be text files that include information about your sbatch submission. You can use 
```
nano filename
```
to inspect these logs.

A successful run of a nf-core RNAseq pipeline may have a .txt log header that looks like this. 
```
 N E X T F L O W   ~  version 24.04.2

Launching `https://github.com/nf-core/rnaseq` [voluminous_mccarthy] DSL2 - revision: b89fac3265 [3.14.0]



------------------------------------------------------
                                        ,--./,-.
        ___     __   __   __   ___     /,-._.--~'
  |\ | |__  __ /  ` /  \ |__) |__         }  {
  | \| |       \__, \__/ |  \ |___     \`-._,-`-,
                                        `._,._,'
  nf-core/rnaseq v3.14.0-gb89fac3
------------------------------------------------------
Core Nextflow options
  revision        : 3.14.0
  runName         : voluminous_mccarthy
  containerEngine : singularity
  launchDir       : /gpfs2/scratch/jdoe/GenomeProjectTutorial/scripts
  workDir         : /gpfs2/scratch/jdoe/GenomeProjectTutorial/scripts/work
  projectDir      : /users/j/d/jdoe/.nextflow/assets/nf-core/rnaseq
  userName        : jdoe
  profile         : singularity
```

If your sbatch submission encountered an error the error may appear in the log file that was generated. 

Give your submission some time and then check on its runtime with
```
squeue -u $USER
```

If you expect your job should still be running but the previous command does not display any active jobs, check the most recent log file to see if an error was encountered. 

---