# Issue

**Title:** Modified sites with compatibility for GRCH38 (hg38)

## Description

Sites used to identify relatedness between individuals were picked based on a metric that calculates the combined cohort relatedness difference, providing a site score for the cohort based off specific sites. Sites were first filtered using an SVM trained on a data set with labeled sites with multiple features. LD scores and allele frequencies were then used to further filter the sites. Sites were then mapped to GRCH37 and GRCH38 for compatible use between the two builds. Functionality of site specific designation was added to peddy. 

The relatedness sites score improved by 748.44. (Original relatedness sites score = 2542.605, new relatedness sites score = 1794.16382684) Number of sites in the new file is 23770 compared to the ordinal 23556.

To run peddy the user will need to provide the location of the sites file using the --sites flag. The bin.gz file should be located in the same file.


python -m peddy -p 4 --plot **--sites peddy/GRCH37.sites** --prefix ceph-1463 data/ceph1463.vcf.gz data/ceph1463.ped

## Original Sites File
![original1kg 1](https://user-images.githubusercontent.com/35238534/39549602-aec419c0-4e1b-11e8-98ff-8f6de2e25362.png)
## New Sites File
![aafabove 01 1](https://user-images.githubusercontent.com/35238534/39549600-aeae640e-4e1b-11e8-911a-23d126d4acf1.png)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a19372d74eab`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.