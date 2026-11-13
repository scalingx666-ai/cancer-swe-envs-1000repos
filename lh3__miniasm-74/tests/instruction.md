# Issue

**Title:** Explicitly add circularising links to unitig GFA

## Description

This is a small change to the unitig GFA output. Instead of just relying on the last character of the unitig name to indicate circularity (`l` for linear and `c` for circular), this change gives circular unitigs an explicit overlap-free link in the GFA file.

Before:
```
S       utg000030c      GGAACAAACTGCATTAATTC...TATCACCAGAAAAGACAGAT	LN:i:69013
a       utg000030c      0       0ab4d3ed-f533-4bfd-880c-fa1a0568443b:17-68951    +       3431
a       utg000030c      3431    1e81464e-9194-40f4-ba59-d29f9b1a7d65:33-68891    +       16745
a       utg000030c      20176   fb2dd196-c8bb-4770-b693-d02329c1dab2:1-67957     +       24
```

After:
```
S       utg000030c      GGAACAAACTGCATTAATTC...TATCACCAGAAAAGACAGAT	LN:i:69013
L       utg000030c      +       utg000030c      +       0M
L       utg000030c      -       utg000030c      -       0M
a       utg000030c      0       0ab4d3ed-f533-4bfd-880c-fa1a0568443b:17-68951    +       3431
a       utg000030c      3431    1e81464e-9194-40f4-ba59-d29f9b1a7d65:33-68891    +       16745
a       utg000030c      20176   fb2dd196-c8bb-4770-b693-d02329c1dab2:1-67957     +       24
```

This change is mainly to make miniasm assemblies for bacterial genomes (in which circular unitigs are common) display as circular when loaded in Bandage.

Thanks so much for this great tool (and all your others), and let me know if you have any questions!

Ryan

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cdcb49dc8aed`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.