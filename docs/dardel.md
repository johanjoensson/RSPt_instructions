# Dardel
For running jobs on a compute node on Dardel, use the `srun` command. Set the `MPIRUN` variable
in the `testsuite/runcommand` (or if it does not exist, `testsuite/runcommand.default`) file to
match, i.e.

```
MPIRUN="srun -n 2"
```
On Dardel, in order to optimize code for the CPU partition you should load the correct module, i.e.,
```
ml craype-x86-milan
```
By default `craype-x86-rome` is loaded, which optimizes code for the login nodes.
By loading these modules you should not need to specify any other flags for optimizing
the code for certain CPU architectures (i.e. `-march` for GCC).

## GNU compiler
On Dardel load the GNU programming environment, for the compiler and scientific libraries.
Also load the Cray FFTW libraries.

```
ml PrgEnv-gnu/8.5.0
ml cray-fftw/3.3.10.6
```
On Dardel, ftn is an alias for the fortran compiler you have loaded, cc is an
alias for the C compiler, and CC is an alias for the C++ compiler.

### RSPtmake.inc
```
OPTIMIZATIONS    = -O2 -march=znver2 -mtune=znver2 -mfma -mavx2 -m3dnow -fomit-frame-pointer
FHOME            =
FCOMPILER        = ftn
FCOMPILERFLAGS   = $(OPTIMIZATIONS) -fallow-argument-mismatch

FCPPFLAGS        = -DMPI -DMEMORY_STORE
FTARGETARCH      =
FORTRANLIBS      = -lmpifort_gnu_91
F90COMPILER      = $(FCOMPILER)
F90COMPILERFLAGS =
# GNU
CCOMPILER        = cc
CCOMPILERFLAGS   = $(OPTIMIZATIONS)
CTARGETARCH      =
CPPFLAGS         = -DMPI -DMEMORY_STORE
CLOADER          =

## LIBRARIES AND INCLUDE DIRECTORIES
LAPACKLIB        =
BLASLIB          =
FFTWLIB          =
EXTRALIBS        = -z muldefs -fno-strict-aliasing
INCLUDEDIRS      =
```

## Cray compiler
The Cray compiler settings below are old, and may not work! The Cray compiler suite is meant to
do aggressive optimization for running code on the compute nodes. This might not work correctly
for parts of RSPt.

```
OPTIMIZATIONS    = -O3 -h ipa5 -h vector0
FHOME            =
FCOMPILER        = ftn
FCOMPILERFLAGS   = $(OPTIMIZATIONS)

FCPPFLAGS        = -DMPI -DMEMORY_STORE
FTARGETARCH      =
FORTRANLIBS      =
F90COMPILER      = $(FCOMPILER)
F90COMPILERFLAGS =
# Cray
CCOMPILER        = cc
CCOMPILERFLAGS   = $(OPTIMIZATIONS)
CTARGETARCH      =
CPPFLAGS         = -DMPI -DMEMORY_STORE
CLOADER          =

## LIBRARIES AND INCLUDE DIRECTORIES
LAPACKLIB        =
BLASLIB          =
FFTWLIB          =
EXTRALIBS        = -z muldefs -fno-strict-aliasing -lmpifort_cray
#EXTRALIBS        =
INCLUDEDIRS      =
```
