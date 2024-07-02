# **Sample Sheets**

### What is a sample sheet?

A sample sheet is often a .csv file holding information about your samples such as the paths to their fastq files. It is easiest to make then in a spreadsheet editor like Microsoft excel, or a text editor.

Sample sheets that will be used in a nextflow pipeline must adhere to a specific format
  
| sample | fastq_1 | fastq_2 | strandedness |
|--------|---------|---------|--------------|
| T0-s1  |Epic_Project1/reads/0hr_S1_R1.fastq.gz|Epic_Project1/reads/0hr_S1_R2.fastq.gz | auto
| T0-s2  |Epic_Project1/reads/0hr_S2_R1.fastq.gz |Epic_Project1/reads/0hr_S2_R2.fastq.gz | auto
| T48-s3 |Epic_Project1/reads/48hr_S3_R1.fastq.gz |Epic_Project1/reads/48hr_S3_R2.fastq.gz | auto
| T48-s4 |Epic_Project1/reads/48hr_S4_R1.fastq.gz |Epic_Project1/reads/48hr_S4_R2.fastq.gz | auto
---

* In this format your desired sample name goes in the leftmost column.  
* The second column is for the first fastq file path for that sample.   
* The third column is for the reverse fastq file path for that sample. 
* The third column is for unstranded, forward, reverse, or auto depending on what you know about the sequencing process. 

Once your sample sheet has been creating it should be exported as a .csv file to your scripts directory in your project directory. This is an escpecially easy process if you are using a file managment app such as Filezilla to transfer your .csv file from your local machine to the VACC. 

---