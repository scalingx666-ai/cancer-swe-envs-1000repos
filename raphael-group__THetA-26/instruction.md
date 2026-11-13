# Issue

**Title:** ⚡ Vectorize array operations in L2, L3

## Description

Dear ThetA2 team,

Thank you for making this tool available! I am a bioinformatics engineer working with the Gabriella Miller Kids First Pediatric Research Program at the Children's Hospital of Philadelphia, and we use THetA2 in one of our workflows. 

We recently noticed that the program was taking a while to finish with some large inputs, and after looking into it I believe that a considerable speedup can be achieved by vectorizing the array operations in the `L2` and `L3` functions of the `CalcAllC` module. I have implemented these changes in this pull request, and I would be grateful if you would be willing to discuss them. 

Included in the PR are Python `pickle` objects containing inputs and outputs for the modified functions. `L2args.pkl` and `L3args.pkl` contain inputs for the functions on both the master branch and this one. The objects can be unpacked by e.g. 
```
with open('L2args.pkl', 'rb') as pkl:
    mu, C, m, r = pickle.load(pkl)
```
 and likewise for `L3`, except that there is an additional `n` argument.

The other included `pickle` files contain the outputs of both functions on the master branch and this one. To unpack, for example, the outputs of `L2` from this branch, 
```
with open('L2outputs_branch.pkl', 'rb') as pkl:
    total_sum, vals = pickle.load(pkl)
```

I am including these files to assist in comparing the outputs of the versions of the functions, which are the same to ~15 decimal places. My intention is that they would be removed prior to merge. 

Python 2.7.15 was used for this work, as well as numpy 1.15.4.

One potential issue concerns the arguments `m` of `L2` and `m` and `n` of `L3`. Although I did not modify the call signature of the functions, these arguments are not used in my proposed versions. I found them to refer to the dimensions of the array `C`. I added code to catch any instance in which their values differed from the dimensions of `C`, and I was able to run `RunTHetA.py` on our large inputs without these exceptions being raised. For this reason I believe that my understanding of the origin of the values of `m` and (in `L3`) `n` is correct, but I would be grateful if you were able to tell me that this relationship between the arguments cannot be assumed. 

I appreciate your consideration of this request, and thank you again for making THetA2 available. 

Best,
Nathan Johnson

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b11019e095bd`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.