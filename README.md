# X3D-benchmarking

This repository is intended to collect publicly available benchmarking data from the Xcompact3D user
group, it will also standardise the run setup and collection of data for future benchmarks.

There are four main files in the repository:
- [input.i3d](./input.i3d) - the input file for running the benchmark
- [input-io.i3d](./input-io.i3d) - the input file for running the benchmark with IO
- [benchmarks.csv](./benchmarks.csv) - a comma separated value file for recording benchmark data
- [benchmarks-io.csv](./benchmarks-io.csv) - as above, but for recording data from benchmarks involving IO
- [historical-benchmarks.csv](./historical-benchmarks.csv) - a comma separated value file for
historical benchmark data

The input.i3d file should be copied to your run directory for performing the benchmark, it should
not be editted except to change the system size (nx=ny=nz) and set p_row and p_col appropriately -
this ensures benchmarking is consistent across sites.
The files benchmarks.csv and benchmarks-io.csv are intended to be living documents, and will collect
data based on the input defined in this repository, historical-benchmarks.csv is intended to collect
data from benchmarking performed prior to the creation of this repository and as such may include
incomplete data.

## The Benchmark

The benchmark is based on the 3D Taylor Green Vortex case, defined in the box x=[0,pi]^3 with Neumann
boundary conditions.
The benchmark runs for 100 timesteps using AB2 timestepping and full 6th order compact schemes for
first and second derivatives, no IO or post-processing is performed.

The file [input-io.i3d](./input-io.i3d) sets up the same case, however it runs for only 10 timesteps
whilst writing output (`ux`,`uy`,`uz` and `p`) at each timestep, note that depending on problem size
this will result in potentially a significant amount of disk space being used!

### Adapting the Benchmark

Whilst the majority of the input file should be unchanged, the variables `nx`, `ny`, `nz`, `p_row` and
`p_col` should be set appropriately
- `nx=ny=nz=n` set as large as possible to fit in available memory
- `n` should be (a combination of) power(s) of 2 plus 1, e.g. `n=129=128+1` or `n=145=128+16+1`
- `p_row`x`p_col`=`nranks`
- `p_col`>=`p_row`
- `p_row` and `p_col` both divide into `n` exactly

### Running the Benchmark

To run the benchmark first build Xcompact3d, in the simplest case this entails simply running `make`
to build with GNU compilers (assuming MPI-wrappers are available), otherwise passing different
values of `CMP` to `make` allows building with different compilers - see the `Makefile` in the
Xcompact3d root directory for details.

With a working Xcompact3d, run on the machine to be benchmarked (copying the appropriate input file
to the working directory, and renaming to `input.i3d`), the command to run Xcompact3d is simply
`/path/to/xcompact3d`.
At the end of the `std` output you will find a summary of the run, in particular a line with the
average time per timestep, this is the value that should be recorded for the benchmark, for more
information on how to submit your results see [CONTRIBUTING](./CONTRIBUTING.md).

## Contributing

If you run Xcompact3D on a new machine and are willing and able to share the data, we request that
you contribute to this repository.
To do so, fork the repository, add your data to your fork and submit a pull request.

For further details see [CONTRIBUTING](./CONTRIBUTING.md).
