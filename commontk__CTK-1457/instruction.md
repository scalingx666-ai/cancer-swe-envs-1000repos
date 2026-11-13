# Issue

**Title:** PERF: Speed up retrieving DICOM tag values for many files

## Description

Add API for faster access of DICOM tags. It allows approximately 10x faster examination of large DICOM studies.

Retrieving tag values with `ctkDICOMDatabase::fileValue()` requires two database queries per call: one to find the SOP instance UID for the file name, and one to get the value from the tag cache. Applications typically retrieve several tags for every file of a series. For example, 3D Slicer's DICOM plugins make about 260,000 `fileValue()` calls to examine one patient with a 5628-file 4D cardiac CT series, so examination took tens of seconds.

This PR adds `QStringList fileValues(const QStringList& fileNames, const QString& tag)`:

- It returns the value of a tag for many files, in the same order as the input, using batched SQL queries (500 items per query) for both the file-name lookup and the tag-cache lookup.
- The result is identical to calling `fileValue()` for each file. Values that are not in the tag cache, and instances referenced by URL, are still retrieved through `fileValue()`, so reading from the file and caching work as before.
- It returns a `QStringList` rather than a map so that it can be used from Python via PythonQt. The existing `instanceValues()` returns a `QMap<QString, QString>`, which PythonQt cannot convert.
- It does not keep any state between calls (the SOP instance UIDs of the files are looked up in each call), so it is safe to use when the database is modified by another process or another database connection. Applications can cache the retrieved values for the duration of an operation (3D Slicer does this while examining or loading data).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a5c2e4d1cdac`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.