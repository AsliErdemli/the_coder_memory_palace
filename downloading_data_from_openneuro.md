# Downloading datasets from OpenNeuro
## What is OpenNeuro? 

## Code:
Create a conda environment: 

`conda create --name myproject_env`

Activate the conda environment: 

`conda activate myproject_env`

Download Python to that conda environment: 

`conda install python==3.12`

Dowload git-annex to that conda environment: 

`conda install -c conda-forge git-annex =*=alldep*`

Download datalad to that conda environment: 

`conda install -c conda-forge datalad` 
Beware! this might need to be updated to work better : get 'pip install datalad' might fix your issues

Get datalad to install the data's structure: 

`cd to_directory_starting_with_ds` 
`datalad get *`



