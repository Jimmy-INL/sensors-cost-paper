# sensors-cost-paper

This repository contains the software companion
to the paper "Greedy Sensor Placement With Cost Constraints"
[preprint on arXiv](https://arxiv.org/abs/1805.03717).

## How to use

To start, be sure to add the src directory to your
MATLAB path.

The code takes in samples of data as the rows of
a matrix (so that columns correspond to sensor
locations) and a vector representing the costs
at each location. It is then possible to trace
out a cost-error curve by scaling the input cost
vector for the algorithm (this changes its relative
strength in the algorithm).

There is a simple demonstration of the code and
algorithm in simple_qrpc_example.m

## Figure generation

For reproducibility, we have included here the
codes used to generate most of the figures in the
preprint. These codes take a very long time to run
(especially using the pure matlab implementation
of the code, see below). If you would like to run
them more quickly but less accurately, reduce LCV
(the number of cross validations) in Reconstruction*.m.
You can also reduce the number of elements in p and
Gamma for additional speed-ups, but this may affect
the plotting.

### Obtaining the data

The data for the various experiments can be
obtained as follows.

#### Yale Faces

You can download the relevant file for the
Yale faces data with
[this dropbox link](https://www.dropbox.com/s/vp1pl8jriy5twzf/YaleB_32x32.mat?dl=0)

#### Sea Surface Temperature

This data is hosted by NOAA [here](https://www.esrl.noaa.gov/psd/data/gridded/data.noaa.oisst.v2.html).
Download sst.wkmean.1990-present.nc and lsmask.nc.

#### Cylinder flow

This data is included with the companion to the
Dynamic Mode Decomposition book [here](http://dmdbook.com/).
Download DATA.zip (note that this file is 417 MB). The
fluid flow data can be found in DATA\FLUIDS\CYLINDER_ALL.mat.

## Faster Option With MEX

We've included a MEX wrapper to a FORTRAN routine.
The codes seem to compile and run well on UNIX systems
with standard gnu compilers. 

These can be compiled by changing directory to
the src directory and running build_xqrmc_m and build_xormqr_m.
The success of this step will likely be the make-or-break
point, but if you have some experience with
MEX files you could try messing with the flags in
build_xqrmc_m and build_xormqr_m

Be sure to then test the code with test_xqrmc_m.
If a zero is output, things should be good.

The CostError function will automatically use the
MEX version if it exists.
If you find that this has broken everything, simply
delete the MEX binary to restore the slower operation.

Note that xormqr_m is only used to access the Householder
reflectors stored in the output. It is possible to find
the sensor locations without this routine.

## Documentation

Documentation for many of these files can be accessed by
typing help [function or script name] in MATLAB.
