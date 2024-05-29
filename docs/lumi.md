# LUMI
## GNU compiler
On LUMI load the GNU programming environment, for the compiler and scientific libraries.
Also load the Cray FFTW libraries.

```
ml PrgEnv-gnu/8.4.0
ml cray-fftw/3.3.10.5
```

On LUMI, ftn is an alias for the fortran compiler you have loaded, cc is an
alias for the C compiler, and CC is an alias for the C++ compiler.

### RSPtmake.inc
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
So far, I have not found a working configuration for the Cray compilers on LUMI.
