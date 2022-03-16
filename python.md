
# How to run python in Umich Great Lakes

## Login
```
ssh username@greatlakes.arc-ts.umich.edu
```

## Load A Pyhton Environment
```
module available python
module load python3.8-anaconda/2021.05
```

> For my project, conda environment is enough. I have not explored how to activate a virtual environment.

## Create a Bash
```
#!/bin/bash
# The interpreter used to execute the script

#“#SBATCH” directives that convey submission options:

#SBATCH --job-name=example_job
#SBATCH --mail-type=BEGIN,END
#SBATCH --nodes=4
#SBATCH --ntasks-per-node=4
#SBATCH --mem-per-cpu=4000m
#SBATCH --time=10:00:00
#SBATCH --account=youraccount
#SBATCH --partition=standard

# The application(s) to execute along with its input arguments and options:
# python test.py
python test.py
```

>  If you are not familiar with vim or other console text editor, you can edit it through dashboard. 
>  Go to https://greatlakes.arc-ts.umich.edu/pun/sys/dashboard.
>  And it is also easy to upload and delete files.
## Run & monitor
```
sbatch task.sh
```
And then monitor it on dashboard which mentioned above. DashBoard -> Jobs -> Active Jobs
