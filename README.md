# X3D-benchmarking

This repository is intended to collect publicly available benchmarking data from the Xcompact3D user
group, it will also standardise the run setup and collection of data for future benchmarks.

There are four main files in the repository:
- [input.i3d](./input.i3d) - the input file for running the benchmark
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

### Adapting the Benchmark

Whilst the majority of the input file should be unchanged, the variables `nx`, `ny`, `nz`, `p_row` and
`p_col` should be set appropriately
- `nx=ny=nz=n` set as large as possible to fit in available memory
- `n` should be (a combination of) power(s) of 2 plus 1, e.g. `n=129=128+1` or `n=145=128+16+1`
- `p_row`x`p_col`=`nranks`
- `p_col`>=`p_row`
- `p_row` and `p_col` both divide into `n` exactly

## Contributing

If you run Xcompact3D on a new machine and are willing and able to share the data, we request that
you contribute to this repository.
To do so, fork the repository, add your data to your fork and submit a pull request.

For further details see [CONTRIBUTING](./CONTRIBUTING.md).
