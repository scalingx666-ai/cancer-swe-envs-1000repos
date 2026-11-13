# Issue

**Title:** fix(dataset): set same device to self.coords.

## Description

Hello, thanks for your great work. When I tried to run `python train.py --config ./config/jaw_50.yaml`, I received this error message: 

```bash
python train.py --config ./config/jaw_50.yaml
[Start] exp: jaw_50, net: Basic network
[EVAL] epoch: 0/3000, proj_mse: 0.0362, proj_psnr: 8.15, psnr_3d: 6.47, ssim_3d: 0.154                                                                                               
  0%|                                                                                                                                                     | 0/150000 [00:12<?, ?it/s]Traceback (most recent call last):
  File "/mnt/d/Git/github/naf_cbct/train.py", line 109, in <module>
    trainer.start()
  File "/mnt/d/Git/github/naf_cbct/src/trainer.py", line 104, in start
    for data in self.train_dloader:
  File "/home/lebenito/miniconda3/envs/naf/lib/python3.9/site-packages/torch/utils/data/dataloader.py", line 633, in __next__
    data = self._next_data()
  File "/home/lebenito/miniconda3/envs/naf/lib/python3.9/site-packages/torch/utils/data/dataloader.py", line 677, in _next_data
    data = self._dataset_fetcher.fetch(index)  # may raise StopIteration
  File "/home/lebenito/miniconda3/envs/naf/lib/python3.9/site-packages/torch/utils/data/_utils/fetch.py", line 51, in fetch
    data = [self.dataset[idx] for idx in possibly_batched_index]
  File "/home/lebenito/miniconda3/envs/naf/lib/python3.9/site-packages/torch/utils/data/_utils/fetch.py", line 51, in <listcomp>
    data = [self.dataset[idx] for idx in possibly_batched_index]
  File "/mnt/d/Git/github/naf_cbct/src/dataset/tigre.py", line 82, in __getitem__
    coords_valid = self.coords[projs_valid]
RuntimeError: indices should be either on cpu or on the same device as the indexed tensor (cpu)
```

It seems the problem is `self.coords` doesn't assign a device. So, I fixed the code by adding a device param.
But I’m not sure if this is a problem that everyone will encounter, or if it’s caused by my conda environment.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0ce036d4ab6b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.