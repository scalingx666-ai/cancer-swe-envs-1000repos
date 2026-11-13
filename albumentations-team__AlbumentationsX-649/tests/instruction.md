# Issue

**Title:** perf(pixel): reverse RGB channels in one batch operation

## Description

Reverse RGB channels for an NHWC batch in one OpenCV call by combining the batch and height axes. The `float16` path reuses the bit-preserving `uint16` view from the single-image implementation.

All 102 before/after cases matched byte for byte. Regression tests cover `uint8`, `float16`, and `float32` through both `Compose(images=...)` and the functional API. General NHWC permutations use the batch handler, including empty batches. RGB volumes accept a reversal order supplied as a sequence such as `range(2, -1, -1)`. Tests check read-only inputs, reversed column strides, arbitrary floating-point bit patterns including NaNs and signed zeros, and a separate contiguous output.

### CPU benchmarks

Apple M4 Max, macOS arm64, one CPU thread, NumKong NEON enabled. Python 3.11.18, NumPy 2.4.6, Albucore 0.3.5, OpenCV 5.0.0.93, NumKong 7.8.7, and PyTorch 2.15.0. Baseline `dd12884b737eaef6815e019bf58aa845b346b6b1`, candidate `ca3470ddd7f9edfe48db63851dbfee7dded73297`. Both paths run in the same process on seed-137 synthetic arrays. Timings are medians of three paired batches of calls after warmup and include output allocation.

| `Compose(images=...)`, 256×256×3 | `uint8` | `float16` | `float32` |
| --- | ---: | ---: | ---: |
| Batch 4 | 217.0 → 25.0 (8.69×) | 228.3 → 40.3 (5.66×) | 255.1 → 67.0 (3.81×) |
| Batch 8 | 447.6 → 35.7 (12.54×) | 448.3 → 66.2 (6.77×) | 501.7 → 119.8 (4.19×) |
| Batch 16 | 854.4 → 72.8 (11.73×) | 916.2 → 122.1 (7.50×) | 995.7 → 220.5 (4.51×) |

All times are in µs per batch. The per-image comparison calls the optimized single-image `Compose(image=...)` once per image and stacks the results.

<details>
<summary>Full timing matrix</summary>

