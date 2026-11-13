# Issue

**Title:** Fix chromToUcsc bug with online chromAlias files

## Description

The script crashes when using gzipped online chromAlias files on Python 2,

```
$ python2 chromToUcsc -a https://hgdownload.soe.ucsc.edu/goldenPath/hg19/database/chromAlias.txt.gz
Traceback (most recent call last):
  File "chromToUcsc", line 279, in <module>
    main()
  File "chromToUcsc", line 277, in main
    chromToUcsc(aliasFname, fieldIdx, skipUnknown, ifh, ofh)
  File "chromToUcsc", line 145, in chromToUcsc
    toUcsc = parseAlias(aliasFname)
  File "chromToUcsc", line 114, in parseAlias
    data = gzip.GzipFile(fileobj=ifh).read().decode()
  File "/usr/local/lib/python2.7/gzip.py", line 260, in read
    self._read(readsize)
  File "/usr/local/lib/python2.7/gzip.py", line 294, in _read
    pos = self.fileobj.tell()   # Save current position
AttributeError: addinfourl instance has no attribute 'tell'
```

and uncompressed online chromAlias files on Python 3.

```
$ python3 chromToUcsc -a https://hgdownload.soe.ucsc.edu/goldenPath/hg38/bigZips/latest/hg38.chromAlias.txt
Traceback (most recent call last):
  File "chromToUcsc", line 279, in <module>
    main()
  File "chromToUcsc", line 277, in main
    chromToUcsc(aliasFname, fieldIdx, skipUnknown, ifh, ofh)
  File "chromToUcsc", line 145, in chromToUcsc
    toUcsc = parseAlias(aliasFname)
  File "chromToUcsc", line 123, in parseAlias
    if line.startswith("#") and firstLine:
TypeError: startswith first arg must be bytes or a tuple of bytes, not str
```

Utilize `downloadUrl` introduced in commit 2567ad8ce3a to fix the problem.

CC: @maximilianh

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4ef80e66feef`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.