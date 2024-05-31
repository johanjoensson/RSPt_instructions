# LUMI
For running jobs on a compute node on LUMI, use the `srun` command. Set the `MPIRUN` variable
in the `testsuite/runcommand` (or if it does not exist, `testsuite/runcommand.default`) file to
match, i.e.

```
MPIRUN="srun -n 2"
```

On LUMI, in order to optimize code for the CPU partition you should load the correct module, i.e.,
```
ml craype-x86-milan
```
By default `craype-x86-rome` is loaded, which optimizes code for the login nodes.
By loading these modules you should not need to specify any other flags for optimizing
the code for certain CPU architectures (i.e. `-march` for GCC).

## GNU compiler
On LUMI load the GNU programming environment, for the compiler and scientific libraries.
Also load the Cray FFTW libraries.

```
ml PrgEnv-gnu/8.4.0
ml cray-fftw/3.3.10.5
```

On LUMI, ftn is an alias for the fortran compiler you have loaded, cc is an
alias for the C compiler, and CC is an alias for the C++ compiler.

### RSPTmake.inc
```
OPTIMIZATIONS    = -O2 -ftree-vectorize -funroll-loops
FHOME            =
FCOMPILER        = ftn
FCOMPILERFLAGS   = $(OPTIMIZATIONS) -fallow-argument-mismatch

FCPPFLAGS        = -DMPI -DMEMORY_STORE
FTARGETARCH      =
FORTRANLIBS      = -lmpifort_gnu_91
F90COMPILER      = $(FCOMPILER)
F90COMPILERFLAGS =
# GNU compilers
CCOMPILER        = cc
CCOMPILERFLAGS   = $(OPTIMIZATIONS)
CTARGETARCH      =
CPPFLAGS         = -DMPI -DMEMORY_STORE
CLOADER          =

## LIBRARIES AND INCLUDE DIRECTORIES
LAPACKLIB        =
BLASLIB          =
FFTWLIB          =
EXTRALIBS        = -z muldefs
INCLUDEDIRS      =
```

## Cray compiler
So far, I have not found a working configuration for the Cray compilers on LUMI. The Cray compiler suite
is meant to apply heavy optimizations, these might not work with parts of the RSPt code.
