# Tetralith
On Tetralith, set the following variable in the `testsuite/runcommand` file (if it does not exist, use `testsuite/runcommand.default` instead)
```
MPIRUN="mpprun -n 2"
```
## GNU compiler
Load the GNU compiler build environment, this loads the compilers, BLAS, LAPACK, FFTW3, etc.
```
ml buildenv-gcc/2022a-eb.
```
On Tetralith, using the GNU compilers, mpifort is an alias for the (MPI) fortran compiler you have loaded, mpicc is an
alias for the (MPI) C compiler, and mpic++ is an alias for the (MPI) C++ compiler.

### RSPtmake.inc
```
OPTIMIZATIONS    = -O2 -march=native
FHOME            =
FCOMPILER        = mpifort
FCOMPILERFLAGS   = $(OPTIMIZATIONS) -fallow-argument-mismatch
FCPPFLAGS        = -DMPI -DMEMORY_STORE
FTARGETARCH      =
FORTRANLIBS      = -lgfortran -lm -lmpi_mpifh
F90COMPILER      = $(FCOMPILER)
# GNU
CCOMPILER        = mpicc
CCOMPILERFLAGS   = $(OPTIMIZATIONS)
CTARGETARCH      =
CPPFLAGS         = -DMPI -DMEMORY_STORE
CLOADER          =

## LIBRARIES AND INCLUDE DIRECTORIES
BLASLIB          = -lopenblas
FFTWLIB          = -lfftw3
EXTRALIBS        = -z muldefs
INCLUDEDIRS      =
```

## Intel compiler
Load the Intel compiler build environment, this loads the compilers, MKL, etc.
```
ml buildenv-intel/2023.1.0-oneapi
```
On Tetralith, using the Intel compilers, mpiifort is an alias for the (MPI) fortran compiler you have loaded, mpiicc is an
alias for the (MPI) C compiler, and mpiicpc is an alias for the (MPI) C++ compiler.

### RSPtmake.inc
```
OPTIMIZATIONS    = -O3 -ipo -xHost -mkl=sequential
FHOME            =
FCOMPILER        = mpiifort
FCOMPILERFLAGS   = $(OPTIMIZATIONS)
FCPPFLAGS        = -DMPI -DMEMORY_STORE -DMKLFFT
FTARGETARCH      =
FORTRANLIBS      = -lifcore -lsvml -lirc -lifport -limf
F90COMPILER      = mpiifort
# intel
CCOMPILER        = mpiicc
CCOMPILERFLAGS   = $(OPTIMIZATIONS)
CTARGETARCH      =
CPPFLAGS         = -DMPI -DMEMORY_STORE -DMKLFFT
CLOADER          =

## LIBRARIES AND INCLUDE DIRECTORIES
BLASLIB          =
FFTWLIB          =
EXTRALIBS        =
INCLUDEDIRS      =
```
