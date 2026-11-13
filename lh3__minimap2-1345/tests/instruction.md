# Issue

**Title:** Fix use-after-free in mappy

## Description

`cmappy.mm_map_aux()` takes in `b._b` which can end up reallocating `km` at the end of `mm_map_frag_core()`:

https://github.com/lh3/minimap2/blob/e2542e6425a40adaa710e07ae5e6188c91f8728c/python/mappy.pyx#L192-L208

https://github.com/lh3/minimap2/blob/e2542e6425a40adaa710e07ae5e6188c91f8728c/map.c#L374-L375

Since the address of `km` is cached before those calls it ends up pointing to freed memory.

This can result in a crash as seen in #1183, however it also happens to Just Work most of the time since the new allocation often lands at the same address as the old one. Preloading ASAN or a similar replacement allocator that doesn't have that behaviour results in a reliable crash:
```
AddressSanitizer:DEADLYSIGNAL
=================================================================
==6003==ERROR: AddressSanitizer: SEGV on unknown address 0x7cc7aa102810 (pc 0x7cca265cba44 bp 0x0000000002c9 sp 0x7ffca6624630 T0)
==6003==The signal is caused by a READ memory access.
    #0 0x7cca265cba44 in kmalloc minimap2/kalloc.c:141
    #1 0x7cca265c115e in write_cs_ds_or_MD minimap2/format.c:340
    #2 0x7cca265c26aa in write_cs_ds_or_MD minimap2/format.c:339
    #3 0x7cca265c26aa in mm_gen_cs_ds_or_MD minimap2/format.c:371
    #4 0x7cca265c270d in mm_gen_cs_or_MD minimap2/format.c:379
    #5 0x7cca265c2772 in mm_gen_MD minimap2/format.c:394
    #6 0x7cca265ee5b8 in __pyx_gb_5mappy_7Aligner_8generator python/mappy.c:7758
    #7 0x7cca265ddfa8 in __Pyx_Coroutine_SendEx python/mappy.c:19463
    #8 0x7cca265e199b in __Pyx_Generator_Next python/mappy.c:19729
```

Moving the caching until when it's needed fixes the crash.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e2542e6425a4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.