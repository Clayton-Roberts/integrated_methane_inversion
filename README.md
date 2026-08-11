# Integrated Methane Inversion (IMI) Workflow
## Overview:

This directory contains the source code for setting up and running the
[Integrated Methane Inversion](https://carboninversion.com/) with GEOS-Chem. This fork has been created specifically to accomodate the needs of scientists at SRON who use the IMI on the Dutch National Supercomputer Snellius.


## Documentation:

For official IMI documentation, please see the [IMI readthedocs site](https://imi.readthedocs.io).

## SRON installation steps

1. Step one: clone the SRON-specific fork of the IMI:
```shell
git clone https://github.com/Clayton-Roberts/integrated_methane_inversion.git
```

2. Move into the IMI directory you've created and clone GCClassic. Use the -recursive flag to download links from previous commits: 
```shell
cd integrated_methane_inversion
git clone https://github.com/geoschem/GCClassic.git
cd GCClassic
git submodule update --init –-recursive
```

 (to download links from previous commits)

3. Download Anaconda into your home directory. Run the command 
```
bash ./Anaconda.sh
```
and accept everything. Then make sure the following is in your .bashrc file in your home directory (make sure to change croberts to your username!):
```
# >>> conda initialize >>>
# !! Contents within this block are managed by 'conda init' !!
__conda_setup="$('/home/croberts/miniconda3/bin/conda' 'shell.bash' 'hook' 2> /dev/null)"
if [ $? -eq 0 ]; then
    eval "$__conda_setup"
else
    if [ -f "/home/croberts/miniconda3/etc/profile.d/conda.sh" ]; then
        . "/home/croberts/miniconda3/etc/profile.d/conda.sh"
    else
        export PATH="/home/croberts/miniconda3/bin:$PATH"
    fi
fi
unset __conda_setup
# <<< conda initialize <<<
```

4. Navigate to 
```
envs/Snellius
```
and edit the last line of imi_env.yml so that the prefix references your own home directory. Then run the command

```
conda create --file imi_env.yml
```

When that's finished (it may take some time), activate this environment via 

```
conda activate imi_env
```

and install this custom package from Github that we need:

```
python -m pip install git+https://github.com/LiamBindle/sparselt.git
```

## Extra steps for when you want to set up a project

1. You need to have the appropriate boundary condition files downloaded for your project. Check out the script at `/projects/0/src17245/IMI/Inputs/ExtData/GCinput/download_boundary_files.sh` to see how to do this.

2. You need to make sure that you have the GEOS-FP meteorological data to run your simulation. For example, if you were using North American (NA) data at 25km resolution, this data needs to be located at `/projects/0/src17245/IMI/Inputs/ExData/GEOS_0.25x0.3125_NA`, with the appropriate date range in the sub-folders. Importantly, this should NOT be located in the `Meteo` folder; the IMI expects it to be just underneath `ExtData`.

## Things to discuss with Matthieu/Shubham: 

1. I altered surc/utilities/common.sh so that submit_slurm_job has --export=ALL in it; this passes the loaded environment .env file through to job nodes. 

2. I needed to alter the .env file to make sure that our MPI and NETCDF libraries are linked correctly; we have EasyBuild-built modules instead of FASRC-built modules.

3. I also needed to alter src/geoschem_run_scripts/submit_jacobian_simulations_array.sh as sbatch is called here directly instead of using the function defined in common.sh; thus, we also needed to include --export=ALL to make sure that our loaded modules are passed through to the job nodes.

4. I think there is an error on line 57 of make_jacobian_icbc.py as this is an incorrectly formatted f-string.

5. Also needed to make some changes to the end of create_simulation_dir to get the HEMCO_Config.rc file to read in the correct methane field.

## References:

* Estrada, L.A., D.J. Varon, M. Sulprizio, H. Nesser, Z. Chen, N. Balasus, S.E. Hancock, M. He, J.D. East, T.A. Mooring, A. Oort Alonso, J.D. Maasakkers, I. Aben, S. Baray, K.W. Bowman, J.R. Worden, F.J. Cardoso-Saldaña, E. Reidy, and D.J. Jacob, Integrated Methane Inversion (IMI) 2.0: an improved research and stakeholder tool for monitoring total methane emissions with high resolution worldwide using TROPOMI satellite observations, Geoscientific Model Development, 18, 3311–3330, [https://doi.org/10.5194/gmd-18-3311-2025](https://doi.org/10.5194/gmd-18-3311-2025), 2025.
* Varon, D. J., Jacob, D. J., Sulprizio, M., Estrada, L. A., Downs, W. B., Shen, L., Hancock, S. E., Nesser, H., Qu, Z., Penn, E., Chen, Z., Lu, X., Lorente, A., Tewari, A., and Randles, C. A.: Integrated Methane Inversion (IMI 1.0): a user-friendly, cloud-based facility for inferring high-resolution methane emissions from TROPOMI satellite observations, Geosci. Model Dev., 15, 5787–5805, [https://doi.org/10.5194/gmd-15-5787-2022](https://doi.org/10.5194/gmd-15-5787-2022), 2022.