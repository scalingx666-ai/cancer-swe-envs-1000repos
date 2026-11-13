# Issue

**Title:** download all supplementary file instead of only one

## Description

When using GEOparse to download suplamentry files from GEO accession that includes more than one  suplamentry file I got this erorr:

Traceback (most recent call last):
  File "C:/Users/User/PycharmProjects/test_geo/main.py", line 17, in <module>
    get_sup_data(out_dir, gse_num)
  File "C:/Users/User/PycharmProjects/test_geo/main.py", line 15, in get_sup_data
    print(gse.gsms[gsm].download_supplementary_files(directory=out_dir, download_sra=False))
  File "C:\Users\User\PycharmProjects\test_geo\venv\lib\site-packages\GEOparse\GEOTypes.py", line 493, in download_supplementary_files
    assert len(metavalue) == 1 and metavalue != ""
AssertionError


I found that the script is expecting one file only. I changed the code to allow download of all supplementary files.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `10abe10cbb2c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.