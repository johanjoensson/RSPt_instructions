# RSPt_instructions
Instructions for building/running [RSPt](https://github.com/uumaterialstheory/rspt)

## Compiling and running RSPt
RSPt uses makefiles to build. In order to use the correct compilers, libraries, flags, etc. for the build
the file RSPTmake.inc is used. It contains declarations of which compilers, flags, libraries, etc. to use.
The settings have to be adjusted for each cluster you build on.


Basic compilation settings for some clusters can be found below. These settings are a basic starting point,
 they are not heavily optimized.
- [Tetralith](docs/tetralith.md)
- [Dardel](docs/dardel.md)
- [Lumi](docs/lumi.md)

To build RSPt use the command `make`, this should build RSPt and all the helper programs. To clean the build
directory use `make pristine`.

Make sure that the basic tests run correctly on a compute node. Use a short interactive job, and use `make test`.

### Things to consider for optimizations
RSPt contains some fortran code that was written a long time ago, when compilers were not very good at
automatic optimization. Newer compilers that try to apply very heavy optimizations, such as the Cray
compilers, can create binaries that do not work correctly. The solution in this case is usually to decrease the
optimization level, usually this is controlled by the `-O` flag, `-O2` is usually safe, but setting it lower is
sometimes needed.

If you use architecture specific optimizations (`-march` for GNU compilers), your binary will be built
to run on one specific CPU architecture. If the login node on the cluster uses a different architecture than the
compute nodes your code might only run correctly on one of them. To solve this, either remove the architecture
specific optimizations, or build RSPt first for the login node without architecture specific optimizations. Then
change the `RSPTmake.inc` settings to include them, go into the `lib` folder, do `make pristine` followed by `make`.
Then go into the `../rsptDir/src` folder and do `make pristine` followed by `make`. This will build all the helper
programs without the CPU specific optimizations, so that they should run on both the login nodes and the compute
nodes and will optimize the `rspt` binary for running on the compute nodes.
