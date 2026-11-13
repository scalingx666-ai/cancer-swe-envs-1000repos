# Issue

**Title:** Declare total_size outside of try block so it can't be undeclared.

## Description

While using GEOparse I got the following error:

```
Traceback (most recent call last):
  File "/usr/local/lib/python3.6/dist-packages/GEOparse/utils.py", line 80, in download_from_url
    fn.download(silent=silent, force=force)
  File "/usr/local/lib/python3.6/dist-packages/GEOparse/downloader.py", line 82, in download
    _download()
  File "/usr/local/lib/python3.6/dist-packages/GEOparse/downloader.py", line 53, in _download
    self._download_ftp(silent=silent)
  File "/usr/local/lib/python3.6/dist-packages/GEOparse/downloader.py", line 187, in _download_ftp
    if total_size != 0:
UnboundLocalError: local variable 'total_size' referenced before assignment

During handling of the above exception, another exception occurred:

Traceback (most recent call last):
  File "/home/user/data_refinery_foreman/surveyor/external_source.py", line 171, in survey
    experiment, samples = self.discover_experiment_and_samples()
  File "/home/user/data_refinery_foreman/surveyor/geo.py", line 500, in discover_experiment_and_samples
    experiment, samples = self.create_experiment_and_samples_from_api(experiment_accession_code)
  File "/home/user/data_refinery_foreman/surveyor/geo.py", line 246, in create_experiment_and_samples_from_api
    gse = GEOparse.get_GEO(experiment_accession_code, destdir=self.get_temp_path(), silent=True)
  File "/usr/local/lib/python3.6/dist-packages/GEOparse/GEOparse.py", line 103, in get_GEO
    aspera=aspera,
  File "/usr/local/lib/python3.6/dist-packages/GEOparse/GEOparse.py", line 263, in get_GEO_file
    utils.download_from_url(url, filepath, silent=silent, aspera=aspera)
  File "/usr/local/lib/python3.6/dist-packages/GEOparse/utils.py", line 84, in download_from_url
    + "data might not be public yet."
OSError: Download failed due to 'local variable 'total_size' referenced before assignment'. ID could be incorrect or the data might not be public yet.
```

This PR should prevent a local variable being referenced before assignment.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `10abe10cbb2c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.