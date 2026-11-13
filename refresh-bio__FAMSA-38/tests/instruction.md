# Issue

**Title:** Fix error in "STATIC_LINK=true" section due to extra "-".

## Description

```console
$ make STATIC_LINK=true
*** Detecting g++ version 7 ***
*** x86-64 with AVX2 extensions***
make -C libs/libdeflate
make[1]: Entering directory '/nfs4/core/home/davised/opt/code/FAMSA/libs/libdeflate'
make[1]: Leaving directory '/nfs4/core/home/davised/opt/code/FAMSA/libs/libdeflate'
g++ -Wall -Wno-char-subscripts -Wno-attributes -O3 -msse4 -DNO_PROFILE_PAR -DOLD_ATOMIC_FLAG -DSIMD=2 -DGIT_COMMIT=26e61df  -static -Wl,--whole-archive -lpthread -Wl,--no-whole-archive -std=c++14 -I libs -c src/famsa.cpp -o src/famsa.o
g++ -Wall -Wno-char-subscripts -Wno-attributes -O3 -msse4 -DNO_PROFILE_PAR -DOLD_ATOMIC_FLAG -DSIMD=2 -DGIT_COMMIT=26e61df  -static -Wl,--whole-archive -lpthread -Wl,--no-whole-archive -std=c++14 -I libs -c src/msa.cpp -o src/msa.o
src/msa.cpp: In member function ‘void CFAMSA::sortAndExtendSequences(std::vector<CSequence>&)’:
src/msa.cpp:255:20: warning: comparison between signed and unsigned integer expressions [-Wsign-compare]
  for (int i = 0; i < seq_ptrs.size(); ++i) {
                  ~~^~~~~~~~~~~~~~~~~
g++ -Wall -Wno-char-subscripts -Wno-attributes -O3 -msse4 -DNO_PROFILE_PAR -DOLD_ATOMIC_FLAG -DSIMD=2 -DGIT_COMMIT=26e61df  -static -Wl,--whole-archive -lpthread -Wl,--no-whole-archive -std=c++14 -I libs -c src/msa_refinement.cpp-o src/msa_refinement.o
g++ -Wall -Wno-char-subscripts -Wno-attributes -O3 -msse4 -DNO_PROFILE_PAR -DOLD_ATOMIC_FLAG -DSIMD=2 -DGIT_COMMIT=26e61df  -static -Wl,--whole-archive -lpthread -Wl,--no-whole-archive -std=c++14 -I libs -c src/tree/AbstractTreeGenerator.cpp -o src/tree/AbstractTreeGenerator.o
g++ -Wall -Wno-char-subscripts -Wno-attributes -O3 -msse4 -DNO_PROFILE_PAR -DOLD_ATOMIC_FLAG -DSIMD=2 -DGIT_COMMIT=26e61df  -static -Wl,--whole-archive -lpthread -Wl,--no-whole-archive -std=c++14 -I libs -c src/tree/Clustering.cpp -o src/tree/Clustering.o
g++ -Wall -Wno-char-subscripts -Wno-attributes -O3 -msse4 -DNO_PROFILE_PAR -DOLD_ATOMIC_FLAG -DSIMD=2 -DGIT_COMMIT=26e61df  -static -Wl,--whole-archive -lpthread -Wl,--no-whole-archive -std=c++14 -I libs -c src/tree/DistanceCalculator.cpp -o src/tree/DistanceCalculator.o
g++ -Wall -Wno-char-subscripts -Wno-attributes -O3 -msse4 -DNO_PROFILE_PAR -DOLD_ATOMIC_FLAG -DSIMD=2 -DGIT_COMMIT=26e61df  -static -Wl,--whole-archive -lpthread -Wl,--no-whole-archive -std=c++14 -I libs -c src/tree/FastTree.cpp -o src/tree/FastTree.o
g++ -Wall -Wno-char-subscripts -Wno-attributes -O3 -msse4 -DNO_PROFILE_PAR -DOLD_ATOMIC_FLAG -DSIMD=2 -DGIT_COMMIT=26e61df  -static -Wl,--whole-archive -lpthread -Wl,--no-whole-archive -std=c++14 -I libs -c src/tree/GuideTree.cpp-o src/tree/GuideTree.o
g++ -Wall -Wno-char-subscripts -Wno-attributes -O3 -msse4 -DNO_PROFILE_PAR -DOLD_ATOMIC_FLAG -DSIMD=2 -DGIT_COMMIT=26e61df  -static -Wl,--whole-archive -lpthread -Wl,--no-whole-archive -std=c++14 -I libs -c src/tree/MSTPrim.cpp -o src/tree/MSTPrim.o
g++ -Wall -Wno-char-subscripts -Wno-attributes -O3 -msse4 -DNO_PROFILE_PAR -DOLD_ATOMIC_FLAG -DSIMD=2 -DGIT_COMMIT=26e61df  -static -Wl,--whole-archive -lpthread -Wl,--no-whole-archive -std=c++14 -I libs -c src/tree/NeighborJoining.cpp -o src/tree/NeighborJoining.o
g++ -Wall -Wno-char-subscripts -Wno-attributes -O3 -msse4 -DNO_PROFILE_PAR -DOLD_ATOMIC_FLAG -DSIMD=2 -DGIT_COMMIT=26e61df  -static -Wl,--whole-archive -lpthread -Wl,--no-whole-archive -std=c++14 -I libs -c src/tree/NewickParser.cpp -o src/tree/NewickParser.o
g++ -Wall -Wno-char-subscripts -Wno-attributes -O3 -msse4 -DNO_PROFILE_PAR -DOLD_ATOMIC_FLAG -DSIMD=2 -DGIT_COMMIT=26e61df  -static -Wl,--whole-archive -lpthread -Wl,--no-whole-archive -std=c++14 -I libs -c src/tree/SingleLinkage.cpp -o src/tree/SingleLinkage.o
g++ -Wall -Wno-char-subscripts -Wno-attributes -O3 -msse4 -DNO_PROFILE_PAR -DOLD_ATOMIC_FLAG -DSIMD=2 -DGIT_COMMIT=26e61df  -static -Wl,--whole-archive -lpthread -Wl,--no-whole-archive -std=c++14 -I libs -c src/tree/UPGMA.cpp -o src/tree/UPGMA.o
g++ -Wall -Wno-char-subscripts -Wno-attributes -O3 -msse4 -DNO_PROFILE_PAR -DOLD_ATOMIC_FLAG -DSIMD=2 -DGIT_COMMIT=26e61df  -static -Wl,--whole-archive -lpthread -Wl,--no-whole-archive -std=c++14 -I libs -c src/utils/timer.cpp -osrc/utils/timer.o
g++ -Wall -Wno-char-subscripts -Wno-attributes -O3 -msse4 -DNO_PROFILE_PAR -DOLD_ATOMIC_FLAG -DSIMD=2 -DGIT_COMMIT=26e61df  -static -Wl,--whole-archive -lpthread -Wl,--no-whole-archive -std=c++14 -I libs -c src/utils/log.cpp -o src/utils/log.o
g++ -Wall -Wno-char-subscripts -Wno-attributes -O3 -msse4 -DNO_PROFILE_PAR -DOLD_ATOMIC_FLAG -DSIMD=2 -DGIT_COMMIT=26e61df  -static -Wl,--whole-archive -lpthread -Wl,--no-whole-archive -std=c++14 -I libs -c src/core/io_service.cpp -o src/core/io_service.o
g++ -Wall -Wno-char-subscripts -Wno-attributes -O3 -msse4 -DNO_PROFILE_PAR -DOLD_ATOMIC_FLAG -DSIMD=2 -DGIT_COMMIT=26e61df  -static -Wl,--whole-archive -lpthread -Wl,--no-whole-archive -std=c++14 -I libs -c src/core/params.cpp -osrc/core/params.o
g++ -Wall -Wno-char-subscripts -Wno-attributes -O3 -msse4 -DNO_PROFILE_PAR -DOLD_ATOMIC_FLAG -DSIMD=2 -DGIT_COMMIT=26e61df  -static -Wl,--whole-archive -lpthread -Wl,--no-whole-archive -std=c++14 -I libs -c src/core/profile.cpp -o src/core/profile.o
g++ -Wall -Wno-char-subscripts -Wno-attributes -O3 -msse4 -DNO_PROFILE_PAR -DOLD_ATOMIC_FLAG -DSIMD=2 -DGIT_COMMIT=26e61df  -static -Wl,--whole-archive -lpthread -Wl,--no-whole-archive -std=c++14 -I libs -c src/core/profile_par.cpp -o src/core/profile_par.o
g++ -Wall -Wno-char-subscripts -Wno-attributes -O3 -msse4 -DNO_PROFILE_PAR -DOLD_ATOMIC_FLAG -DSIMD=2 -DGIT_COMMIT=26e61df  -static -Wl,--whole-archive -lpthread -Wl,--no-whole-archive -std=c++14 -I libs -c src/core/profile_seq.cpp -o src/core/profile_seq.o
g++ -Wall -Wno-char-subscripts -Wno-attributes -O3 -msse4 -DNO_PROFILE_PAR -DOLD_ATOMIC_FLAG -DSIMD=2 -DGIT_COMMIT=26e61df  -static -Wl,--whole-archive -lpthread -Wl,--no-whole-archive -std=c++14 -I libs -c src/core/sequence.cpp -o src/core/sequence.o
g++ -Wall -Wno-char-subscripts -Wno-attributes -O3 -msse4 -DNO_PROFILE_PAR -DOLD_ATOMIC_FLAG -DSIMD=2 -DGIT_COMMIT=26e61df  -static -Wl,--whole-archive -lpthread -Wl,--no-whole-archive -std=c++14 -I libs -c src/core/queues.cpp -osrc/core/queues.o
g++ -Wall -Wno-char-subscripts -Wno-attributes -O3 -msse4 -DNO_PROFILE_PAR -DOLD_ATOMIC_FLAG -DSIMD=2 -DGIT_COMMIT=26e61df  -static -Wl,--whole-archive -lpthread -Wl,--no-whole-archive -std=c++14 -I libs -c libs/mimalloc/static.cpp -o libs/mimalloc/static.o
g++ -Wall -Wno-char-subscripts -Wno-attributes -O3 -msse4 -DNO_PROFILE_PAR -DOLD_ATOMIC_FLAG -DSIMD=2 -DGIT_COMMIT=26e61df  -static -Wl,--whole-archive -lpthread -Wl,--no-whole-archive -std=c++14 -I libs -c src/lcs/lcsbp.cpp -o src/lcs/lcsbp.o
g++ -Wall -Wno-char-subscripts -Wno-attributes -O3 -msse4 -DNO_PROFILE_PAR -DOLD_ATOMIC_FLAG -DSIMD=2 -DGIT_COMMIT=26e61df  -static -Wl,--whole-archive -lpthread -Wl,--no-whole-archive -std=c++14 -I libs -c src/lcs/lcsbp_classic.cpp -o src/lcs/lcsbp_classic.o
g++ -Wall -Wno-char-subscripts -Wno-attributes -O3 -msse4 -DNO_PROFILE_PAR -DOLD_ATOMIC_FLAG -DSIMD=2 -DGIT_COMMIT=26e61df  -static -Wl,--whole-archive -lpthread -Wl,--no-whole-archive -std=c++14 -I libs -mavx -fabi-version=0  -mpopcnt -funroll-loops -c src/lcs/lcsbp_avx_intr.cpp -o src/lcs/lcsbp_avx_intr.o
g++ -Wall -Wno-char-subscripts -Wno-attributes -O3 -msse4 -DNO_PROFILE_PAR -DOLD_ATOMIC_FLAG -DSIMD=2 -DGIT_COMMIT=26e61df  -static -Wl,--whole-archive -lpthread -Wl,--no-whole-archive -std=c++14 -I libs -mavx2 -fabi-version=0  -mpopcnt -funroll-loops -c src/lcs/lcsbp_avx2_intr.cpp -o src/lcs/lcsbp_avx2_intr.o
g++ -Wall -Wno-char-subscripts -Wno-attributes -O3 -msse4 -DNO_PROFILE_PAR -DOLD_ATOMIC_FLAG -DSIMD=2 -DGIT_COMMIT=26e61df  -static -Wl,--whole-archive -lpthread -Wl,--no-whole-archive -std=c++14 -I libs -c src/utils/utils.cpp -osrc/utils/utils.o
g++ -Wall -Wno-char-subscripts -Wno-attributes -O3 -msse4 -DNO_PROFILE_PAR -DOLD_ATOMIC_FLAG -DSIMD=2 -DGIT_COMMIT=26e61df  -static -Wl,--whole-archive -lpthread -Wl,--no-whole-archive -std=c++14 -I libs -mavx -fabi-version=0  -mpopcnt -funroll-loops -c src/utils/utils_avx.cpp -o src/utils/utils_avx.o
g++ -Wall -Wno-char-subscripts -Wno-attributes -O3 -msse4 -DNO_PROFILE_PAR -DOLD_ATOMIC_FLAG -DSIMD=2 -DGIT_COMMIT=26e61df  -static -Wl,--whole-archive -lpthread -Wl,--no-whole-archive -std=c++14 -I libs -mavx2 -fabi-version=0  -mpopcnt -funroll-loops -c src/utils/utils_avx2.cpp -o src/utils/utils_avx2.o
g++ -lm -static -O3 -msse4 -Wl,--whole-archive -lpthread -Wl,--no-whole-archive -std=c++14 -o famsa src/famsa.o src/msa.o src/msa_refinement.o src/tree/AbstractTreeGenerator.o src/tree/Clustering.o src/tree/DistanceCalculator.o src/tree/FastTree.o src/tree/GuideTree.o src/tree/MSTPrim.o src/tree/NeighborJoining.o src/tree/NewickParser.o src/tree/SingleLinkage.o src/tree/UPGMA.o src/utils/timer.o src/utils/log.o src/core/io_service.o src/core/params.o src/core/profile.o src/core/profile_par.o src/core/profile_seq.o src/core/sequence.o src/core/queues.o libs/mimalloc/static.o src/lcs/lcsbp.o src/lcs/lcsbp_classic.o src/lcs/lcsbp_avx_intr.o src/lcs/lcsbp_avx2_intr.o src/utils/utils.osrc/utils/utils_avx.o src/utils/utils_avx2.o libs/libdeflate/libdeflate.a
make STATIC_LINK=true  77.05s user 5.53s system 79% cpu 1:43.55 total
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7eb7612c6613`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.