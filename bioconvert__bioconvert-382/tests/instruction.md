# Issue

**Title:** Add 3D genome Hi-C format converters: HIC2COOL and COOL2HIC

## Description

Bioconvert lacked support for 3D genome data formats. This adds bidirectional conversion between the two dominant Hi-C contact map formats: Juicer `.hic` and Cooler `.cool`/`.mcool`.

## New converters

- **`HIC2COOL`** (`hic2cool.py`) — wraps the [`hic2cool`](https://github.com/4dn-dcic/hic2cool) CLI; `resolution=0` (default) extracts all resolutions into `.mcool`, a specific bp value produces a single-resolution `.cool`
- **`COOL2HIC`** (`cool2hic.py`) — wraps [`HiCLift`](https://github.com/XiaoTaoWang/HiCLift) with `--assembly-from` == `--assembly-to` (pure format conversion, no liftover); `assembly` parameter defaults to `hg38`

## Supporting changes

- **`core/extensions.py`** — registers `hic` (`.hic`) and `cool` (`.cool`, `.mcool`) so the auto-discovery registry picks them up automatically
- **`requirements.txt` / `pyproject.toml`** — adds `hic2cool` and `HiCLift` as dependencies
- **Tests** — parametrized on `available_methods` (skip when tools absent), guarded with `skipif` when test data files are missing, assert output file exists and is non-empty

## Usage

```python
from bioconvert.hic2cool import HIC2COOL
from bioconvert.cool2hic import COOL2HIC

# .hic → all-resolution .mcool
HIC2COOL("contacts.hic", "contacts.mcool")()

# .hic → single-resolution .cool
HIC2COOL("contacts.hic", "contacts.cool")(resolution=10000)

# .cool → .hic (hg38 assembly)
COOL2HIC("contacts.cool", "contacts.hic")(assembly="hg38")
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `307907547aca`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.