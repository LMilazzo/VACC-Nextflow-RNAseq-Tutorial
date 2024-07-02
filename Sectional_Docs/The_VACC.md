## Process Outline

1. The VACC  
    * ssh connection
    * file manegment software
    * user account structure
    * VACC navigation
    * checking out computing nodes


# **THE VACC**

The Vermont Advanced Computing Center (VACC), provides access to services like data/file managment and high-performance computing clusters used for small and large jobs or workflows. VACC is responsible for multiple clusters the one used in this process is Bluemoon.
[University of Vermont VACC](https://www.uvm.edu/vacc)

### SSH Connection

The VACC may be accessed through Secure Shell Protocol (SSH). 

VACC Access With SSH:

1. Open a command prompt or powershell like application
    * [Command Prompt](https://en.wikipedia.org/wiki/Cmd.exe#:~:text=Command%20Prompt%2C%20also%20known%20as,On%20Windows%20CE%20.)
    * [Power Shell](https://en.wikipedia.org/wiki/PowerShell)

2. Within your shell create an SSH connection to the VACC

```
ssh jdoe@vacc-user1.uvm.edu
```
As of July 2024, the VACC has been expanded to a total of 4 user systems. user2, user3, and user4 are also available for VACC users to log onto. Users may represent physical machines, however personal files on the VACC are stored virtually so they may be accessed from all 4 user systems equally. If you find your login is being slower than expected:

* Use a different user in the ssh command
* Check your email for scheduled maintenence notifications  
* If issues persist try contacting [Vermont Advanced Computing Center](https://www.uvm.edu/vacc/contact-us)

3. You will then be asked for your password  

    * If done correctly you should be in a directory like below:
    ```
    [jdoe@vacc-user1 jdoe]$
    ```

### File Management Application Connection

If you intend on creating new directories, moving files to the vacc, or downloading vacc hosted files to your computer it may be easier to log in using a file managment application such as [Filezilla](https://filezilla-project.org/). 

To acccess the VACC using a filemanegment the credentials are as follows:

**Host** :  vacc-user1.uvm.edu  
**Username** : first initial + last name  
Example: jdoe  
**Password** : Same as if you logged in through SSH  
**Port** : 22



## Navigating the VACC / HPC Enviroments

While navigating through files and directories in a file managment application like 
[Filezilla](https://filezilla-project.org/) 
is easy, the process in
[Command Prompt](https://en.wikipedia.org/wiki/Cmd.exe#:~:text=Command%20Prompt%2C%20also%20known%20as,On%20Windows%20CE%20.)
or
[Power Shell](https://en.wikipedia.org/wiki/PowerShell)
is a little more complicated. The navigation of the VACC in these instances will require the use of 
[BASH](https://tiswww.case.edu/php/chet/bash/bashtop.html). 

#### Common Bash Commands

cd -> Use cd followed by a directory name to navigate to that directory  
cd ../ -> Used to navigate to the current directories parent directory  
ls -> Displays all contents of a directory  
pwd -> Displays the current directory path  
mkdir -> Makes a new directory with the given name  
rmdir -> Deletes the given empty directory  
rm -r -> Recursivly deletes a directoy and all contents, ***USE CAREFULLY***  
cat -> Display file contents  
squeue -u -> Displays the active jobs & computing nodes for a given user   
scancel -> Cancels a job with a given job id  
scancel -u -> Cancels all jobs for the given username

Some helpful documentation for using an HPC can be found on [VACC's site](https://www.uvm.edu/vacc/kb/article-categories/commands-terms/).

  
## VACC Computing Nodes

In order to use the VACC to proccess data or make downloads you must check out a computing node.

This command communicates with SLURM, the VACC's workload manager, to check out a single interactive compute node with 5G of memory and 1 CPU.
```
srun --qos=interactive --mem=5G --cpus-per-task 1 --pty bash
```

---