#  Singularity image containing Freesurfer and HCP Conncectome Workbench
This Singularity image will be about 6GB when built using Singularity 2.4.2. It installs the latest development version of freesurfer and HCP Connectome Workbench


## Build Singularity Image

* You will need to have at least singularity 2.4 installed. Simply clone this repository to a convenient directory.
* Navigate into the `nklab-neuro-HCP`directory and check that you have a Singularity definiton file `Singularity` and the directory `src`
* Confirm that `src` folder and all the files in `src` have full read and write privileges. if not then `sudo chmod -R 777 src` should accomplish this.
* Now simply build the image as  `sudo singularity build nklab-neuro-HCP.simg Singularity` - note that the image name is assumed to be `nklab-neuro-HCP.simg` but this can be changed to a more convenient label. 

## Run Singularity Image
You can now run commands by simply appending them to the end of  `singularity run nklab-neuro-HCP.simg` So for example to run `wb_command` simply enter `singularity run nklab-neuro-tools.HCP wb_command ....`