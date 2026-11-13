# Issue

**Title:** [batch] create and bill n4 external storage disks as Hyperdisk

## Description

## Change Description

A pool job whose storage request doesn't fit on the worker's data disk gets its own disk, created and attached by the worker. That disk was always pd-ssd, which n4 instances cannot attach, and it was always billed as pd-ssd. Job-private instances never create one, so n4 job-private support didn't hit this; n4 pool instances will.

The worker now creates the disk with `gcp_external_storage_disk_type` for its machine family (hyperdisk-balanced on n4, pinned to the free IOPS and throughput baseline; pd-ssd otherwise), and the instance config bills it with the same type.

### Validation
Tested on a dev deploy where I temporarily changed the pool VM type to n4 (`GCP_MACHINE_FAMILY = 'n4'`). I was able to attach an external disk to a standard n4 pool worker, and was billed appropriately for it.

Test input:
```python
b = hb.Batch(backend=hb.ServiceBackend(billing_project='grohlice-trial'))
j = b.new_job()
j.image('ubuntu:24.04')
j.cpu(0.25)
j.storage('400Gi')
j.command('df -h /io; fallocate -l 390GiB /io/foo')
b.run()
```
Output:
```
+ df -h /io
Filesystem      Size  Used Avail Use% Mounted on
/dev/nvme0n3    393G   28K  393G   1% /io
+ fallocate -l 390GiB /io/foo
+ ls -l /io
total 408944704
-rw-r--r-- 1 root root 418759311360 Nov  9 22:26 foo
drwx------ 2 root root        16384 Nov  9 22:26 lost+found
+ sleep 300
```

## Security Assessment

- This change potentially impacts the Hail Batch instance as deployed by Broad Institute in GCP

### Impact Rating
- This change has a low security impact


### Impact Description
No impact right now; relates to an upcoming change to the worker pool to include n4 instances. Minimal impact after that pool upgrade too, since this is ultimately a billing consistency fix.

### Appsec Review

- [x] Required: The impact has been assessed and approved by appsec

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c396a39dac4f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.