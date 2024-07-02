## Process Outline
2. Installations  
    * Conda, Miniconda, Bioconda
    * Nf-core & Nextflow
    * Singularity (check version/should be installed)
    * reference libraries

# **Installations**

There are a couple single time installations that you must do to move onto the next step of this process. To continue with installations you must have access to the VACC, using an SSH connection and in a BASH enviroment. 

### Navigate to your home directory

Should look like 
```
[jdoe@vacc-user1 jdoe]$
or
[jdoe@vacc-user1 ~]$
```
Either is fine 


## Conda

The version of Conda you will be installing is [Miniconda](https://docs.anaconda.com/miniconda/#:~:text=Miniconda%20is%20a%20free%20minimal,%2C%20and%20a%20few%20others). This is a bootstrap version of [Anaconda](https://en.wikipedia.org/wiki/Anaconda_(Python_distribution)) that includes only Conda, Python, as well as some important and useful packages.

Navigate to your home directory
```
cd
```
[Install Miniconda](https://docs.anaconda.com/miniconda/#quick-command-line-install)
```
mkdir -p ~/miniconda3
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda3/miniconda.sh
bash ~/miniconda3/miniconda.sh -b -u -p ~/miniconda3
rm -rf ~/miniconda3/miniconda.sh
```
Initialize Miniconda for use with BASH and ZSH shells
```
~/miniconda3/bin/conda init bash
~/miniconda3/bin/conda init zsh
```
Add Miniconda to your global path
```
export PATH=~/miniconda3/bin/conda:$PATH
```

[Bioconda](https://bioconda.github.io/#usage) is a specific channel of Conda that provides access to the installation of certain software used in biomedical research. In this case we need to change our Miniconda channel to Bioconda to install NF-Core and Nextflow.
```
conda config --add channels defaults
conda config --add channels bioconda
```

## NF-core & Nextflow

[NF-core](https://nf-co.re/) is a workflow management software. Using NF-core pipelines is a powerful way to ensure experimental reproducability in case something fails, or it must be rerun.

To [install NF-core & Nextflow](https://nf-co.re/docs/nf-core-tools/installation#activate-shell-completions-for-nf-coretools) as one, which is what we want in this case, run the following lines in your VACC home directory.
```
conda create --name nf-core python=3.12 nf-core nextflow
conda activate nf-core
```
After running these lines Bioconda will automatically install NF-core & Nextflow.  

You can check your installation of NF-core by activating an Nf-core enviroment within your SSH connection.

```
conda activate nf-core
#or
source activate nf-core
```

After running this line you should see something like

```
(nf-core) [jdoe@vacc-user1 ~]$
```
If this does not appear there was most likely an error with the installation.

The nf-core enviroment can be deactivated with 

```
conda deactivate nf-core
```

## Singularity
Singularity is a container software used to containers that hold applications and their needed operating system libraries. Using singularity helps ensure that all needed packages and applications are in a single place in case you were to run your scripts or jobs on another device.   
  
Singularity should be preestablished within your VACC enviroment.  
Ensure Singularity exists within your enviroment with
```
which singularity
```
This should output a path which includes the current version being used.

## Reference Library
In most cases it is required that you install a reference library that nextflow can reference while running. This may library may be specific to your research being conducted.
  
An example of downloading a good reference library for humans from the Ensembl.  
  
Ensure that you are in an empty directory with a name such as "Reference_Genomes" or "Human_Genome_Refrences" so that your reference files can be found easy.
  
Retrieve the latest version of the Ensemble software from its REST API
```
latest_release=$(curl -s 'http://rest.ensembl.org/info/software?content-type=application/json' | grep -o '"release":[0-9]*' | cut -d: -f2)
```
Download their latest FASTA file for humans
```
wget -L ftp://ftp.ensembl.org/pub/release-${latest_release}/fasta/homo_sapiens/dna/Homo_sapiens.GRCh38.dna_sm.primary_assembly.fa.gz
```
Download their latest gtf file for humans
```
wget -L ftp://ftp.ensembl.org/pub/release-${latest_release}/gtf/homo_sapiens/Homo_sapiens.GRCh38.${latest_release}.gtf.gz
```
[Ensembl](https://useast.ensembl.org/index.html) also has options for other reference libraries too.


---