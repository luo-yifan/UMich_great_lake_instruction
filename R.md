# How to run R in Umich Great Lakes

## Login
```
ssh username@greatlakes.arc-ts.umich.edu
```

## Load R Environment
If you are in a conda environment(your terminal start with a (base)), run command below
```
conda deactivate
```
And then load R environment.
```
module load R
```
And then it will automatically load gcc 8.2. You can use module list to check it.
```
module list
```
If you are working with jags, (for example, rjags), you have to load a jags environment.
```
module load jags/4.3.0
```
## Install a package
```
R
```
Now you are in a R terminal, and then you can install your package.
```
install.packages('rjags')
```

## Create a Bash
```
#!/bin/bash

##################
####  Slurm preamble

#### #### ####  These are the most frequently changing options

####  Job name
#SBATCH --job-name=l2stest_job

####  Request resources here
####    These are typically, number of processors, amount of memory,
####    an the amount of time a job requires.  May include processor
####    type, too.

#SBATCH --nodes=1
#SBATCH --ntasks-per-node=1
#SBATCH --cpus-per-task=1
#SBATCH --mem-per-cpu=4000m
#SBATCH --time=1:00:00
 

####  Slurm account and partition specification here
####    These will change if you work on multiple projects, or need
####    special hardware, like large memory nodes or GPUs.

#SBATCH --account={youraccount}
#SBATCH --partition=standard

#### #### ####  These are the least frequently changing options

####  Your e-mail address and when you want e-mail

#SBATCH --mail-user={yourusermail}
#SBATCH --mail-type=BEGIN,END

# Add a note here to say what software modules should be loaded.
# for this job to run successfully.
# It will be convenient if you give the actual load command(s), e.g.,
#
module load R

####  End Slurm preamble

####  Show dynamic job information
####    This information is highly useful for job analysis & debugging
my_job_header
##################


####  Commands your job should run follow this line

echo "Running from $(pwd)"

R CMD BATCH --no-restore --no-save --quiet {yourr}.r Rbatch.out

##  If you copied any files to /tmp, make sure you delete them here!
```
Replace all the {yourcontent} with your information.

## Run & monitor
```
sbatch task.sh
```
And then monitor it on dashboard which mentioned above. DashBoard -> Jobs -> Active Jobs
If there is any error, you can check your work directory to find files like slurm-32683857.out.
