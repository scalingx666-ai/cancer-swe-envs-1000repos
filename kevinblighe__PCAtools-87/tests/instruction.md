# Issue

**Title:** Replace ggalt with ggforce

## Description

As ggalt is still off CRAN, ggforce seems to provide a (mostly) drop-in alternative...

Adapting the `biplot` example:

```r
options(scipen=10)
options(digits=6)
col <- 20
row <- 20000
mat1 <- matrix(
  rexp(col*row, rate = 0.1),
  ncol = col)
rownames(mat1) <- paste0('gene', 1:nrow(mat1))
colnames(mat1) <- paste0('sample', 1:ncol(mat1))
mat2 <- matrix(
rexp(col*row, rate = 0.1),
  ncol = col)
rownames(mat2) <- paste0('gene', 1:nrow(mat2))
colnames(mat2) <- paste0('sample', (ncol(mat1)+1):(ncol(mat1)+ncol(mat2)))
mat <- cbind(mat1, mat2)
metadata <- data.frame(row.names = colnames(mat))
metadata$Group <- rep(NA, ncol(mat))
metadata$Group[seq(1,40,2)] <- 'A'
metadata$Group[seq(2,40,2)] <- 'B'
metadata$CRP <- sample.int(100, size=ncol(mat), replace=TRUE)
metadata$ESR <- sample.int(100, size=ncol(mat), replace=TRUE)
p <- pca(mat, metadata = metadata, removeVar = 0.1)

biplot(p, colby = 'Group', colkey = c(A='forestgreen', B='gold'),
  shape = 'Group', shapekey = c(A=10, B=21), legendPosition = 'bottom',
  encircle=TRUE)
```

<img width="2096" height="2098" alt="tmp1" src="https://github.com/user-attachments/assets/c547756e-6668-45fc-92f9-1f8d2ea2da8e" />

```r
biplot(p, colby = 'Group', colkey = c(A='forestgreen', B='gold'),
  shape = 'Group', shapekey = c(A=10, B=21), legendPosition = 'bottom',
  encircle=TRUE, encircleFill=FALSE)
```

<img width="2096" height="2098" alt="tmp2" src="https://github.com/user-attachments/assets/f2412e80-cbf8-4d91-aafe-f909504a70f8" />

```r
biplot(p, colby = 'Group', colkey = c(A='forestgreen', B='gold'),
  shape = 'Group', shapekey = c(A=10, B=21), legendPosition = 'bottom',
  encircle=TRUE, encircleFill=TRUE, encircleFillKey=c(A="red", B="blue"))
```

<img width="2096" height="2098" alt="tmp3" src="https://github.com/user-attachments/assets/1c6a6349-9d87-479e-aee7-247b415367bb" />

```r
biplot(p, colby = 'Group', colkey = c(A='forestgreen', B='gold'),
  shape = 'Group', shapekey = c(A=10, B=21), legendPosition = 'bottom',
  encircle=TRUE, encircleFill=TRUE, encircleFillKey=c(A="red", B="blue"), encircleAlpha=1)
```

<img width="2096" height="2098" alt="tmp4" src="https://github.com/user-attachments/assets/e803252a-a92b-4d26-b2f6-c7f94a5b5247" />

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `67f1f10f6efa`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.