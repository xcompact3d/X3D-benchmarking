# X3D-benchmarking

This repository is intended to collect publicly available benchmarking data from the Xcompact3D user
group, it will also standardise the run setup and collection of data for future benchmarks.

There are three main files in the repository: input.i3d. historical-benchmarks.csv and
benchmarks.csv.
The input.i3d file should be copied to your run directory for performing the benchmark, it should
not be editted except to change the system size (nx=ny=nz) and set p_row and p_col appropriately -
this ensures benchmarking is consistent across sites.
The file benchmarks.csv is intended as a living document, and will collect the data based on the
input defined in this repository, histroical-benchmarks.csv is intended to collect data from
benchmarking performed prior to the creation of this repository and as such may include incomplete
data.

## Contributing

If you run Xcompact3D on a new machine and are willing and able to share the data, we request that
you contribute to this repository.
To do so, fork the repository, add your data to your fork and submit a pull request.
