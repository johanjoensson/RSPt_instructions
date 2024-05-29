# Dardel
## GNU compiler
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
The Cray compiler settings below are old, and may not work!

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
