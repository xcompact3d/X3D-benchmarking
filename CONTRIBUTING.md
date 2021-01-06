# CONTRIBUTING

This project seeks input from the Xcompact3d community to collect benchmarking data on as wide a
range of machines as possible - if you have access to a machine not present, and are able to, please
consider contributing.

## Getting started

If you plan to contribute to the benchmarks repository, the first step is to fork the repository by
clicking the `fork` button on the repository main page.
After forking the repository clone your fork somewhere convenient (for editing the `.csv` files it
is useful to have a spreadsheet program, although with care they can be editted by hand).

## Running the benchmark

See the [README](./README.md) for an overview - in summary: build Xcompact3d; copy the appropriate
input file from this repository to the run directory; run Xcompact3d (using job queue if necessary);
record the average time per timestep.

## Recording data

There are two data files: [benchmarks.csv](./benchmarks.csv) and
[benchmarks-io.csv](./benchmarks-io.csv) for recording data without, and with, performing IO, both
follow a similar format.

The columns record:
- the machine name
- a label to identify a series of runs, the suggested format is `MACHINE-TAG-DATE` where `MACHINE`
  is a contraction of the machine name, `TAG` is some identifier associated with the runs and `DATE`
  is in the format `YYYYMMDD`, e.g. the set of runs performed on Fulhame on 4th January 2021 and
  built with `-O3` are labelled `FHM-O3-20210104`.
- the number of compute nodes used for the run
- number of `MPI` ranks per node
- the number of `SMT` threads used in a run (also known as HyperThreading)
- the code version (printed at the top of `std` output)
- the compiler and `MPI` wrapper combination used (with versions)
- the `FFLAGS` used when building (these are set in the `Makefile` or otherwise specified by the
  user on the command line)
- which `FFT` option was used when building (default value is `generic`)
- the precision used (single or double, double is the default)
- mesh size
- number of time steps
- the timescheme used
- and the timing value for each of three runs to account for variability

For benchmarks with IO, the following additional fields are recorded:
- number of files written per timestep (generally this should be 4 for `ux`,`uy`,`uz` and `p`
  fields)
- file size in GB

### Machine summary

In addition to the benchmarking data, if you are running on a new machine, a machine summary should
be added to [machines.org](./machines.org), this file is intended to be human, rather than machine,
readable.
This file records details of each machine run on that could be useful for comparing results, these
include:
- the machine name
- number of nodes
- processor name/family
- sockets (`CPU`s) per node
- cores per socket
- `SMT` threads available per core
- clock speed
- memory per socket
- cache size
- compute rate (double precision GFLOPs, measure or theoretical if available)
- peak bandwidth per node (measured or theoretical if available)

## Submitting data

After recording your data, commit and push your changes back to your fork.
Once pushed to your fork, go to your fork's GitHub page and start a pull request, once approved your
contribution will be available to the benefit of the Xcompact3d community.
