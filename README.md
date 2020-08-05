# GEOS files in Singularity
These files are various definition files for using GEOSfvdycore and GEOSgcm within Singularity. Most are on the Singularity library.

## Which files are which?

Files ending in:


`b.def`   : Indicate the container installs base libraries

`fvy.def` : Indicate the container installs GEOSfvdycore

`gcm.def` : Indicate the container installs GEOSgcm

## How do I use these?

When using the containers for GEOSfvdycore and GEOSgcm, the install directories are located at `/GEOSfvdycore` and `/GEOSgcm` inside their containers respectively. Documentation for running GEOSgcm can be found at the [GEOS-5 wiki](https://geos5.org/wiki/index.php?title=GEOS_GCM_Quick_Start#Running_GEOS_GCM). Running GEOSfvdycore is a similar process.

You go to `/installdirectory/install/bin` for one of them, and then use their setup scripts to create an experiment directory. GEOSfvdycore has `fv3_setup` and GEOSgcm has `gcm_setup`. If you want to run this with slurm, you can create a slurm script and use something like:

```
singularity exec image.sif experimentdirectory/./fv3.j
```

## It takes time to convert to a sandbox with each run. Is there a way around this?

You should convert your `.sif` file to a sandbox and use that for each run, especially if you use a container multiple times. 

```
singularity build -s yoursandbox/ yourimage.sif
```

Now you can use that sandbox for runs instead of the image. This will save time in converting the image and having to clean it. You do not need the original `.sif` file for the sandbox.

## Do I have to make changes to the run script for these containers to work with slurm?

If you want to change the amount of tasks the run script specifies or use multiple nodes, then yes. A specified amount of tasks (`ntasks`) will already be mad/e once an experiment derictory is created, and you should ideally go by this. However, if you'd like to change these values, the variables `FV_NX` and `FV_NY` in the runscript will have to be changed to what number of nodes / number of cores you'd like. 