| Layout | Shape N×H×W×C | dtype | Functional before → after, µs | Compose before → after, µs | Per-image Compose, µs |
| --- | --- | --- | ---: | ---: | ---: |
| RGB | 4×256×256×3 | `uint8` | 205.2 → 11.4 (17.96×) | 217.0 → 25.0 (8.69×) | 75.5 |
| RGB | 4×256×256×3 | `float16` | 214.8 → 28.2 (7.63×) | 228.3 → 40.3 (5.66×) | 103.2 |
| RGB | 4×256×256×3 | `float32` | 238.9 → 52.8 (4.53×) | 255.1 → 67.0 (3.81×) | 145.4 |
| RGB | 4×512×512×3 | `uint8` | 833.9 → 59.1 (14.11×) | 839.8 → 65.6 (12.81×) | — |
| RGB | 4×512×512×3 | `float16` | 875.1 → 109.2 (8.01×) | 927.5 → 141.5 (6.55×) | — |
| RGB | 4×512×512×3 | `float32` | 959.5 → 212.6 (4.51×) | 965.5 → 225.4 (4.28×) | — |
| RGB | 4×1024×1024×3 | `uint8` | 3368.1 → 211.2 (15.95×) | 3338.8 → 223.9 (14.91×) | — |
| RGB | 4×1024×1024×3 | `float16` | 3501.2 → 424.6 (8.25×) | 3502.9 → 463.7 (7.55×) | — |
| RGB | 4×1024×1024×3 | `float32` | 4001.1 → 892.6 (4.48×) | 3963.3 → 901.8 (4.39×) | — |
| RGB | 8×256×256×3 | `uint8` | 421.4 → 27.5 (15.33×) | 447.6 → 35.7 (12.54×) | 157.8 |
| RGB | 8×256×256×3 | `float16` | 452.5 → 53.9 (8.39×) | 448.3 → 66.2 (6.77×) | 213.4 |
| RGB | 8×256×256×3 | `float32` | 479.6 → 102.8 (4.67×) | 501.7 → 119.8 (4.19×) | 297.2 |
| RGB | 8×512×512×3 | `uint8` | 1727.5 → 88.3 (19.56×) | 1740.7 → 127.9 (13.61×) | — |
| RGB | 8×512×512×3 | `float16` | 1816.6 → 228.3 (7.96×) | 1857.5 → 231.1 (8.04×) | — |
| RGB | 8×512×512×3 | `float32` | 1985.1 → 449.6 (4.42×) | 1985.3 → 451.6 (4.40×) | — |
| RGB | 8×1024×1024×3 | `uint8` | 6720.5 → 422.0 (15.93×) | 6702.0 → 442.9 (15.13×) | — |
| RGB | 8×1024×1024×3 | `float16` | 7188.3 → 865.0 (8.31×) | 7214.7 → 883.9 (8.16×) | — |
| RGB | 8×1024×1024×3 | `float32` | 7884.5 → 1854.1 (4.25×) | 8077.5 → 1855.9 (4.35×) | — |
| RGB | 16×256×256×3 | `uint8` | 852.6 → 60.2 (14.15×) | 854.4 → 72.8 (11.73×) | 308.9 |
| RGB | 16×256×256×3 | `float16` | 885.9 → 108.7 (8.15×) | 916.2 → 122.1 (7.50×) | 421.8 |
| RGB | 16×256×256×3 | `float32` | 962.3 → 215.1 (4.47×) | 995.7 → 220.5 (4.51×) | 592.3 |
| RGB | 16×512×512×3 | `uint8` | 3438.9 → 220.5 (15.60×) | 3385.8 → 230.3 (14.70×) | — |
| RGB | 16×512×512×3 | `float16` | 3492.5 → 422.8 (8.26×) | 3608.5 → 458.7 (7.87×) | — |
| RGB | 16×512×512×3 | `float32` | 4004.5 → 893.1 (4.48×) | 4034.0 → 915.3 (4.41×) | — |
| RGB | 16×1024×1024×3 | `uint8` | 13562.3 → 889.3 (15.25×) | 13641.0 → 868.7 (15.70×) | — |
| RGB | 16×1024×1024×3 | `float16` | 14359.3 → 1736.1 (8.27×) | 14436.1 → 1855.3 (7.78×) | — |
| RGB | 16×1024×1024×3 | `float32` | 16050.9 → 3670.8 (4.37×) | 15990.2 → 3662.3 (4.37×) | — |
| strided RGB | 8×256×256×3 | `uint8` | 1762.2 → 1365.9 (1.29×) | 1754.8 → 1404.6 (1.25×) | — |
| single RGB | 1×256×256×3 | `uint8` | 4.4 → 4.5 (0.99×) | 16.8 → 17.1 (0.98×) | — |
| strided RGB | 8×256×256×3 | `float16` | 2108.3 → 1767.3 (1.19×) | 2210.3 → 1872.7 (1.18×) | — |
| single RGB | 1×256×256×3 | `float16` | 7.9 → 7.9 (1.00×) | 20.4 → 20.8 (0.98×) | — |
| strided RGB | 8×256×256×3 | `float32` | 2089.0 → 1699.0 (1.23×) | 2094.9 → 1800.9 (1.16×) | — |
| single RGB | 1×256×256×3 | `float32` | 14.3 → 14.0 (1.02×) | 26.4 → 26.9 (0.98×) | — |
| generic 1-channel | 8×256×256×1 | `uint8` | 14.3 → 14.1 (1.02×) | 12.0 → 11.9 (1.01×) | — |
| generic 1-channel | 8×256×256×1 | `float16` | 27.0 → 28.1 (0.96×) | 12.1 → 12.1 (1.00×) | — |
| generic 1-channel | 8×256×256×1 | `float32` | 52.5 → 53.2 (0.99×) | 12.1 → 12.0 (1.01×) | — |
| generic 5-channel | 8×256×256×5 | `uint8` | 725.3 → 718.7 (1.01×) | 731.4 → 731.5 (1.00×) | — |
| generic 5-channel | 8×256×256×5 | `float16` | 731.7 → 749.1 (0.98×) | 760.4 → 749.5 (1.01×) | — |
| generic 5-channel | 8×256×256×5 | `float32` | 789.8 → 810.1 (0.97×) | 839.2 → 835.0 (1.00×) | — |
| generic 1-channel | 8×512×512×1 | `uint8` | 53.3 → 54.2 (0.98×) | 13.3 → 11.9 (1.12×) | — |
| generic 1-channel | 8×512×512×1 | `float16` | 105.3 → 104.7 (1.01×) | 11.7 → 12.2 (0.96×) | — |
| generic 1-channel | 8×512×512×1 | `float32` | 209.6 → 206.2 (1.02×) | 11.8 → 11.8 (1.00×) | — |
| generic 5-channel | 8×512×512×5 | `uint8` | 2781.4 → 2782.1 (1.00×) | 2799.3 → 2831.3 (0.99×) | — |
| generic 5-channel | 8×512×512×5 | `float16` | 2931.6 → 2931.7 (1.00×) | 2991.7 → 3056.3 (0.98×) | — |
| generic 5-channel | 8×512×512×5 | `float32` | 3421.1 → 3297.6 (1.04×) | 3321.3 → 3308.8 (1.00×) | — |
| generic 1-channel | 8×1024×1024×1 | `uint8` | 230.7 → 224.9 (1.03×) | 12.2 → 12.1 (1.01×) | — |
| generic 1-channel | 8×1024×1024×1 | `float16` | 440.7 → 419.0 (1.05×) | 12.1 → 12.0 (1.01×) | — |
| generic 1-channel | 8×1024×1024×1 | `float32` | 907.0 → 903.9 (1.00×) | 11.7 → 11.8 (1.00×) | — |
| generic 5-channel | 8×1024×1024×5 | `uint8` | 11267.8 → 11312.4 (1.00×) | 11356.0 → 11429.8 (0.99×) | — |
| generic 5-channel | 8×1024×1024×5 | `float16` | 11896.5 → 11835.1 (1.00×) | 11925.3 → 12075.2 (0.99×) | — |
| generic 5-channel | 8×1024×1024×5 | `float32` | 14113.0 → 14073.3 (1.00×) | 14510.4 → 14512.1 (1.00×) | — |

The one- and five-channel controls use eight images at each size. The public one-channel control uses `ChannelShuffle` and the five-channel control uses a fixed reversal through `ChannelSwap`. Across these controls no case slowed by more than 5%.

</details>

The local suite passed on the original PR commit. The updated commit passed 298 focused tests and the changed-file pre-commit checks.

## Summary by Sourcery

Accelerate batched RGB channel reversal without changing its output semantics.

Enhancements:
- Optimize RGB channel reversal for batched NHWC images by processing the batch in a single operation while preserving supported dtypes and bit patterns.

Tests:
- Expand channel-reversal regression coverage across functional and Compose APIs, supported dtypes, read-only and strided inputs, arbitrary floating-point bit patterns, and contiguous outputs.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

* **Improvements**
  * RGB channel swapping now supports batches of `uint8`, `float16`, and `float32` images, including non-contiguous inputs, while preserving exact pixel values and returning independent, contiguous results.
  * RGB volume channel swapping provides the same behavior for supported four-dimensional inputs. Other volume inputs remain unchanged, and channel permutations continue to work across different channel counts.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `dd12884b737e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.