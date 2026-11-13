# Issue

**Title:** Giraffe edge case tweaks

## Description

## Changelog Entry
To be copied to the [draft changelog](https://github.com/vgteam/vg/wiki/Draft-Changelog) by merger:

 * Minor Giraffe long-read mode (`--align-from-chains`/`-b hifi`/`-b r10`) improvements:
     * logged-gap/rec-penalty rescoring occurs before filtering by score
     * multiplicity calculation takes into account all alignment attempts

## Description

I moved rescoring so that it happens earlier. Sometimes the initial affine-gap scored alignment will look terrible (with a different affine-gap score being better), or will be score 0. In either case that alignment will be ignored _even if rescoring would make it look good_. By simply putting rescoring before the step where we filter by score, this problem goes away. 

The multiplicity thing is more complicated:

- When calculating final alignment multiplicity, we care about how many chains had similar sparse DP score to the chain which produced this alignment. Chains of the same score which never got pushed through base-level DP may have been better than the ones which were, and we wouldn't know.
- However, we _don't_ want to penalize an alignment for chains of the same score which _were_ pushed through base-level DP. In that case we know exactly what score it got. The later MAPQ calculation could handle it. Therefore, we do (count of equal/better chain scores) minus (count of alignments made).
- However however, we were only counting alignments which were _saved_. Significantly worse base-level alignment scores would lead to an alignment not being recorded anywhere. 

For a concrete example, say we have two chains of identical score. We take both through to base-level alignment. One turns out gloriously, the other a disaster. The disaster is so bad that we [decide to avoid observing it](https://github.com/vgteam/vg/blob/a0907af0ad0e749cbe77dd7b3c6f727769d5c7df/src/minimizer_mapper_from_chains.cpp#L2192-L2199). Later on, when calculating MAPQ, we see that there was one chain of equal/better score but zero other alignments, so we think that maybe this other chain would've turned out well too. Thus we penalize our alignment on multiplicity despite that being unfair.

My solution to this is to track how many base-level alignments we _try_ to make, and use that to calculate final multiplicity. Thus in my example we'd note that there was one chain of equal/better score, and one other alignment attempt, so we can be confident that if we need to consider that other alignment in MAPQ it would be saved and handled later.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5bb0cd75f6bd`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.