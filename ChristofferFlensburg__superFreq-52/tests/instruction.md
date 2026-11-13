# Issue

**Title:** Feature/51 conda support

## Description

@ChristofferFlensburg sorry it took so long, but I was able to create an installable conda package (r-superfreq) using the recipe in this pull request.

 I wanted to include all the steps that I took to create the pull request. 

I created a conda recipe using the cran skeleton. This is why I asked for the tag.

`conda skeleton cran https://github.com/ChristofferFlensburg/superFreq`

That created the r-superfreq folder. 

I then changed the conda packages to the correct bioconductor packages.

I ran the following to build the package. It took around 15 minutes for me. The channels are important since that is where the packages are hosted. I added these in the README.md I can take it out if you want.

`cd r-superfreq`
`conda build -c bioconda -c conda-forge --debug .`

That created a file for me like this.

`/path/to/anaconda3/conda-bld/osx-64/r-superfreq-1.3.2-r35_0.tar.bz2`

To test it, I created a new conda environment and installed it from the local .tar.bz2. This takes about 6 minutes for me mostly because downloading the reference genomes takes awhile.

`conda create -n superfreq`
` conda activate superfreq`
`conda install -c bioconda -c conda-forge --use-local r-superfreq`

That worked for me. I am using a Mac, so I haven't tested the build process for Windows (bld.bat). Would you mind testing this to see if it works for you?

Once you have created the .tar.bz2, you can upload it to anaconda. [Click here for instructions](https://docs.conda.io/projects/conda-build/en/latest/user-guide/tutorials/build-r-pkgs.html#optional-uploading-packages-to-anaconda-org). I imagine you might want to put it under your own name and channel. I have seen that many people have been uploading their bioinformatics tools to the _bioconda_ channel.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `119bbe3d4c0a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.